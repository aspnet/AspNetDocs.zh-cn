---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET数据访问 - 推荐资源 |微软文档
author: rick-anderson
description: 本主题提供指向文档资源的链接，了解如何访问ASP.NET Web 应用程序中的数据，主要是通过使用实体框架和 SQL Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675783"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 数据访问 - 推荐的资源

> 本主题提供指向文档资源的链接，了解如何访问ASP.NET Web 应用程序中的数据，主要是通过使用实体框架和 SQL Server。
> 
> 如果您知道一个伟大的博客文章，[堆栈溢出](http://stackoverflow.com)线程，或任何其他链接将有用，[给我们发一封电子邮件](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)与链接。
> 
> 最后更新 4/3/2014

本主题包含以下各节：

- [ASP.NET 开始使用数据访问](#gettingstarted)
- [使用实体框架](#ef)

    - [首先使用实体框架代码](#cf)
    - [使用实体框架代码首次迁移](#efcfmigrations)
    - [首先使用实体框架数据库或模型（EF 设计器）](#efdbf)
    - [在实体框架中加载相关数据（延迟加载、热切加载和显式加载）](#efrelateddata)
    - [优化实体框架性能](#optimizingef)
    - [在实体框架应用程序中处理并发性](#efconcurrency)
    - [有关实体框架的书籍](#efbooks)
    - [其他实体框架资源](#otherefresources)
- [ASP.NET Web 窗体应用程序中的数据绑定](#wfdatabinding)

    - [使用 Web 窗体模型绑定](#wfmodelbinding)
    - [使用 Web 窗体数据源控件](#wfdsc)
    - [使用 Web 窗体数据绑定控件和数据绑定表达式](#wfdbc)
- [使用 SQL 服务器数据库](#sqlserver)

    - [使用 SQL 服务器快速本地数据库](#sslocaldb)
    - [使用 SQL 服务器快速数据库](#sse)
    - [使用 Windows Azure SQL 数据库](#ssdb)
    - [在 SQL 服务器和 Windows Azure SQL 数据库之间进行选择](#ssdbchoosing)
- [使用 NoSQL 数据库管理系统](#nosql)
- [在ASP.NET应用程序中使用 LINQ 查询](#linq)
- [使用动态数据基架](#dd)
- [保护数据访问](#securing)
- [优化数据访问性能](#optimizingdataaccess)
- [部署数据库](#deploying)
- [通过 Web 服务访问数据](#webservice)
- [其他资源](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET 开始使用数据访问

- [数据存储选项（使用 Windows Azure 构建真实世界的云应用）。](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) 关于云开发电子书的章节。 引入 NoSQL 数据库作为许多熟悉关系数据库的开发人员倾向于忽视的替代方法。 介绍在选择关系或 NoSQL 或选择特定平台时要考虑的准则。
- [ASP.NET数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx)（MSDN）。 关系数据库的数据访问选项简介，用于ASP.NET以及如何选择适合您的方案的平台和访问方法。
- [关系数据库](http://en.wikipedia.org/wiki/Relational_database). 维基百科）。 如果您尚未使用关系数据库，请参阅此页面，了解关系数据库术语和概念的介绍。 有关 SQL Server 的简介，请参阅本主题后面使用[SQL Server 数据库](#sqlserver)。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>使用实体框架

- [实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)（MSDN）。 有关如何选择实体框架开发方法数据库优先、模型优先或代码优先的指导。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>首先使用实体框架代码

以下教程提供可下载的示例应用程序：

- [使用 MVC 5 开始使用 EF 6。](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 涵盖各种实体框架代码优先方案，包括迁移和 EF 6 功能，如连接恢复能力、命令拦截和异步。 这是[EF 5 / MVC 4 系列的](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)更新版本。 前面的系列包括有关新系列中未包括的存储库和工作单位模式的教程。
- [ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md)简介 。 涵盖实体框架代码优先方案的范围较窄，但采用更全面的工作来引入 MVC 功能。
- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 在 Web 窗体应用程序中首先使用代码。
- [开始使用ASP.NET 4.5 Web 表单](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 Web 表单简介，其中介绍了代码优先。 使用模型绑定。
- [MVC音乐商店](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 在电子商务 MVC 3 应用程序中使用代码优先，该应用程序还实现了成员资格和授权。 此处使用的 MVC 版本和ASP.NET成员资格（身份验证和授权）系统已过时;有关ASP.NET成员资格的更多最新信息，请参阅[https://asp.net/identity](https://asp.net/identity)。

其他资源：

- [实体框架 - 代码首先到现有数据库](https://msdn.microsoft.com/data/jj200620)。 Msdn。 视频和演练，演示如何将代码优先用于现有数据库。
- [数据开发人员中心 - 实体框架](https://msdn.microsoft.com/data/ef)。 Msdn。 有关实体框架团队创建和维护的实体框架文档的指南，请参阅[入门](https://msdn.microsoft.com/data/ee712907)链接。

请参阅本主题后面的[有关实体框架](#efbooks)[和其他实体框架资源](#otherefresources)的书籍。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>使用实体框架代码首次迁移

上面列出的大多数代码第一教程都涵盖了迁移。 另请参阅以下资源。

- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 由两部分组成的教程系列，演示如何使用代码优先迁移来部署数据库。
- [将具有成员资格、OAuth 和 SQL 数据库的安全ASP.NET MVC 5 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 微软 Azure）。 如何使用迁移将成员身份和应用程序数据部署到 Azure。
- [可视化工作室和ASP.NET的 Web 部署概述](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 有关代码优先迁移如何集成到可视化工作室 Web 部署功能的说明，请参阅**可视化工作室中的"配置数据库部署**"部分。
- [数据开发人员中心 - 代码优先迁移](https://msdn.microsoft.com/data/jj591621)（MSDN）。 实体框架团队的迁移文档。
- [迁移截屏广播系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF 博客）。 关于代码优先迁移中高级主题的三个视频。
- [使用ASP.NET网站进行代码优先迁移](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)。 迈克斯多特网博客）。 演示如何通过将数据上下文放在 Visual Studio 类库项目中，将代码优先迁移与ASP.NET Web Pages 网站结合使用。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>首先使用实体框架数据库或模型（EF 设计器）

- [首先使用 MVC 5 开始使用实体框架 6 数据库](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 在服务器资源管理器中运行脚本以创建数据库，然后使用实体框架设计器创建数据模型。 演示如何创建简单的 CRUD 网页，以及对于其他数据处理功能，您可以遵循代码优先教程之一，因为所有 EF 工作流都使用相同的 DbContext API。

以下资源较旧。 如果要使用实体框架的版本 4.0，并且希望在 Web 窗体应用程序中使用数据源控件进行数据绑定，则它们非常有用。

- [开始使用实体框架 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。 演示如何使用**实体数据源**控件。
- [继续实体框架](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)（演示如何使用**ObjectDataSource**控件）。 包括关于并发处理的教程、关于 EF 性能的教程以及有关 EF 4.0 中新增功能的教程。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>在实体框架中处理相关数据（延迟加载、热切加载和显式加载）

- [在 ASP.NETmVC应用程序中使用实体框架读取相关数据](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代码优先，MVC 示例应用程序。 显示的方法也适用于 Web 窗体模型绑定和数据库优先工作流。
- [数据开发人员中心 - 加载相关实体](https://msdn.microsoft.com/data/jj574232)（MSDN）。 实体框架团队有关加载相关数据的文档。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>优化实体框架性能

- [ASP.NET应用程序的高级实体框架方案](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 演示如何执行自己的 SQL 语句或调用自己的存储过程、如何禁用更改检测以及如何在保存更改时禁用验证。
- [实体框架 5](https://msdn.microsoft.com/data/hh949853) （MSDN） 的性能注意事项。
- [性能注意事项（实体框架](https://msdn.microsoft.com/library/cc853327)）（MSDN）。
- [在ASP.NET Web 应用程序中使用实体框架最大化性能](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架 4.0。
- 请参阅本主题后面的[优化ASP.NET数据访问](#optimizingdataaccess)。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>在实体框架应用程序中处理并发性

- [在 ASP.NET mVC 应用程序中处理与实体框架的并发](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代码优先，DbContext API，使用 MVC 示例应用程序。
- [数据开发人员中心 – 乐观并发模式](https://msdn.microsoft.com/data/jj592904)（MSDN）。 实体框架团队的并发文档。
- [在ASP.NET Web 应用程序中处理与实体框架的并发](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架 4.0。 数据库优先，对象上下文 API，使用 Web 窗体示例应用程序。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>有关实体框架的书籍

- [编程实体框架：朱莉](http://shop.oreilly.com/product/0636920022237.do)·莱曼和罗文·米勒的DbContext。
- [编程实体框架：朱莉](http://shop.oreilly.com/product/0636920022220.do)·莱曼和罗文·米勒首先编写代码。

这两本书都是最新的最新推荐技术。 与互联网上任何可用的内容相比，它们为实体框架提供了更全面但易于遵循的介绍。 另一本书，由朱莉·莱曼[编程实体框架](http://shop.oreilly.com/product/9780596807252.do)，是更大和更全面的，但它是旧的，它涵盖的许多技术不再是推荐的方式使用实体框架。 另请参阅[数据开发人员中心实体](https://msdn.microsoft.com/data/aa937716)框架团队推荐的书籍列表 - MSDN 网站上的书籍。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>其他实体框架资源

- [实体框架 （ADO.NET） 团队博客](https://blogs.msdn.com/b/adonet/). 最新信息和发布新增强功能的最佳资源之一。 有关其他与 EF 相关的博客，请参阅"[开始实体框架"](https://msdn.microsoft.com/data/ee712907)中的博客卷。
- [MSDN杂志](https://msdn.microsoft.com/magazine/default.aspx). 请参阅 **"数据点**"列，该列经常介绍与实体框架相关的主题。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web 窗体应用程序中的数据绑定

- [ASP.NET Web 窗体数据访问选项](https://msdn.microsoft.com/library/jj822927.aspx)（MSDN） 。<a id="wfmodelbinding"></a>

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>使用 Web 窗体模型绑定

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF 代码优先的教程系列。
- [Web 表单模型绑定第 1 部分：选择数据](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)（斯科特·古斯里博客）。 在这些较旧的博客文章中，当前名为 ItemType 的属性名为 ModelType，但除此之外，它们包含的信息是有效的。
- [Web 表单模型绑定第 2 部分：筛选数据](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)（斯科特·古斯里博客）。
- [Web 表单模型绑定第 3 部分：更新和验证](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)（斯科特·古斯里博客）。
- [ASP.NET 4.5 Web 窗体模型绑定](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)。 （视频）。
- [模型绑定第 1 部分 - 选择数据](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)（视频）。
- [模型绑定第 2 部分 - 筛选](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)（视频）。
- [开始使用ASP.NET 4.5 Web 表单 - 显示数据项和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>使用 Web 窗体数据源控件

- [数据源 Web 服务器控件](https://msdn.microsoft.com/library/ms247258.aspx)（MSDN）。
- [宣布发布实体框架 6 的动态数据提供程序和实体数据源控件](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)（Microsoft Web 开发博客）。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>使用 Web 窗体数据绑定控件和数据绑定表达式

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 首先使用 EF 代码的教程系列。
- [开始使用ASP.NET 4.5 Web 表单 - 显示数据项和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。
- [强类型数据控制](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)（斯科特·古斯里博客）。
- [强类型数据控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（视频）。
- [ASP.NET 4.5 Web 窗体强类型数据控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)（视频）。
- [数据绑定 Web 服务器控件](https://msdn.microsoft.com/library/ms228214.aspx)（MSDN）。
- [数据绑定表达式概述](https://msdn.microsoft.com/library/ms178366.aspx)（MSDN）。 本页仅涵盖**Eval**和**Bind**;它尚未更新，包括**项目和****绑定项目**。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>使用 SQL 服务器数据库

- [SQL 服务器数据库功能](https://msdn.microsoft.com/library/hh230827.aspx)（MSDN）。 有关各种 SQL Server 主题的一般介绍，请参阅 TOC 中此主题下的条目。
- [SQL 服务器版本](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)（MSDN）。 可用 SQL Server 版本的摘要，并包含指向每个版本的详细信息的链接。
- 用于ASP.NET Web 应用程序 （MSDN）[的 SQL 服务器连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。
- [将 SQL 服务器压缩用于ASP.NET Web 应用程序](https://msdn.microsoft.com/library/ms247257.aspx)（MSDN）。
- [微软 SQL 服务器：数据库产品示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 示例冒险工程数据库。
- [安装示例数据库](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 除了此处显示的方法外，您还可以将其中一个示例 .mdf 文件下载到 Web\_项目的 App Data 文件夹，将数据库转换为本地DB，并创建 LocalDB 连接字符串。 有关如何执行此操作的信息，请参阅[如何：升级到本地数据库](https://msdn.microsoft.com/library/hh873188.aspx)。

有关使用 SQL Server Express 和本地 DB 以及 SQL Server 和 SQL 数据库之间的选择，请参阅以下部分。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>使用 SQL 服务器快速本地数据库

- [SQL 服务器快速 2012 本地数据库](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx)（MSDN）。 本地 DB 的官方 MSDN 介绍。
- 用于ASP.NET Web 应用程序 （MSDN）[的 SQL 服务器连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。
- [如何：升级到本地数据库](https://msdn.microsoft.com/library/hh873188.aspx)（MSDN）。 如何将 .mdf 文件从早期版本的 SQL Server Express 迁移到本地DB。 如果下载[SQL Server 2012 示例数据库](https://go.microsoft.com/fwlink/?linkid=117483)之一，还必须完成此过程。
- [介绍本地数据库，改进后的 SQL Express（SQL](https://go.microsoft.com/fwlink/?LinkId=234375)服务器快速博客）。 与 MSDN 中包含的背景相比，具有更多有关创建 LocalDB 的原因的背景。
- [本地数据库：我的数据库在哪里？](https://go.microsoft.com/fwlink/?LinkId=234376) （SQL 服务器快速博客）。 有关本地DB数据库文件的创建位置的信息。
- [将本地DB与完整 IIS 一起使用，第 1 部分：用户配置文件](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)（SQL 服务器快速博客）。 本地DB并非旨在与 IIS 配合使用。 这一系列博客文章解释了问题和一些解决方法。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>使用 SQL 服务器快速数据库

- 用于ASP.NET Web 应用程序 （MSDN）[的 SQL 服务器连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。 如果将附加DBFileName连接字符串设置与 SQL Server Express 一起使用，请参阅此页面的用户实例部分。
- [如何取得本地 SQL Server Express 2008（SQL Server Express](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx)博客）的所有权。 一个常见的问题是不能使用 SQL Server Express 数据库，因为您不是 SQL Server Express 实例上的管理员。 默认情况下，只有安装 SQL Server Express 的人员是管理员。 此博客说明如果您是计算机上的管理员，如何使自己成为 SQL Server Express 管理员。
- [我的ASP.NET Web 应用程序是否可以在生产中使用 SQL Server Express 数据库？](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) （MSDN）。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>使用 Windows Azure SQL 数据库

- [将具有成员资格、OAuth 和 SQL 数据库的安全ASP.NET MVC 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)（Microsoft Azure 网站）。
- [SQL 数据库](https://docs.microsoft.com/azure/sql-database/)（微软 Azure 站点）。 入门教程和入门指南。
- [Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx)（MSDN）。 MSDN 中 SQL 数据库的目录的顶级节点。
- [Windows Azure SQL 数据库 TechNet 维基文章索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)（微软技术网网站）。
- [瞬态故障处理应用程序块](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)。 一个框架，使您能够处理由限制导致的瞬态网络故障和连接错误。 在 NuGet 软件包中提供：[企业库 5.0 - 瞬态故障处理应用程序块](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [开始使用 SQL 数据库和实体框架](https://msdn.microsoft.com/data/jj556244)（MSDN）。
- [Windows Azure 培训工具包](https://www.microsoft.com/download/details.aspx?id=8396)（微软下载中心）。 包括用于 SQL 数据库的动手实验。
- [Windows Azure SQL 数据库社区论坛](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [移动到 Windows Azure SQL 数据库](https://msdn.microsoft.com/library/ff803375.aspx)（MSDN）。 Microsoft 模式和实践团队全面端到端方案的一章。 介绍了可能想要迁移的原因以及如何从 SQL Server 迁移到 SQL 数据库。
- [将 SQL 服务器数据库迁移到 Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)（MSDN）。
- [SQL 数据库迁移向导](http://sqlazuremw.codeplex.com/)。 用于将数据库迁移到 SQL 数据库和从 SQL 数据库迁移到的开源工具。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>在 SQL 服务器和 Windows Azure SQL 数据库之间进行选择

- [将 SQL 服务器与 Windows Azure SQL 数据库](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx)（微软技术网站点）进行比较。
- [数据迁移到 Windows Azure SQL 数据库：工具和技术](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)（MSDN）。 包括将 SQL Server 与 SQL 数据库进行比较的部分，并提供有关何时从 SQL Server 迁移到 SQL 数据库的指导。
- [Windows Azure SQL 数据库交付指南](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)（微软技术网网站）。
- [SQL 服务器功能限制（Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx)）（MSDN）。
- [Windows Azure 表存储和 Windows Azure SQL 数据库 - 比较和对比](https://msdn.microsoft.com/library/jj553018.aspx)（MSDN）。 对于部署到 Windows Azure 的应用程序，Windows Azure 表存储可能是 Windows Azure SQL 数据库的替代方法。 本主题可帮助您在这些备选方案之间进行决策。
- [Windows Azure SQL 数据库](https://msdn.microsoft.com/library/windowsazure/ee336279)（MSDN）。
- [指导原则和限制 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>使用 NoSQL 数据库管理系统

- [Windows Azure 数据服务](https://www.windowsazure.com/develop/net/data/)（微软 Azure 站点）。 请参阅[页面的"表服务"功能指南](https://docs.microsoft.com/azure/)和**大数据**部分。
- [ASP.NET使用存储表、队列和 Blob（Microsoft](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) Azure 站点）的多层应用程序。 使用 Windows Azure 存储 NoSQL 表的可下载示例应用程序的端到端教程。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>在ASP.NET应用程序中使用 LINQ 查询

- [ASP.NET数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx#linq)（MSDN）。 包括 LINQ 简介。
- [LINQ培训视频](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)（乔·斯塔格纳的博客）。
- [ASP.NET论坛线程与动态LINQ资源的链接](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>使用动态数据基架

- [动态数据项目模板](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)（MSDN）。 有关何时使用动态数据项目的指导。
- [ASP.NET动态数据](https://msdn.microsoft.com/library/ee845452.aspx)（MSDN）。

<a id="securing"></a>

## <a name="securing-data-access"></a>保护数据访问

- 保护ASP.NET （MSDN）[中的数据访问](https://msdn.microsoft.com/library/ms178375.aspx)。
- [安全注意事项（实体框架](https://msdn.microsoft.com/library/cc716760.aspx)）（MSDN）。
- [如何：使用数据源控件](https://msdn.microsoft.com/library/ms178372.aspx)（MSDN） 时保护连接字符串。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>优化数据访问性能

- [ASP.NET性能概述](https://msdn.microsoft.com/library/cc668225.aspx)（MSDN）。
- [ASP.NET缓存](https://msdn.microsoft.com/library/xsbfdd8c.aspx)（MSDN）。
- [提高ASP.NET性能](https://msdn.microsoft.com/library/ff647787)（MSDN）。 此页面顶部有"已停用内容"警告，但大多数信息仍相关，并且没有可比较的更新资源。
- [提高 SQL 服务器性能](https://msdn.microsoft.com/library/ff647793)（MSDN）。 与上一个链接相同的注释。

请参阅本主题前面前面[优化实体框架性能](#optimizingef)。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>部署数据库

- [ASP.NET Web 部署 - 推荐资源](aspnet-web-deployment-content-map.md)（MSDN）。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>通过 Web 服务访问数据

- [通过 Web 服务](https://msdn.microsoft.com/library/ms178359.aspx#webservice)（MSDN） 访问数据。 有关何时使用 Web API 与 WCF 的指导。
- [开始使用ASP.NET Web API](../web-api/index.md)。
- [WCF 数据服务](https://msdn.microsoft.com/data/bb931106)（MSDN）。

<a id="additional"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET数据访问常见问题解答](https://msdn.microsoft.com/library/jj653753.aspx)（MSDN）。
- [ASP.NET Web 表单教程 - 数据](../web-forms/overview/data-access/index.md)。 这些教程大多比较旧;请确保首先阅读[ASP.NET数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx)和[数据存储选项（使用 Windows Azure 构建真实世界云应用），](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)以免过多地进入不适合您的方案的数据访问方法。
- [ASP.NET MVC 内容映射](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET网页教程 - 数据](../web-pages/overview/data/index.md)。
- [访问可视化工作室](https://msdn.microsoft.com/library/wzabh8c4.aspx)（MSDN） 中的数据。 提供与此内容映射类似的链接列表，但侧重于可视化工作室，而不是ASP.NET。

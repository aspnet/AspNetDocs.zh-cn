---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 数据访问-建议的资源 |Microsoft Docs
author: rick-anderson
description: 本主题提供有关如何在 ASP.NET web 应用程序中访问数据的文档资源的链接，主要通过使用实体框架和 SQL Se .。。
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345142"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 数据访问 - 推荐的资源

> 本主题提供了一些链接，这些链接指向有关如何访问 ASP.NET web 应用程序中的数据的文档资源，主要通过使用实体框架和 SQL Server。
> 
> 如果你知道一篇非常有用的博客文章、 [stackoverflow](http://stackoverflow.com) 或任何其他链接，请 [向我们发送一封电子邮件](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) ，其中包含该链接。
> 
> 上次更新时间4/3/2014

本主题包含以下各节：

- [使用 ASP.NET 中的数据访问入门](#gettingstarted)
- [使用实体框架](#ef)

    - [使用实体框架 Code First](#cf)
    - [使用 Entity Framework Code First 迁移](#efcfmigrations)
    - [使用实体框架 Database First 或 Model First (EF 设计器) ](#efdbf)
    - [将相关数据加载到实体框架 (延迟加载、预先加载和显式加载) ](#efrelateddata)
    - [优化实体框架性能](#optimizingef)
    - [在实体框架应用程序中处理并发](#efconcurrency)
    - [有关实体框架的书籍](#efbooks)
    - [其他实体框架资源](#otherefresources)
- [ASP.NET Web 窗体应用程序中的数据绑定](#wfdatabinding)

    - [使用 Web 窗体模型绑定](#wfmodelbinding)
    - [使用 Web 窗体数据源控件](#wfdsc)
    - [使用 Web 窗体 Data-Bound 控件和 Data-Binding 表达式](#wfdbc)
- [使用 SQL Server 数据库](#sqlserver)

    - [使用 SQL Server Express LocalDB 数据库](#sslocaldb)
    - [使用 SQL Server Express 数据库](#sse)
    - [使用 Microsoft Azure SQL 数据库](#ssdb)
    - [在 SQL Server 和 Microsoft Azure SQL 数据库之间进行选择](#ssdbchoosing)
- [使用 NoSQL 数据库管理系统](#nosql)
- [在 ASP.NET 应用程序中使用 LINQ 查询](#linq)
- [使用动态数据基架](#dd)
- [保护数据访问](#securing)
- [优化数据访问性能](#optimizingdataaccess)
- [部署数据库](#deploying)
- [通过 Web 服务访问数据](#webservice)
- [其他资源](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>使用 ASP.NET 中的数据访问入门

- [数据存储选项 (通过 Windows Azure) 生成 Real-World 云应用 ](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)。 有关云开发的电子书的章节。 引入 NoSQL 数据库作为替代方法，很多熟悉关系数据库的开发人员往往会忽视。 介绍了选择关系或 NoSQL 或选择特定平台时需要考虑的事项。
- ASP.NET)  (的[数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx)。 介绍适用于 ASP.NET 的关系数据库的数据访问选项，以及如何选择适用于你的方案的平台和访问方法的指南。
- [关系数据库](http://en.wikipedia.org/wiki/Relational_database)。 维基百科) 。 如果尚未使用关系数据库，请参阅此页面，了解相关数据库术语和概念的简介。 有关 SQL Server 的详细介绍，请参阅本主题后面的使用 [SQL Server 数据库](#sqlserver) 部分。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>使用实体框架

- [实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN) 。 有关如何选择实体框架开发方法 Database First、Model First 或 Code First 的指导。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>使用实体框架 Code First

以下教程提供可下载的示例应用程序：

- [使用 MVC 5 入门与 EF 6 一起使用](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 涵盖各种实体框架 Code First 方案，包括迁移和 EF 6 功能，如连接复原、命令拦截和异步。 这是 [EF 5/MVC 4 系列](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)的更新版本。 前面的系列包含有关存储库的教程和新系列中未包含的工作单元模式。
- [ASP.NET MVC 5 简介](../mvc/overview/getting-started/introduction/getting-started.md)。 涵盖一系列更广泛的实体框架 Code First 方案，但执行 MVC 功能的引入更为全面。
- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 Web 窗体应用程序中的 Code First。
- [入门 ASP.NET 4.5 Web 窗体](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 Web 窗体简介，其中包含某些 Code First。 使用模型绑定。
- [MVC 音乐商店](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 使用电子商务 MVC 3 应用程序中的 Code First，该应用程序还实现成员身份和授权。 此处使用的 MVC 版本和 ASP.NET 成员身份 () 系统的身份验证和授权已过时;有关 ASP.NET 成员身份的详细信息，请参阅 [https://asp.net/identity](https://asp.net/identity) 。

其他资源：

- [对现有数据库实体框架 Code First](https://msdn.microsoft.com/data/jj200620)。 期. 视频和演练，演示如何将 Code First 与现有数据库一起使用。
- [数据开发人员中心-实体框架](https://msdn.microsoft.com/data/ef)。 期. 有关实体框架团队创建和维护实体框架文档的指南，请参阅 [入门](https://msdn.microsoft.com/data/ee712907) 链接。

有关详细信息，请参阅本主题后面 [的有关实体框架](#efbooks) 和 [其他实体框架资源](#otherefresources) 的书籍。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>使用 Entity Framework Code First 迁移

上面列出的大部分 Code First 教程都涵盖了迁移。 另请参阅以下资源。

- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 2部分教程系列，其中演示了如何使用 Code First 迁移来部署数据库。
- [将包含成员资格、OAuth 和 SQL 数据库的 Secure ASP.NET MVC 5 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)网站。 Microsoft Azure) 。 如何使用迁移将成员身份和应用程序数据部署到 Azure。
- [Visual Studio 和 ASP.NET 的 Web 部署概述](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 有关如何将 Code First 迁移集成到 Visual Studio web 部署功能的说明，请参阅在 **Visual studio 中配置数据库部署** 部分。
- [数据开发人员中心-Code First 迁移](https://msdn.microsoft.com/data/jj591621) (MSDN) 。 实体框架团队的迁移文档。
- [迁移 Screencast 系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF 博客) 。 Code First 迁移中的高级主题的三个视频。
- [与 ASP.NET 网页网站 Code First 迁移](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)。 Mikesdotnetting 博客) 。 演示如何通过将数据上下文放在 Visual Studio 类库项目中，将 Code First 迁移与 ASP.NET 网页站点一起使用。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>使用实体框架 Database First 或 Model First (EF 设计器) 

- [使用 MVC 5 实体框架 6 Database First 入门](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 在服务器资源管理器中运行脚本来创建数据库，然后使用实体框架设计器创建数据模型。 演示如何创建简单的 CRUD 网页，对于其他数据处理函数，你可以遵循其中一个 Code First 教程，因为所有 EF 工作流都使用相同的 DbContext API。

以下资源较旧。 如果要使用实体框架的4.0 版，并且想要在 Web 窗体应用程序中使用数据绑定来进行数据绑定，则这些方法非常有用。

- [入门实体框架 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。 演示如何使用 **EntityDataSource** 控件。
- [继续实体框架](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) (演示如何使用 **ObjectDataSource** 控件。 包括有关并发处理的教程、EF 性能教程和 EF 4.0 中的新增功能的教程。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>处理实体框架 (延迟加载、预先加载和显式加载的相关数据) 

- [使用 ASP.NET MVC 应用程序中的实体框架读取相关数据](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 Code First，MVC 示例应用程序。 所显示的方法也适用于 Web 窗体模型绑定和 Database First 工作流。
- [数据开发人员中心-)  (加载相关实体](https://msdn.microsoft.com/data/jj574232) 。 实体框架团队有关加载相关数据的文档。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>优化实体框架性能

- [ASP.NET 应用程序的高级实体框架方案](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 说明如何执行您自己的 SQL 语句或调用自己的存储过程，如何禁用更改检测以及如何在保存更改时禁用验证。
-  (MSDN) [实体框架5的性能注意事项](https://msdn.microsoft.com/data/hh949853)。
-  (MSDN) [实体框架)  (性能注意事项](https://msdn.microsoft.com/library/cc853327)。
- [使用 ASP.NET Web 应用程序中的实体框架最大化性能](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架4.0。
- 请参阅本主题后面的 [优化 ASP.NET 数据访问](#optimizingdataaccess) 。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>在实体框架应用程序中处理并发

- [使用 ASP.NET MVC 应用程序中的实体框架处理并发](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 使用 MVC 示例应用程序 Code First DbContext API。
- [数据开发人员中心-](https://msdn.microsoft.com/data/jj592904) (MSDN) 的开放式并发模式。 实体框架团队的并发文档。
- [使用 ASP.NET Web 应用程序中的实体框架处理并发](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)。 适用于实体框架4.0。 使用 Web 窗体示例应用程序 Database First、ObjectContext API。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>有关实体框架的书籍

- [编程实体框架： DbContext](http://shop.oreilly.com/product/0636920022237.do) By Julie Lerman 和 Rowan 莎莎。
- [编程实体框架：](http://shop.oreilly.com/product/0636920022220.do) 通过 Julie Lerman 和 Rowan 莎莎 Code First。

这两本书都是最新的，其中包含当前的建议方法。 除了 Internet 上提供的任何内容外，它们还提供了更全面但又易于理解的实体框架。 另一本书是 Julie Lerman 的 [编程实体框架](http://shop.oreilly.com/product/9780596807252.do) ，它更大且更全面，但它是较旧的，而且它所涵盖的许多技巧不再是使用实体框架的建议方法。 另请参阅 MSDN 网站上的 [数据开发人员中心](https://msdn.microsoft.com/data/aa937716) 的实体框架团队建议的书籍列表。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>其他实体框架资源

- [实体框架 (ADO.NET) 团队博客](https://blogs.msdn.com/b/adonet/)。 最新信息的最佳资源之一和新增强功能的公告。 有关其他与 EF 相关的博客，请参阅 [实体框架入门](https://msdn.microsoft.com/data/ee712907)中的 Blogroll。
- [MSDN 杂志](https://msdn.microsoft.com/magazine/default.aspx)。 请参阅 **数据点** 列，这通常是与实体框架相关的主题。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web 窗体应用程序中的数据绑定

- [ASP.NET Web 窗体数据访问选项](https://msdn.microsoft.com/library/jj822927.aspx) (MSDN) <a id="wfmodelbinding"></a> 。

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>使用 Web 窗体模型绑定

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 教程系列。
- [Web 窗体模型绑定第1部分：选择数据](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie 的博客) 。 在这些较旧的博客文章中，当前名为 ItemType 的属性名为 ModelType，但其包含的信息是有效的。
- [Web 窗体模型绑定第2部分：筛选数据](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthrie 的博客) 。
- [Web 窗体模型绑定第3部分：更新和验证](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie 的博客) 。
- [ASP.NET 4.5 Web 窗体模型绑定](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)。  (视频) 。
- [模型绑定第1部分-选择数据](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (视频) 。
- [模型绑定第2部分-筛选](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (视频) 。
- [入门 ASP.NET 4.5 Web 窗体-显示数据项和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>使用 Web 窗体数据源控件

-  (MSDN) 的[数据源 Web 服务器控件](https://msdn.microsoft.com/library/ms247258.aspx)。
- [宣布发布适用于实体框架 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (Microsoft Web 开发博客) 的动态数据提供程序和 EntityDataSource 控件。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>使用 Web 窗体 Data-Bound 控件和 Data-Binding 表达式

- [模型绑定和 Web 窗体](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF Code First 教程系列。
- [入门 ASP.NET 4.5 Web 窗体-显示数据项和详细信息](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。
- [强类型化数据控件](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie 的博客) 。
- [强类型化数据控件](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (视频) 。
- [ASP.NET 4.5 Web 窗体 (视频) 的强类型化数据控件](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) 。
-  (MSDN) 的[数据绑定 Web 服务器控件](https://msdn.microsoft.com/library/ms228214.aspx)。
- [数据绑定表达式概述](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN) 。 此页仅涵盖 **Eval** 和 **Bind**;尚未对其进行更新以包括 **项** 和 **BindItem**。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>使用 SQL Server 数据库

-  (MSDN) [SQL Server 数据库功能](https://msdn.microsoft.com/library/hh230827.aspx)。 有关大量 SQL Server 主题的常规介绍，请参阅目录中此项下的条目。
- [SQL Server 版本](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN) 。 可用 SQL Server 版本的摘要，其中包含有关每个版本的详细信息的链接。 ) 
- SQL Server (MSDN) [的 ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。
- 将[SQL Server Compact 用于 ASP.NET Web 应用程序](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN) 。
- [Microsoft SQL Server：数据库产品示例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 示例 AdventureWorks 数据库。
- [安装示例数据库](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 除了此处所示的方法之外，你还可以将一个示例 .mdf 文件下载到 web 项目的应用 \_ 数据文件夹，将数据库转换为 localdb，并创建 localdb 连接字符串。 有关如何执行此操作的信息，请参阅 [如何：升级到 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx)。

另请参阅以下部分，了解如何使用 SQL Server Express 和 LocalDB，以及如何在 SQL Server 和 SQL 数据库之间进行选择。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>使用 SQL Server Express LocalDB 数据库

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN) 。 LocalDB 的官方 MSDN 简介。
- SQL Server (MSDN) [的 ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。
- [如何：升级到 LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN) 。 如何将 .mdf 文件从早期版本的 SQL Server Express 迁移到 LocalDB。 如果下载 [SQL Server 2012 示例数据库](https://go.microsoft.com/fwlink/?linkid=117483)之一，还必须完成此过程。
- [引入 LocalDB，它是改进的 SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express 博客) 。 具有更多有关创建 LocalDB 的原因，而不包括在 MSDN 中。
- [LocalDB：我的数据库在哪里？](https://go.microsoft.com/fwlink/?LinkId=234376) SQL Server Express 博客)  (。 有关创建 LocalDB 数据库文件的位置的信息。
- 将[LocalDB 与完整 IIS 一起使用：第1部分：用户配置文件](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express 博客) 。 LocalDB 不能用于 IIS。 这一系列博客文章介绍了问题和一些解决方法。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>使用 SQL Server Express 数据库

- SQL Server (MSDN) [的 ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。 如果在 SQL Server Express 中使用 AttachDBFileName 连接字符串设置，请参阅此页的 "用户实例" 部分。
- [如何获得本地 SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express 博客) 的所有权。 一个常见问题无法与 SQL Server Express 数据库一起使用，因为你不是 SQL Server Express 实例的管理员。 默认情况下，只有安装 SQL Server Express 的人员是管理员。 此博客介绍了如何使自己成为计算机上的管理员 SQL Server Express 管理员。
- [我的 ASP.NET web 应用程序是否可以在生产中使用 SQL Server Express 数据库？](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) )  (MSDN。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>使用 Microsoft Azure SQL 数据库

- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) 网站 (Microsoft Azure 站点) 。
- [SQL 数据库](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure 站点) 。 入门教程和操作方法指南。
- [Windows AZURE SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN) 。 MSDN 中的 SQL 数据库的目录的顶级节点。
- [Windows AZURE SQL 数据库 Technet Wiki 文章索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft TechNet 网站) 。
- [暂时性故障处理应用程序块](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)。 一个框架，使你能够处理由限制导致的暂时性网络故障和连接错误。 在 NuGet 包中提供： [企业库 5.0-暂时性故障处理应用程序块](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)。
- [与 SQL 数据库和实体框架](https://msdn.microsoft.com/data/jj556244) (MSDN) 入门。
- Microsoft 下载中心)  (Microsoft [Azure 培训工具包](https://www.microsoft.com/download/details.aspx?id=8396)。 包括 SQL 数据库的动手实验。
- [Windows AZURE SQL 数据库社区论坛](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [转到 Windows AZURE SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN) 。 Microsoft 模式和实践团队的一个全面的端到端方案。 介绍为何要迁移，以及如何从 SQL Server 迁移到 SQL 数据库。
-  (MSDN) [将 SQL Server 数据库迁移到 Windows AZURE SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) 。
- [SQL 数据库迁移向导](http://sqlazuremw.codeplex.com/)。 用于在 SQL 数据库之间迁移数据库的开源工具。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>在 SQL Server 和 Microsoft Azure SQL 数据库之间进行选择

- 将[SQL Server 与 Windows AZURE SQL Database](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet 站点) 进行比较。
- [数据迁移到 Windows AZURE SQL Database： MSDN)  (工具和技术](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) 。 包括将 SQL Server 与 SQL 数据库进行比较的部分，并提供有关何时从 SQL Server 迁移到 SQL 数据库的指导。
- [Windows AZURE SQL 数据库交付指南](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet 网站) 。
-  (MSDN) [ (Windows AZURE SQL 数据库) SQL Server 功能限制](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx)。
- [Windows Azure 表存储和 Windows AZURE SQL 数据库-比较和](https://msdn.microsoft.com/library/jj553018.aspx) 对照 MSDN)  (。 对于部署到 Windows Azure 的应用程序，Microsoft azure 表存储可能是 Windows Azure SQL 数据库的替代方案。 本主题将帮助您决定这两种方法。
- [Windows AZURE SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN) 。
- [指导原则和限制 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>使用 NoSQL 数据库管理系统

- [Windows Azure 数据服务](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure 站点) 。 请参阅 " [表服务功能指南](https://docs.microsoft.com/azure/) " 和 " **大数据** " 部分。
- [使用存储表、队列和 blob 的 ASP.NET 多层应用程序](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure 站点) 。 使用 Microsoft Azure 存储 NoSQL 表的可下载示例应用程序的端到端教程。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>在 ASP.NET 应用程序中使用 LINQ 查询

- ASP.NET)  (的[数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx#linq)。 包括 LINQ 的简介。
- [LINQ 培训视频](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagner 的博客) 。
- [包含动态 LINQ 资源链接的 ASP.NET 论坛线程](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>使用动态数据基架

- [动态数据项目模板](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN) 。 有关何时使用动态数据项目的指导。
- [ASP.NET 动态数据](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN) 。

<a id="securing"></a>

## <a name="securing-data-access"></a>保护数据访问

-  (MSDN) [保护 ASP.NET 中的数据访问](https://msdn.microsoft.com/library/ms178375.aspx)。
-  (MSDN) [实体框架)  (安全注意事项](https://msdn.microsoft.com/library/cc716760.aspx)。
- [如何：在 (MSDN) 使用数据源控件时保护连接字符串](https://msdn.microsoft.com/library/ms178372.aspx) 。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>优化数据访问性能

- [ASP.NET)  (性能概述](https://msdn.microsoft.com/library/cc668225.aspx) 。
- [ASP.NET](https://msdn.microsoft.com/library/xsbfdd8c.aspx))  (的缓存。
- ) MSDN ([提高 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787)。 此页面顶部有一个 "已停用的内容" 警告，但大多数信息仍是相关的，且没有可比较的更新资源。
- 提高 (MSDN) [SQL Server 性能](https://msdn.microsoft.com/library/ff647793)。 与上一个链接相同的注释。

另请参阅本主题前面的 [优化实体框架性能](#optimizingef) 。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>部署数据库

- [ASP.NET Web 部署-](aspnet-web-deployment-content-map.md) MSDN)  (推荐资源。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>通过 Web 服务访问数据

- [通过 Web 服务](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN) 访问数据。 有关何时使用 Web API 与 WCF 的指导。
- [与 ASP.NET Web API 入门](../web-api/index.md)。
-  (MSDN) [WCF 数据服务](https://msdn.microsoft.com/data/bb931106)。

<a id="additional"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET 数据访问常见问题](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN) 。
- [ASP.NET Web 窗体教程-数据](../web-forms/overview/data-access/index.md)。 其中的大多数教程相对陈旧;请确保阅读  [ASP.NET 数据访问选项](https://msdn.microsoft.com/library/ms178359.aspx) 和 [数据存储选项 (使用 Windows Azure) 生成 Real-World 的云应用程序 ](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) ，以便你不会过太多地进入不适合你的方案的数据访问方法。
- [ASP.NET MVC 内容映射](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET 网页教程-数据](../web-pages/overview/data/index.md)。
- [在 Visual Studio 中访问数据](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN) 。 提供类似于此内容映射的链接的列表，但侧重于 Visual Studio 而不是 ASP.NET。

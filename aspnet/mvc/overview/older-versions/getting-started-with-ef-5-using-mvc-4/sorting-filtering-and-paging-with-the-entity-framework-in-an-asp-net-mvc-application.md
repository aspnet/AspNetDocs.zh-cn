---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架进行排序、筛选和分页， (3 个) 中Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: c387223ec99e50fc8505e59697093b5bb482c58b
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985630"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>使用 ASP.NET MVC 应用程序中的实体框架进行排序、筛选和分页 (第3项，共10个) 

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你为实体的基本 CRUD 操作实现了一组网页 `Student` 。 在本教程中，您将向 **学生** 索引页添加排序、筛选和分页功能。 同时，还将创建一个执行简单分组的页面。

下图展示了完成操作后的页面外观。 列标题是用户可以单击以按该列排序的链接。 重复单击列标题可在升降排序顺序之间切换。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>向学生索引页添加列排序链接

若要将排序添加到 "学生索引" 页，您将更改 `Index` 控制器的方法， `Student` 并将代码添加到 " `Student` 索引" 视图中。

### <a name="add-sorting-functionality-to-the-index-method"></a>向 Index 方法添加排序功能

在 *Controllers\StudentController.cs* 中，将 `Index` 方法替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。 查询字符串值由 ASP.NET MVC 作为操作方法的参数提供。 该参数将是一个字符串，可为“Name”或“Date”，可选择后跟下划线和字符串“desc”来指定降序。 默认排序顺序为升序。

首次请求索引页时，没有任何查询字符串。 学生将按升序显示 `LastName` ，这是语句中的贯穿事例建立的默认设置 `switch` 。 当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。

使用这两个 `ViewBag` 变量，以便视图可以使用适当的查询字符串值配置列标题超链接：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

这些是三元语句。 第一个参数指定如果 `sortOrder` 参数为 null 或为空，则 `ViewBag.NameSortParm` 应将设置为 "名称 \_ desc"; 否则，它应设置为空字符串。 通过这两个语句，视图可如下设置列标题超链接：

| 当前排序顺序 | 姓氏超链接 | 日期超链接 |
| --- | --- | --- |
| 姓氏升序 | descending | ascending |
| 姓氏降序 | ascending | ascending |
| 日期升序 | ascending | descending |
| 日期降序 | ascending | ascending |

方法使用 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 指定排序所依据的列。 此代码在语句之前创建 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 变量 `switch` ，在语句中对其进行修改 `switch` ，并在 `ToList` 语句后调用方法 `switch` 。 当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。 在您 `IQueryable` 通过调用方法（如）将对象转换为集合之前，不会执行查询 `ToList` 。 因此，此代码将产生单个查询，该查询在语句之前不会执行 `return View` 。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>向 "学生索引" 视图添加列标题超链接

在 *Views\Student\Index.cshtml* 中，将 `<tr>` 标题行的和元素替换为 `<th>` 突出显示的代码：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

此代码使用属性中的信息 `ViewBag` 设置具有适当查询字符串值的超链接。

运行页面，然后单击 " **姓氏** " 和 " **注册日期** " 列标题，验证排序是否正常。

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

单击 **姓氏** 标题后，学生会按姓氏的降序顺序显示。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>向 "学生索引" 页添加搜索框

要向学生索引页添加筛选功能，需将文本框和提交按钮添加到视图，并在 `Index` 方法中做出相应的更改。 在文本框中输入一个字符串以在名字和姓氏字段中进行搜索。

### <a name="add-filtering-functionality-to-the-index-method"></a>向 Index 方法添加筛选功能

在 *Controllers\StudentController.cs* 中，将 `Index` 方法替换为以下代码 (突出显示更改) ：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

已向 `Index` 方法添加 `searchString` 参数。 还向 LINQ 语句添加了一个 `where` 子句，该子句仅选择其名字或姓氏中包含搜索字符串的学生。 将从要添加到 "索引" 视图中的文本框接收搜索字符串值。仅当存在要搜索的值时，才会执行添加 [where](https://msdn.microsoft.com/library/bb535040.aspx) 子句的语句。

> [!NOTE]
> 在许多情况下，你可以对实体框架实体集或作为内存中集合上的扩展方法调用同一方法。 结果通常是相同的，但在某些情况下可能会有所不同。 例如，将 `Contains` 空字符串传递给它时，方法的 .NET Framework 实现将返回所有行，但 SQL Server Compact 4.0 的实体框架提供程序将为空字符串返回零行。 因此，该示例中的代码 (将 `Where` 语句放入 `if` 语句) 确保为所有版本的 SQL Server 获取相同的结果。 此外，默认情况下，方法的 .NET Framework 实现会 `Contains` 执行区分大小写的比较，但实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。 因此，调用 `ToUpper` 方法以使测试明确区分大小写确保在稍后更改代码以使用存储库时结果不会更改，这将返回 `IEnumerable` 集合而不是 `IQueryable` 对象。 （在 `IEnumerable` 集合上调用 `Contains` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）

### <a name="add-a-search-box-to-the-student-index-view"></a>向“学生索引”视图添加搜索框

在 *Views\Student\Index.cshtml* 中，将突出显示的代码添加到开始标记之前，以便 `table` 创建标题、文本框和 **搜索** 按钮。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

运行页面，输入搜索字符串，并单击 " **搜索** " 以验证筛选是否正常工作。

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

请注意，该 URL 不包含 "a" 搜索字符串，这意味着，如果您将此页面做成书签，则在使用书签时，不会收到筛选后的列表。 在本教程后面的部分中，您将更改 " **搜索** " 按钮以使用筛选器条件的查询字符串。

## <a name="add-paging-to-the-students-index-page"></a>向学生索引页添加分页

若要将分页添加到 "学生索引" 页，你将首先安装 **PagedList** NuGet 包。 然后在方法中进行其他更改 `Index` ，并向视图添加分页链接 `Index` 。 **PagedList** 是 ASP.NET Mvc 的许多良好分页和排序包之一，这里的用途只是一个示例，而不是针对其他选项的建议。 下图显示了页面链接。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>安装 PagedList NuGet 包

NuGet **PagedList** 包会自动将 **PagedList** 包作为依赖项安装。 **PagedList** 包 `PagedList` 为和集合安装集合类型和扩展方法 `IQueryable` `IEnumerable` 。 扩展方法在或的集合中创建单个数据页 `PagedList` `IQueryable` `IEnumerable` ，而 `PagedList` 集合提供了几个便于分页的属性和方法。 **PagedList** 包安装显示分页按钮的分页帮助程序。

从 " **工具** " 菜单中，选择 " **Nuget 包管理器** "，然后 **管理解决方案的 nuget 包**。

在 " **管理 NuGet 包** " 对话框中，单击左侧的 " **联机** " 选项卡，然后在搜索框中输入 "分页"。 看到 **PagedList** 包时，单击 " **安装**"。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在 " **选择项目** " 框中，单击 **"确定"**。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>向 Index 方法添加分页功能

在 *Controllers\StudentController.cs* 中， `using` 为 `PagedList` 命名空间添加语句：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

将 `Index` 方法替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此代码会将 `page` 参数、当前排序顺序参数和当前筛选器参数添加到方法签名，如下所示：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

第一次显示页面时，或者如果用户没有单击分页或排序链接，所有参数都将为 NULL。 如果单击了页面链接，则该 `page` 变量将包含要显示的页码。

`A ViewBag` 属性提供当前排序顺序的视图，因为它必须包含在分页链接中，以便在分页时保持排序顺序相同：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

其他属性 `ViewBag.CurrentFilter` 提供当前筛选器字符串的视图。 此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。 如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。 在文本框中输入值并按 "提交" 按钮时，将更改搜索字符串。 在这种情况下， `searchString` 参数不为 null。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

在方法结束时， `ToPagedList` 学生对象上的扩展方法 `IQueryable` 会将学生查询转换为支持分页的集合类型中的一页学生。 然后，将一页学生传递到视图：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 方法需要一个页码。 这两个问号表示 [null 合并运算符](https://msdn.microsoft.com/library/ms173224.aspx)。 NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>向 "学生索引" 视图添加寻呼链接

在 *Views\Student\Index.cshtml* 中，将现有代码替换为以下代码：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

页面顶部的 `@model` 语句指定视图现在获取的是 `PagedList` 对象，而不是 `List` 对象。

的 `using` 语句 `PagedList.Mvc` 提供对分页按钮的 MVC 帮助器的访问。

代码使用 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 的重载，以允许它指定 [FormMethod](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

默认 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 使用 POST 提交窗体数据，这意味着参数将在 HTTP 消息正文中传递，而不是作为查询字符串在 URL 中传递。 当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。 [使用 HTTP GET 的 W3C 准则](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定当操作不会导致更新时，应使用 get。

文本框使用当前的搜索字符串进行初始化，因此，当您单击新页时，您可以看到当前搜索字符串。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

显示当前页面和总页数。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

如果没有要显示的页，则显示 "页 0/0"。  (在这种情况下，页号大于页计数，因为 `Model.PageNumber` 为1，并且 `Model.PageCount` 为0。 ) 

页面按钮由 `PagedListPager` 帮助器显示：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`帮助程序提供了许多可自定义的选项，包括 url 和样式。 有关详细信息，请参阅 GitHub 站点上的 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。

运行页面。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

单击不同排序顺序的分页链接，以确保分页正常工作。 然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>创建显示学生统计信息的 "关于" 页面

对于 Contoso 大学网站的“关于”页，将显示每个注册日期注册了多少名学生。 这需要对组进行分组和简单计算。 若要完成此操作，需要执行以下操作：

- 为需要传递给视图的数据创建一个视图模型类。
- 修改 `About` 控制器中的方法 `Home` 。
- 修改 `About` 视图。

### <a name="create-the-view-model"></a>创建视图模型

创建 *viewmodel* 文件夹。 在该文件夹中，添加一个类文件 *EnrollmentDateGroup.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改主控制器

在 *HomeController.cs* 中，在 `using` 文件顶部添加以下语句：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

直接在类的左大括号之后为数据库上下文添加类变量：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

将 `About` 方法替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。

添加 `Dispose` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改“关于”视图

将 *Views\Home\About.cshtml* 文件中的代码替换为以下代码：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

运行应用，并单击 " **关于** " 链接。 表格中会显示每个注册日期的学生计数。

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>可选：将应用部署到 Microsoft Azure

到目前为止，你的应用程序已在本地 IIS Express 开发计算机上运行。 要使其可供其他人通过 Internet 使用，你必须将其部署到 web 托管提供商。 在本教程的此可选部分中，你会将其部署到 Microsoft Azure 网站。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>使用 Code First 迁移部署数据库

若要部署数据库，你将使用 Code First 迁移。 当你创建用于配置从 Visual Studio 部署的设置的发布配置文件时，你将选择一个标记为 **"执行 Code First 迁移 (在应用程序启动) 上运行** 的复选框。 此设置会导致部署过程在目标服务器上自动配置应用程序 *Web.config* 文件，使 Code First 使用 `MigrateDatabaseToLatestVersion` 初始值设定项类。

在部署过程中，Visual Studio 不会对数据库执行任何操作。 部署后，当部署的应用程序首次访问数据库时，Code First 会自动创建数据库，或将数据库架构更新到最新版本。 如果应用程序实现了迁移 `Seed` 方法，则该方法将在创建数据库或更新架构之后运行。

迁移 `Seed` 方法插入测试数据。 如果要部署到生产环境，则必须更改 `Seed` 方法，使其只插入要插入到生产数据库中的数据。 例如，在您的当前数据模型中，您可能希望在开发数据库中有真实的课程，但实际的学生。 你可以编写一个 `Seed` 方法，用于在开发中加载，然后在部署到生产环境之前注释掉虚构的学生。 或者，您可以编写一个 `Seed` 方法以仅加载课程，并使用应用程序的 UI 手动输入测试数据库中的虚构学生。

### <a name="get-a-windows-azure-account"></a>获取 Microsoft Azure 帐户

需要一个 Microsoft Azure 帐户。 如果还没有，只需花费几分钟就能创建一个免费试用帐户。 有关详细信息，请参阅 [Windows Azure 免费试用版](https://azure.microsoft.com/free/dotnet/)。

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>在 Microsoft Azure 中创建网站和 SQL 数据库

您的 Microsoft Azure 网站将在共享宿主环境中运行，这意味着它将在与其他 Microsoft Azure 客户端共享的虚拟机 (VM) 上运行。 共享宿主环境是一种在云中开始工作的低成本方式。 稍后，如果你的 Web 流量增加，则应用程序可进行扩展，通过在专用 VM 上运行来满足需要。 如果您需要一个更复杂的体系结构，则可迁移到 Microsoft Azure 云服务。 云服务在你可根据自己的需求进行配置的专用 VM 上运行。

Microsoft Azure SQL 数据库是根据 SQL Server 技术构建的基于云的关系数据库服务。 与 SQL Server 一起使用的工具和应用程序也可用于 SQL 数据库。

1. 在 [Windows Azure 管理门户](https://manage.windowsazure.com/)中，单击左侧选项卡中的 " **网站** "，然后单击 " **新建**"。

    ![管理门户中的“新建”按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. 单击 " **自定义创建**"。

    ![管理门户中的“与数据库一起创建”链接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   " **新建网站-自定义创建** " 向导将打开。
3. 在向导的 " **新建** 网站" 步骤中，在 " **URL** " 框中输入要用作应用程序的唯一 URL 的字符串。 完整的 URL 将包含你在此处输入的内容和你在文本框旁边看到的后缀。 图中显示 "ConU"，但该 URL 可能已被使用，因此你必须选择其他 URL。

    ![管理门户中的“与数据库一起创建”链接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. 在 " **区域** " 下拉列表中，选择靠近你的区域。 此设置指定您的网站将在哪个数据中心运行。
5. 在 " **数据库** " 下拉列表中，选择 " **创建免费的 20 MB SQL 数据库**"。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. 在 " **数据库连接字符串名称**" 中，输入 *SchoolContext*。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 单击对话框底部的向右箭头。 向导将前进到 " **数据库设置** " 步骤。
8. 在 " **名称** " 框中，输入 *ContosoUniversityDB*。
9. 在 " **服务器** " 框中，选择 " **新建 SQL 数据库服务器**"。 或者，如果你以前创建了一个服务器，则可以从下拉列表中选择该服务器。
10. 输入管理员的 **登录名** 和 **密码**。 如果选择了“新建 SQL 数据库服务器”，则在此处不要输入现有名称和密码。应输入新的名称和密码，现在定义的名称和密码会在以后访问数据库时使用。 如果选择了之前创建的服务器，则需输入该服务器的凭据。 对于本教程，不选中 " **_高级_*_" 复选框。您可以使用 _*_高级_** 选项设置数据库 [排序规则](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。
11. 选择为网站选择的相同 **区域** 。
12. 单击框右下角的复选标记以指示你已完成。   
  
    ![“新建网站 - 与数据库一起创建”向导的“数据库设置”步骤](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    下图显示了使用现有 SQL Server 和登录名。   
  
    ![“新建网站 - 与数据库一起创建”向导的“数据库设置”步骤](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    管理门户返回到 "网站" 页面，" **状态** " 列显示正在创建该网站。 一段时间后 (通常不到一分钟) ，" **状态** " 列会显示已成功创建网站。 在左侧的导航栏中，你的帐户中拥有的网站的数量会显示在 **"网站" 图标旁边** ，而数据库的数量会显示在 " **SQL 数据库** " 图标旁边。

## <a name="deploy-the-application-to-windows-azure"></a>将应用程序部署到 Microsoft Azure

1. 在 Visual Studio 中，在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。  
  
    ![项目上下文菜单中的“发布”](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. 在 "**发布 Web** " 向导的 "**配置文件**" 选项卡中，单击 "**导入**"。  
  
    ![导入发布设置](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. 如果您之前未在 Visual Studio 中添加 Microsoft Azure 订阅，请执行下列步骤。 在这些步骤中，您将添加订阅，以便 **从 Microsoft Azure 网站导入** 下的下拉列表将包含您的网站。

    a. 在 " **导入发布配置文件** " 对话框中，单击 " **从 Microsoft Azure 网站导入**"，然后单击 " **添加 microsoft azure 订阅**"。

    ![添加 Microsoft Azure 订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. 在 " **导入 Microsoft Azure 订阅** " 对话框中，单击 " **下载订阅文件**"。

    ![下载订阅文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 在浏览器窗口中，保存 *.publishsettings* 文件。

    ![下载 .publishsettings 文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 安全性- *.publishsettings* 文件包含用于管理 microsoft Azure 订阅和服务 (未编码) 的凭据。 此文件的最佳安全方案是，将其暂时存储在源目录的外部 (例如，在 *Libraries\Documents* 文件夹中) ，然后在导入完成后将其删除。 获得文件访问权的恶意用户 `.publishsettings` 可以编辑、创建和删除您的 Microsoft Azure 服务。

    d. 在 " **导入 Microsoft Azure 订阅** " 对话框中，单击 " **浏览** " 并导航到 *.publishsettings* 文件。

    ![下载订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. 单击“导入”。

    ![进口](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. 在 " **导入发布配置文件** " 对话框中，选择 " **从 Microsoft Azure 网站导入**"，从下拉列表中选择你的网站，然后单击 **"确定"**。  
  
    ![导入发布配置文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. 在 " **连接** " 选项卡中，单击 " **验证连接** " 确保设置正确。  
  
    ![验证连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 验证连接后，" **验证连接** " 按钮旁边会显示一个绿色复选标记。 单击 **“下一步”** 。  
  
    ![验证成功的连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. 打开 " **SchoolContext** " 下的 "**远程连接字符串**" 下拉列表，然后选择您创建的数据库的连接字符串。
8. 选择 **"执行" Code First 迁移 (在应用程序启动) 运行**。
9. 取消选中 "在运行时对 **UserContext (DefaultConnection)****使用此连接字符串**，因为此应用程序未使用成员资格数据库。   
  
    ![“设置”选项卡](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. 单击 **“下一步”** 。
11. 在 " **预览** " 选项卡中，单击 " **开始预览**"。  
  
    ![“预览”选项卡中的“开始预览”按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    该选项卡会显示将复制到服务器的文件的列表。 显示预览并不是发布应用程序所必需的，但它是一个需要了解的很有用的功能。 在本例中，你不需要对显示的文件列表执行任何操作。 下次部署该应用程序时，此列表中仅包含已更改的文件。  
  
    ![“开始预览”文件输出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. 单击“发布” 。  
    Visual Studio 开始执行将文件复制到 Microsoft Azure 服务器的过程。
13. “输出”窗口会显示已执行的部署操作并报告部署的成功完成。  
  
    ![报告部署成功的输出窗口](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 成功完成部署后，默认浏览器会自动打开并指向已部署网站的 URL。  
    创建的应用程序现在云中运行。 单击 "学生" 选项卡。  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

此时，你的 *SchoolContext* 数据库已在 WINDOWS Azure SQL 数据库中创建，因为你选择了 **"执行 Code First 迁移 (在应用启动) 上运行**。 已在已部署的网站中更改 *Web.config* 文件，以便 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始值设定项在第一次读取或写入数据库中的数据时运行 (在您选择 " **学生** " 选项卡) 时，会发生这种情况：

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

部署过程还会创建一个新的连接字符串， *(SchoolContext \_ DatabasePublish*) 用于更新数据库架构和播种数据库的 Code First 迁移。

![Database_Publish 连接字符串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection* 连接字符串适用于在本教程中未使用的成员资格数据库 () 。 *SchoolContext* 连接字符串是针对 ContosoUniversity 数据库的。

可以在 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config* 的计算机上查找 Web.config 文件的已部署版本。你可以通过使用 FTP 访问已部署的 *Web.config* 文件本身。 有关说明，请参阅 [使用 Visual Studio 进行 ASP.NET Web 部署：部署代码更新](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 按照以 "使用 FTP 工具" 开头的说明操作，需要以下三项内容： FTP URL、用户名和密码。 "

> [!NOTE]
> Web 应用不会实现安全性，因此查找 URL 的任何人都可以更改数据。 有关如何保护网站的说明，请参阅将 [包含成员资格、OAuth 和 SQL 数据库的 secure ASP.NET MVC 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)网站。 可以通过使用 Microsoft Azure 管理门户或 Visual Studio 中的 **服务器资源管理器** 阻止其他人使用该站点来停止站点。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First 初始值设定项

在 "部署" 部分中，你看到了正在使用的 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始值设定项。 Code First 还提供了可使用的其他初始值设定项（包括默认) 、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx)和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx) (的[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) ）。 `DropCreateAlways`初始值设定项可用于设置单元测试的条件。 您还可以编写自己的初始值设定项，如果您不想等到应用程序从数据库中读取或写入数据，则可以显式调用初始值设定项。 有关初始值设定项的全面说明，请参阅本书 [编程实体框架：](http://shop.oreilly.com/product/0636920022220.do) 通过 Julie Lerman 和 Rowan 莎莎 Code First 的第6章。

## <a name="summary"></a>总结

在本教程中，您已了解如何创建数据模型并实现基本的 CRUD、排序、筛选、分页和分组功能。 在下一教程中，您将通过扩展数据模型开始查看更高级的主题。

可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [下一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

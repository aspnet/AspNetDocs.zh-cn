---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: 检查 ) 的编辑方法和编辑视图 (Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 .。。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: baa300c66bfae9fe602a8fe597e21b0abbaf3a63
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044982"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>检查 Edit 方法和编辑视图 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。
> 
> 
> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些 [程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0) (运行时 + 工具支持) 
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含 c # 源代码的 Visual Web Developer 项目。 [下载 c # 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的 [Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md) 。

在本部分中，你将检查电影控制器的生成的操作方法和视图。 然后，将添加自定义搜索页面。

运行应用程序，并通过将 `Movies` */Movies* 追加到浏览器地址栏中的 URL 来浏览到控制器。 将鼠标指针停留在 **编辑** 链接上可查看它所链接到的 URL。

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

**编辑**链接由 `Html.ActionLink` *Views\Movies\Index.cshtml*视图中的方法生成：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html`对象是一个使用基类上的属性公开的帮助器 `WebViewPage` 。 `ActionLink`利用帮助器的方法，可以轻松地动态生成链接到控制器操作方法的 HTML 超链接。 方法的第一个参数 `ActionLink` 是要呈现的链接文本 (例如 `<a>Edit Me</a>`) 。 第二个参数是要调用的操作方法的名称。 最后一个自变量是在此示例中生成路由数据 (的 [匿名对象](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) ，ID 为 4) 。

上图中显示的生成链接是 `http://localhost:xxxxx/Movies/Edit/4` 。 默认路由采用 URL 模式 `{controller}/{action}/{id}` 。 因此，ASP.NET 将转换为 `http://localhost:xxxxx/Movies/Edit/4` `Edit` 控制器操作方法的请求，该方法的 `Movies` 参数 `ID` 等于4。

你还可以使用查询字符串传递操作方法参数。 例如，URL 还将 `http://localhost:xxxxx/Movies/Edit?ID=4` 4 的参数传递 `ID` 给 `Edit` 控制器的操作方法 `Movies` 。

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

打开 `Movies` 控制器。 下面显示了这两个 `Edit` 操作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

请注意第二个 `Edit` 操作方法的前面是 `HttpPost` 特性。 此特性指定只能 `Edit` 为 POST 请求调用方法的重载。 您可以将属性应用于 `HttpGet` 第一个编辑方法，但这并不是必需的，因为它是默认值。  (将引用隐式分配属性作为方法的操作方法 `HttpGet` `HttpGet` 。 ) 

`HttpGet` `Edit` 方法采用 "影片 ID" 参数，使用实体框架方法查找电影 `Find` ，并将所选电影返回到 "编辑" 视图。 当基架系统创建“编辑”视图时，它会检查 `Movie` 类并创建代码为类的每个属性呈现 `<label>` 和 `<input>` 元素。 下面的示例演示生成的编辑视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

请注意视图模板如何 `@model MvcMovie.Models.Movie` 在文件顶部包含一条语句，这会指定该视图要求视图模板的模型为类型 `Movie` 。

基架代码使用多个 *帮助器方法* 来简化 HTML 标记。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)帮助器将显示字段的名称， ( "Title"、"ReleaseDate"、"流派" 或 "Price" ) 。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)帮助器显示 HTML `<input>` 元素。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)帮助器将显示与该属性相关联的所有验证消息。

运行应用程序并导航到 */Movies* URL。 点击“编辑”链接。 在浏览器中查看页面的源。 页面中的 HTML 类似于下面的示例。 为清楚起见，已排除菜单标记 () 

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

`<input>`元素位于一个 HTML 元素中， `<form>` 其 `action` 特性设置为发布到 */Movies/Edit* URL。 单击 " **编辑** " 按钮后，窗体数据将发布到服务器。

## <a name="processing-the-post-request"></a>处理 POST 请求

以下列表显示了 `Edit` 操作方法的 `HttpPost` 版本。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

ASP.NET framework 模型联编程序使用已发布的窗体值并创建 `Movie` 作为参数传递的对象 `movie` 。 此 `ModelState.IsValid` 代码中的检查将验证在表单中提交的数据是否可用于修改 `Movie` 对象。 如果数据有效，则代码会将电影数据保存到实例的 `Movies` 集合中 `MovieDBContext` 。 然后，该代码通过调用的方法将新的电影数据保存到数据库 `SaveChanges` `MovieDBContext` 中，这将保持对数据库的更改。 保存数据后，代码会将用户重定向到 `Index` 类的操作方法 `MoviesController` ，这会使已更新的电影显示在电影列表中。

如果已发布的值无效，则会在窗体中重新显示这些值。 `Html.ValidationMessageFor`*编辑.* view 模板中的帮助器负责显示适当的错误消息。

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **有关区域设置的注释** 如果通常使用非英语区域设置，请参阅 [支持使用非英语区域设置的 ASP.NET MVC 3 验证。](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)

## <a name="making-the-edit-method-more-robust"></a>使编辑方法更可靠

`HttpGet` `Edit` 基架系统生成的方法不会检查传递给它的 ID 是否有效。 如果用户删除 URL (的 ID 段 `http://localhost:xxxxx/Movies/Edit`) ，将显示以下错误：

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

用户还可以传递数据库中不存在的 ID，例如 `http://localhost:xxxxx/Movies/Edit/1234` 。 您可以对操作方法进行两次更改 `HttpGet` `Edit` 以解决此限制。 首先，将 `ID` 参数更改为在未显式传递 ID 时将默认值设置为零。 您还可以检查该 `Find` 方法是否确实找到了电影，然后再将 movie 对象返回到视图模板。 更新的 `Edit` 方法如下所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

如果未找到电影，则 `HttpNotFound` 调用方法。

所有 `HttpGet` 方法都遵循类似的模式。 它们获取影片对象 (或对象列表（在) 情况下）， `Index` 并将模型传递给视图。 `Create`方法将空电影对象传递到 "创建" 视图。 在方法的 `HttpPost` 重载中，创建、编辑、删除或以其他方式修改数据的所有方法都执行此操作。 修改 HTTP GET 方法中的数据存在安全风险，如博客文章 [ASP.NET MVC Tip #46 中所述–不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的数据也违反了 HTTP 最佳做法和体系结构 REST 模式，该模式指定 GET 请求不应更改应用程序的状态。 换句话说，执行 GET 操作应该是没有任何副作用的安全操作。

## <a name="adding-a-search-method-and-search-view"></a>添加搜索方法和搜索视图

在本部分中，你将添加一个 `SearchIndex` 操作方法，该方法允许你按流派或名称搜索电影。 这将使用 */Movies/SearchIndex* URL 提供。 请求将显示一个 HTML 窗体，其中包含用户可以填充的输入元素，以便搜索电影。 当用户提交窗体时，操作方法将获取用户发布的搜索值，并使用这些值来搜索数据库。

## <a name="displaying-the-searchindex-form"></a>显示 SearchIndex 窗体

首先 `SearchIndex` 向现有类添加操作方法 `MoviesController` 。 方法将返回包含 HTML 窗体的视图。 代码如下：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

方法的第一行 `SearchIndex` 创建以下 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 查询来选择电影：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

此时将定义该查询，但尚未针对数据存储区运行该查询。

如果 `searchString` 参数包含一个字符串，则使用以下代码修改电影查询以筛选搜索字符串的值：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

LINQ 查询在定义或通过调用方法（如或）进行修改时，不会执行 `Where` `OrderBy` 。 相反，查询执行延迟，这意味着表达式的计算会延迟，直到实际循环访问它的实际值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 调用方法。 在此 `SearchIndex` 示例中，在 SearchIndex 视图中执行查询。 有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。

现在，您可以实现 `SearchIndex` 将向用户显示窗体的视图。 在方法内右键单击 `SearchIndex` ，然后单击 " **添加视图**"。 在 " **添加视图** " 对话框中，指定要将 `Movie` 对象作为其模型类传递到视图模板。 在 **基架模板** 列表中，选择 " **列表**"，然后单击 " **添加**"。

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

单击 " **添加** " 按钮时，会创建 *Views\Movies\SearchIndex.cshtml* 视图模板。 由于在**基架模板**列表中选择了 "**列表**"，Visual Web Developer 会自动生成 (基架) 该视图中的某些默认内容。 基架创建了一个 HTML 窗体。 它检查 `Movie` 类并创建了代码，以便为 `<label>` 类的每个属性呈现元素。 下面的列表显示了生成的 "创建" 视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

运行应用程序并导航到 */Movies/SearchIndex*。 将查询字符串（如 `?searchString=ghost`）追加到 URL。 筛选的电影将显示出来。

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

如果将方法的签名更改 `SearchIndex` 为具有一个名为的参数 `id` ，则该 `id` 参数将与 `{id}` *global.asax* 文件中设置的默认路由的占位符匹配。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

修改后的 `SearchIndex` 方法如下所示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

但是，不能指望用户在每次要搜索电影时都修改 URL。 现在，你将添加 UI 来帮助他们筛选电影。 如果更改了方法的签名 `SearchIndex` 以测试如何传递路由绑定 ID 参数，请将其更改回，使 `SearchIndex` 方法使用名为的字符串参数 `searchString` ：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

打开 *Views\Movies\SearchIndex.cshtml* 文件，并在后面 `@Html.ActionLink("Create New", "Create")` 添加以下内容：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

下面的示例显示了 *Views\Movies\SearchIndex.cshtml* 文件的一部分，其中包含添加的筛选标记。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

`Html.BeginForm`帮助器创建开始 `<form>` 标记。 `Html.BeginForm`当用户通过单击 "**筛选器**" 按钮提交窗体时，帮助器会使窗体发布到其自身。

运行应用程序并尝试搜索电影。

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

`HttpPost`方法没有重载 `SearchIndex` 。 不需要该方法，因为该方法不会更改应用程序的状态，只是对数据进行筛选。

可添加以下 `HttpPost SearchIndex` 方法。 在这种情况下，操作调用程序将与 `HttpPost SearchIndex` 方法匹配， `HttpPost SearchIndex` 方法将运行，如下图所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

但是，即使添加 `SearchIndex` 方法的 `HttpPost` 版本，其实现方式也受到限制。 假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。 请注意，HTTP POST 请求的 URL 与 GET 请求的 URL (localhost： xxxxx/电影/SearchIndex) 相同--URL 本身中没有搜索信息。 目前，搜索字符串信息将作为窗体字段值发送到服务器。 这意味着你无法捕获该搜索信息以在 URL 中将其书签或发送给朋友。

解决方案是使用 `BeginForm` 的重载，该重载指定 POST 请求应将搜索信息添加到 URL，并且应路由到该方法的 HttpGet 版本 `SearchIndex` 。 将现有的无参数 `BeginForm` 方法替换为以下内容：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

现在，在提交搜索时，URL 包含搜索查询字符串。 即使具备 `HttpPost SearchIndex` 方法，搜索也将转到 `HttpGet SearchIndex` 操作方法。

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>按流派添加搜索

如果已添加该 `HttpPost` 方法的版本 `SearchIndex` ，请立即将其删除。

接下来，你将添加一项功能，使用户能够按流派搜索电影。 将 `SearchIndex` 方法替换为以下代码：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

此版本的 `SearchIndex` 方法采用其他参数，即 `movieGenre` 。 前几行代码创建一个 `List` 对象，用于保存数据库中的电影流派。

下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

该代码使用 `AddRange` 泛型集合的方法 `List` 将所有不同的流派添加到列表中。  (没有 `Distinct` 修饰符，将添加重复的流派，例如，在我们的示例) 中添加了两次。 然后，代码会在对象中存储流派列表 `ViewBag` 。

下面的代码演示如何检查 `movieGenre` 参数。 如果不为空，则代码会进一步限制影片查询，以将所选电影限制为指定的流派。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>将标记添加到 SearchIndex 视图以支持按流派搜索

将 `Html.DropDownList` helper 添加到 *Views\Movies\SearchIndex.cshtml* 文件中的 `TextBox` 帮助器之前。 完成的标记如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

运行应用程序并浏览到 */Movies/SearchIndex*。 尝试按流派、电影名称和这两个条件进行搜索。

本部分介绍了由框架生成的 CRUD 操作方法和视图。 你创建了一个搜索操作方法和视图，它允许用户按电影标题和流派进行搜索。 在下一部分中，你将了解如何将属性添加到 `Movie` 模型，以及如何添加将自动创建测试数据库的初始化表达式。

> [!div class="step-by-step"]
> [上一页](accessing-your-models-data-from-a-controller.md)
> [下一页](adding-a-new-field.md)

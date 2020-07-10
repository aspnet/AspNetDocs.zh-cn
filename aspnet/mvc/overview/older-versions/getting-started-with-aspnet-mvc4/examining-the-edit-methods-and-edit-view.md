---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: 检查 "编辑" 方法和 "编辑视图" |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 .。。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162944"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>检查 Edit 方法和编辑视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本部分中，你将检查电影控制器的生成的操作方法和视图。 然后，将添加自定义搜索页面。

运行应用程序，并通过将 `Movies` */Movies*追加到浏览器地址栏中的 URL 来浏览到控制器。 将鼠标指针停留在**编辑**链接上可查看它所链接到的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**编辑**链接由 `Html.ActionLink` *Views\Movies\Index.cshtml*视图中的方法生成：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`对象是一个使用[WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基类上的属性公开的帮助器。 `ActionLink`利用帮助器的方法，可以轻松地动态生成链接到控制器操作方法的 HTML 超链接。 方法的第一个参数 `ActionLink` 是要呈现的链接文本 (例如 `<a>Edit Me</a>`) 。 第二个参数是要调用的操作方法的名称。 最后一个自变量是在此示例中生成路由数据 (的[匿名对象](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，ID 为 4) 。

上图中显示的生成链接是 `http://localhost:xxxxx/Movies/Edit/4` 。 在*应用 \_ Start\RouteConfig.cs*中建立的默认路由 () 采用 URL 模式 `{controller}/{action}/{id}` 。 因此，ASP.NET 将转换为 `http://localhost:xxxxx/Movies/Edit/4` `Edit` 控制器操作方法的请求，该方法的 `Movies` 参数 `ID` 等于4。 从*应用程序 \_ Start\RouteConfig.cs*文件中检查以下代码。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

你还可以使用查询字符串传递操作方法参数。 例如，URL 还将 `http://localhost:xxxxx/Movies/Edit?ID=4` 4 的参数传递 `ID` 给 `Edit` 控制器的操作方法 `Movies` 。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

打开 `Movies` 控制器。 下面显示了这两个 `Edit` 操作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

请注意第二个 `Edit` 操作方法的前面是 `HttpPost` 特性。 此特性指定只能 `Edit` 为 POST 请求调用方法的重载。 您可以将属性应用于 `HttpGet` 第一个编辑方法，但这并不是必需的，因为它是默认值。  (将引用隐式分配属性作为方法的操作方法 `HttpGet` `HttpGet` 。 ) 

`HttpGet` `Edit` 方法采用 "影片 ID" 参数，使用实体框架方法查找电影 `Find` ，并将所选电影返回到 "编辑" 视图。 如果在没有参数的情况下调用方法，ID 参数将指定[默认值](https://msdn.microsoft.com/library/dd264739.aspx)零 `Edit` 。 如果找不到电影，则返回[HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 。 当基架系统创建“编辑”视图时，它会检查 `Movie` 类并创建代码为类的每个属性呈现 `<label>` 和 `<input>` 元素。 下面的示例演示生成的编辑视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

请注意视图模板如何 `@model MvcMovie.Models.Movie` 在文件顶部包含一条语句，这会指定该视图要求视图模板的模型为类型 `Movie` 。

基架代码使用多个*帮助器方法*来简化 HTML 标记。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)帮助器显示 (&quot; 标题 &quot; 、 &quot; ReleaseDate &quot; 、 &quot; 流派 &quot; 或 &quot; 价格 &quot;) 的字段的名称。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)帮助器呈现一个 HTML `<input>` 元素。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)帮助器将显示与该属性相关联的所有验证消息。

运行应用程序并导航到 */Movies* URL。 点击“编辑”链接。 在浏览器中查看页面的源。 窗体元素的 HTML 如下所示。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`元素位于一个 HTML 元素中， `<form>` 其 `action` 特性设置为发布到 */Movies/Edit* URL。 单击 "**编辑**" 按钮后，窗体数据将发布到服务器。

## <a name="processing-the-post-request"></a>处理 POST 请求

以下列表显示了 `Edit` 操作方法的 `HttpPost` 版本。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 模型联编](https://msdn.microsoft.com/magazine/hh781022.aspx)程序使用已发布的窗体值并创建 `Movie` 作为参数传递的对象 `movie` 。 `ModelState.IsValid` 方法验证表单中提交的数据是否可以用于修改（编辑或更新）`Movie` 对象。 如果数据有效，则会将电影数据保存到 `Movies` 实例) 的集合中 `db(MovieDBContext` 。 通过调用的方法，将新的电影数据保存到数据库中 `SaveChanges` `MovieDBContext` 。 保存数据后，代码会将用户重定向到 `Index` 类的操作方法 `MoviesController` ，后者显示电影集合的，其中包括刚刚做出的更改。

如果已发布的值无效，则会在窗体中重新显示这些值。 `Html.ValidationMessageFor`*编辑.* view 模板中的帮助器负责显示适当的错误消息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 若要支持使用逗号 (的非英语区域设置的 jQuery 验证 &quot; ， &quot;) 对于小数点，必须包括*globalize.js* ，并从 (和 JavaScript ) 使用特定*区域性/globalize.cultures.js*文件 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) `Globalize.parseFloat` 。 下面的代码演示对 Views\Movies\Edit.cshtml 文件所做的修改，以便使用 &quot; fr-fr &quot; 区域性：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

小数字段可能需要逗号，而不是小数点。 作为临时修补程序，你可以将全球化元素添加到项目根 web.config 文件中。 下面的代码演示将区域性设置为美国英语的全球化元素。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

所有 `HttpGet` 方法都遵循类似的模式。 它们获取影片对象 (或对象列表（在) 情况下）， `Index` 并将模型传递给视图。 `Create`方法将空电影对象传递到 "创建" 视图。 在方法的 `HttpPost` 重载中，创建、编辑、删除或以其他方式修改数据的所有方法都执行此操作。 修改 HTTP GET 方法中的数据存在安全风险，如博客文章[ASP.NET MVC Tip #46 中所述–不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的数据也违反了 HTTP 最佳做法和体系结构[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式，该模式指定 GET 请求不应更改应用程序的状态。 换句话说，执行 GET 操作应是没有任何隐患的安全操作，也不会修改持久数据。

## <a name="adding-a-search-method-and-search-view"></a>添加搜索方法和搜索视图

在本部分中，你将添加一个 `SearchIndex` 操作方法，该方法允许你按流派或名称搜索电影。 这将使用 */Movies/SearchIndex* URL 提供。 请求将显示一个 HTML 窗体，其中包含用户可以输入的输入元素，以便搜索电影。 当用户提交窗体时，操作方法将获取用户发布的搜索值，并使用这些值来搜索数据库。

## <a name="displaying-the-searchindex-form"></a>显示 SearchIndex 窗体

首先 `SearchIndex` 向现有类添加操作方法 `MoviesController` 。 方法将返回包含 HTML 窗体的视图。 代码如下：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

方法的第一行 `SearchIndex` 创建以下[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询来选择电影：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

此时将定义该查询，但尚未针对数据存储区运行该查询。

如果 `searchString` 参数包含一个字符串，则使用以下代码修改电影查询以筛选搜索字符串的值：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

上面的 `s => s.Title` 代码是 [Lambda 表达式](https://msdn.microsoft.com/library/bb397687.aspx)。 Lambda 在基于方法的[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询中用作标准查询运算符方法的参数，如以上代码中使用的[Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)方法。 LINQ 查询在定义或通过调用方法（如或）进行修改时，不会执行 `Where` `OrderBy` 。 相反，查询执行延迟，这意味着表达式的计算会延迟，直到实际循环访问它的实际值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 调用方法。 在此 `SearchIndex` 示例中，在 SearchIndex 视图中执行查询。 有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。

现在，您可以实现 `SearchIndex` 将向用户显示窗体的视图。 在方法内右键单击 `SearchIndex` ，然后单击 "**添加视图**"。 在 "**添加视图**" 对话框中，指定要将 `Movie` 对象作为其模型类传递到视图模板。 在**基架模板**列表中，选择 "**列表**"，然后单击 "**添加**"。

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

单击 "**添加**" 按钮时，会创建*Views\Movies\SearchIndex.cshtml*视图模板。 由于你在**基架模板**列表中选择了 "**列表**"，Visual Studio 会自动生成 (基架) 该视图中的某些默认标记。 基架创建了一个 HTML 窗体。 它检查 `Movie` 类并创建了代码，以便为 `<label>` 类的每个属性呈现元素。 下面的列表显示了生成的 "创建" 视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

运行应用程序并导航到 */Movies/SearchIndex*。 将查询字符串（如 `?searchString=ghost`）追加到 URL。 筛选的电影将显示出来。

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

如果将方法的签名更改 `SearchIndex` 为具有一个名为的参数 `id` ，则该 `id` 参数将与 `{id}` *global.asax*文件中设置的默认路由的占位符匹配。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

原始方法如下所 `SearchIndex` 示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

修改后的 `SearchIndex` 方法如下所示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

但是，不能指望用户在每次要搜索电影时都修改 URL。 现在，你将添加 UI 来帮助他们筛选电影。 如果更改了方法的签名 `SearchIndex` 以测试如何传递路由绑定 ID 参数，请将其更改回，使 `SearchIndex` 方法使用名为的字符串参数 `searchString` ：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

打开*Views\Movies\SearchIndex.cshtml*文件，并在后面 `@Html.ActionLink("Create New", "Create")` 添加以下内容：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

下面的示例显示了*Views\Movies\SearchIndex.cshtml*文件的一部分，其中包含添加的筛选标记。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`帮助器创建开始 `<form>` 标记。 `Html.BeginForm`当用户通过单击 "**筛选器**" 按钮提交窗体时，帮助器会使窗体发布到其自身。

运行应用程序并尝试搜索电影。

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

`HttpPost`方法没有重载 `SearchIndex` 。 不需要该方法，因为该方法不会更改应用程序的状态，只是对数据进行筛选。

可添加以下 `HttpPost SearchIndex` 方法。 在这种情况下，操作调用程序将与 `HttpPost SearchIndex` 方法匹配， `HttpPost SearchIndex` 方法将运行，如下图所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

但是，即使添加 `SearchIndex` 方法的 `HttpPost` 版本，其实现方式也受到限制。 假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。 请注意，HTTP POST 请求的 URL 与 GET 请求的 URL (localhost： xxxxx/电影/SearchIndex) 相同--URL 本身中没有搜索信息。 目前，搜索字符串信息将作为窗体字段值发送到服务器。 这意味着你无法捕获该搜索信息以在 URL 中将其书签或发送给朋友。

解决方案是使用 `BeginForm` 的重载，该重载指定 POST 请求应将搜索信息添加到 URL，并且应将其路由到该方法的 HttpGet 版本 `SearchIndex` 。 将现有的无参数 `BeginForm` 方法替换为以下内容：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

现在，在提交搜索时，URL 包含搜索查询字符串。 即使具备 `HttpPost SearchIndex` 方法，搜索也将转到 `HttpGet SearchIndex` 操作方法。

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>按流派添加搜索

如果已添加该 `HttpPost` 方法的版本 `SearchIndex` ，请立即将其删除。

接下来，你将添加一项功能，使用户能够按流派搜索电影。 将 `SearchIndex` 方法替换为以下代码：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

此版本的 `SearchIndex` 方法采用其他参数，即 `movieGenre` 。 前几行代码创建一个 `List` 对象，用于保存数据库中的电影流派。

下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

该代码使用 `AddRange` 泛型集合的方法 `List` 将所有不同的流派添加到列表中。  (没有 `Distinct` 修饰符，将添加重复的流派，例如，在我们的示例) 中添加了两次。 然后，代码会在对象中存储流派列表 `ViewBag` 。

下面的代码演示如何检查 `movieGenre` 参数。 如果不为空，则代码会进一步限制影片查询，以将所选电影限制为指定的流派。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>将标记添加到 SearchIndex 视图以支持按流派搜索

将 `Html.DropDownList` helper 添加到*Views\Movies\SearchIndex.cshtml*文件中的 `TextBox` 帮助器之前。 完成的标记如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

运行应用程序并浏览到 */Movies/SearchIndex*。 尝试按流派、电影名称和这两个条件进行搜索。

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

本部分介绍了由框架生成的 CRUD 操作方法和视图。 你创建了一个搜索操作方法和视图，它允许用户按电影标题和流派进行搜索。 在下一部分中，你将了解如何将属性添加到 `Movie` 模型，以及如何添加将自动创建测试数据库的初始化表达式。

> [!div class="step-by-step"]
> [上一页](accessing-your-models-data-from-a-controller.md)
> [下一页](adding-a-new-field-to-the-movie-model-and-table.md)

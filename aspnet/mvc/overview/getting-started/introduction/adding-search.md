---
uid: mvc/overview/getting-started/introduction/adding-search
title: 搜索 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211472"
---
# <a name="search"></a>搜索

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a>添加搜索方法和搜索视图

在本部分中，你将向操作方法添加搜索功能 `Index` ，以允许你按流派或名称搜索电影。

## <a name="prerequisites"></a>必备条件

若要匹配此部分的屏幕截图，需要运行应用程序 (F5) 并将以下电影添加到数据库中。

| 标题 | 发布日期 | 流派 | 价格 |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | 喜剧 | 6.99 |
| Ghostbusters II | 6/16/1989 | 喜剧 | 6.99 |
| Apes 的世界 | 3/27/1986 | 操作 | 5.99 |

## <a name="updating-the-index-form"></a>更新索引窗体

首先将 `Index` 操作方法更新到现有 `MoviesController` 类。 代码如下：

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

方法的第一行 `Index` 创建以下[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询来选择电影：

[!code-csharp[Main](adding-search/samples/sample2.cs)]

此时将定义该查询，但尚未对该数据库运行该查询。

如果 `searchString` 参数包含一个字符串，则使用以下代码修改电影查询以筛选搜索字符串的值：

[!code-csharp[Main](adding-search/samples/sample3.cs)]

上面的 `s => s.Title` 代码是 [Lambda 表达式](https://msdn.microsoft.com/library/bb397687.aspx)。 Lambda 在基于方法的[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询中用作标准查询运算符方法的参数，如以上代码中使用的[Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)方法。 LINQ 查询在定义或通过调用方法（如或）进行修改时，不会执行 `Where` `OrderBy` 。 相反，查询执行延迟，这意味着表达式的计算会延迟，直到实际循环访问它的实际值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 调用方法。 在此 `Search` 示例中，将在 "*索引*" 视图中执行查询。 有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。

> [!NOTE]
> [Contains](https://msdn.microsoft.com/library/bb155125.aspx)方法在数据库上运行，而不是上面的 c # 代码。 在数据库上，[包含](https://msdn.microsoft.com/library/bb155125.aspx)映射到[SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx)，这是不区分大小写的。

现在可以更新 `Index` 将向用户显示窗体的视图。

运行应用程序并导航到 */Movies/Index*。 将查询字符串（如 `?searchString=ghost`）追加到 URL。 筛选的电影将显示出来。

![SearchQryStr](adding-search/_static/image1.png)

如果将方法的签名更改 `Index` 为具有一个名为的参数 `id` ，则该 `id` 参数将与 `{id}` *应用 \_ Start\RouteConfig.cs*文件中设置的默认路由的占位符匹配。

[!code-json[Main](adding-search/samples/sample4.json)]

原始方法如下所 `Index` 示：

[!code-csharp[Main](adding-search/samples/sample5.cs)]

修改后的 `Index` 方法如下所示：

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。

![](adding-search/_static/image2.png)

但是，不能指望用户在每次要搜索电影时都修改 URL。 因此需要添加 UI 来帮助他们筛选电影。 如果更改了方法的签名 `Index` 以测试如何传递路由绑定 ID 参数，请将其更改回，使 `Index` 方法使用名为的字符串参数 `searchString` ：

[!code-csharp[Main](adding-search/samples/sample7.cs)]

打开*Views\Movies\Index.cshtml*文件，并在后面 `@Html.ActionLink("Create New", "Create")` 添加以下突出显示的窗体标记：

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

`Html.BeginForm`帮助器创建开始 `<form>` 标记。 `Html.BeginForm`当用户通过单击 "**筛选器**" 按钮提交窗体时，帮助器会使窗体发布到其自身。

Visual Studio 2013 在显示和编辑视图文件时具有良好的改善。 当你运行应用程序时打开了一个视图文件，Visual Studio 2013 会调用正确的控制器操作方法来显示视图。

![](adding-search/_static/image3.png)

在 Visual Studio 中打开索引视图 (如上图) 中所示），点击 Ctr F5 或 F5 运行应用程序，然后尝试搜索电影。

![](adding-search/_static/image4.png)

`HttpPost`方法没有重载 `Index` 。 不需要该方法，因为该方法不会更改应用程序的状态，只是对数据进行筛选。

可添加以下 `HttpPost Index` 方法。 在这种情况下，操作调用程序将与 `HttpPost Index` 方法匹配， `HttpPost Index` 方法将运行，如下图所示。

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

但是，即使添加 `Index` 方法的 `HttpPost` 版本，其实现方式也受到限制。 假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。 请注意，HTTP POST 请求的 URL 与 GET 请求的 URL (localhost： xxxxx/电影/索引) 相同--URL 本身中没有搜索信息。 目前，搜索字符串信息将作为窗体字段值发送到服务器。 这意味着你无法捕获该搜索信息以在 URL 中将其书签或发送给朋友。

解决方案是使用 `BeginForm` 的重载，该重载指定 POST 请求应将搜索信息添加到 URL，并且应将其路由到该 `HttpGet` 方法的版本 `Index` 。 将现有的无参数 `BeginForm` 方法替换为以下标记：

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

现在，在提交搜索时，URL 包含搜索查询字符串。 即使具备 `HttpPost Index` 方法，搜索也将转到 `HttpGet Index` 操作方法。

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>按流派添加搜索

如果已添加该 `HttpPost` 方法的版本 `Index` ，请立即将其删除。

接下来，你将添加一项功能，使用户能够按流派搜索电影。 将 `Index` 方法替换为以下代码：

[!code-csharp[Main](adding-search/samples/sample11.cs)]

此版本的 `Index` 方法采用其他参数，即 `movieGenre` 。 前几行代码创建一个 `List` 对象，用于保存数据库中的电影流派。

下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。

[!code-csharp[Main](adding-search/samples/sample12.cs)]

该代码使用 `AddRange` 泛型集合的方法 `List` 将所有不同的流派添加到列表中。  (没有 `Distinct` 修饰符，将添加重复的流派，例如，在我们的示例) 中添加了两次。 然后，代码会在对象中存储流派列表 `ViewBag.MovieGenre` 。 将类别数据 (此类电影流派) 为中的[SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx)对象 `ViewBag` ，然后访问下拉列表框中的类别数据是 MVC 应用程序的典型方法。

下面的代码演示如何检查 `movieGenre` 参数。 如果不为空，则代码会进一步限制影片查询，以将所选电影限制为指定的流派。

[!code-csharp[Main](adding-search/samples/sample13.cs)]

如前文所述，此查询不会在数据库上运行，直到在该 `Index` 操作方法返回) 后，将电影列表循环访问后 (会发生在视图中。

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>将标记添加到索引视图以支持按流派搜索

将 `Html.DropDownList` helper 添加到*Views\Movies\Index.cshtml*文件中的 `TextBox` 帮助器之前。 完成的标记如下所示：

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

在以下代码中：

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

参数 "MovieGenre" 为 `DropDownList` 帮助器提供用于在中查找的键 `IEnumerable<SelectListItem>` `ViewBag` 。 在 `ViewBag` 操作方法中填充：

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

参数 "All" 提供选项标签。 如果在浏览器中检查该选项，将看到其 "value" 属性为空。 由于控制器仅筛选 `if` 字符串不为 `null` 或空，因此提交的空值将 `movieGenre` 显示所有流派。

还可以设置默认情况下选择的选项。 如果需要将 "喜剧" 作为默认选项，可以更改控制器中的代码，如下所示：

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

运行应用程序并浏览到 */Movies/Index*。 尝试按流派、电影名称和这两个条件进行搜索。

![](adding-search/_static/image8.png)

在本部分中，你创建了一个搜索操作方法和视图，让用户按电影标题和流派进行搜索。 在下一部分中，你将了解如何将属性添加到 `Movie` 模型，以及如何添加将自动创建测试数据库的初始化表达式。

> [!div class="step-by-step"]
> [上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-a-new-field.md)

---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效的数据分页 |微软文档
author: rick-anderson
description: 步骤 8 演示如何向 /Dinners URL 添加寻呼支持，以便我们一次不显示 1000 份晚餐，我们仅在...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541320"
---
# <a name="implement-efficient-data-paging"></a>实现高效数据分页

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第8步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。
> 
> 步骤 8 演示如何向我们的 /Dinners URL 添加寻呼支持，以便我们一次只显示 10 份即将举办的晚餐，并且允许最终用户以 SEO 友好的方式回传整个列表。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-8-paging-support"></a>神经晚餐步骤 8： 寻呼支持

如果我们的网站成功，它将有成千上万的即将到来的晚餐。 我们需要确保我们的 UI 扩展以处理所有这些晚餐，并允许用户浏览它们。 为了启用这一点，我们将添加分页支持到我们的 */Dinners* URL，以便我们不是一次显示 1000 份晚餐，而是一次只显示 10 份即将举办的晚餐 -并允许最终用户以 SEO 友好的方式回传和转发整个列表。

### <a name="index-action-method-recap"></a>索引（） 操作方法回顾

我们的 DinnersController 类中的 Index（） 操作方法当前如下所示：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

当对 */Dinners* URL 发出请求时，它会检索所有即将举办的晚宴的列表，然后呈现所有这些晚宴的列表：

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>了解可&lt;查询 T&gt;

*IQuery&lt;T&gt;* 是 LINQ 作为 .NET 3.5 的一部分引入的接口。 它支持强大的"延迟执行"方案，我们可以利用这些场景来实现分页支持。

在我们的晚餐存储库中，我们将从我们的"查找晚餐&lt;"&gt;方法返回一个可查询的晚餐序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

我们的 Find对&lt;托&gt;晚餐（） 方法返回的 I 可查询晚餐对象封装了一个查询，以便使用 LINQ 从我们的数据库中检索 Dinner 对象，使用 LINQ 到 SQL。 重要的是，在我们尝试访问/迭代查询中的数据之前，或者直到我们调用查询上的 ToList（） 方法之前，它不会对数据库执行查询。 调用我们的 Find对兴晚餐（） 方法的代码可以选择在执行查询之前向 IQuery&lt;Dinner&gt;对象添加其他"链接"操作/筛选器。 然后，LINQ 到 SQL 足够智能，在请求数据时对数据库执行组合查询。

为了实现分页逻辑，我们可以更新我们的 DinnersController Index（） 操作方法，以便它在调用 ToList（） 之前，将其他"跳过"和"&lt;获取&gt;"运算符应用于返回的可查询晚餐序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上述代码跳过数据库中即将进行的 10 份晚餐，然后返回 20 份晚餐。 LINQ 到 SQL 足够智能，可以构造优化的 SQL 查询，该查询在 SQL 数据库中执行此跳过逻辑，而不是在 Web 服务器中执行此跳过逻辑。 这意味着，即使我们数据库中有数百万个即将推出的 Dinner，也只能检索我们想要的 10 个，作为此请求的一部分（使其高效且可扩展）。

### <a name="adding-a-page-value-to-the-url"></a>向 URL 添加"页面"值

我们希望我们的 URL 包含一个"页面"参数，指示用户请求的"晚餐范围"，而不是对特定页面范围进行硬编码。

#### <a name="using-a-querystring-value"></a>使用查询字符串值

下面的代码演示如何更新我们的 Index（） 操作方法以支持查询字符串参数，并启用 URL，如 */Dinners？page_2*：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上面的 Index（） 操作方法具有名为"页"的参数。 参数声明为空整数（即 int？ 指示）。 这意味着 */Dinners？page_2* URL 将导致将值"2"作为参数值传递。 */Dinners* URL（没有查询字符串值）将导致传递空值。

我们将页面值乘以页面大小（本例中为 10 行），以确定要跳过的晚餐数。 我们使用[C# null"合并"运算符 （？），](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)在处理可无类型时非常有用。 如果页面参数为空，上述代码将值为 0 分配给页。

#### <a name="using-embedded-url-values"></a>使用嵌入式 URL 值

使用查询字符串值的替代方法是将页面参数嵌入到实际 URL 本身中。 例如 *：/晚餐/页/2*或 */Dinner/2*。 ASP.NET MVC 包含强大的 URL 路由引擎，便于支持类似方案。

我们可以注册自定义路由规则，将任何传入 URL 或 URL 格式映射到所需的任何控制器类或操作方法。 我们只需要在我们的项目中打开 Global.asax 文件：

![](implement-efficient-data-paging/_static/image2.png)

然后使用 MapRoute（） 帮助器方法注册新的映射规则，如对路由的第一次调用。地图路线（） 如下：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

上图，我们正在注册一个名为"即将推出的晚餐"的新路由规则。 我们指示它有 URL 格式"Dinners/page/{页面}" - 其中 [页面] 是嵌入在 URL 中的参数值。 MapRoute（） 方法的第三个参数指示我们应该映射此格式与 DinnersController 类上的 Index（） 操作方法相匹配的 URL。

我们可以在查询字符串方案中使用我们以前完全相同的 Index（） 代码 ，除非现在我们的"页面"参数将来自 URL 而不是查询字符串：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

现在，当我们运行应用程序并输入 */Dinner 时*，我们将看到前 10 场即将举办的晚宴：

![](implement-efficient-data-paging/_static/image3.png)

当我们输入 */Dinner/Page/1*时，我们将看到晚餐的下一页：

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>添加页面导航 UI

完成寻呼方案的最后一步是在我们的视图模板中实现"下一步"和"上一个"导航 UI，以便用户轻松跳过 Dinner 数据。

要正确实现这一点，我们需要知道数据库中的 Dinner 的总数，以及它转换为的数据页数。 然后，我们需要计算当前请求的"页面"值是在数据开头还是结尾，并相应地显示或隐藏"上一个"和"下一个"UI。 我们可以在 Index（） 操作方法中实现此逻辑。 或者，我们可以向项目添加帮助器类，以更可重用的方式封装此逻辑。

下面是一个简单的"分页列表"帮助器类，派生自内置于 .NET&lt;&gt;框架中的列表 T 集合类。 它实现了一个可重用的集合类，可用于分页任何 IQuery 数据序列。 在我们的 NerdDinner&lt;应用程序中，我们将针对 IQuery Dinner&gt;结果进行工作，但它在其他应用程序方案中可以同样轻松地用于 I可&lt;查询&gt;产品或可&lt;查询客户&gt;结果：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

请注意，它如何计算，然后公开属性，如"页面索引"，"页面大小"，"总计数"和"总页"。 然后，它还公开两个帮助属性"Has上页"和"HasNextPage"，指示集合中的数据页是原始序列的开头还是结尾。 上述代码将导致运行两个 SQL 查询 - 第一个查询检索 Dinner 对象总数的计数（这不会返回对象- 而是执行返回整数的"SELECT COUNT"语句），第二个代码将仅从数据库中检索当前数据页所需的数据行。

然后，我们可以更新我们的晚餐控制器.Index（） 帮助方法，从我们的晚餐存储库创建一个&lt;&gt; PaginatedList 晚餐。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

然后，我们可以更新 [Views_Dinners_Index.aspx 视图模板》，以便从&lt;ViewPage NerdDinner.Helpers.PaginatedList&lt;&gt;&gt;晚餐&lt;而不是 ViewPage&lt;&gt;&gt;IE500s 晚宴上继承，然后将以下代码添加到视图模板的底部，以显示或隐藏下一个和以前的导航 UI：

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

请注意，我们使用 Html.RouteLink（） 帮助器方法生成超链接的方式。 此方法类似于我们以前使用过的 Html.ActionLink（） 帮助程序方法。 区别在于，我们使用在 Global.asax 文件中设置的"即将到达的晚餐"路由规则生成 URL。 这可确保我们将生成索引（） 操作方法的 URL，该方法的格式为 *：/Dinners/page/{page}* - 其中 [page] 值是我们基于当前 PageIndex 提供上述变量。

现在，当我们再次运行应用程序时，我们将在浏览器中一次看到 10 份晚餐：

![](implement-efficient-data-paging/_static/image5.png)

我们还在页面&lt;&lt;&lt;底部&gt;&gt;&gt;具有和导航 UI，允许我们使用搜索引擎可访问的 URL 向前和向后跳过数据：

![](implement-efficient-data-paging/_static/image6.png)

| **侧主题：了解可&lt;查询 T 的含义&gt;** |
| --- |
| IQueryable&lt;&gt; T 是一个非常强大的功能，支持各种有趣的延迟执行方案（如分页和基于合成的查询）。 与所有强大的功能一样，您希望小心如何使用它，并确保它不受滥用。 请务必认识到，从存储库返回 IQuery 可&lt;查询&gt;T 结果可以调用代码来追加到它上的链式运算符方法，从而参与最终查询执行。 如果不想提供此能力的调用代码，则应&lt;返回 IList T&gt;或 IE55ble&lt;T&gt;结果 - 其中包含已执行的查询的结果。 对于分页方案，这将要求您将实际数据暂停逻辑推送到被调用的存储库方法中。 在此方案中，我们可能会更新我们的 Find对价晚餐（） 查找方法，以有一个签名，该签名要么返回一个分页列表&lt;&gt;：paginatedList 晚餐查找要约晚餐（int pageIndex，int page_info=2>）=或&lt;返回 IList 晚餐&gt;，并使用"总计数"外参数返回晚餐的&lt;总数&gt;：Ilist 晚餐查找要约晚餐（int 页索引，int 页大小） |

### <a name="next-step"></a>下一步

现在，让我们来看看如何向应用程序添加身份验证和授权支持。

> [!div class="step-by-step"]
> [上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)

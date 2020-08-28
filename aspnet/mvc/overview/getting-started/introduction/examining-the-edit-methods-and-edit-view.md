---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: 检查 "编辑" 方法和 "编辑视图" |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045203"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>检查 Edit 方法和编辑视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本部分中，你将检查电影控制器的生成的 `Edit` 操作方法和视图。 但首先我们要 diversion，使发布日期看起来更好。 打开 *Models\Movie.cs* 文件，并添加以下突出显示的行：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

你还可以将日期区域性指定为以下形式：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

我们将在下一教程中介绍 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。 [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) 特性指定要显示的字段名称的内容（本例中应为“Release Date”，而不是“ReleaseDate”）。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性指定数据的类型，在本例中为日期，因此不显示存储在字段中的时间信息。 Chrome 浏览器中的 bug 所需的 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 属性不正确地呈现日期格式。

运行应用程序并浏览到 `Movies` 控制器。 将鼠标指针停留在 **编辑** 链接上可查看它所链接到的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**编辑**链接由 `Html.ActionLink` *Views\Movies\Index.cshtml*视图中的方法生成：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`对象是一个使用[WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基类上的属性公开的帮助器。 `ActionLink`利用帮助器的方法，可以轻松地动态生成链接到控制器操作方法的 HTML 超链接。 方法的第一个参数 `ActionLink` 是要呈现的链接文本 (例如 `<a>Edit Me</a>`) 。 第二个参数是要调用的操作方法的名称，在此示例中 (`Edit`) 操作。 最后一个自变量是在此示例中生成路由数据 (的 [匿名对象](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) ，ID 为 4) 。

上图中显示的生成链接是 `http://localhost:1234/Movies/Edit/4` 。 在 *应用 \_ Start\RouteConfig.cs* 中建立的默认路由 () 采用 URL 模式 `{controller}/{action}/{id}` 。 因此，ASP.NET 将转换为 `http://localhost:1234/Movies/Edit/4` `Edit` 控制器操作方法的请求，该方法的 `Movies` 参数 `ID` 等于4。 从 *应用程序 \_ Start\RouteConfig.cs* 文件中检查以下代码。 [Maproute.html](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法用于将 HTTP 请求路由到正确的控制器和操作方法，并提供可选的 ID 参数。 [HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx)使用[maproute.html](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法 `ActionLink` 来生成 url，如控制器、操作方法和任何路由数据。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

你还可以使用查询字符串传递操作方法参数。 例如，URL 还将 `http://localhost:1234/Movies/Edit?ID=3` 3 的参数传递 `ID` 给 `Edit` 控制器的操作方法 `Movies` 。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

打开 `Movies` 控制器。 下面显示了这两个 `Edit` 操作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

请注意第二个 `Edit` 操作方法的前面是 `HttpPost` 特性。 此特性指定只能 `Edit` 为 POST 请求调用方法的重载。 您可以将属性应用于 `HttpGet` 第一个编辑方法，但这并不是必需的，因为它是默认值。  (将引用隐式分配属性作为方法的操作方法 `HttpGet` `HttpGet` 。 ) [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 特性是另一个重要的安全机制，可防止黑客将数据过度发布到模型。 只应在要更改的 bind 特性中包括属性。 可以在我的 [过多发布安全说明](https://go.microsoft.com/fwlink/?LinkId=317598)中阅读过多发布和 bind 属性。 在本教程中使用的简单模型中，将绑定模型中的所有数据。 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性用于防止请求伪造，并 `@Html.AntiForgeryToken()` 在编辑视图文件 (*Views\Movies\Edit.cshtml*) 中配对，部分如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` 生成一个隐藏的窗体 anti-spam 标记，该标记在控制器的方法中必须匹配 `Edit` `Movies` 。 有关跨站点请求 (伪造的详细信息，请参阅 XSRF 或 CSRF) 中的教程 [XSRF/CSRF/](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)。

`HttpGet` `Edit` 方法采用 "影片 ID" 参数，使用实体框架方法查找电影 `Find` ，并将所选电影返回到 "编辑" 视图。 如果找不到电影，则返回 [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 。 当基架系统创建“编辑”视图时，它会检查 `Movie` 类并创建代码为类的每个属性呈现 `<label>` 和 `<input>` 元素。 下面的示例演示了 visual studio 基架系统生成的编辑视图：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

请注意视图模板如何 `@model MvcMovie.Models.Movie` 在文件顶部包含一条语句，这会指定该视图要求视图模板的模型为类型 `Movie` 。

基架代码使用多个 *帮助器方法* 来简化 HTML 标记。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)帮助器显示 (&quot; 标题 &quot; 、 &quot; ReleaseDate &quot; 、 &quot; 流派 &quot; 或 &quot; 价格 &quot;) 的字段的名称。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)帮助器呈现一个 HTML `<input>` 元素。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)帮助器将显示与该属性相关联的所有验证消息。

运行应用程序并导航到 */Movies* URL。 点击“编辑”链接。 在浏览器中查看页面的源。 窗体元素的 HTML 如下所示。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>`元素位于一个 HTML 元素中， `<form>` 其 `action` 特性设置为发布到 */Movies/Edit* URL。 单击 " **保存** " 按钮后，窗体数据将发布到服务器。 第二行显示调用生成的隐藏的 [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 标记 `@Html.AntiForgeryToken()` 。

## <a name="processing-the-post-request"></a>处理 POST 请求

以下列表显示了 `Edit` 操作方法的 `HttpPost` 版本。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性验证视图中的调用生成的[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)标记 `@Html.AntiForgeryToken()` 。

[ASP.NET MVC 模型联编](https://msdn.microsoft.com/library/dd410405.aspx)程序使用已发布的窗体值并创建 `Movie` 作为参数传递的对象 `movie` 。 `ModelState.IsValid`验证在表单中提交的数据是否可用于修改对象)  (编辑或更新 `Movie` 。 如果数据有效，则会将电影数据保存到 `Movies` `db`)  (实例的集合中 `MovieDBContext` 。 通过调用的方法，将新的电影数据保存到数据库中 `SaveChanges` `MovieDBContext` 。 保存数据后，代码将用户重定向到 `MoviesController` 类的 `Index` 操作方法，此方法显示电影集合，包括刚才所做的更改。

一旦客户端验证确定字段的值无效，就会显示一条错误消息。 如果禁用 JavaScript，将禁用客户端验证。 但是，服务器会检测到已发布的值无效，并且将显示错误消息的窗体值。

稍后将在本教程中更详细地检查验证。

`Html.ValidationMessageFor`*编辑.* view 模板中的帮助器负责显示适当的错误消息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

所有 `HttpGet` 方法都遵循类似的模式。 它们获取影片对象 (或对象列表（在) 情况下）， `Index` 并将模型传递给视图。 `Create`方法将空电影对象传递到 "创建" 视图。 在方法的 `HttpPost` 重载中，创建、编辑、删除或以其他方式修改数据的所有方法都执行此操作。 修改 HTTP GET 方法中的数据存在安全风险，如博客文章 [ASP.NET MVC Tip #46 中所述–不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的数据也违反了 HTTP 最佳做法和体系结构 [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) 模式，该模式指定 GET 请求不应更改应用程序的状态。 换句话说，执行 GET 操作应是没有任何隐患的安全操作，也不会修改持久数据。

## <a name="jquery-validation-for-non-english-locales"></a>非英语区域设置的 jQuery 验证

如果你使用的是美国英语计算机，则可以跳过本部分并转到下一教程。 你可以在 [此处](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)下载本教程的全球化版本。 有关国际化的优秀两部分教程，请参阅 [Nadeem 的 ASP.NET MVC 5 国际化](http://afana.me/post/aspnet-mvc-internationalization.aspx)。

> [!NOTE]
> 若要支持使用逗号 (的非英语区域设置的 jQuery 验证 &quot; 、 &quot;) 用于小数点和非美国英语日期格式，你必须将 *globalize.js* 和特定 *区域性/globalize.cultures.js* 文件从 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) (和 JavaScript ) 到使用 `Globalize.parseFloat` 。 可以从 NuGet 获取 jQuery 非英语验证。 如果你使用的是英语区域设置， (不安装全球化。 ) 

1. 从 " **工具** " 菜单中，单击 " **Nuget 包管理器**"，然后单击 " **管理解决方案的 NuGet 包**"。

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 在左侧窗格中，选择 "<strong>浏览"*。</strong> * (参阅下图。 ) 
3. 在 "输入" 框中，输入 * 全球化 * *。

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) 选择 `jQuery.Validation.Globalize` "选择"， `MvcMovie` 然后单击 " **安装**"。 *Scripts\jquery.globalize\globalize.js*文件将添加到你的项目中。 * Scripts\jquery.globalize\cultures \* 文件夹将包含许多区域性 JavaScript 文件。 请注意，安装此包可能需要5分钟。

   下面的代码演示对 Views\Movies\Edit.cshtml 文件所做的修改：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

若要避免在每个编辑视图中重复此代码，可以将其移动到布局文件中。 若要优化脚本下载，请参阅我的教程 [捆绑和缩减](../../performance/bundling-and-minification.md)。

有关详细信息，请参阅 [ASP.NET mvc 3 国际化](http://afana.me/post/aspnet-mvc-internationalization.aspx) 和 [ASP.NET MVC 3 国际化-第2部分 (NerdDinner) ](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)。

作为临时修补程序，如果无法在区域设置中使用验证，则可以强制计算机使用美国英语，或者可以在浏览器中禁用 JavaScript。 若要强制计算机使用美国英语，可以将全球化元素添加到项目根 *web.config* 文件中。 下面的代码演示将区域性设置为美国英语的全球化元素。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> 在下一教程中，我们将实现搜索功能。

> [!div class="step-by-step"]
> [上一页](accessing-your-models-data-from-a-controller.md)
> [下一页](adding-search.md)

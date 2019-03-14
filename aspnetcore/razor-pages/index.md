---
title: ASP.NET Core 中的 Razor 页面介绍
author: Rick-Anderson
description: 了解 ASP.NET Core 中的 Razor 页面如何使基于页面的编码方式比使用 MVC 更简单高效。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/12/2018
uid: razor-pages/index
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a>ASP.NET Core 中的 Razor 页面介绍

作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Ryan Nowak](https://github.com/rynowak)

Razor 页面是 ASP.NET Core MVC 的一个新特性，它可以使基于页面的编码方式更简单高效。

若要查找使用模型视图控制器方法的教程，请参阅 [ASP.NET Core MVC 入门](xref:tutorials/first-mvc-app/start-mvc)。

本文档介绍 Razor 页面。 它并不是分步教程。 如果认为某些部分过于复杂，请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。 有关 ASP.NET Core 的概述，请参阅 [ASP.NET Core 简介](xref:index)。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

<a name="rpvs17"></a>

## <a name="create-a-razor-pages-project"></a>创建 Razor Pages 项目

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

请参阅 [Razor Pages 入门](xref:tutorials/razor-pages/razor-pages-start)，获取关于如何创建 Razor Pages 项目的详细说明。

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.1"

在命令行中运行 `dotnet new webapp`。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

在命令行中运行 `dotnet new razor`。

::: moniker-end

在 Visual Studio for Mac 中打开生成的 .csproj 文件。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

::: moniker range=">= aspnetcore-2.1"

在命令行中运行 `dotnet new webapp`。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

在命令行中运行 `dotnet new razor`。

::: moniker-end

---

## <a name="razor-pages"></a>Razor 页面

Startup.cs 中已启用 Razor 页面：

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

请考虑一个基本页面：<a name="OnGet"></a>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

上述代码看上去类似于一个 Razor 视图文件。 不同之处在于 `@page` 指令。 `@page` 使文件转换为一个 MVC 操作 ，这意味着它将直接处理请求，而无需通过控制器处理。 `@page` 必须是页面上的第一个 Razor 指令。 `@page` 将影响其他 Razor 构造的行为。

将在以下两个文件中显示使用 `PageModel` 类的类似页面。 Pages/Index2.cshtml 文件：

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

Pages/Index2.cshtml.cs 页面模型：

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

按照惯例，`PageModel` 类文件的名称与追加 .cs 的 Razor 页面文件名称相同。 例如，前面的 Razor 页面的名称为 Pages/Index2.cshtml。 包含 `PageModel` 类的文件的名称为 Pages/Index2.cshtml.cs。

页面的 URL 路径的关联由页面在文件系统中的位置决定。 下表显示了 Razor 页面路径及匹配的 URL：

| 文件名和路径               | 匹配的 URL |
| ----------------- | ------------ |
| */Pages/Index.cshtml* | `/` 或 `/Index` |
| */Pages/Contact.cshtml* | `/Contact` |
| */Pages/Store/Contact.cshtml* | `/Store/Contact` |
| */Pages/Store/Index.cshtml* | `/Store` 或 `/Store/Index` |

注意：

* 默认情况下，运行时在“Pages”文件夹中查找 Razor 页面文件。
* URL 未包含页面时，`Index` 为默认页面。

## <a name="write-a-basic-form"></a>编写基本窗体

由于 Razor 页面的设计，在构建应用时可轻松实施用于 Web 浏览器的常用模式。 [模型绑定](xref:mvc/models/model-binding)、[标记帮助程序](xref:mvc/views/tag-helpers/intro)和 HTML 帮助程序均只可用于 Razor 页面类中定义的属性。 请参考为 `Contact` 模型实现基本的“联系我们”窗体的页面：

在本文档中的示例中，`DbContext` 在 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 文件中进行初始化。

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

数据模型：

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

数据库上下文：

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

Pages/Create.cshtml 视图文件：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

Pages/Create.cshtml.cs 页面模型：

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

按照惯例，`PageModel` 类命名为 `<PageName>Model`并且它与页面位于同一个命名空间中。

使用 `PageModel` 类，可以将页面的逻辑与其展示分离开来。 它定义了页面处理程序，用于处理发送到页面的请求和用于呈现页面的数据。 借助这种分离，可以通过[依赖关系注入](xref:fundamentals/dependency-injection)管理页面依赖关系，并对页面执行[单元测试](xref:test/razor-pages-tests)。

页面包含 `OnPostAsync` 处理程序方法，它在 `POST` 请求上运行（当用户发布窗体时）。 可以为任何 HTTP 谓词添加处理程序方法。 最常见的处理程序是：

* `OnGet`，用于初始化页面所需的状态。 [OnGet](#OnGet) 示例。
* `OnPost`，用于处理窗体提交。

`Async` 命名后缀为可选，但是按照惯例通常会将它用于异步函数。 前面示例中的 `OnPostAsync` 代码看上去与通常在控制器中编写的内容相似。 前面的代码通常用于 Razor 页面。 多数 MVC 基元（例如[模型绑定](xref:mvc/models/model-binding)、[验证](xref:mvc/models/validation)和操作结果）都是共享的。  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

之前的 `OnPostAsync` 方法：

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

`OnPostAsync` 的基本流：

检查验证错误。

*  如果没有错误，则保存数据并重定向。
*  如果有错误，则再次显示页面并附带验证消息。 客户端验证与传统的 ASP.NET Core MVC 应用程序相同。 很多情况下，都会在客户端上检测到验证错误，并且从不将它们提交到服务器。

成功输入数据后，`OnPostAsync` 处理程序方法调用 `RedirectToPage` 帮助程序方法来返回 `RedirectToPageResult` 的实例。 `RedirectToPage` 是新的操作结果，类似于 `RedirectToAction` 或 `RedirectToRoute`，但是已针对页面进行自定义。 在前面的示例中，它将重定向到根索引页 (`/Index`)。 [页面 URL 生成](#url_gen)部分中详细介绍了 `RedirectToPage`。

提交的窗体存在（已传递到服务器的）验证错误时，`OnPostAsync` 处理程序方法调用 `Page` 帮助程序方法。 `Page` 返回 `PageResult` 的实例。 返回 `Page` 的过程与控制器中的操作返回 `View` 的过程相似。 `PageResult` 是处理程序方法的默认 <!-- Review  --> 返回类型。 返回 `void` 的处理程序方法将显示页面。

`Customer` 属性使用 `[BindProperty]` 特性来选择加入模型绑定。

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

默认情况下，Razor 页面只绑定带有非 GET 谓词的属性。 绑定属性可以减少需要编写的代码量。 绑定通过使用相同的属性显示窗体字段 (`<input asp-for="Customer.Name" />`) 来减少代码，并接受输入。

[!INCLUDE[](~/includes/bind-get.md)]

主页 (Index.cshtml)：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

关联的 `PageModel` 类 (Index.cshtml.cs)：

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

Index.cshtml 文件包含以下标记来创建每个联系人项的编辑链接：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

[定位点标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) 使用 `asp-route-{value}` 属性生成“编辑”页面的链接。 此链接包含路由数据及联系人 ID。 例如 `http://localhost:5000/Edit/1`。

Pages/Edit.cshtml 文件：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

第一行包含 `@page "{id:int}"` 指令。 路由约束 `"{id:int}"` 告诉页面接受包含 `int` 路由数据的页面请求。 如果页面请求未包含可转换为 `int` 的路由数据，则运行时返回 HTTP 404（未找到）错误。 若要使 ID 可选，请将 `?` 追加到路由约束：

 ```cshtml
@page "{id:int?}"
```

Pages/Edit.cshtml.cs 文件：

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

Index.cshtml 文件还包含用于为每个客户联系人创建删除按钮的标记：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

删除按钮采用 HTML 呈现，其 `formaction` 包括参数：

* `asp-route-id` 属性指定的客户联系人 ID。
* `asp-page-handler` 属性指定的 `handler`。

下面是呈现的删除按钮的示例，其中客户联系人 ID 为 `1`：

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

选中按钮时，向服务器发送窗体 `POST` 请求。 按照惯例，根据方案 `OnPost[handler]Async` 基于 `handler` 参数的值来选择处理程序方法的名称。

因为本示例中 `handler` 是 `delete`，因此 `OnPostDeleteAsync` 处理程序方法用于处理 `POST` 请求。 如果 `asp-page-handler` 设置为不同值（如 `remove`），则选择名称为 `OnPostRemoveAsync` 的页面处理程序方法。

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

`OnPostDeleteAsync` 方法：

* 接受来自查询字符串的 `id`。
* 使用 `FindAsync` 查询客户联系人的数据库。
* 如果找到客户联系人，则从客户联系人列表将其删除。 数据库将更新。
* 调用 `RedirectToPage`，重定向到根索引页 (`/Index`)。

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-as-required"></a>按需标记页面属性

`PageModel` 上的属性可通过 [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) 特性进行修饰：

[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]

有关详细信息，请参阅[模型验证](xref:mvc/models/validation)。

## <a name="manage-head-requests-with-the-onget-handler"></a>使用 OnGet 处理程序管理 HEAD 请求

HEAD 请求可以检索特定资源的标头。 与 GET 请求不同，HEAD 请求不返回响应正文。

通常，针对 HEAD 请求创建和调用 HEAD 处理程序： 

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

如果未定义 HEAD 处理程序 (`OnHead`)，Razor 页面会回退以调用 ASP.NET Core 2.1 或更高版本中的 GET 页处理程序 (`OnGet`)。 在 ASP.NET Core 2.1 和 2.2 中，`Startup.Configure` 中的 [SetCompatibilityVersion](xref:mvc/compatibility-version) 会发生此行为：

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

默认模板在 ASP.NET Core 2.1 和 2.2 中生成 `SetCompatibilityVersion` 调用。

`SetCompatibilityVersion` 有效地将 Razor 页面选项 `AllowMappingHeadRequestsToGetHandler` 设置为 `true`。

可以显式地选择使用特定行为，而不是通过 `SetCompatibilityVersion` 选择使用所有 2.1 行为。 以下代码选择使用将 HEAD 映射到 GET 处理程序这一行为。

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```

::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a>XSRF/CSRF 和 Razor 页面

无需为[防伪验证](xref:security/anti-request-forgery)编写任何代码。 Razor 页面自动将防伪标记生成过程和验证过程包含在内。

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a>将布局、分区、模板和标记帮助程序用于 Razor 页面

页面可使用 Razor 视图引擎的所有功能。 布局、分区、模板、标记帮助程序、_ViewStart.cshtml 和 _ViewImports.cshtml 的工作方式与它们在传统的 Razor 视图中的工作方式相同。

让我们使用其中的一些功能来整理此页面。

::: moniker range=">= aspnetcore-2.1"

向 Pages/Shared/_Layout.cshtml 添加[布局页面](xref:mvc/views/layout)：

::: moniker-end

::: moniker range="= aspnetcore-2.0"

向 Pages/_Layout.cshtml 添加[布局页面](xref:mvc/views/layout)：

::: moniker-end

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

[布局](xref:mvc/views/layout)：

* 控制每个页面的布局（页面选择退出布局时除外）。
* 导入 HTML 结构，例如 JavaScript 和样式表。

请参阅[布局页面](xref:mvc/views/layout)了解详细信息。

在 Pages/_ViewStart.cshtml 中设置 [Layout](xref:mvc/views/layout#specifying-a-layout) 属性：

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

::: moniker range=">= aspnetcore-2.1"

布局位于“页面/共享”文件夹中。 页面按层次结构从当前页面的文件夹开始查找其他视图（布局、模板、分区）。 可以从“页面/共享”文件夹下的任意 Razor 页面使用“页面”文件夹中的布局。

布局文件应位于 Pages/Shared 文件夹中。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

布局位于“页面”文件夹中。 页面按层次结构从当前页面的文件夹开始查找其他视图（布局、模板、分区）。 可以从“页面”文件夹下的任意 Razor 页面使用“页面”文件夹中的布局。

::: moniker-end

建议不要将布局文件放在“视图/共享”文件夹中。 视图/共享 是一种 MVC 视图模式。 Razor 页面旨在依赖文件夹层次结构，而非路径约定。

Razor 页面中的视图搜索包含“页面”文件夹。 用于 MVC 控制器和传统 Razor 视图的布局、模板和分区可直接工作。

添加 Pages/_ViewImports.cshtml 文件：

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

本教程的后续部分中将介绍 `@namespace`。 `@addTagHelper` 指令将[内置标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/Index)引入“页面”文件夹中的所有页面。

<a name="namespace"></a>

页面上显式使用 `@namespace` 指令后：

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

此指令将为页面设置命名空间。 `@model` 指令无需包含命名空间。

_ViewImports.cshtml 中包含 `@namespace` 指令后，指定的命名空间将为在导入 `@namespace` 指令的页面中生成的命名空间提供前缀。 生成的命名空间的剩余部分（后缀部分）是包含 _ViewImports.cshtml 的文件夹与包含页面的文件夹之间以点分隔的相对路径。

例如，`PageModel` 类 Pages/Customers/Edit.cshtml.cs 显式设置命名空间：

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

Pages/_ViewImports.cshtml 文件设置以下命名空间：

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

为 Pages/Customers/Edit.cshtml Razor 页面生成的命名空间与 `PageModel` 类相同。

`@namespace` 也可用于传统的 Razor 视图。

原始的 Pages/Create.cshtml 视图文件：

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

更新后的 Pages/Create.cshtml 视图文件：

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

[Razor 页面初学者项目](#rpvs17)包含 Pages/_ValidationScriptsPartial.cshtml，它与客户端验证联合。

有关分部视图的详细信息，请参阅 <xref:mvc/views/partial>。

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a>页面的 URL 生成

之前显示的 `Create` 页面使用 `RedirectToPage`：

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

应用具有以下文件/文件夹结构：

* /Pages

  * Index.cshtml
  * /Customers

    * Create.cshtml
    * Edit.cshtml
    * Index.cshtml

成功后，Pages/Customers/Create.cshtml 和 Pages/Customers/Edit.cshtml 页面将重定向到 Pages/Index.cshtml。 字符串 `/Index` 是用于访问上一页的 URI 的组成部分。 可以使用字符串 `/Index` 生成 Pages/Index.cshtml 页面的 URI。 例如：

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

页面名称是从根“/Pages”文件夹到页面的路径（包含前导 `/`，例如 `/Index`）。 与硬编码 URL 相比，前面的 URL 生成示例提供了改进的选项和功能。 URL 生成使用[路由](xref:mvc/controllers/routing)，并且可以根据目标路径定义路由的方式生成参数并对参数编码。

页面的 URL 生成支持相对名称。 下表显示了 Pages/Customers/Create.cshtml 中不同的 `RedirectToPage` 参数选择的索引页：

| RedirectToPage(x)| 页面 |
| ----------------- | ------------ |
| RedirectToPage("/Index") | *Pages/Index* |
| RedirectToPage("./Index"); | *Pages/Customers/Index* |
| RedirectToPage("../Index") | *Pages/Index* |
| RedirectToPage("Index")  | *Pages/Customers/Index* |

`RedirectToPage("Index")`、`RedirectToPage("./Index")` 和 `RedirectToPage("../Index")` 是相对名称。 结合 `RedirectToPage` 参数与当前页的路径来计算目标页面的名称。  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

构建结构复杂的站点时，相对名称链接很有用。 如果使用相对名称链接文件夹中的页面，则可以重命名该文件夹。 所有链接仍然有效（因为这些链接未包含此文件夹名称）。

::: moniker range=">= aspnetcore-2.1"

## <a name="viewdata-attribute"></a>ViewData 特性

可以通过 [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute) 将数据传递到页面。 控制器或 Razor 页面模型上使用 `[ViewData]` 修饰的属性将其值存储在 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 中并从此处进行加载。

在下面的示例中，`AboutModel` 包含使用 `[ViewData]` 修饰的 `Title` 属性。 `Title` 属性设置为“关于”页面的标题：

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

在“关于”页面中，以模型属性的形式访问 `Title` 属性：

```cshtml
<h1>@Model.Title</h1>
```

在布局中，从 ViewData 字典读取标题：

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

## <a name="tempdata"></a>TempData

ASP.NET 在[控制器](/dotnet/api/microsoft.aspnetcore.mvc.controller)上公开了 [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 属性。 此属性存储未读取的数据。 `Keep` 和 `Peek` 方法可用于检查数据，而不执行删除。 多个请求需要数据时，`TempData` 有助于进行重定向。

`[TempData]` 是 ASP.NET Core 2.0 中的新属性，在控制器和页面上受支持。

下面的代码使用 `TempData` 设置 `Message` 的值：

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

Pages/Customers/Index.cshtml 文件中的以下标记使用 `TempData` 显示 `Message` 的值。

```cshtml
<h3>Msg: @Model.Message</h3>
```

Pages/Customers/Index.cshtml.cs 页面模型将 `[TempData]` 属性应用到 `Message` 属性。

```cs
[TempData]
public string Message { get; set; }
```

有关详细信息，请参阅 [TempData](xref:fundamentals/app-state#tempdata)。

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a>针对一个页面的多个处理程序

以下页面使用 `asp-page-handler` 标记帮助程序为两个页面处理程序生成标记：

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

前面示例中的窗体包含两个提交按钮，每个提交按钮均使用 `FormActionTagHelper` 提交到不同的 URL。 `asp-page-handler` 是 `asp-page` 的配套属性。 `asp-page-handler` 生成提交到页面定义的各个处理程序方法的 URL。 未指定 `asp-page`，因为示例已链接到当前页面。

页面模型：

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

前面的代码使用已命名处理程序方法。 已命名处理程序方法通过采用名称中 `On<HTTP Verb>` 之后及 `Async` 之前的文本（如果有）创建。 在前面的示例中，页面方法是 OnPost**JoinList**Async 和 OnPost**JoinListUC**Async。 删除 OnPost 和 Async 后，处理程序名称为 `JoinList` 和 `JoinListUC`。

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

使用前面的代码时，提交到 `OnPostJoinListAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`。 提交到 `OnPostJoinListUCAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`。

## <a name="custom-routes"></a>自定义路由

使用 `@page` 指令，执行以下操作：

* 指定页面的自定义路由。 例如，使用 `@page "/Some/Other/Path"` 将“关于”页面的路由设置为 `/Some/Other/Path`。
* 将段追加到页面的默认路由。 例如，可使用 `@page "item"` 将“item”段添加到页面的默认路由。
* 将参数追加到页面的默认路由。 例如，`@page "{id}"` 页面需要 ID 参数 `id`。

支持开头处以波形符 (`~`) 指定的相对于根目录的路径。 例如，`@page "~/Some/Other/Path"` 和 `@page "/Some/Other/Path"` 相同。

可以通过指定路由模板 `@page "{handler?}"`，将 URL 中的查询字符串 `?handler=JoinList` 更改为路由段 `/JoinList`。

如果你不喜欢 URL 中的查询字符串 `?handler=JoinList`，可以更改路由，将处理程序名称放在 URL 的路径部分。 可以通过在 `@page` 指令后面添加使用双引号括起来的路由模板来自定义路由。

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

使用前面的代码时，提交到 `OnPostJoinListAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH/JoinList`。 提交到 `OnPostJoinListUCAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH/JoinListUC`。

`handler` 前面的 `?` 表示路由参数为可选。

## <a name="configuration-and-settings"></a>配置和设置

若要配置高级选项，请在 MVC 生成器上使用 `AddRazorPagesOptions` 扩展方法：

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

目前，可以使用 `RazorPagesOptions` 设置页面的根目录，或者为页面添加应用程序模型约定。 通过这种方式，我们在将来会实现更多扩展功能。

若要预编译视图，请参阅 [Razor 视图编译](xref:mvc/views/view-compilation)。

[下载或查看示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).

请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)，这篇文章以本文为基础编写。

### <a name="specify-that-razor-pages-are-at-the-content-root"></a>指定 Razor 页面位于内容根目录中

默认情况下，Razor 页面位于 /Pages 目录的根位置。 向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot)，以指定 Razor 页面位于应用的内容根目录 ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) 中：

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a>指定 Razor 页面位于自定义根目录中

向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot)，以指定 Razor 页面位于应用中自定义根目录位置（提供相对路径）：

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="additional-resources"></a>其他资源

* <xref:index>
* <xref:mvc/views/razor>
* <xref:tutorials/razor-pages/razor-pages-start>
* <xref:security/authorization/razor-pages-authorization>
* <xref:razor-pages/razor-pages-conventions>
* <xref:test/razor-pages-tests>
* <xref:mvc/views/partial>

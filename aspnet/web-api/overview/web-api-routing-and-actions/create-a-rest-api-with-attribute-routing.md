---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: 使用 ASP.NET Web API 2 中的属性路由创建 REST API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045177"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>使用 ASP.NET Web API 2 中的属性路由创建 REST API

作者： [Mike Wasson](https://github.com/MikeWasson)

Web API 2 支持一种新的路由类型，称为 *属性路由*。 有关属性路由的一般概述，请参阅 [WEB API 2 中的属性路由](attribute-routing-in-web-api-2.md)。 在本教程中，您将使用属性路由为书籍集合创建 REST API。 该 API 将支持以下操作：

| 操作 | 示例 URI |
| --- | --- |
| 获取所有书籍的列表。 | /api/books |
| 按 ID 获取书籍。 | /api/books/1 |
| 获取书籍的详细信息。 | /api/books/1/details |
| 按流派获取书籍列表。 | /api/books/fantasy |
| 按发布日期获取书籍列表。 | /api/books/date/2013-02-16/api/books/date/2013/02/16 (备用形式)  |
| 获取特定作者的书籍列表。 | /api/authors/1/books |

所有方法都是只读的 (HTTP GET 请求) 。

对于数据层，我们将使用实体框架。 图书记录将具有以下字段：

- ID
- 标题
- 流派
- 发布日期
- 价格
- 说明
- AuthorID (作者表的外键) 

但对于大多数请求，API 将返回此数据的子集， (标题、作者和流派) 。 若要获取完整记录，客户端将请求 `/api/books/{id}/details` 。

## <a name="prerequisites"></a>先决条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) 社区版、专业版或企业版。

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

首先运行 Visual Studio。 从“文件”菜单中，选择“新建”，然后选择“项目”************。

展开 "**已安装**的  >  **Visual c #** " 类别。 在 **Visual c #** 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET Web 应用程序 ( .NET Framework) **"。 将项目命名为 &quot; BooksAPI &quot; 。

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

在 " **新建 ASP.NET Web 应用程序** " 对话框中，选择 " **空** " 模板。 在 "添加文件夹和核心引用" 下，选择 " **WEB API** " 复选框。 单击“确定”。

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

这会创建一个为 Web API 功能配置的主干项目。

### <a name="domain-models"></a>域模型

接下来，添加域模型的类。 在解决方案资源管理器中，右键单击“模型”文件夹。 选择 " **添加**"，然后选择 " **类**"。 命名类 `Author`。

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

将 Author.cs 中的代码替换为以下代码：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

现在，添加另一个名为 `Book` 的类。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>添加 Web API 控制器

在此步骤中，我们将添加一个使用实体框架作为数据层的 Web API 控制器。

按 Ctrl+Shift+B 生成项目。 实体框架使用反射来发现模型的属性，因此它需要已编译的程序集来创建数据库架构。

在“解决方案资源管理器”中，右键单击“控制器”文件夹。 选择 " **添加**"，然后选择 " **控制器**"。

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

在 " **添加基架** " 对话框中，选择 **"包含操作的 Web API 2 控制器"，并使用实体框架**。

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

在 " **添加控制器** " 对话框中的 " **控制器名称**" 下输入 &quot; BooksController &quot; 。 选中 " &quot; 使用异步控制器操作" &quot; 复选框。 对于 " **模型类**"，选择 " &quot; 书籍" &quot; 。  (如果未在 `Book` 下拉列表中看到该类，请确保生成项目。 ) 然后单击 "+" 按钮。

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

单击 "**新建数据上下文**" 对话框中的 "**添加**"。

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

在 "**添加控制器**" 对话框中单击 "**添加**"。 基架添加一个名为 `BooksController` 的类，该类定义 API 控制器。 它还会在模型文件夹中添加一个名为的类 `BooksAPIContext` ，该类定义实体框架的数据上下文。

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>设定数据库种子

从 "工具" 菜单中，选择 " **NuGet 包管理器**"，然后选择 " **程序包管理器控制台**"。

在“Package Manager Console”窗口中，输入以下命令：

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

此命令创建一个迁移文件夹并添加一个名为 Configuration.cs 的新代码文件。 打开此文件，并将以下代码添加到 `Configuration.Seed` 方法。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

在 "包管理器控制台" 窗口中，键入以下命令。

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

这些命令将创建一个本地数据库，并调用 Seed 方法来填充该数据库。

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>添加 DTO 类

如果现在运行应用程序并将 GET 请求发送到/api/books/1，则响应类似于以下内容。  (添加了缩进以提高可读性。 ) 

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

而是希望此请求返回字段的子集。 此外，我希望它返回作者姓名，而不是作者 ID。 为实现此目的，我们将修改控制器方法，以将 *数据传输对象* (DTO) （而不是 EF 模型）返回。 DTO 是仅用于携带数据的对象。

在解决方案资源管理器中，右键单击项目并选择 "**添加**  |  **新文件夹**"。 将文件夹命名为 &quot; dto &quot; 。 `BookDto`使用以下定义，将名为的类添加到 dto 文件夹中：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

添加名为 `BookDetailDto` 的另一个类。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

接下来，更新 `BooksController` 类以返回 `BookDto` 实例。 我们将使用可 [查询的 Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 方法将 `Book` 实例投影到 `BookDto` 实例。 下面是控制器类的更新代码。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> 我删除了 `PutBook` 、 `PostBook` 和 `DeleteBook` 方法，因为本教程不需要它们。

现在，如果您运行应用程序并请求/api/books/1，则响应正文应如下所示：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>添加路由属性

接下来，将控制器转换为使用属性路由。 首先，将 **RoutePrefix** 属性添加到控制器。 此属性定义此控制器上所有方法的初始 URI 段。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

然后将 **[Route]** 特性添加到控制器操作，如下所示：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

每个控制器方法的路由模板都是前缀加上 **route** 特性中指定的字符串。 对于 `GetBook` 方法，路由模板包含参数化字符串 &quot; {id： int} &quot; ，如果 URI 段包含整数值，则匹配。

| 方法 | 路由模板 | 示例 URI |
| --- | --- | --- |
| `GetBooks` | "api/书籍" | `http://localhost/api/books` |
| `GetBook` | "api/书籍/{id： int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>获取书籍详细信息

若要获取书籍详细信息，客户端将向发送 GET 请求 `/api/books/{id}/details` ，其中 *{id}* 是书籍的 id。

将以下方法添加到 `BooksController` 类。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

如果请求 `/api/books/1/details` ，响应如下所示：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>按流派获取书籍

若要获取特定流派的书籍列表，客户端将向发送 GET 请求 `/api/books/genre` ，其中， *流派* 为流派的名称。 （例如：`/api/books/fantasy`。）

将以下方法添加到 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

此处定义的路由包含 URI 模板中的 {流派} 参数。 请注意，Web API 能够区分这两个 Uri 并将它们路由到不同的方法：

`/api/books/1`

`/api/books/fantasy`

这是因为该 `GetBook` 方法包含一个约束，该约束的 "id" 段必须是整数值：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

如果请求/api/books/fantasy，响应如下所示：

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>按作者获取书籍

若要获取特定作者的书籍列表，客户端将向发送 GET 请求 `/api/authors/id/books` ，其中 *id* 是作者的 id。

将以下方法添加到 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

此示例很有趣，因为 &quot; 书籍 &quot; 被视为作者的子 &quot; 资源 &quot; 。 此模式在 RESTful Api 中非常常见。

路由模板中的波形符 (~) 会替代 **RoutePrefix** 属性中的路由前缀。

## <a name="get-books-by-publication-date"></a>按发布日期获取书籍

若要按发布日期获取书籍列表，客户端将向发送 GET 请求 `/api/books/date/yyyy-mm-dd` ，其中 *yyyy-mm-dd* 为日期。

下面是执行此操作的一种方法：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`参数被约束为与**DateTime**值匹配。 这种方法很有效，但实际上比我们更喜欢。 例如，这些 Uri 还会与路由匹配：

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

允许这些 Uri 没有任何错误。 但是，您可以通过将正则表达式约束添加到路由模板，来限制特定格式的路由：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

现在，只有 yyyy-mm-dd 格式的日期才 &quot; &quot; 匹配。 请注意，我们不会使用 regex 来验证我们是否获得了真实的数据。 当 Web API 尝试将 URI 分段转换为 **日期时间** 实例时进行处理。 无效日期（如 "2012-47-99"）将失败，客户端将收到404错误。

还可以 `/api/books/date/yyyy/mm/dd` 通过使用其他 regex 添加另一个 **[Route]** 属性， () 来支持斜线分隔符。

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

这里有一个微妙但重要的细节。 第二个路由模板 \* 在 {e} 参数的开头有一个通配符 () ：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

这将告知 {e} 应与 URI 的其余部分匹配的路由引擎。 默认情况下，模板参数匹配单个 URI 段。 在这种情况下，我们希望 {e} 跨越几个 URI 段：

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>控制器代码

下面是 BooksController 类的完整代码。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>摘要

在设计 API 的 Uri 时，属性路由可提供更多控制和更大的灵活性。

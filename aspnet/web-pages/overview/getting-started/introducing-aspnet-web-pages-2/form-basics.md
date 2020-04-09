---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍ASP.NET网页 - HTML表单基础知识 |微软文档
author: Rick-Anderson
description: 本教程介绍如何创建输入表单以及使用ASP.NET网页 （Razor） 时如何处理用户输入的基础知识。 现在你...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675921"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>介绍ASP.NET网页 - HTML表单基础知识

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介绍如何创建输入表单以及使用ASP.NET网页 （Razor） 时如何处理用户输入的基础知识。 现在您已经有了一个数据库，您将使用表单技能让用户在数据库中查找特定影片。 它假定您已经通过[介绍使用ASP.NET网页显示数据](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成了该系列。
> 
> 学习内容：
> 
> - 如何使用标准 HTML 元素创建窗体。
> - 如何读取表单中的用户输入。
> - 如何创建 SQL 查询，该查询通过使用用户提供的搜索词选择性地获取数据。
> - 如何在页面中"记住"用户输入的内容。
>   
> 
> 讨论的功能/技术：
> 
> - `Request` 对象。
> - SQL`Where`子句。

## <a name="what-youll-build"></a>所需操作

在前面的教程中，您创建了一个数据库，向它添加了数据，然后使用`WebGrid`帮助器来显示数据。 在本教程中，您将添加一个搜索框，允许您查找特定流派的电影或其标题包含您输入的任何单词。 （例如，您可以查找所有类型为"行动"或标题包含"Harry"或"冒险"的电影。

完成本教程后，您将有一个像这样的页面：

![包含流派和标题搜索的电影页面](form-basics/_static/image1.png)

页面的列表部分与上一教程&mdash;中网格相同。 区别在于网格将仅显示您搜索的电影。

## <a name="about-html-forms"></a>关于 HTML 表单

（如果您在创建 HTML 窗体方面拥有经验，并且具有 和`GET``POST`之间的差异，则可以跳过此部分。

窗体具有用户输入元素&mdash;文本框、按钮、单选按钮、复选框、下拉列表等。 用户填写这些控件或进行选择，然后通过单击按钮提交表单。

以下示例说明了窗体的基本 HTML 语法：

[!code-html[Main](form-basics/samples/sample1.html)]

当此标记在页面中运行时，它将创建一个类似于下图的简单窗体：

![在浏览器中呈现的基本 HTML 表单](form-basics/_static/image2.png)

该`<form>`元素包含要提交的 HTML 元素。 （一个简单的错误是向页面添加元素，但随后忘记将它们放入`<form>`元素中。 在这种情况下，不会提交任何内容。该`method`属性告诉浏览器如何提交用户输入。 `post`如果在服务器上执行更新，或者`get`只是从服务器获取数据，则可以将此设置为

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **获取、POST 和 HTTP 动词安全**
> 
> HTTP是浏览器和服务器用来交换信息的协议，其基本操作非常简单。 浏览器仅使用几个谓词向服务器发出请求。 为 Web 编写代码时，了解这些谓词以及浏览器和服务器如何使用这些谓词会很有帮助。 远外最常用的动词是：
> 
> - `GET`. 浏览器使用此谓词从服务器获取内容。 例如，当您在浏览器中键入 URL 时，浏览器将执行操作`GET`以请求所需的页面。 如果页面包含图形，浏览器将执行其他`GET`操作以获取图像。 如果`GET`操作必须将信息传递到服务器，则信息将作为查询字符串中 URL 的一部分传递。
> - `POST`. 浏览器发送`POST`请求以提交要在服务器上添加或更改的数据。 例如，谓`POST`词用于在数据库中创建记录或更改现有记录。 大多数时候，当您填写表单并单击提交按钮时，浏览器将执行操作`POST`。 在操作`POST`中，传递给服务器的数据位于页面正文中。
> 
> 这些谓词之间的一个重要区别是，操作`GET`不应更改服务器上的任何内容，或者以稍微抽象的方式将其放在操作中，`GET`操作不会导致服务器上的状态更改。 您可以根据需要多次对`GET`同一资源执行操作，并且这些资源不会更改。 （操作`GET`通常说是"安全的"，或者使用技术术语，是*幂*等的。当然，与此相反，每次执行`POST`操作时，请求都会更改服务器上的内容。
> 
> 两个例子将有助于说明这一区别。 当您使用必应或 Google 等引擎执行搜索时，您将填写包含一个文本框的表单，然后单击搜索按钮。 浏览器执行操作`GET`，输入到框中的值作为 URL 的一部分传递。 对这种类型的`GET`窗体使用操作很好，因为搜索操作不会更改服务器上的任何资源，因此只需获取信息。
> 
> 现在考虑在线订购内容的过程。 您填写订单详细信息，然后单击提交按钮。 此操作将是一个`POST`请求，因为该操作将导致服务器上的更改，例如新订单记录、帐户信息的更改，以及许多其他更改。 与`GET`操作不同，您不能重复请求`POST`- 如果重复请求，则每次重新提交请求时，都会在服务器上生成新订单。 （在这种情况下，网站通常会警告您不要多次单击提交按钮，或者将禁用提交按钮，以便您不会意外重新提交表单。
> 
> 在本教程中，您将使用`GET`操作和`POST`操作来处理 HTML 窗体。 我们将在每种情况下解释为什么您使用的动词是合适的。
> 
> （要了解有关 HTTP 谓词的更多信息，请参阅 W3C 网站上的[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章。

大多数用户输入元素是`<input>`HTML 元素。 它们看起来像`<input type="type" name="name">,`*类型*指示所需用户输入控件的类型。 这些元素是常见的元素：

- 文本框：`<input type="text">`
- 复选框：`<input type="check">`
- 单选按钮：`<input type="radio">`
- 按钮：`<input type="button">`
- 提交按钮：`<input type="submit">`

您还可以使用 元素`<textarea>`创建多行文本框和`<select>`元素以创建下拉列表或可滚动列表。 （有关 HTML 表单元素的更多内容，请参阅 W3Schools 网站上的[HTML 表单和输入](http://www.w3schools.com/html/html_forms.asp)。

该`name`属性非常重要，因为名称是以后获取元素值的方式，稍后将看到。

有趣的部分是您，页面开发人员，对用户输入所做的操作。 没有与这些元素关联的内置行为。 相反，您必须获取用户已输入或选择的值，并对其进行操作。 这是您将在本教程中学到的。

> [!TIP] 
> 
> **HTML5 和输入表单**
> 
> 您可能知道，HTML 处于过渡状态，最新版本 （HTML5） 包括支持用户输入信息的更直观方式。 例如，在 HTML5 中，您可以告诉页面您希望用户输入日期。 然后，浏览器可以自动显示日历，而不是要求用户手动输入日期。 但是，HTML5 是新的，并非所有浏览器都支持 HTML5。
> 
> ASP.NET网页支持 HTML5 输入，只要用户的浏览器支持 HTML5 输入。 有关 HTML5 中`<input>`元素的新属性的概念，请参阅 W3Schools 站点上的 HTML[&lt;输入&gt;类型属性](http://www.w3schools.com/html/html_form_input_types.asp)。

## <a name="creating-the-form"></a>创建窗体

在 WebMatrix 中，在 **"文件**"工作区中，打开 *"电影.cshtml"* 页面。

在结束`</h1>`标记之后和`<div>``grid.GetHtml`呼叫的开头标记之前，添加以下标记：

[!code-html[Main](form-basics/samples/sample2.html)]

此标记创建一个窗体，该窗体具有名为`searchGenre`文本框和提交按钮。 文本框和提交按钮包含在其`<form>``method`属性设置为`get`的元素中。 （请记住，如果不将文本框和提交按钮放在`<form>`元素中，则单击该按钮时不会提交任何内容。您在此处使用`GET`谓词是因为您正在创建一个不会在服务器上进行任何更改的窗体 - 它只是导致搜索。 （在前面的教程中，您使用了一`post`种方法，即向服务器提交更改的方式。 您将在下一教程中再次看到这一点。

运行页面。 尽管尚未为窗体定义任何行为，但您可以看到它的外观：

![带有"流派"搜索框的影片页面](form-basics/_static/image3.png)

在文本框中输入一个值，如"喜剧"。 然后单击**搜索流派**。

记下页面的 URL。 由于将`<form>`元素的属性`method`设置为`get`，因此您输入的值现在是 URL 中查询字符串的一部分，如下所示：

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>读取窗体值

该页已包含一些代码，这些代码获取数据库数据并在网格中显示结果。 现在，您必须添加一些读取文本框值的代码，以便运行包含搜索词的 SQL 查询。

由于将窗体的方法设置为`get`，因此可以使用如下所示的代码读取输入到文本框中的值：

`var searchTerm = Request.QueryString["searchGenre"];`

对象`Request.QueryString`（`QueryString``Request`对象的属性）包括作为`GET`操作的一部分提交的元素的值。 属性`Request.QueryString`包含表单中提交的值*的集合*（列表）。 要获取任何单个值，请指定所需的元素的名称。 这就是为什么您必须在创建文本框`name``<input>`的元素 （`searchTerm`） 上具有属性的原因。 （有关对象的更多，`Request`请参阅侧[边栏](#BKMK_TheRequestObject)。

阅读文本框的值非常简单。 但是，如果用户在文本框中根本不输入任何内容，但无论如何都单击 **"搜索"，** 则可以忽略该单击，因为没有什么可搜索的。

以下代码是演示如何实现这些条件的示例。 （您不必添加此代码，您一会儿就将添加。

[!code-csharp[Main](form-basics/samples/sample3.cs)]

测试以这种方式分解：

- 获取 的值`Request.QueryString["searchGenre"]`，即输入到名为`<input>``searchGenre`的元素中的值。
- 使用`IsEmpty`方法了解其是否为空。 此方法是确定某些内容（例如窗体元素）是否包含值的标准方法。 但实际上，你只关心，如果它*不*是空的，因此...
- 在`!``IsEmpty`测试前添加运算符。 （运算符`!`表示逻辑 NOT）。

在纯英语中，整个`if`条件将转换为以下内容：*如果窗体的 searchGenre 元素不为空，则 ...*

此块设置创建使用搜索词的查询的阶段。 将在下一部分执行该操作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **请求对象**
> 
> 该`Request`对象包含浏览器在请求或提交页面时发送到应用程序的所有信息。 此对象包括用户提供的任何信息，如文本框值或要上载的文件。 它还包括各种附加信息，如 Cookie、URL 查询字符串中的值（如果有）、正在运行的页面的文件路径、用户使用的浏览器类型、在浏览器中设置的语言列表等等。
> 
> 该`Request`对象是值*的集合*（列表）。 通过指定单个值的名称，从集合中获取单个值：
> 
> `var someValue = Request["name"];`
> 
> 该`Request`对象实际上公开了几个子集。 例如：
> 
> - `Request.Form`如果请求是`POST`请求，则从提交`<form>`元素中的元素提供值。
> - `Request.QueryString`仅为您提供 URL 查询字符串中的值。 （在 URL`http://mysite/myapp/page?searchGenre=action&page=2`中，URL 的`?searchGenre=action&page=2`部分是查询字符串。
> - `Request.Cookies`集合允许您访问浏览器发送的 Cookie。
> 
> 要获取您知道在提交的窗体中的值，可以使用`Request["name"]`。 或者，`Request.Form["name"]`您可以使用更具体的版本（用于`POST`请求）或`Request.QueryString["name"]`（用于`GET`请求）。 当然，*名称*是要获取的项的名称。
> 
> 要获取的项的名称必须在要使用的集合中是唯一的。 这就是为什么`Request`对象提供子集，如`Request.Form`和`Request.QueryString`。 假设您的页面包含名为 的`userName`窗体元素，*并且还*包含名为 的`userName`Cookie。 如果得到`Request["userName"]`，则是模糊的是想要表单值还是 Cookie。 但是，如果您得到`Request.Form["userName"]`或`Request.Cookie["userName"]`，则明确要获取的值。
> 
> 最好是具体使用您感兴趣的子集`Request`，例如`Request.Form`或`Request.QueryString`。 对于您在本教程中创建的简单页面，它可能没有任何区别。 但是，当您创建更复杂的页面时，使用显式版本`Request.Form`或`Request.QueryString`可以帮助您避免在页面包含窗体（或多个窗体）、Cookie、查询字符串值等时可能出现的问题。

## <a name="creating-a-query-by-using-a-search-term"></a>使用搜索词创建查询

现在，您已经知道如何获取用户输入的搜索词，您可以创建使用它的查询。 请记住，要将所有影片项从数据库中获取出来，您使用的是 SQL 查询，该查询如下所示：

`SELECT * FROM Movies`

要仅获取某些影片，必须使用包含子句的`Where`查询。 此子句允许您设置查询返回行的条件。 下面是一个示例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式为`WHERE column = value`。 除了（`=`大于`>`）、（小于）、（`<`不等于）、（`<>``<=`小于或等于）等之外，还可以使用不同的运算符，具体取决于您要查找的内容。

如果您想知道，SQL 语句不是大小写敏感&mdash;`SELECT`与`Select`（或 甚至`select`） 相同。 但是，人们通常使用 SQL 语句中的关键字（`SELECT`如`WHERE`和）来使其更易于阅读。

### <a name="passing-the-search-term-as-a-parameter"></a>将搜索词作为参数传递

搜索特定流派非常简单 （），`WHERE Genre = 'Action'`但您希望能够搜索用户输入的任何流派。 为此，您可以创建为 SQL 查询，其中包含要搜索的值的占位符。 它将看起来像此命令：

`SELECT * FROM Movies WHERE Genre = @0`

占位符是字符`@`后跟零。 正如您可能猜到的，查询可以包含多个占位符，并且它们将命名为`@0`、、、、、、、、、、、、、、`@1``@2`它们。

要设置查询并实际传递该值，请使用如下所示的代码：

[!code-sql[Main](form-basics/samples/sample4.sql)]

此代码类似于您为在网格中显示数据所做的。 唯一的区别是：

- 查询包含占位符 （`WHERE Genre = @0"`。
- 查询被放入变量 （`selectCommand`;之前，您将查询直接传递给 方法`db.Query`。
- 调用`db.Query`方法时，将传递查询和要用于占位符的值。 （如果查询有多个占位符，则将它们全部作为单独的值传递给方法。

如果将所有这些元素放在一起，您将获得以下代码：

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要！** 使用占位符`@0`（如 ） 将值传递给 SQL 命令对于安全性*至关重要*。 此处查看的方式（使用变量数据的占位符）是构建 SQL 命令的唯一方法。
> 
> 切勿通过将从用户获得的文本和值组合（串联）来构造 SQL 语句。 将用户输入串联到 SQL 语句中会将您的网站置于*SQL 注入攻击*中，恶意用户向您的页面提交入侵数据库的值。 （您可以在文章[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 网站中阅读更多内容。

## <a name="updating-the-movies-page-with-search-code"></a>使用搜索代码更新电影页面

现在，您可以更新 *"电影.cshtml"* 文件中的代码。 首先，用以下代码替换页面顶部的代码块中的代码：

[!code-csharp[Main](form-basics/samples/sample6.cs)]

此处的区别是，您已将查询放入变量中`selectCommand`，稍后将传递给`db.Query`该变量。 将 SQL 语句放入变量中可以更改语句，这是执行搜索时执行的操作。

您还删除了这两行，稍后将重新放入：

[!code-csharp[Main](form-basics/samples/sample7.cs)]

您还不想运行查询（即调用`db.Query`），并且也不想初始化`WebGrid`帮助程序。 在找出必须运行哪些 SQL 语句后，您将执行这些操作。

重写此块后，可以添加新逻辑来处理搜索。 已完成的代码如下所示。 更新页面中的代码，使其与此示例匹配：

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

页面现在像这样工作。 每次运行页面时，代码都会打开数据库，`selectCommand`变量将设置为 SQL 语句，该语句从`Movies`表中获取所有记录。 代码还会初始化`searchTerm`变量。

但是，如果当前请求包含`searchGenre`元素的值，则代码将设置`selectCommand`为不同的查询，即包含用于搜索流派`Where`的子句。 它还设置`searchTerm`到搜索框传递的一切（可能什么都不）。

无论 SQL 语句在`selectCommand`中哪个，代码都会`db.Query`调用以运行查询，将其传递给`searchTerm`中的任何内容。 如果 中`searchTerm`没有任何内容，则无关紧要，因为在这种情况下，没有参数可以无论如何将值传递给`selectCommand`。

最后，代码使用查询结果初始化`WebGrid`帮助程序，就像以前一样。

您可以看到，通过将 SQL 语句和搜索词放入变量中，增加了代码的灵活性。 正如本教程稍后将看到的那样，您可以使用此基本框架，并继续为不同类型的搜索添加逻辑。

## <a name="testing-the-search-by-genre-feature"></a>测试按类型搜索功能

在 WebMatrix 中，运行 *"电影.cshtml"* 页。 您将看到带有流派文本框的页面。

输入您为其中一个测试记录输入的流派，然后单击 **"搜索**"。 这一次，你看到一个列表，只是电影匹配该流派：

![电影页面列表后搜索流派"喜剧"](form-basics/_static/image4.png)

输入其他流派并再次搜索。 尝试使用所有小写或所有大写字母输入流派，以便您可以看到搜索不区分大小写。

## <a name="remembering-what-the-user-entered"></a>"记住"用户输入的内容

您可能已经注意到，在您输入一个流派并单击**搜索流派**后，您看到了该流派的列表。 但是，搜索文本框换句话说是&mdash;空的，它不记得您输入的内容。

了解此行为发生的原因非常重要。 提交页面时，浏览器会向 Web 服务器发送请求。 当ASP.NET收到请求时，它会创建页面的全新实例，在其中运行代码，然后将页面再次呈现给浏览器。 实际上，该页面不知道您只是使用自身的早期版本。 它只知道，它得到了一个请求，其中有一些表单数据。

每次请求页面时，无论是&mdash;首次请求还是提交页面&mdash;，您都会获得新页面。 Web 服务器没有您上次请求的内存。 浏览器也不ASP.NET，浏览器也不ASP.NET。 页面的这些单独实例之间的唯一连接是您在它们之间传输的任何数据。 例如，如果提交页面，则新页面实例可以获取前一个实例发送的表单数据。 （在页面之间传递数据的另一种方法是使用 Cookie。

描述这种情况的一个正式方法是说网页是*无状态的*。 Web 服务器和页面本身以及页面中的元素不保留有关页面以前状态的任何信息。 Web 之所以以这种方式设计，是因为维护单个请求的状态会迅速耗尽 Web 服务器的资源，而 Web 服务器通常每秒处理数千甚至数十万个请求。

因此，文本框为空的原因。 提交页面后，ASP.NET创建了该页的新实例，并运行了代码和标记。 该代码中没有任何内容告诉ASP.NET在文本框中输入值。 因此ASP.NET什么都没做，文本框呈现时没有值。

实际上，有一个简单的方法来解决此问题。 您在文本框中输入的流派*可在*文本框中的代码&mdash;中`Request.QueryString["searchGenre"]`使用。

更新文本框的标记，以便`value`属性从 获取`searchTerm`其值，如下所示：

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此页中`value`，还可以将属性设置为`searchTerm`变量，因为该变量还包含您输入的流派。 但是，`Request`使用 对象设置如下所示`value`的属性是完成此任务的标准方法。 （假设在某些情况下甚至想要执行此操作&mdash;，则可能需要呈现*没有*字段中值的页面。 这完全取决于你的应用发生了什么。

> [!NOTE]
> 您无法"记住"用于密码的文本框的值。 使用代码允许人们填写密码字段是一个安全漏洞。

再次运行页面，输入流派，然后单击**搜索流派**。 这一次，您不仅看到搜索结果，而且文本框会记住您上次输入的内容：

![显示文本框已"记住"上一个条目的页面](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>在标题中搜索任何单词

您现在可以搜索任何流派，但您可能还需要搜索标题。 搜索时很难完全正确获取标题，因此您可以搜索标题内任何位置的单词。 要在 SQL 中执行此操作，`LIKE`请使用运算符和语法，如下所示：

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令获取其标题包含"冒险"的所有影片。 使用运算符时，`LIKE`将通配符`%`作为搜索词的一部分。 搜索`LIKE 'adventure%'`意味着"从'冒险'开始"。 （从技术上讲，它意味着"字符串'冒险'后跟任何东西。同样，搜索词`LIKE '%adventure'`的意思是"任何后面跟着字符串'冒险'"，这是另一种方式说"以'冒险'结束"。

因此，搜索`LIKE '%adventure%'`词表示"与标题中的任何位置都具有'冒险性'"。 （从技术上讲，"标题中的任何内容，然后是'冒险'，然后是任何东西。

在元素`<form>`中，在流派搜索的关闭`</div>`标记下方添加以下标记（就在结束`</form>`元素之前）：

[!code-html[Main](form-basics/samples/sample10.html)]

处理此搜索的代码与流派搜索的代码类似，只不过您必须组装`LIKE`搜索。 在页面顶部的代码块中，在流派搜索`if``if`的块之后添加此块：

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此代码使用之前看到的相同逻辑，只不过搜索使用`LIKE`运算符，并且代码在搜索词之前和之后放置""。`%`

请注意如何轻松地向页面添加另一个搜索。 你所要做的就是：

- 创建测试`if`的块以查看相关搜索框是否具有值。
- 将`selectCommand`变量设置为新的 SQL 语句。
- 将`searchTerm`变量设置为要传递给查询的值。

下面是完整的代码块，其中包含标题搜索的新逻辑：

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

下面总结了此代码的用途：

- 变量`searchTerm`和`selectCommand`在顶部初始化。 您将根据用户在页面中所做的操作将这些变量设置为相应的搜索词（如果有）和相应的 SQL 命令。 默认搜索是从数据库中获取所有影片的简单示例。
- 在 和`searchGenre``searchTitle`的测试中，代码将`searchTerm`设置到要搜索的值。 这些代码块还设置为`selectCommand`该搜索的相应 SQL 命令。
- 该方法`db.Query`仅调用一次，使用 中`selectedCommand`的任何 SQL 命令和 中`searchTerm`的任何值。 如果没有搜索词（没有流派，没有标题词），则 值`searchTerm`为空字符串。 但是，这并不重要，因为在这种情况下，查询不需要参数。

## <a name="testing-the-title-search-feature"></a>测试标题搜索功能

现在，您可以测试已完成的搜索页面。 运行*电影.cshtml*.

输入流派，然后单击**搜索流派**。 网格显示该流派的电影，就像以前一样。

输入标题字，然后单击 **"搜索标题**"。 网格显示标题中具有该单词的电影。

![在标题中搜索"The"后的电影页面列表](form-basics/_static/image6.png)

将两个文本框留空，然后单击任一按钮。 网格显示所有影片。

## <a name="combining-the-queries"></a>组合查询

您可能会注意到，您可以执行的搜索是独占的。 不能同时搜索标题和流派，即使两个搜索框中都有值。 例如，您无法搜索标题包含"冒险"的所有动作影片。 （现在对页面进行编码时，如果同时输入流派和标题的值，则标题搜索将优先。要创建结合条件的搜索，必须创建具有如下语法的 SQL 查询：

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

您必须使用如下语句来运行查询（大致而言）：

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

如您所见，创建逻辑以允许搜索条件的许多排列，可能会涉及一些内容。 因此，我们将在这里停留。

## <a name="coming-up-next"></a>下一步

在下一教程中，您将创建一个页面，该页面使用窗体允许用户向数据库添加影片。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>影片页面的完整列表（通过搜索更新）

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法进行 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3学校网站上的[SQL WHERE 条款](http://www.w3schools.com/sql/sql_where.asp)
- [方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 站点上的文章

> [!div class="step-by-step"]
> [上一页](displaying-data.md)
> [下一页](entering-data.md)

---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045164"
---
# <a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本部分中，您将创建一个新 `MoviesController` 类并编写代码来检索电影数据，并使用视图模板在浏览器中显示该数据。

在继续执行下一步之前，请**生成应用程序**。 如果不生成应用程序，则会在添加控制器时出现错误。

在解决方案资源管理器中，右键单击 " *控制器* " 文件夹，然后依次单击 " **添加**"、" **控制器**"。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

在 " **添加基架** " 对话框中，单击 " **包含视图的 MVC 5 控制器，使用实体框架**"，然后单击 " **添加**"。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 为 Model 类选择 " **电影 (MvcMovie") ** 。
- 为数据上下文类选择 **MovieDBContext (MvcMovie) ** 。
- 对于控制器名称，请输入 **MoviesController**。

  下图显示了 "已完成" 对话框。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

单击“添加”。  (如果出现错误，则可能不会在开始添加控制器之前构建应用程序。 ) Visual Studio 会创建以下文件和文件夹：

- "*控制器*" 文件夹中的*MoviesController.cs*文件。
- 一个 *Views\Movies* 文件夹。
- 在新的*Views\Movies* *文件夹中**创建. cshtml、Delete （* cshtml）、Details、

Visual Studio 会自动创建 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (创建、读取、更新和删除) 操作方法和视图， (自动创建 crud 操作方法和视图称为基架) 。 现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。

运行应用程序，单击 " **MVC 电影** " 链接 (或 `Movies` 通过将 */Movies* 追加到浏览器的地址栏中的 URL 来浏览到控制器) 。 由于应用程序依赖于 *应用 \_ Start\RouteConfig.cs* 文件) 中定义的默认路由 (，因此浏览器请求 `http://localhost:xxxxx/Movies` 将路由到控制器的默认 `Index` 操作方法 `Movies` 。 换句话说，浏览器请求实际上与 `http://localhost:xxxxx/Movies` 浏览器请求相同 `http://localhost:xxxxx/Movies/Index` 。 结果为空电影列表，因为尚未添加任何影片。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击 " **创建** " 按钮。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 您可能无法在 "价格" 字段中输入小数点或逗号。 若要支持使用逗号 (的非英语区域设置的 jQuery 验证 &quot; 、 &quot;) 用于小数点和非美国英语日期格式，你必须将 *globalize.js* 和特定 *区域性/globalize.cultures.js* 文件从 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) (和 JavaScript ) 到使用 `Globalize.parseFloat` 。 下一教程将演示如何执行此操作。 目前，只能输入整数，例如 10。

单击 " **创建** " 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。 然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

再创建几个其他的电影条目。 试用“编辑”****、“详细信息”**** 和“删除”**** 链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开 *Controllers\MoviesController.cs* 文件并检查生成的 `Index` 方法。 下面显示了包含方法的影片控制器的部分 `Index` 。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

对控制器的请求将 `Movies` 返回表中的所有条目 `Movies` ，然后将结果传递给 `Index` 视图。 `MoviesController`如前文所述，类中的以下行将实例化电影数据库上下文。 可以使用影片数据库上下文来查询、编辑和删除影片。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和 @model 关键字

在本教程的前面部分，你已了解控制器如何使用对象将数据或对象传递到视图模板 `ViewBag` 。 `ViewBag`是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。

MVC 还提供将 *强* 类型对象传递到视图模板的功能。 此强类型方法可在 Visual Studio 编辑器中更好地编译代码和更丰富的 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 。 Visual Studio 中的基架机制使用这种方法 (也就是说，在创建方法和视图时，传递 *强* 类型化模型) `MoviesController` 和类和视图模板。

在 *Controllers\MoviesController.cs* 文件中，检查生成的 `Details` 方法。 此 `Details` 方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`参数通常作为路由数据传递，例如， `http://localhost:1234/movies/details/1` 将控制器设置为电影控制器，将操作设置为 `details` 并将设置为 `id` 1。 你还可以使用查询字符串传入 id，如下所示：

`http://localhost:1234/movies/details?id=1`

如果找到了，则会将 `Movie` 模型的实例 `Movie` 传递给 `Details` 视图：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

检查 *Views\Movies\Details.cshtml* 文件的内容：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

通过将 `@model` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。 创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句**：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。 例如，在 *详细信息* 模板中，代码将每个电影字段传递给 `DisplayNameFor` 强类型化对象的和 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助程序 `Model` 。 `Create`和 `Edit` 方法和视图模板也会传递影片模型对象。

检查 MoviesController.cs 文件中的*索引 cshtml*视图模板和 `Index` 方法。 *MoviesController.cs* 请注意，代码在 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` 操作方法中调用帮助程序方法时如何创建对象 `Index` 。 然后，该代码将此 `Movies` 列表从 `Index` 操作方法传递给视图：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

创建影片控制器时，Visual Studio 会自动将以下语句包含 `@model` 在 *索引 cshtml* 文件的顶部：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

此 `@model` 指令允许使用强类型的对象访问控制器传递给视图的电影列表 `Model` 。 例如，在 *索引 cshtml* 模板中，代码通过对 `foreach` 强类型对象执行语句来循环播放电影 `Model` ：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

由于 `Model` 对象已强类型化 (作为 `IEnumerable<Movie>` 对象) ，因此循环中的每个 `item` 对象都被类型化为 `Movie` 。 除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 自动创建数据库。 可以通过查看 *应用 \_ 数据* 文件夹来验证是否已创建。 如果看不到 "*电影 .mdf* " 文件，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用程序 \_ 数据*" 文件夹。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

双击 *""，以打开* " **服务器资源管理器**"，然后展开 " **表** " 文件夹以查看 "电影" 表。 请注意 ID 旁边的密钥图标。 默认情况下，EF 会将名为 ID 的属性设置为主键。 有关 [EF 和 mvc](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)的详细信息，请参阅 Tom Dykstra 的绝佳教程。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

右键单击 `Movies` 该表，然后选择 " **显示表数据** " 以查看创建的数据。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

右键单击 `Movies` 该表，然后选择 " **打开表定义** "，查看实体框架 Code First 创建的表结构。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

请注意，表的架构如何 `Movies` 映射到 `Movie` 前面创建的类。 实体框架 Code First 会根据你的类自动为你创建此架构 `Movie` 。

完成后，请通过右键单击 *MovieDBContext* 并选择 " **关闭连接**" 来关闭连接。  (如果未关闭连接，则在下次运行项目时可能会收到错误) 。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。 在下一教程中，我们将研究基架代码的其余部分并添加 `SearchIndex` 方法和 `SearchIndex` 视图，以便在此数据库中搜索电影。 有关将实体框架与 MVC 结合使用的详细信息，请参阅为 [ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

> [!div class="step-by-step"]
> [上一页](creating-a-connection-string.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)

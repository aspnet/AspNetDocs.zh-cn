---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |微软文档
author: rick-anderson
description: 步骤 4 演示如何向应用程序添加控制器，该应用程序利用我们的模型为用户提供数据列表/详细信息导航体验...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541307"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>使用控制器和视图实现列表/详细信息 UI

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第4步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。
> 
> 步骤 4 演示如何向应用程序添加控制器，该应用程序利用我们的模型为用户提供在 NerdDinner 网站上晚餐的数据列表/详细信息导航体验。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-4-controllers-and-views"></a>神经晚餐步骤 4：控制器和视图

对于传统的 Web 框架（经典 ASP、PHP、ASP.NET Web 窗体等），传入 URL 通常映射到磁盘上的文件。 例如：诸如"/Products.aspx"或"/Products.php"这样的 URL 请求可能由"Products.aspx"或"Products.php"文件处理。

基于 Web 的 MVC 框架以略有不同的方式将 URL 映射到服务器代码。 它们不是将传入 URL 映射到文件，而是将 URL 映射到类上的方法。 这些类称为"控制器"，它们负责处理传入的 HTTP 请求、处理用户输入、检索和保存数据以及确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他 URL 等）。

现在，我们已经为我们的NerdDinner应用程序建立了基本模型，我们的下一步将是向应用程序添加一个控制器，利用它为用户提供我们网站上的 Dinner 的数据列表/详细信息导航体验。

### <a name="adding-a-dinnerscontroller-controller"></a>添加晚餐控制器控制器

我们将从右键单击 Web 项目中的"控制器"文件夹开始，然后选择 **"添加-&gt;控制器"** 菜单命令（您也可以通过键入 Ctrl-M、Ctrl-C 来执行此命令）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

这将弹出"添加控制器"对话框：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

我们将命名新的控制器"DinnersController"，然后单击"添加"按钮。 然后，Visual Studio 将在我们的 @控制器目录下添加DinnersController.cs文件：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

它还将在代码编辑器中打开新的 DinnersController 类。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>向晚餐控制器类添加索引（） 和详细信息（） 操作方法

我们希望让使用我们的应用程序的访问者浏览即将举办的晚宴列表，并允许他们点击列表中的任何晚餐以查看有关此晚餐的具体细节。 我们将通过发布应用程序的以下 URL 来执行此操作：

| **URL** | **目标** |
| --- | --- |
| */晚餐/* | 显示即将来临的晚宴的 HTML 列表 |
| */晚餐/详情/[id]* | 显示 URL 中嵌入的"id"参数指示的特定晚餐的详细信息 ， 这将与数据库中的晚餐 ID 匹配。 例如：/Dinners/详细信息/2 将显示一个 HTML 页面，其中详细介绍了晚餐 ID 值为 2 的晚餐。 |

我们将通过向 DinnersController 类中添加两种公共"操作方法"来发布这些 URL 的初始实现，如下所示：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

然后，我们将运行 NerdDinner 应用程序，并使用我们的浏览器来调用它们。 键入 *"/Dinners/"URL*将导致我们的*Index（）* 方法运行，并且它将发送回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

键入 *"/晚餐/详细信息/2"URL*将导致运行*我们的详细信息（）* 方法，并发送回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

您可能想知道 - ASP.NET MVC 如何知道创建我们的 DinnersController 类并调用这些方法？ 为了理解这一点，让我们快速了解路由的工作原理。

### <a name="understanding-aspnet-mvc-routing"></a>了解ASP.NET MVC 路由

ASP.NET MVC 包含强大的 URL 路由引擎，在控制 URL 如何映射到控制器类方面提供了很大的灵活性。 它允许我们完全自定义ASP.NET MVC 如何选择要创建的控制器类、调用哪种方法，以及配置不同的方式，以便变量可以从 URL/Querystring 自动解析并传递给方法作为参数参数。 它提供了灵活性，完全优化了SEO网站（搜索引擎优化），以及发布任何我们想要从应用程序。

默认情况下，新的ASP.NET MVC 项目附带一组已注册的 URL 路由规则。 这使我们能够轻松启动应用程序，而无需显式配置任何内容。 默认路由规则注册可以在项目的"应用程序"类中找到 ， 我们可以通过双击项目根目录中的"Global.asax"文件来打开：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

默认ASP.NET MVC 路由规则在此类的"注册路由"方法中注册：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"路线。上面的 MapRoute（）方法调用注册了一个默认路由规则，该规则使用 URL 格式将传入 URL 映射到控制器类："//{控制器}/{{{操作}/{id}" - 其中"控制器"是要实例化的控制器类的名称，"操作"是要调用它的公共方法的名称，"id"是嵌入在 URL 中的可选参数，可以作为参数传递给该方法。 传递给"MapRoute（）"方法调用的第三个参数是一组默认值，用于在 URL 中不存在的控制器/操作/id 值（控制器 = "Home"，操作 ="索引"，Id="）。

下面是一个表，演示如何使用默认的<em>"//控制器\/{操作}/{id}"</em>路由规则映射各种 URL：

| **URL** | **控制器类** | **操作方法** | **传递的参数** |
| --- | --- | --- | --- |
| */晚餐/细节/2* | 晚餐控制器 | 详细信息（ID） | id=2 |
| */晚餐/编辑/5* | 晚餐控制器 | 编辑（ID） | id=5 |
| */晚餐/创建* | 晚餐控制器 | Create() | 空值 |
| */晚餐* | 晚餐控制器 | 索引（） | 空值 |
| */首页* | 家庭控制器 | 索引（） | 空值 |
| */* | 家庭控制器 | 索引（） | 空值 |

最后三行显示正在使用的默认值（控制器 = 主页、操作 + 索引、ID =""）。 由于"Index"方法注册为默认操作名称（如果未指定），因此"/Dinners"和"/home"URL 会导致在其控制器类上调用 Index（） 操作方法。 由于"Home"控制器在未指定时注册为默认控制器，因此"/" URL 会导致创建 HomeController，并调用其上的索引（） 操作方法。

如果您不喜欢这些默认 URL 路由规则，好消息是它们很容易更改 - 只需在上面的注册路由方法中编辑它们即可。 但是，对于我们的 NerdDinner 应用程序，我们不会更改任何默认 URL 路由规则，而只是将它们作为本操作使用。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>使用我们的晚餐控制器的晚餐存储库

现在，让我们用使用我们的模型的实现替换当前对 DinnersController Index（） 和详细信息（）操作方法的实现。

我们将使用之前构建的 DinnerRepository 类来实现该行为。 我们将首先添加一个"使用"语句，该语句引用"NerdDinner.Model"命名空间，然后声明我们的 DinnerRepository 的实例作为 DinnerController 类上的字段。

在本章的后面部分，我们将介绍"依赖注入"的概念，并展示我们的控制器获取对 DinnerRepository 的引用的另一种方法，该存储库可实现更好的单元测试 -但现在，我们将创建一个类似于下面的 DinnerRepository 内联实例。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

现在，我们准备使用检索到的数据模型对象生成 HTML 响应。

### <a name="using-views-with-our-controller"></a>将视图与我们的控制器一起使用

虽然可以在我们的操作方法中编写代码来组装 HTML，然后使用*Response.Write（）* 帮助器方法将其发送回客户端，但这种方法很快就会变得相当笨拙。 更好的方法是，我们只能在 DinnersController 操作方法中执行应用程序和数据逻辑，然后将呈现 HTML 响应所需的数据传递给负责提供其 HTML 表示的单独"视图"模板。 正如我们在一瞬间看到的，"视图"模板是一个文本文件，通常包含 HTML 标记和嵌入呈现代码的组合。

将控制器逻辑与视图渲染分离带来了几个大好处。 特别是，它有助于在应用程序代码和 UI 格式/呈现代码之间强制实施明确的"关注点分离"。 这使得与 UI 呈现逻辑隔离的单元测试应用程序逻辑变得更加容易。 它便于以后修改 UI 呈现模板，而无需更改应用程序代码。 而且，它可以使开发人员和设计人员更轻松地在项目上协作。

我们可以更新 DinnersController 类，以指示我们希望使用视图模板发送回 HTML UI 响应，方法是将两种操作方法的方法签名从返回类型的"void"改为"ActionResult"。" 然后，我们可以调用控制器基类上的*View（）* 帮助器方法返回如下所示的"ViewResult"对象：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

我们在上面使用的*View（）* 帮助器方法的签名如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View（）* 帮助程序方法的第一个参数是我们要用于呈现 HTML 响应的视图模板文件的名称。 第二个参数是一个模型对象，其中包含视图模板为呈现 HTML 响应所需的数据。

在我们的 Index（） 操作方法中，我们调用*View（）* 帮助器方法，并指示我们希望使用"Index"视图模板呈现晚餐的 HTML 列表。 我们正在传递视图模板一系列 Dinner 对象，以便从以下角度生成列表：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

在我们的"详细信息"操作方法中，我们尝试使用 URL 中提供的 ID 检索 Dinner 对象。 如果找到有效的"晚餐"，我们调用*View（）* 帮助器方法，指示我们要使用"详细信息"视图模板来呈现检索到的 Dinner 对象。 如果请求无效的晚餐，我们会呈现一条有用的错误消息，指示使用"NotFound"视图模板（以及仅采用模板名称的*View（）* 帮助器方法的重载版本不存在 Dinner：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

现在，让我们实现"未找到"、"详细信息"和"索引"视图模板。

### <a name="implementing-the-notfound-view-template"></a>实现"未找到"视图模板

我们将首先实现"NotFound"视图模板 -它显示一条友好的错误消息，指示找不到请求的晚餐。

我们将通过在控制器操作方法中定位文本光标来创建新的视图模板，然后右键单击并选择"添加视图"菜单命令（我们还可以通过键入 Ctrl-M、Ctrl-V 来执行此命令）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

这将弹出一个"添加视图"对话框，如下所示。 默认情况下，对话框将预填充创建视图的名称，以匹配启动对话框时光标所采用的操作方法的名称（在本例中为"详细信息"）。 由于我们想要首先实现"未找到"模板，我们将重写此视图名称并将其设置为"未找到"：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

单击"添加"按钮时，Visual Studio 将在"_Views_Dinners"目录中为我们创建新的"NotFound.aspx"视图模板（如果目录不存在，它还会创建该模板）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

它还将在代码编辑器中打开我们新的"NotFound.aspx"视图模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

默认情况下，查看模板有两个"内容区域"，我们可以在其中添加内容和代码。 第一个允许我们自定义发回的 HTML 页面的"标题"。 第二个允许我们自定义发回的 HTML 页面的"主要内容"。

要实现我们的"未找到"视图模板，我们将添加一些基本内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

然后，我们可以在浏览器中试用。 为此，让我们请求 *"/晚餐/详细信息/9999"URL。* 这将引用数据库中当前不存在的晚餐，并导致我们的 DinnersController.详细信息（） 操作方法呈现我们的"未找到"视图模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

在上面的屏幕截图中，您会注意到一件事，那就是我们的基本视图模板继承了一堆环绕屏幕上主要内容的 HTML。 这是因为我们的视图模板使用"母版页"模板，使我们能够在网站上的所有视图上应用一致的布局。 我们将在本教程的后续部分讨论母版页如何工作。

### <a name="implementing-the-details-view-template"></a>实现"详细信息"视图模板

现在，让我们实现"详细信息"视图模板 ， 它将为单个晚餐模型生成 HTML。

我们将通过将文本光标定位到"详细信息"操作方法中，然后右键单击并选择"添加视图"菜单命令（或按 Ctrl-M，Ctrl-V） 来执行此操作：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

这将弹出"添加视图"对话框。 我们将保留默认视图名称（"详细信息"）。 我们还在对话框中选择"创建强类型视图"复选框，并选择（使用组合框下拉下）我们从控制器传递到视图的模型类型的名称。 对于此视图，我们传递一个 Dinner 对象（此类型的完全限定名称为："NerdDinner.Model.Dinner"）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

与之前选择创建"空视图"的模板不同，这次我们将选择使用"详细信息"模板自动"基架"视图。 我们可以通过更改上面对话框中的"查看内容"下拉列表来指示这一点。

"Scaffold"将根据我们传递给它的 Dinner 对象生成我们详细信息视图模板的初始实现。 这为我们提供了一种快速开始视图模板实现的简单方法。

当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"详细信息.aspx"视图模板文件：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

它还将在代码编辑器中打开我们新的"Details.aspx"视图模板。 它将包含基于 Dinner 模型的详细信息视图的初始基架实现。 基架引擎使用 .NET 反射来查看通过该数据库的类上公开的公共属性，并将根据找到的每个类型添加适当的内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

我们可以请求 *"/晚餐/详细信息/1"URL*以查看浏览器中此"详细信息"基架实现的外观。 使用此 URL 将显示我们首次创建数据库时手动添加到数据库的晚餐之一：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

这让我们快速启动和运行，并为我们提供了详细信息.aspx 视图的初始实现。 然后，我们可以去调整它，以自定义 UI，以让我们满意。

当我们更仔细地查看 Details.aspx 模板时，我们会发现它包含静态 HTML 以及嵌入式呈现代码。 &lt;%&gt; % 代码块在视图模板呈现时执行代码&lt;，%= %&gt;代码块执行其中包含的代码，然后将结果呈现给模板的输出流。

我们可以在 View 中编写代码，该代码访问使用强类型"Model"属性从控制器传递的"Dinner"模型对象。 Visual Studio 在编辑器中访问此"模型"属性时，为我们提供了完整的代码无意义：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

让我们做一些调整，以便我们最终的详细信息视图模板的源如下所示：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

当我们再次访问 *"/晚餐/细节/1"URL*时，它现在将呈现如下：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>实现"索引"视图模板

现在，让我们实现"索引"视图模板 - 这将生成即将推出的晚餐的列表。 为此，我们将将文本光标定位在 Index 操作方法中，然后右键单击并选择"添加视图"菜单命令（或按 Ctrl-M、Ctrl-V）。

在"添加视图"对话框中，我们将保留名为"索引"的视图模板，并选择"创建强类型视图"复选框。 这一次，我们将选择自动生成"列表"视图模板，并选择"NerdDinner.Model.Dinner"作为传递给视图的模型类型（由于我们已指示我们正在创建"列表"基架将导致添加视图对话框假定我们将一系列 Dinner 对象从控制器传递到视图）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"Index.aspx"视图模板文件。 它将"支架"在其中的初始实现，提供我们传递给视图的 Dinner 的 HTML 表列表。

当我们运行应用程序并访问 *"/Dinners/"URL*时，它将呈现我们的晚餐列表，如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上面的表格解决方案为我们提供了一个网格般的布局，我们的晚餐数据 - 这不是我们想要为我们的消费者面对晚餐上市。 我们可以更新 Index.aspx 视图模板并对其进行修改以列出较少的数据列，并使用&lt;ul&gt;元素呈现它们，而不是使用以下代码呈现表：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

当我们循环展示模型中的每个晚餐时，我们使用上述"var"关键字。 不熟悉 C# 3.0 的人可能会认为使用"var"意味着晚餐对象是后期绑定的。 相反，这意味着编译器使用针对强类型"模型"属性的类型推理（类型为&lt;&gt;"IE500Dinner"），并将本地"Dinner"变量编译为 Dinner 类型 - 这意味着我们在代码块中获取完全的无意义和编译时间检查：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

当我们在浏览器中的 */Dinners* URL 上刷新时，我们更新的视图现在如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

看起来更好，但还没有完全存在。 我们的最后一步是使最终用户能够点击列表中的单个晚餐并查看有关它们的详细信息。 我们将通过呈现链接到晚餐控制器上"详细信息"操作方法的 HTML 超链接元素来实现此内容。

我们可以在 Index 视图中以两种方式之一生成这些超链接。 第一种是手动创建 HTML &lt;&gt;元素，如下所示，其中我们在&lt;&gt;HTML&gt;元素中&lt;嵌入 % 块：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

我们可以使用的替代方法是利用 MVC 中ASP.NET内置的"Html.ActionLink（））"帮助器方法，该方法支持以编程方式创建 HTML 元素，&lt;该&gt;元素链接到控制器上的另一个操作方法：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink（） 帮助器方法的第一个参数是要显示的链接文本（在本例中为 Dinner 的标题），第二个参数是我们想要将链接生成的控制器操作名称（在本例中为详细信息方法），第三个参数是一组要发送到操作的参数（作为具有属性名称/值的匿名类型实现）。 在这种情况下，我们指定我们要链接到的晚餐的"id"参数，并且由于 ASP.NET MVC 中的默认 URL 路由规则为 Html.ActionLink（） 帮助器方法的"{控制器}/{操作}/{id}"，因此 Html.ActionLink（） 帮助程序方法将生成以下输出：

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

对于我们的 Index.aspx 视图，我们将使用 Html.ActionLink（） 帮助器方法方法，并将每个晚餐都包含到相应详细信息 URL 的链接中：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

现在，当我们点击 */Dinners* URL 时，我们的晚餐列表如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

当我们单击列表中的任何晚餐时，我们将导航以查看有关它的详细信息：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>基于约定的命名和 _Views 目录结构

默认情况下ASP.NET MVC 应用程序在解决视图模板时使用基于约定的目录命名结构。 这允许开发人员在从 Controller 类中引用视图时避免对位置路径进行完全限定。 默认情况下ASP.NET MVC 将在应用程序下方的 [视图\[控制器名称]\*目录中查找视图模板文件。

例如，我们一直在研究 DinnersController 类，该类显式引用三个视图模板："索引"、"详细信息"和"未找到"。 默认情况下，ASP.NET MVC 将在应用程序根目录下的 *[Views_Dinners]* 目录中查找这些视图：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

请注意，项目中当前存在三个控制器类（DinnersController、HomeController 和 AccountController - 在创建项目时默认添加了后两个控制器类），并且 _Views 目录中有三个子目录（每个控制器一个）。

从"主页"和"帐户"控制器引用的视图将自动解析其视图模板，这些模板来自相应的 *[视图]主页*和 *[视图]帐户*目录。 *[Views]共享*子目录提供了一种存储在应用程序中多个控制器中重复使用的视图模板的方法。 当 ASP.NET MVC 尝试解析视图模板时，它将首先在 *[视图\[控制器]* 特定目录中进行检查，如果无法找到视图模板，它将在 *[Views_Shared]* 目录中查找。

在命名单个视图模板时，建议的指导是让视图模板共享与导致其呈现的操作方法相同的名称。 例如，上面的"Index"操作方法是使用"索引"视图来呈现视图结果，而"详细信息"操作方法使用"详细信息"视图来呈现其结果。 这样，就可以轻松快速查看与每个操作关联的模板。

当视图模板与在控制器上调用的操作方法具有相同的名称时，开发人员不需要显式指定视图模板名称。 相反，我们可以将模型对象传递给"View（）"帮助器方法（不指定视图名称），并且ASP.NET MVC 将自动推断我们希望在磁盘上使用 *[视图\[控制器名称]\[操作名称]* 视图模板来呈现它。

这使我们能够稍微清理一下控制器代码，并避免在代码中重复两次名称：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上述代码是实现一个不错的晚餐列表/细节体验的网站所需要的一切。

#### <a name="next-step"></a>下一步

我们现在有一个不错的晚餐浏览体验建立。

现在，让我们启用 CRUD（创建、读取、更新、删除）数据表单编辑支持。

> [!div class="step-by-step"]
> [上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)

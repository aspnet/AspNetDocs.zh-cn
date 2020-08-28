---
title: 将视图添加到 MVC 应用
author: Rick-Anderson
description: 将视图添加到 MVC 应用
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045008"
---
# <a name="adding-a-view"></a>添加视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本部分中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。 

使用 [Razor 视图引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)可以创建视图模板文件。 基于 Razor 的视图模板的文件扩展名为 *cshtml* ，并提供使用 c # 创建 HTML 输出的简洁方法。 Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。

当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。 更改 `Index` 方法以调用控制器 [视图](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) 方法，如以下代码所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

`Index`上面的方法使用视图模板生成浏览器的 HTML 响应。 控制器方法 (也称为 [操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)) （如 `Index` 上面的方法）通常返回 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (或派生自 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)) 的类，而不是字符串等基元类型。

右键单击 *Views\HelloWorld* 文件夹，然后单击 " **添加**"，然后单击 " ** (Razor) 的布局" 的 "MVC 5 视图页 **"。
  
![](adding-a-view/_static/image1.png)   
  
在 " **指定项目的名称** " 对话框中，输入 *Index*，然后单击 **"确定"**。  
  
![](adding-a-view/_static/image2.png)  
  
在 "**选择布局页**" 对话框中，接受默认的** \_ 布局 Cshtml** ，然后单击 **"确定"**。  
  
![](adding-a-view/_static/image3.png)  
  
在上面的对话框中，在左窗格中选择了 " *Views\Shared* " 文件夹。 如果在其他文件夹中有自定义的布局文件，则可以选择它。 我们稍后将在本教程中讨论布局文件

将创建 *MvcMovie\Views\HelloWorld\Index.cshtml* 文件。

![](adding-a-view/_static/image4.png)

添加以下突出显示的标记。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

右键单击该 *索引的 cshtml* 文件，然后选择 **"在浏览器中查看"**。

![PI](adding-a-view/_static/image5.png)

您还可以右键单击该 *索引的 cshtml* 文件，然后 **在 Page Inspector 中选择 "查看"。** 有关详细信息，请参阅 [Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md) 。

或者，运行应用程序并浏览到 `HelloWorld` 控制器 (`http://localhost:xxxx/HelloWorld`) 。 `Index`控制器中的方法不做很多工作; 它只是运行了语句，该语句 `return View()` 指定方法应使用视图模板文件来呈现对浏览器的响应。 由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用*\Views\HelloWorld*文件夹中的*视图文件。* 下图显示了视图 &quot; 模板中的字符串 Hello！ &quot; 在视图中进行了硬编码。

![](adding-a-view/_static/image6.png)

看起来不错。 但请注意，浏览器的标题栏显示 "Index-My ASP.NET 应用程序"，页面顶部的大链接显示 "应用程序名称"。 根据浏览器窗口的大小，可能需要单击右上角的三个栏才能看到 " **主页**"、" **关于**"、" **联系人**"、" **注册** " 和 **"登录** " 链接。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页

首先，您需要更改 &quot; 页面顶部的 "应用程序名称" &quot; 链接。 该文本对于每个页面都是通用的。 它实际上只在项目中的一个位置实现，即使它显示在应用程序的每一页上也是如此。 中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 " * \_ Layout* " 文件。 此文件称为 *布局页面* ，位于所有其他页面都使用的共享文件夹中。

![_LayoutCshtml](adding-a-view/_static/image7.png)

布局模板使你能够在一个位置指定网站的 HTML 容器布局，然后将它应用到网站中的多个页面。 查找 `@RenderBody()` 行。 `RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。 例如，如果选择 " **关于** " 链接，则会在方法中呈现 *Views\Home\About.cshtml* 视图 `RenderBody` 。

更改标题元素的内容。 将布局模板中的 [html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) 从 &quot; 应用程序名称更改 &quot; 为 &quot; MVC 电影 &quot; ，并将控制器从更改 `Home` 为 `Movies` 。 完整的布局文件如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

运行该应用程序，请注意，它现在显示 &quot; MVC 电影 &quot; 。 单击 " **关于** " 链接，你将看到该页面也会显示 &quot; MVC 电影 &quot; 。 我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。

![](adding-a-view/_static/image8.png)

首次创建 *Views\HelloWorld\Index.cshtml* 文件时，它包含以下代码：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

上述 Razor 代码显式设置布局页。 检查 * \\ _ViewStart cshtml* 文件的视图，它包含的 Razor 标记完全相同。 *[视图 \\ _ViewStart 的视图](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 用于定义所有视图都将使用的通用布局，因此你可以从*Views\HelloWorld\Index.cshtml*文件中注释掉或删除该代码。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

可以使用 `Layout` 属性设置不同的布局视图，或将它设置为 `null`，这样将不会使用任何布局文件。

现在，让我们更改索引视图的标题。

打开 *MvcMovie\Views\HelloWorld\Index.cshtml*。 有两个位置可进行更改：第一项是在浏览器标题中显示的文本，然后在辅助标题中 (`<h2>` 元素) 。 稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

若要指示要显示的 HTML 标题，以上代码将设置 `Title` `ViewBag` (的对象的属性，该对象位于*Index.cshtml*) 的 请注意，布局模板 ( *Views\Shared \\ _Layout* ) 将此值 `<title>` 作为 `<head>` 之前修改的 HTML 部分的一部分使用。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

使用此 `ViewBag` 方法，您可以轻松地在视图模板和布局文件之间传递其他参数。

运行应用程序。 请注意，浏览器标题、主标题和辅助标题已更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 来强制加载来自服务器的响应。 ) 浏览器标题是通过在 `ViewBag.Title` *Index. cshtml*视图模板中设置的，以及在布局文件中添加的附加 &quot; 电影应用来创建的。 &quot;

另请注意， *Index.* view 模板中的内容如何与* \_ Layout*视图模板合并，并向浏览器发送单个 HTML 响应。 凭借布局模板可以很容易地对应用程序中所有页面进行更改。

![](adding-a-view/_static/image9.png)

&quot; &quot; 在这种情况下，我们的一些数据 (在这种情况下 &quot; ，我们的视图模板中的 Hello！ &quot; 消息) 是硬编码的。 MVC 应用程序具有一个 &quot; &quot; (视图) ，并且您有一个 &quot; C &quot; (控制器) ，但没有 (&quot; &quot;) 模型。 稍后，我们将演练如何创建数据库并从中检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。 为了响应传入 URL 请求，将调用控制器类。 通过控制器类，您可以编写处理传入浏览器请求的代码，从数据库中检索数据，并最终决定要发送回浏览器的响应类型。 然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。

控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。 最佳做法： **视图模板不应执行业务逻辑或直接与数据库交互**。 相反，视图模板应仅适用于控制器为其提供的数据。 维护这 &quot; 一问题分离 &quot; 有助于使你的代码更干净、可测试、更易于维护。

目前， `Welcome` 类中的操作方法 `HelloWorldController` 采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。 不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。 视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。 为此，可以让控制器将动态数据 (参数) 在 `ViewBag` 视图模板可以访问的对象中的视图模板需要的参数。

返回到 *HelloWorldController.cs* 文件，然后更改 `Welcome` 方法，将 `Message` 和值添加 `NumTimes` 到 `ViewBag` 对象。 `ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中;在 `ViewBag` 将对象放入其中之前，对象没有定义的属性。 [ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数 `name` `numTimes` 从地址栏中的查询字符串映射到方法中的参数 (和) 。 完整的 HelloWorldController.cs 文件如下所示：

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

现在， `ViewBag` 对象包含将自动传递到视图的数据。 接下来，需要一个欢迎视图模板！ 在 " **生成** " 菜单中，选择 " **生成解决方案** " (或按 Ctrl + Shift + B) 以确保编译项目。 右键单击 *Views\HelloWorld* 文件夹，然后单击 " **添加**"，然后单击 " ** (Razor) 的布局" 的 "MVC 5 视图页 **"。
  
![](adding-a-view/_static/image10.png)   
  
在 " **指定项目的名称** " 对话框中，输入 " *欢迎*"，然后单击 **"确定"**。   
  
在 "**选择布局页**" 对话框中，接受默认的** \_ 布局 Cshtml** ，然后单击 **"确定"**。  
  
![](adding-a-view/_static/image11.png)   

将创建 *MvcMovie\Views\HelloWorld\Welcome.cshtml* 文件。

替换 *欢迎的 cshtml* 文件中的标记。 你将创建一个循环，该循环显示 &quot; &quot; 的是用户所应的时间。 下面显示了完整的 *欢迎. cshtml* 文件。

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

运行应用程序并浏览到以下 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在，数据是从 URL 获取的，并使用 [模型绑定](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)器传递到控制器。 控制器将数据打包到一个 `ViewBag` 对象中，并将该对象传递给视图。 然后，视图将以 HTML 格式向用户显示数据。

![](adding-a-view/_static/image12.png)

在上面的示例中，我们使用 `ViewBag` 对象将数据从控制器传递到视图。 稍后在本教程中，我们将使用视图模型将数据从控制器传递给视图。 用于传递数据的视图模型方法通常比查看包方法更可取。 有关详细信息，请参阅博客文章 [动态 V 强类型视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 。 

这种情况下，这是 &quot; 模型的 M 类型 &quot; ，而不是数据库类型。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)

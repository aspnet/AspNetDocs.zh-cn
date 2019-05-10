---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 和实现 ViewModel 类 |Microsoft Docs
author: microsoft
description: 步骤 6 显示了如何启用对更丰富的窗体编辑方案中，支持，并还讨论了可用于将数据从控制器传递到视图的两种方法:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125451"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>使用 ViewData 和实现 ViewModel 类

by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的第 6 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 6 显示了如何启用对更丰富的窗体编辑方案中，支持，并还讨论了可用于将数据从控制器传递到视图的两种方法：ViewData 和 ViewModel。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner 步骤 6:ViewData 和 ViewModel

我们已涵盖了多个窗体发布方案，并讨论了如何实现创建、 更新和删除 (CRUD) 支持。 现在，我们将采取进一步的我们 DinnersController 的实现，并启用对更丰富的窗体编辑方案的支持。 在此期间，我们将讨论可用于将数据从控制器传递到视图的两种方法：ViewData 和 ViewModel。

### <a name="passing-data-from-controllers-to-view-templates"></a>将数据从控制器传递到视图模板

MVC 模式的定义特征之一是严格"关注点分离"它可帮助应用程序的不同组件之间强制实施。 模型、 控制器和视图每个良好定义的角色和责任，并且它们彼此之间相互进行通信以定义完善的方式。 这有助于提升可测试性和代码重用。

当控制器类决定呈现 HTML 响应返回给客户端时，它负责显式传递到视图模板的所有数据所需呈现响应。 视图模板应永远不会执行任何数据检索或应用程序逻辑，并应改为其本身限制为只包含从控制器传递给它的模型/数据驱动的呈现代码。

稍后再试模型数据按我们 DinnersController 传递到我们的视图模板的类很简单，简单 – index （），对于 Dinner 对象的列表，以及单个 Dinner 对象在 Details()、 edit （）、 create （） 和 delete （） 的情况下。 因为我们将更多的 UI 功能添加到我们的应用程序时，我们通常要需要传递多个只是呈现 HTML 响应我们视图模板中的此数据。 例如，我们可能想要修改我们编辑中的"国家/地区"字段，从而成为一个 HTML 文本框，到 dropdownlist 创建视图。 而不是硬编码的视图模板中的国家/地区名称的下拉列表，我们可能想要生成基于的受支持的国家/地区，我们动态填充的列表。 我们将需要一种方法将 Dinner 对象传递*和*支持国家/地区列表从控制器到我们的视图模板。

让我们看看我们可以实现此目的的两种方法。

### <a name="using-the-viewdata-dictionary"></a>使用 ViewData 字典

控制器基类公开可用于将其他数据项从控制器传递给视图的"ViewData"字典属性。

例如，若要支持我们想要从正在 dropdownlist 到一个 HTML 文本框，更改"国家/地区"文本框中的，我们编辑视图中的方案，我们可以更新将可用作 m SelectList 对象传递 （除了一个 Dinner 对象） 我们 edit （） 操作方法国家/地区 dropdownlist odel。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上述 SelectList 的构造函数接受县来填充，下拉 downlist，以及当前所选的值的列表。

然后，我们可以更新我们 Edit.aspx 视图模板，而不是我们使用了以前的 Html.TextBox() 帮助器方法使用 Html.DropDownList() 帮助器方法：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上面的 Html.DropDownList() 帮助程序方法采用两个参数。 第一个是要输出的 HTML 窗体元素的名称。 第二个是我们通过 ViewData 字典传递"SelectList"模型。 我们使用 C#"作为"关键字将强制转换为 SelectList 字典中的类型。

现在，当我们运行我们的应用程序和访问权限和 */Dinners/Edit/1* URL 在浏览器中我们将看到我们编辑 UI 更新以显示 dropdownlist 的国家/地区而不是一个文本框：

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

因为我们还呈现中 （在方案中发生错误时） 的 HTTP POST 编辑方法的编辑视图模板，我们将需要确保我们还更新此方法将 SelectList 添加到 ViewData，在错误情况中呈现的视图模板时：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

并且我们 DinnersController 的编辑方案现在支持 DropDownList。

### <a name="using-a-viewmodel-pattern"></a>使用视图模型的模式

ViewData 字典方法具有优势是相当快速且轻松地实现。 一些开发人员不喜欢使用基于字符串的字典，不过，由于拼写错误可能会导致将不会在编译时捕获的错误。 非类型化的 ViewData 字典还需要使用"为"运算符或强制转换时使用 C# 等视图模板中的强类型化语言。

我们可以使用另一种方法是一个通常称为"视图模型的"模式。 使用此模式时我们将创建强类型化的类，针对我们特定视图的方案，进行了优化和其公开动态值/内容所需的视图模板的属性。 我们的控制器类可以填充，然后将这些视图优化类传递给我们要使用的视图模板。 这样，类型安全性、 编译时检查，以及在视图模板中的编辑器 intellisense。

例如，若要启用 dinner 窗体类似如下的编辑方案，我们可以创建"DinnerFormViewModel"类公开两个强类型属性： 一个 Dinner 对象和所需填充国家/地区 dropdownlist 的 SelectList 模型：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

我们可以然后更新要创建使用从存储库中，我们检索的 Dinner 对象 DinnerFormViewModel 我们 edit （） 操作方法，并将其传递给视图模板：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

然后我们视图模板，因此它需要"DinnerFormViewModel"而不是"Dinner"对象通过更改 edit.aspx 页面顶部的"继承"特性的更新如下所示，我们将：

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

我们执行此操作，我们视图模板中的"模型"属性的 intellisense 将更新以反映我们传递给它的 DinnerFormViewModel 类型的对象模型：

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

我们然后可以更新其工作我们查看代码。 请注意，我们未更改的输入元素的名称如何我们正在创建 （窗体元素将仍被命名为"Title"，"国家/地区"） – 但我们正在更新的 HTML 帮助器方法来检索使用 DinnerFormViewModel 类的值：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

我们还会更新我们编辑 post 方法以呈现错误时所使用的 DinnerFormViewModel 类：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

我们还可以更新我们的 create （） 操作方法，以重复使用的完全相同*DinnerFormViewModel*类来启用的国家/地区 DropDownList 中那些也。 下面是 HTTP GET 实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

下面是创建 HTTP POST 方法的实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

并且我们编辑和创建屏幕现在支持方法是下拉列表选择国家/地区。

### <a name="custom-shaped-viewmodel-classes"></a>自定义形状 ViewModel 类

在上述方案中，我们 DinnerFormViewModel 类直接将 Dinner 模型对象公开为属性，以及支持 SelectList 模型属性。 这种方法，我们要创建我们视图模板中的 HTML UI 方法相对较接近于我们的域模型对象的方案中工作正常。

这并不适合的情况下，可以使用的一种选择是创建一个自定义形状的 ViewModel 类的对象模型更适用于使用由视图 – 和可能看起来完全不同的基础的域模型对象。 例如，它可能会公开不同的属性名和/或从多个模型对象收集的聚合属性。

自定义形状 ViewModel 类可用于同时将数据从控制器传递到要呈现，以及用于帮助处理回发到控制器的操作方法的窗体数据的视图。 对于此更高版本的情况下，可能必须使用窗体发布数据中，更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际域模型对象的操作方法。

自定义形状 ViewModel 类可以提供了很大的灵活性，并需要调查任何时间在您开始太过于复杂的操作方法中的视图模板或窗体发布代码中找到的呈现代码。 这通常是登录域模型不完全对应于要生成的 UI 和中间形自定义 ViewModel 类可帮助。

### <a name="next-step"></a>下一步

让我们现在看一下如何使用分区和母版页的重复使用并在我们的应用程序之间共享 UI。

> [!div class="step-by-step"]
> [上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)

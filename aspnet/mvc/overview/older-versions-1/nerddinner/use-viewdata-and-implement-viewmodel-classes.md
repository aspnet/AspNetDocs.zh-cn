---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用视图数据并实现视图模型类 |微软文档
author: rick-anderson
description: 步骤 6 显示了如何支持更丰富的表单编辑方案，并讨论了两种方法，可用于将数据从控制器传递到视图：...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541099"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>使用 ViewData 和实现 ViewModel 类

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第6步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。
> 
> 步骤 6 显示了如何支持更丰富的表单编辑方案，并讨论了可用于将数据从控制器传递到视图的两种方法：ViewData 和 ViewModel。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>神经晚餐步骤 6：查看数据和视图模型

我们介绍了一些表单发布方案，并讨论了如何实现创建、更新和删除 （CRUD） 支持。 现在，我们将进一步实施 DinnersController，并支持更丰富的表单编辑方案。 在此过程中，我们将讨论两种可用于将数据从控制器传递到视图的方法：ViewData 和 ViewModel。

### <a name="passing-data-from-controllers-to-view-templates"></a>将数据从控制器传递到视图模板

MVC 模式的一个定义特征是严格"关注点分离"，它有助于在应用程序的不同组件之间强制执行。 模型、控制器和视图都有定义明确的角色和职责，它们之间以定义明确的方式相互通信。 这有助于提高可测试性和代码重用性。

当 Controller 类决定将 HTML 响应呈现回客户端时，它负责显式将呈现响应所需的所有数据传递给视图模板。 视图模板绝不应执行任何数据检索或应用程序逻辑，而应限制自己仅具有由控制器从模型/数据中驱动的呈现代码。

现在，我们的 DinnersController 类传递给视图模板的模型数据简单而直接 — 在 Index（）的情况下，是晚餐对象的列表，如果是详细信息（、Edit（）、Create（） 和删除（）的情况下，只有一个晚餐对象。 当我们向应用程序添加更多 UI 功能时，我们通常需要传递的不仅仅是这些数据，才能在视图模板中呈现 HTML 响应。 例如，我们可能希望将"编辑"和"创建视图"中的"国家/地区"字段从 HTML 文本框更改为下拉列表。 我们不是在视图模板中硬编码国家名称的下拉列表，而是希望从我们动态填充的支持国家/地区列表中生成它。 我们需要一种方法，将 Dinner 对象*和支持*的国家/地区列表从控制器传递到视图模板。

让我们来看看两种实现此目的的方法。

### <a name="using-the-viewdata-dictionary"></a>使用视图数据字典

控制器基类公开一个"ViewData"字典属性，该属性可用于将其他数据项从控制器传递到视图。

例如，为了支持我们希望将"编辑"视图中的"国家/地区"文本框从 HTML 文本框更改为下拉列表的方案，我们可以更新我们的 Edit（） 操作方法，以传递（除了晚餐对象之外）可用作国家/地区下拉列表的模型的 SelectList 对象。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上面 SelectList 的构造函数正在接受要使用下拉列表以及当前选择的值填充下拉列表的县列表。

然后，我们可以更新我们的 Edit.aspx 视图模板，以使用 Html.DropDownList（） 帮助程序方法，而不是我们以前使用的 Html.TextBox（） 帮助器方法：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上面的 Html.DropDownList（） 帮助器方法采用两个参数。 第一个是要输出的 HTML 窗体元素的名称。 第二个是我们通过 ViewData 字典传递的"选择列表"模型。 我们使用 C#"as"关键字将字典中的类型转换为 SelectList。

现在，当我们运行应用程序并访问浏览器中的 */Dinners/Edit/1* URL 时，我们将看到我们的编辑 UI 已更新以显示国家/地区列表而不是文本框：

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

由于我们还从 HTTP-POST Edit 方法呈现 Edit 视图模板（在发生错误时），我们希望确保在错误方案中呈现视图模板时，还要更新此方法以将 SelectList 添加到 ViewData：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

现在，我们的晚餐控制器编辑方案支持下拉列表。

### <a name="using-a-viewmodel-pattern"></a>使用视图模型模式

ViewData 字典方法具有相当快速且易于实现的好处。 但是，有些开发人员不喜欢使用基于字符串的字典，因为拼写错误可能导致在编译时不会捕获的错误。 未键入的 ViewData 字典还要求在视图模板中使用强类型语言（如 C#）时使用"as"运算符或强制转换。

我们可以使用的另一种方法是通常称为"视图模型"模式的方法。 使用此模式时，我们创建针对特定视图方案优化的强类型类，并公开视图模板所需的动态值/内容的属性。 然后，我们的控制器类可以填充这些视图优化的类并将其传递给我们的视图模板使用。 这支持视图模板中的类型安全、编译时间检查和编辑器对讲。

例如，为了启用晚餐表单编辑方案，我们可以创建一个"DinnerFormViewModel"类，如下所示，该类公开了两个强类型属性：一个"晚餐"对象，以及填充国家/地区下拉列表所需的 SelectList 模型：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

然后，我们可以更新我们的 Edit（） 操作方法，使用从存储库检索的 Dinner 对象创建 DinnerFormViewModel，然后将其传递到视图模板：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

然后，我们将更新视图模板，以便它期望有一个"DinnerFormViewModel"而不是"Dinner"对象，例如，更改 edit.aspx 页面顶部的"继承"属性：

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

一旦我们这样做，视图模板中"模型"属性的对讲义将更新，以反映我们传递的 DinnerFormViewModel 类型的对象模型：

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

然后，我们可以更新视图代码以摆脱它。 请注意，下面我们如何不更改要创建的输入元素的名称（表单元素仍将命名为"标题"、"国家/地区"），但我们正在更新 HTML 帮助器方法，以便使用 DinnerFormViewModel 类检索值：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

在呈现错误时，我们还将更新编辑帖子方法以使用 DinnerFormViewModel 类：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

我们还可以更新我们的 Create（） 操作方法，以重复使用完全相同的*DinnerFormViewModel*类，使这些国家/地区也能够删除列表。 下面是 HTTP-GET 实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

下面是 HTTP-POST 创建方法的实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

现在，我们的"编辑"和"创建"屏幕都支持选择国家/地区的下拉列表。

### <a name="custom-shaped-viewmodel-classes"></a>自定义形状的视图模型类

在上面的场景中，我们的 DinnerFormViewModel 类直接将 Dinner 模型对象公开为属性，以及支持 SelectList 模型属性。 此方法适用于要在视图模板中创建的 HTML UI 与域模型对象相对接近的情况。

对于情况并非如此的情况，可以使用的一个选项是创建一个自定义形状的 ViewModel 类，其对象模型更优化以供视图使用，并且可能与基础域模型对象的外观完全不同。 例如，它可能会公开从多个模型对象收集的不同属性名称和/或聚合属性。

自定义形状的 ViewModel 类既可用于将数据从控制器传递到要渲染的视图，也可用于帮助处理发回控制器操作方法的表单数据。 对于此后续方案，您可能让操作方法使用发布表单的数据更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际域模型对象。

自定义形状的 ViewModel 类可以提供很大的灵活性，并且每当在视图模板中查找呈现代码或操作方法中的表单发布代码开始变得过于复杂时，都是要调查的内容。 这通常表明域模型与您生成的 UI 不干净对应，并且中间自定义形状的 ViewModel 类可以提供帮助。

### <a name="next-step"></a>下一步

现在，让我们来了解一下如何使用部分页和母版页来重用和共享整个应用程序中的 UI。

> [!div class="step-by-step"]
> [上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)

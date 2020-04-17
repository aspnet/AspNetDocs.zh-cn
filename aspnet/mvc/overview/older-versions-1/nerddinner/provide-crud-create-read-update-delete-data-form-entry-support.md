---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD（创建、读取、更新、删除）数据表单输入支持 |微软文档
author: rick-anderson
description: 步骤 5 演示如何通过支持编辑、创建和删除晚餐来进一步增加我们的 DinnersController 课程。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542620"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>提供 CRUD（创建、读取、更新和删除）数据窗体输入支持

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第5步，它介绍了如何使用 ASP.NETmVC1构建小型但完整的Web应用程序。
> 
> 步骤 5 演示如何通过支持编辑、创建和删除晚餐来进一步增加我们的 DinnersController 课程。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>神经晚餐步骤 5：创建、更新、删除表单方案

我们介绍了控制器和视图，并介绍了如何使用它们在现场为 Dinner 实现列表/详细信息体验。 我们的下一步是进一步提高我们的 DinnersController 课程，并支持编辑、创建和删除晚餐。

### <a name="urls-handled-by-dinnerscontroller"></a>由晚餐控制器处理的 URL

我们之前向 DinnersController 添加了操作方法，这些方法对两个 URL 进行了支持 *：/晚餐*和 */晚餐/详细信息/[id]。*

| **URL** | **动词** | **目标** |
| --- | --- | --- |
| */晚餐/* | GET | 显示即将来临的晚宴的 HTML 列表。 |
| */晚餐/详情/[id]* | GET | 显示有关特定晚餐的详细信息。 |

现在，我们将添加操作方法来实现三个附加*URL：/晚餐/编辑/[id]、/**晚餐/创建*和 */晚餐/删除/[id]。* 这些 URL 将支持编辑现有晚餐、创建新晚餐和删除晚餐。

我们将支持 HTTP GET 和 HTTP POST 谓词与这些新 URL 的交互。 对这些 URL 的 HTTP GET 请求将显示数据的初始 HTML 视图（在"编辑"的情况下填充了 Dinner 数据的窗体，在"创建"的情况下填充了空白表单，在"删除"的情况下显示删除确认屏幕）。 对这些 URL 的 HTTP POST 请求将保存/更新/删除我们的晚餐存储库中的晚餐数据（并从那里保存到数据库）。

| **URL** | **动词** | **目标** |
| --- | --- | --- |
| */晚餐/编辑/[id]* | GET | 显示填充晚餐数据的可编辑 HTML 表单。 |
| POST | 将特定 Dinner 的窗体更改保存到数据库。 |
| */晚餐/创建* | GET | 显示一个空的 HTML 表单，允许用户定义新的晚餐。 |
| POST | 创建新的晚餐并将其保存在数据库中。 |
| */晚餐/删除/[id]* | GET | 显示删除确认屏幕。 |
| POST | 从数据库中删除指定的晚餐。 |

### <a name="edit-support"></a>编辑支持

让我们从实现"编辑"方案开始。

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET 编辑操作方法

我们将首先实现编辑操作方法的 HTTP"GET"行为。 当请求 */Dinners/Edit/[id]* URL 时，将调用此方法。 我们的实现将如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上述代码使用 Dinner 存储库检索 Dinner 对象。 然后，它使用"晚餐"对象呈现视图模板。 由于我们尚未将模板名称显式传递给*View（）* 帮助器方法，它将使用基于约定的默认路径来解决视图模板：/视图/Dinners/Edit.aspx。

现在，让我们创建此视图模板。 我们将在"编辑"方法中右键单击并选择"添加视图"上下文菜单命令来执行此操作：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

在"添加视图"对话框中，我们将指示我们将将 Dinner 对象传递给视图模板作为其模型，并选择自动基脚模式"编辑"模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们添加新的"Edit.aspx"视图模板文件。 它还将在代码编辑器中打开新的"Edit.aspx"视图模板 ， 填充了初始的"编辑"基架实现，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

让我们对生成的默认"编辑"基架进行一些更改，并更新编辑视图模板以包含以下内容（这将删除一些我们不想公开的属性）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

当我们运行应用程序并请求 *"/晚餐/编辑/1"URL*时，我们将看到以下页面：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

我们的视图生成的 HTML 标记如下所示。 它是标准 HTML –&lt;当&gt;按下"保存"&lt;输入类型="提交"/&gt;按钮时，具有对 */Dinners/Edit/1* URL 执行 HTTP POST 的表单元素。 已为每个&lt;可编辑属性输出 HTML&gt;输入类型="文本"/元素：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm（） 和 html.TextBox（） html 帮助器方法

我们的"Edit.aspx"视图模板使用多个"Html 帮助程序"方法：Html.验证摘要（）、Html.BeginForm（）、Html.TextBox（）和 Html.验证消息（）。 除了为我们生成 HTML 标记外，这些帮助程序方法还提供内置的错误处理和验证支持。

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm（） 帮助器方法

Html.BeginForm（） 帮助器方法是在我们的标记中输出&lt;HTML&gt;表单元素的内容。 在我们的 Edit.aspx 视图模板中，您会注意到，在使用此方法时，我们正在应用 C#"使用"语句。 打开的大&lt;括号表示窗体&gt;内容的开始，而关闭的大括号表示&lt;/form&gt;元素的结束：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

或者，如果您发现"使用"语句方法对于这样的方案不自然，则可以使用 Html.BeginForm（） 和 Html.EndForm（） 组合（执行相同的功能）：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

调用 Html.BeginForm（） 没有任何参数将导致它输出对当前请求的 URL 执行 HTTP-POST 的窗体元素。 这就是为什么我们的"编辑"视图生成*&lt;表单操作\"/晚餐/编辑/1"方法="后"&gt;* 元素。 如果我们想要发布到其他 URL，我们也可以将显式参数传递给 Html.BeginForm（）。

##### <a name="htmltextbox-helper-method"></a>Html.TextBox（） 帮助器方法

我们的 Edit.aspx 视图使用 Html.TextBox（） 帮助器&lt;方法输出输入类型="文本&gt;"/元素：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上面的 Html.TextBox（） 方法采用单个参数 ， 用于指定&lt;要输出的输入类型的 id/name 属性= "text"/&gt;元素，以及用于填充文本框值的模型属性。 例如，我们传递给"编辑"视图的 Dinner 对象具有".NET 期货"的"标题"属性值，因此我们的 Html.TextBox（"标题"）方法调用输出：*&lt;输入 id="标题"名称="标题"类型="文本"值=".NET&gt;期货"/。*

或者，我们可以使用第一个 Html.TextBox（） 参数来指定元素的 ID/名称，然后显式传递值以用作第二个参数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

通常，我们希望对输出的值执行自定义格式设置。 内置于 .NET 的 String.Format（） 静态方法对于这些方案很有用。 我们的 Edit.aspx 视图模板正在使用此设置事件日期值（类型为 DateTime）的格式，以便它不显示时间上的秒数：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

可以选择使用 Html.TextBox（） 的第三个参数来输出其他 HTML 属性。 下面的代码段演示如何在&lt;输入类型="text"/&gt;元素上呈现额外的大小="30"属性和类="mycssclass"属性。 请注意，如何使用"类"@" character because "从类属性的名称中转义是 C# 中的保留关键字：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>实现 HTTP-POST 编辑操作方法

现在，我们实现了"编辑"操作方法的 HTTP-GET 版本。 当用户请求 */Dinners/Edit/1* URL 时，他们收到一个 HTML 页面，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

按下"保存"按钮会导致表单发布到 */Dinners/Edit/1* URL，并使用 HTTP POST 谓&lt;词&gt;提交 HTML 输入表单值。 现在，让我们实现编辑操作方法的 HTTP POST 行为 ， 这将处理保存晚餐。

我们将首先向 DinnersController 添加一个重载的"编辑"操作方法，该控制器上具有"AcceptVerbs"属性，指示它处理 HTTP POST 方案：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

当 [AcceptVerbs] 属性应用于重载操作方法时，ASP.NET MVC 根据传入的 HTTP 谓词自动处理向相应操作方法发送请求。 HTTP POST 对 */Dinners/Edit/[id]* URL 的请求将转到上述编辑方法，而所有其他 HTTP 谓词请求 */Dinners/Edit/[id]* URL 将转到我们实现的第一个编辑方法（`[AcceptVerbs]`该方法没有属性）。

| **侧主题：为什么通过 HTTP 谓词进行区分？** |
| --- |
| 您可能会问 – 为什么我们使用单个 URL 并通过 HTTP 谓词区分其行为？ 为什么不只有两个单独的 URL 来处理加载和保存编辑更改？ 例如：/Dinners/Edit/[id]以显示初始窗体和/Dinners/保存/[id]来处理表单帖子以保存它？ 发布两个单独的 URL 的缺点是，如果我们发布到 /Dinners/Save/2，然后由于输入错误而需要重新显示 HTML 表单，最终用户最终将在其浏览器的地址栏中具有 /Dinners/Save/2 URL（因为这是表单发布到的 URL）。 如果最终用户将此重新显示的页面标记为其浏览器收藏夹列表，或将 URL 复制/粘贴并通过电子邮件发送给朋友，则他们最终将保存将来无法工作的 URL（因为该 URL 取决于帖子值）。 通过公开单个 URL（如：/Dinners/Edit/[id]）并通过 HTTP 谓词区分其处理，最终用户可以安全地为编辑页面添加书签和/或将 URL 发送给其他人。 |

#### <a name="retrieving-form-post-values"></a>检索表单过帐值

我们可以通过多种方式访问 HTTP POST"编辑"方法中的已发布的表单参数。 一个简单的方法是只使用 Controller 基类上的 Request 属性来访问窗体集合并直接检索已过帐的值：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

不过，上述方法有点冗长，尤其是在添加错误处理逻辑后。

此方案的更好方法是在控制器基类上利用内置*的 UpdateModel（）* 帮助器方法。 它支持更新使用传入窗体参数传递的对象的属性。 它使用反射来确定对象上的属性名称，然后根据客户端提交的输入值自动转换和分配值。

我们可以使用 UpdateModel（） 方法使用此代码简化我们的 HTTP-POST 编辑操作：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

我们现在可以访问 */Dinners/Edit/1* URL，并更改我们的晚餐标题：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

单击"保存"按钮时，我们将执行"编辑"操作的表单帖子，更新的值将保留在数据库中。 然后，我们将重定向到晚餐的详细信息 URL（将显示新保存的值）：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>处理编辑错误

我们当前的 HTTP-POST 实现工作正常，除非出现错误。

当用户在编辑表单时出错时，我们需要确保表单重新显示一条信息性错误消息，以指导他们修复表单。 这包括最终用户发布不正确的输入（例如：格式不正确的日期字符串）的情况，以及输入格式有效但存在业务规则冲突的情况。 发生错误时，窗体应保留用户最初输入的输入数据，以便不必手动重新填充其更改。 此过程应根据需要重复多次，直到表单成功完成。

ASP.NET MVC 包含一些不错的内置功能，使错误处理和表单重新显示变得简单。 要查看这些功能，让我们使用以下代码更新我们的 Edit 操作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上述代码与之前的实现类似，只是我们现在正在将 try/catch 错误处理块包装在工作周围。 如果在调用 UpdateModel（） 时或尝试保存 DinnerRepository 时出现异常（如果我们试图保存的 Dinner 对象由于模型中的规则冲突而无效，则将引发异常），则将执行 catch 错误处理块。 在其中，我们循环对"晚餐"对象中存在的任何规则冲突，并将其添加到 ModelState 对象（我们稍后将讨论）。 然后，我们重新显示视图。

要看到这个工作，让我们重新运行应用程序，编辑晚餐，并更改它有一个空的标题，事件日期的"BOGUS"，并使用一个英国电话号码与国家国家值的美国。 当我们按下"保存"按钮时，我们的 HTTP POST 编辑方法将无法保存晚餐（因为存在错误），并将重新显示该窗体：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

我们的应用程序有一个体面的错误经验。 具有无效输入的文本元素以红色突出显示，验证错误消息向最终用户显示。 该窗体还保留用户最初输入的输入数据，以便他们不必重新填充任何内容。

你可能会问，这是怎么发生的？ 标题、事件日期和 ContactPhone 文本框如何以红色突出显示自己，并知道要输出最初输入的用户值？ 错误消息是如何显示在顶部列表中的？ 好消息是，这不是魔术造成的，而是因为我们使用了一些内置ASP.NET MVC 功能，使输入验证和错误处理方案变得容易。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>了解模型状态和验证 HTML 帮助器方法

控制器类具有"ModelState"属性集合，它提供了一种指示模型对象传递给 View 存在错误的方法。 ModelState 集合中的错误条目标识具有问题的模型属性的名称（例如："标题"、"事件日期"或"ContactPhone"），并允许指定人性化的错误消息（例如："需要标题"）。

*UpdateModel（）* 帮助器方法在尝试将窗体值分配给模型对象的属性时遇到错误时自动填充模型状态集合。 例如，我们的 Dinner 对象的 EventDate 属性为"日期时间"类型。 当 UpdateModel（） 方法无法在上述方案中为其分配字符串值"BOGUS"时，UpdateModel（） 方法向 ModelState 集合添加了一个条目，指示该属性发生了赋值错误。

开发人员还可以编写代码，将错误条目显式添加到 ModelState 集合中，就像我们在下面的"catch"错误处理块中所做的一样，该块基于"晚餐"对象中的活动规则冲突填充了 ModelState 集合：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Html 帮助器与模型状态集成

HTML 帮助器方法（如 Html.TextBox（） ） - 在呈现输出时选中 ModelState 集合。 如果项存在错误，则呈现用户输入的值和 CSS 错误类。

例如，在我们的"编辑"视图中，我们使用 Html.TextBox（） 帮助器方法来呈现晚餐对象的事件日期：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

在错误方案中呈现视图时，Html.TextBox（） 方法检查了 ModelState 集合，以查看是否存在与 Dinner 对象的"EventDate"属性关联的任何错误。 当它确定存在错误时，它呈现提交的用户输入（"BOGUS"）作为值，并将 css 错误类添加到&lt;它生成的输入类型="textbox"/&gt;标记：

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

您可以自定义 css 错误类的外观，以按所需时间查看。 默认 CSS 错误类 （ "输入验证-错误" ） 在 *_content_site.css*样式表中定义，如下所示：

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

此 CSS 规则导致无效输入元素突出显示的原因如下：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.验证消息（） 帮助器方法

Html.验证消息（） 帮助器方法可用于输出与特定模型属性关联的 ModelState 错误消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上述代码输出：*&lt;跨类="字段验证错误"&gt;值"BOGUS"无效&lt;/跨&gt;*

Html.验证消息（） 帮助器方法还支持第二个参数，该参数允许开发人员重写显示的错误文本消息：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上述代码输出：*&lt;跨类="字段验证-错误"/span，&gt;\*&lt;&gt;* 而不是当 EventDate 属性存在错误时，而不是默认错误文本。

##### <a name="htmlvalidationsummary-helper-method"></a>Html.验证摘要（） 帮助器方法

Html.验证摘要（） 帮助程序方法可用于呈现摘要错误消息，并附带 ModelState 集合中&lt;所有&gt;&lt;详细错误消息&gt;&lt;的&gt;ul li//ul 列表：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.验证摘要（） 帮助程序方法采用可选字符串参数 ， 它定义一个摘要错误消息，以显示在详细错误列表的上方：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

您可以选择使用 CSS 来覆盖错误列表的外观。

#### <a name="using-a-addruleviolations-helper-method"></a>使用添加规则冲突帮助器方法

我们的初始 HTTP-POST 编辑实现使用 catch 块中的 foreach 语句来循环访问 Dinner 对象的"规则冲突"，并将它们添加到控制器的 ModelState 集合中：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

通过将"控制器帮助器"类添加到 NerdDinner 项目中，并在其中实现"AddRuleRule冲突"扩展方法，将帮助器方法添加到ASP.NET MVC ModelState字典类，我们可以使此代码更简洁一些。 此扩展方法可以使用规则冲突错误列表封装填充 ModelState字典所需的逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

然后，我们可以更新我们的 HTTP-POST 编辑操作方法，以使用此扩展方法使用我们的晚餐规则冲突填充 ModelState 集合。

#### <a name="complete-edit-action-method-implementations"></a>完整的编辑操作方法实现

以下代码实现了编辑方案所需的所有控制器逻辑：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

我们的 Edit 实现好处是，我们的 Controller 类和 View 模板都不需要了解我们的 Dinner 模型正在强制执行的特定验证或业务规则。 将来，我们可以向模型添加其他规则，并且不必对我们的控制器或视图进行任何代码更改，以便支持这些规则。 这为我们提供了灵活性，以便在未来以最少的代码更改轻松发展我们的应用程序需求。

### <a name="create-support"></a>创建支持

我们已经完成了晚餐控制器类的"编辑"行为。 现在，让我们继续实现其上的"创建"支持 - 这将使用户能够添加新的晚餐。

#### <a name="the-http-get-create-action-method"></a>HTTP-GET 创建操作方法

我们将首先实现创建操作方法的 HTTP"GET"行为。 当有人访问 */Dinners/创建*URL 时，将调用此方法。 我们的实现如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上面的代码将创建一个新的 Dinner 对象，并将其事件日期属性分配为将来一周。 然后，它呈现基于新"晚餐"对象的视图。 由于我们尚未显式将名称传递给*View（）* 帮助器方法，它将使用基于约定的默认路径来解决视图模板：/视图/Dinners/Create.aspx。

现在，让我们创建此视图模板。 我们可以在"创建操作"方法中右键单击并选择"添加视图"上下文菜单命令来执行此操作。 在"添加视图"对话框中，我们将指示我们将将 Dinner 对象传递到视图模板，并选择自动基脚手架"创建"模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

单击"添加"按钮时，Visual Studio 会将基于脚手架的新"Create.aspx"视图保存到"_Views_Dinners"目录，并在 IDE 中将其打开：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

让我们对为我们生成的默认"创建"基架文件进行一些更改，并将其修改为如下所示：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

现在，当我们运行应用程序并访问浏览器中的 *"/Dinner/Create"URL*时，它将从我们的"创建操作"实现中呈现如下 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>实现 HTTP-POST 创建操作方法

我们实现了"创建操作方法"的 HTTP-GET 版本。 当用户单击"保存"按钮时，它会执行表单发布到 */Dinners/Create* URL，并使用 HTTP POST 谓词&lt;提交&gt;HTML 输入表单值。

现在，让我们实现创建操作方法的 HTTP POST 行为。 我们将首先向 DinnersController 添加一个重载的"创建"操作方法，该控制器上具有"AcceptVerbs"属性，指示它处理 HTTP POST 方案：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

我们可以通过多种方式访问启用 HTTP-POST 的"创建"方法中的已过帐表单参数。

一种方法是创建新的 Dinner 对象，然后使用*UpdateModel（）* 帮助器方法（就像我们使用"编辑"操作所做的那样）使用张贴的表单值填充它。 然后，我们可以将其添加到 DinnerRepository 中，将其保存到数据库中，并将用户重定向到"详细信息"操作，以便使用以下代码显示新创建的 Dinner：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

或者，我们可以使用一种方法，其中我们的 Create（） 操作方法将 Dinner 对象作为方法参数。 然后ASP.NET MVC 将自动为我们实例化新的 Dinner 对象，使用表单输入填充其属性，并将其传递给我们的操作方法：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上述操作方法通过检查 ModelState.IsValid 属性，验证 Dinner 对象已成功填充表单后值。 如果存在输入转换问题（例如：EventDate 属性的"BOGUS"字符串），并且有任何问题，我们的操作方法将重新显示窗体，则返回 false。

如果输入值有效，则操作方法将尝试将新 Dinner 添加到 DinnerRepository 中。 它将这项工作包装在 try/catch 块中，如果有任何违反业务规则的行为（这将导致晚餐存储库.Save（） 方法引发异常，则重新显示表单。

要查看此错误处理行为是否在起作用，我们可以请求 */Dinners/Create* URL 并填写有关新晚餐的详细信息。 输入或值不正确将导致重新显示创建窗体，并突出显示错误如下：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

请注意，我们的"创建"窗体如何遵守与"编辑"窗体完全相同的验证和业务规则。 这是因为我们的验证和业务规则是在模型中定义的，并且未嵌入到应用程序的 UI 或控制器中。 这意味着我们以后可以在一个位置更改/发展我们的验证或业务规则，并在整个应用程序中应用这些规则。 我们不必更改"编辑"或"创建操作方法"中的任何代码，即可自动遵守任何新规则或对现有规则的修改。

当我们修复输入值并再次单击"保存"按钮时，我们添加到 DinnerRepository 将成功，并且将添加新的 Dinner 添加到数据库中。 然后，我们将重定向到 */Dinners/详细信息/[id]* URL - 我们将向这里介绍有关新创建的晚餐的详细信息：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>删除支持

现在，让我们向"删除"支持添加到我们的晚餐控制器。

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET 删除操作方法

我们将首先实现删除操作方法的 HTTP GET 行为。 当有人访问 */Dinners/Delete/[id]* URL 时，将调用此方法。 以下是实现：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

操作方法尝试检索要删除的"晚餐"。 如果"晚餐"存在，则根据"晚餐"对象呈现视图。 如果对象不存在（或已被删除），它将返回一个视图，该视图呈现了我们之前为"详细信息"操作方法创建的"NotFound"视图模板。

我们可以在"删除操作"方法中右键单击并选择"添加视图"上下文菜单命令来创建"删除"视图模板。 在"添加视图"对话框中，我们将指示我们将将 Dinner 对象作为模型传递给视图模板，并选择创建空模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们添加新的"Delete.aspx"视图模板文件。 我们将向模板添加一些 HTML 和代码，以实现如下删除确认屏幕：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上面的代码显示要删除的 Dinner 的标题，并在最终用户单击其中的"删除&lt;"&gt;按钮时输出对 /Dinners/Delete/[id] URL 执行 POST 的表单元素。

当我们运行应用程序并访问有效 Dinner 对象的 *"/晚餐/删除/[id]"URL*时，它将呈现如下 UI：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **侧主题：我们为什么要进行 POST？** |
| --- |
| 您可能会问 – 我们为什么要在"删除"确认屏幕中&lt;创建&gt;表单？ 为什么不只使用标准超链接链接到执行实际删除操作的操作方法？ 原因是，我们希望小心防范 Web 爬网者和搜索引擎发现我们的 URL，并在跟踪链接时无意中导致数据被删除。 基于 HTTP-GET 的 URL 被视为"安全"的 URL，它们可以访问/爬网，并且它们不应遵循 HTTP-POST URL。 一个好的规则是确保您始终将破坏性或数据修改操作放在 HTTP-POST 请求后面。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>实现 HTTP-POST 删除操作方法

现在，我们实现了 HTTP-GET 版本的删除操作方法，显示删除确认屏幕。 当最终用户单击"删除"按钮时，它将执行表单发布到 */Dinners/Dinner/[id]* URL。

现在，让我们使用以下代码实现删除操作方法的 HTTP"POST"行为：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

HTTP-POST 版本的"删除"操作方法尝试检索要删除的晚餐对象。 如果找不到它（因为它已被删除），它将呈现我们的"未找到"模板。 如果它找到晚餐，它会从晚餐存储库中删除它。 然后，它呈现一个"已删除"模板。

要实现"已删除"模板，我们将在操作方法中右键单击并选择"添加视图"上下文菜单。 我们将视图命名为"已删除"，并将其命名为空模板（而不是采用强类型模型对象）。 然后，我们将向其中添加一些 HTML 内容：

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

现在，当我们运行我们的应用程序，并访问有效的晚餐对象的 *"/晚餐/删除/[id]"URL*时，它将呈现我们的晚餐删除确认屏幕，如下所示：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

当我们单击"删除"按钮时，它将对 */Dinners/Delete/[id]* URL 执行 HTTP-POST，这将从我们的数据库中删除晚餐，并显示我们的"已删除"视图模板：

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>模型绑定安全性

我们讨论了使用ASP.NET MVC 的内置模型绑定功能的两种不同的方法。 第一个使用 UpdateModel（） 方法更新现有模型对象的属性，第二个使用 ASP.NET mVC 支持将模型对象作为操作方法参数传递。 这两种技术都非常强大，非常有用。

这种力量也带来了责任。 在接受任何用户输入时，始终对安全性持偏执状态很重要，在绑定对象以形成输入时也是如此。 您应该始终小心 HTML 编码任何用户输入的值，以避免 HTML 和 JavaScript 注入攻击，并小心 SQL 注入攻击（请注意：我们使用 LINQ 到 SQL 作为应用程序，它会自动对参数进行编码，以防止这些类型的攻击）。 您绝不应仅依赖客户端验证，并且始终使用服务器端验证来防止黑客试图向您发送虚假值。

使用 ASP.NET MVC 的绑定功能时，要确保考虑的另一个安全项是绑定对象的范围。 具体来说，您希望确保您了解允许绑定的属性的安全含义，并确保仅允许最终用户更新真正应该更新的属性。

默认情况下，UpdateModel（） 方法将尝试更新模型对象上与传入窗体参数值匹配的所有属性。 同样，默认情况下作为操作方法参数传递的对象可以通过窗体参数设置其所有属性。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>按使用情况锁定绑定

通过提供可更新的属性的显式"包含列表"，可以按使用情况锁定绑定策略。 这可以通过将额外的字符串数组参数传递给 UpdateModel（） 方法来实现，如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

作为操作方法参数传递的对象还支持 [Bind] 属性，该属性允许如下指定允许属性的"包含列表"：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>在类型上锁定绑定

您还可以按类型锁定绑定规则。 这允许您指定绑定规则一次，然后将它们应用于所有控制器和操作方法的所有方案（包括 UpdateModel 和操作方法参数方案）。

您可以通过将 [Bind] 属性添加到类型上，或通过在应用程序的 Global.asax 文件中注册来自定义每种类型的绑定规则（对于您不拥有该类型的方案非常有用）。 然后，可以使用 Bind 属性的"包含"和"排除"属性来控制特定类或接口可绑定哪些属性。

我们将在 NerdDinner 应用程序中对 Dinner 类使用此技术，并为其添加 [Bind] 属性，将可绑定属性列表限制为以下内容：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

请注意，我们不允许通过绑定操作 RSSP 集合，也不允许通过绑定设置 DinnerID 或托管比属性。 出于安全原因，我们将只使用操作方法中的显式代码来操作这些特定属性。

### <a name="crud-wrap-up"></a>CRUD 总结

ASP.NET MVC 包含许多内置功能，可帮助实现表单发布方案。 我们使用多种功能在晚餐存储库上提供 CRUD UI 支持。

我们使用以模型为中心的方法来实现我们的应用程序。 这意味着我们所有的验证和业务规则逻辑都在我们的模型层中定义，而不是在我们的控制器或视图中定义。 我们的 Controller 类和 View 模板都不知道我们的 Dinner 模型类正在强制执行的特定业务规则。

这将保持我们的应用程序体系结构清洁，并使其更易于测试。 将来，我们可以向模型层添加其他业务规则，而不必对我们的控制器或视图*进行任何代码更改*，以便支持这些规则。 这将为我们提供极大的敏捷性，以便我们在未来发展和改变我们的应用程序。

我们的晚餐控制器现在启用晚餐列表/详细信息，以及创建、编辑和删除支持。 类的完整代码如下所示：

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>下一步

现在，我们的 DinnersController 类中实现了基本的 CRUD（创建、读取、更新和删除）支持。

现在，让我们来看看如何使用 ViewData 和 ViewModel 类在我们的窗体上启用更丰富的 UI。

> [!div class="step-by-step"]
> [上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)

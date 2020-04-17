---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 迭代#7 = 添加 Ajax 功能 （VB） |微软文档
author: rick-anderson
description: 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: 04eaaa129a56b765c090e64118ed528c65987b50
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542295"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>迭代 7 – 添加 Ajax 功能 (VB)

由[微软](https://github.com/microsoft)

[下载代码](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建 MVC 应用程序 （VB） ASP.NET联系人管理

在本系列教程中，我们从头到尾构建整个联系人管理应用程序。 通过联系人管理器应用程序，您可以存储联系人信息 （姓名、电话号码和电子邮件地址） 人员列表。

我们通过多次迭代构建应用程序。 每次迭代时，我们都会逐步改进应用程序。 此多迭代方法的目标是使您能够了解每次更改的原因。

- 迭代#1 - 创建应用程序。 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。

- 迭代#2 - 使应用程序看起来不错。 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。

- 迭代#3 - 添加表单验证。 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证电子邮件地址和电话号码。

- 迭代#4 - 使应用程序松散耦合。 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 例如，我们重构应用程序以使用存储库模式和依赖项注入模式。

- 迭代#5 - 创建单元测试。 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。

- 迭代#6 - 使用测试驱动开发。 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代#7 - 添加Ajax功能。 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。

## <a name="this-iteration"></a>此迭代

在此迭代的联系人管理器应用程序中，我们将重构应用程序以使用 Ajax。 通过使用Ajax，我们使我们的应用程序响应更快。 当只需要更新页面中的某个区域时，我们可以避免呈现整个页面。

我们将重构索引视图，以便每当有人选择新的联系人组时，我们就不需要重新显示整个页面。 相反，当有人单击联系人组时，我们只会更新联系人列表，并单独保留页面的其余部分。

我们还将更改删除链接的工作方式。 我们将显示 JavaScript 确认对话框，而不是显示单独的确认页。 如果确认要删除联系人，则对服务器执行 HTTP DELETE 操作以从数据库中删除联系人记录。

此外，我们将利用 jQuery 将动画效果添加到索引视图中。 当从服务器提取新的联系人列表时，我们将显示一个动画。

最后，我们将利用ASP.NETAJAX框架支持来管理浏览器历史记录。 每当执行 Ajax 调用以更新联系人列表时，我们都会创建历史记录点。 这样，浏览器的后退和向前按钮将工作。

## <a name="why-use-ajax"></a>为什么要使用Ajax？

使用Ajax有很多好处。 首先，将Ajax功能添加到应用程序中可以提供更好的用户体验。 在正常 Web 应用程序中，每次用户执行操作时，都必须将整个页面发回服务器。 每当执行操作时，浏览器都会锁定，用户必须等待，直到提取并重新显示整个页面。

在桌面应用程序的情况下，这是不可接受的体验。 但是，传统上，我们生活在一个Web应用程序的情况下，这种糟糕的用户体验，因为我们不知道我们可以做得更好。 我们认为这是Web应用程序的一个限制，而实际上，这只是我们想象力的一个限制。

在 Ajax 应用程序中，无需仅更新页面就停止用户体验。 相反，您可以在后台执行异步请求以更新页面。 在页面部分更新时，不会强制用户等待。

通过使用Ajax，您还可以提高应用程序的性能。 请考虑联系人管理器应用程序现在如何工作，而无需 Ajax 功能。 单击联系人组时，必须重新显示整个索引视图。 必须从数据库服务器检索联系人列表和联系人组列表。 所有这些数据都必须通过从 Web 服务器到 Web 浏览器的线传递。

但是，在将 Ajax 功能添加到应用程序后，我们可以避免在用户单击联系人组时重新播放整个页面。 我们不再需要从数据库获取联系人组。 我们也不需要将整个索引视图推送到导线上。 通过使用 Ajax，我们减少了数据库服务器必须执行的工作量，并减少了应用程序所需的网络流量。

## <a name="don-t-be-afraid-of-ajax"></a>不要害怕阿贾克斯

一些开发人员避免使用Ajax，因为他们担心低级浏览器。 他们希望确保他们的 Web 应用程序在不受支持 JavaScript 的浏览器访问时仍然有效。 由于Ajax依赖于JavaScript，一些开发人员避免使用Ajax。

但是，如果您对如何实现Ajax很小心，则可以构建同时使用高级浏览器和低级浏览器的应用程序。 我们的联系人管理器应用程序将适用于支持 JavaScript 的浏览器和不支持的浏览器。

如果将联系人管理器应用程序与支持 JavaScript 的浏览器一起使用，那么您将有更好的用户体验。 例如，当您单击联系人组时，将仅更新显示联系人的页面区域。

另一方面，如果将联系人管理器应用程序用于不支持 JavaScript（或禁用了 JavaScript）的浏览器，则您的用户体验将稍逊一筹。 例如，当您单击联系人组时，必须将整个 Index 视图发回浏览器才能显示联系人的匹配列表。

## <a name="adding-the-required-javascript-files"></a>添加所需的 JavaScript 文件

我们需要使用三个 JavaScript 文件将 Ajax 功能添加到我们的应用程序中。 所有这些文件都包含在新的ASP.NET MVC 应用程序的脚本文件夹中。

如果您计划在应用程序中的多个页面中使用Ajax，那么在应用程序的视图母版页中包含所需的 JavaScript 文件是有意义的。 这样，JavaScript 文件将自动包含在应用程序中的所有页面中。

在视图母版页&lt;的头部&gt;标记中添加以下 JavaScript：

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>重构索引视图以使用 Ajax

让我们首先修改我们的 Index 视图，以便单击联系人组仅更新显示联系人的视图区域。 图 1 中的红色框包含我们要更新的区域。

[![仅更新联系人](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**图 01**：仅更新联系人（[单击以查看全尺寸图像](iteration-7-add-ajax-functionality-vb/_static/image2.png)）

第一步是将要异步更新的视图部分分离为单独的部分（视图用户控件）。 显示联系人表的 Index 视图部分已移动到清单 1 中的部分。

**清单 1 - 视图\联系人\联系人列表.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

请注意，清单 1 中的部分具有与索引视图不同的模型。 %@ Page %&lt;&gt;指令中的&lt;*继承*属性指定从 ViewUserControl 组&gt;类的部分继承。

更新的索引视图包含在清单 2 中。

**清单2 - 视图\联系人\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

关于清单2中更新的视图，您应该注意两件事。 首先，请注意，移动到部分的所有内容都将替换为对 Html.Render 部分（）的调用。 首次请求索引视图以显示初始联系人集时调用 Html.Render 部分（） 方法。

其次，请注意，用于显示联系人组的 Html.ActionLink（） 已替换为 Ajax.ActionLink（）。 Ajax.ActionLink（）使用以下参数调用：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

第一个参数表示要显示的链接的文本，第二个参数表示路由值，第三个参数表示 Ajax 选项。 在这种情况下，我们使用 UpdateTargetId Ajax 选项来指向要在 Ajax &lt;&gt;请求完成后更新的 HTML div 标记。 我们希望使用新的联系人列表&lt;更新&gt;div 标记。

联系人控制器的更新索引（） 方法包含在清单 3 中。

**清单3 - 控制器\联系控制器.vb（索引方法）**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

更新的 Index（） 操作有条件地返回两件事情之一。 如果 Ajax 请求调用了 Index（） 操作，则控制器返回部分。 否则，Index（） 操作将返回整个视图。

请注意，当 Ajax 请求调用时，Index（） 操作不需要返回尽可能多的数据。 在正常请求的上下文中，Index 操作返回所有联系人组和所选联系人组的列表。 在 Ajax 请求的上下文中，Index（） 操作仅返回选定的组。 Ajax 意味着数据库服务器上的工作更少。

我们修改的 Index 视图适用于上层浏览器和低级浏览器。 如果单击联系人组，并且您的浏览器支持 JavaScript，则仅更新包含联系人列表的视图区域。 另一方面，如果您的浏览器不支持 JavaScript，则整个视图将更新。

我们更新的索引视图有一个问题。 单击联系人组时，所选组不会突出显示。 由于组列表显示在 Ajax 请求期间更新的区域之外，因此不会突出显示正确的组。 我们将在下一节中解决此问题。

## <a name="adding-jquery-animation-effects"></a>添加 jQuery 动画效果

通常，当您单击网页中的链接时，可以使用浏览器进度栏来检测浏览器是否主动获取更新的内容。 另一方面，当执行 Ajax 请求时，浏览器进度栏不显示任何进度。 这会使用户感到紧张。 您如何知道浏览器是否已冻结？

有几种方法可以向用户指示在执行 Ajax 请求时正在执行工作。 一种方法是显示一个简单的动画。 例如，当 Ajax 请求开始并淡入该区域时，可以淡出该区域。"

我们将使用 Microsoft ASP.NET MVC 框架中包含的 jQuery 库来创建动画效果。 更新的索引视图包含在清单 4 中。

**清单4 - 视图_联系人_Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

请注意，更新的索引视图包含三个新的 JavaScript 函数。 单击新联系人组时，前两个函数使用 jQuery 淡入淡出并淡入联系人列表中。 当 Ajax 请求导致错误（例如，网络超时）时，第三个函数将显示一条错误消息。

第一个函数还负责突出显示所选组。 类* 所选属性将添加到单击的元素的父元素（LI 元素）。 同样，jQuery 便于选择正确的元素并添加 CSS 类。

这些脚本在Ajax.ActionLink（））AjaxOptions参数的帮助下与组链接相关联。 更新的Ajax.ActionLink（）方法调用如下所示：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>添加浏览器历史记录支持

通常，当您单击链接以更新页面时，您的浏览器历史记录将更新。 这样，您可以单击浏览器"后退"按钮以及时移回页面的上一个状态。 例如，如果您单击"好友联系人组"然后单击"业务联系人组"，则可以单击浏览器"后退"按钮，在选择"好友联系人组"时导航回页面状态。

遗憾的是，执行 Ajax 请求不会自动更新浏览器历史记录。 如果单击联系人组，并且使用 Ajax 请求检索匹配联系人的列表，则浏览器历史记录不会更新。 选择新的联系人组后，不能使用浏览器"后退"按钮导航回联系人组。

如果您希望用户在执行 Ajax 请求后能够使用浏览器"后退"按钮，则需要执行更多工作。 您需要利用 ASP.NET AJAX 框架中构建的浏览器历史记录管理功能。

ASP.NET AJAX 浏览器历史记录，您需要执行以下三项操作：

1. 通过将启用浏览器历史记录属性设置为 true，启用浏览器历史记录。
2. 通过调用 addHistoryPoint（） 方法，在视图状态发生变化时保存历史记录点。
3. 引发导航事件时重建视图的状态。

更新的索引视图包含在清单 5 中。

**清单5 - 视图_联系人_Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

在清单5中，浏览器历史记录在页面 Init（） 函数中启用。 pageInit（） 函数还用于设置导航事件的事件处理程序。 每当浏览器"前进"或"后退"按钮导致页面状态更改时，将引发导航事件。

单击联系人组时将调用开始联系人列表（） 方法。 此方法通过调用 add 历史点（） 方法创建新的历史记录点。 单击的联系人组的 ID 将添加到历史记录中。

从联系人组链接上的扩展属性检索组 ID。 链接呈现与以下调用Ajax.ActionLink（）。

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

传递给Ajax.ActionLink（）的最后一个参数将名为 groupid 的 expando 属性添加到链接（XHTML 兼容性小写）。

当用户点击浏览器"后退"或"前进"按钮时，将引发导航事件并调用 navigate（） 方法。 此方法更新页面中显示的联系人，以匹配与传递给导航方法的浏览器历史记录点对应的页面状态。

## <a name="performing-ajax-deletes"></a>执行 Ajax 删除

目前，要删除联系人，您需要单击"删除"链接，然后单击删除确认页中显示的"删除"按钮（参见图 2）。 这似乎是很多页面请求，以做一些简单的事情，如删除数据库记录。

[![删除确认页](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**图 02**： 删除确认页（[单击以查看全尺寸图像](iteration-7-add-ajax-functionality-vb/_static/image4.png)）

最好跳过删除确认页，直接从索引视图中删除联系人。 您应该避免这种诱惑，因为采用这种方法会将应用程序打开到安全漏洞中。 通常，在调用修改 Web 应用程序状态的操作时，不希望执行 HTTP GET 操作。 执行删除时，要执行 HTTP POST，或者更好的是执行 HTTP DELETE 操作。

"删除"链接包含在"联系人列表"部分中。 清单 6 中包含联系人列表部分的更新版本。

**清单 6 - 视图\联系人列表.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

删除链接呈现与以下调用 Ajax.ImageActionLink（） 方法：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink（）不是mVCASP.NET标准部分。 Ajax.ImageActionLink（）是联系人管理器项目中包括的自定义帮助器方法。

AjaxOptions 参数有两个属性。 首先，"确认"属性用于显示弹出的 JavaScript 确认对话框。 其次，HttpMethod 属性用于执行 HTTP DELETE 操作。

清单7包含已添加到联系人控制器的新 AjaxDelete（） 操作。

**清单7 - 控制器\联系控制器.vb（Ajax删除）**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete（） 操作使用 AcceptVerbs 属性进行修饰。 此属性可防止调用操作，但 HTTP DELETE 操作以外的任何 HTTP 操作除外。 特别是，您不能使用 HTTP GET 调用此操作。

删除数据库记录后，需要显示不包含已删除记录的联系人的更新列表。 AjaxDelete（） 方法返回联系人列表部分和更新的联系人列表。

## <a name="summary"></a>总结

在此迭代中，我们将 Ajax 功能添加到我们的联系人管理器应用程序中。 我们使用Ajax来提高应用程序的响应性和性能。

首先，我们重构了 Index 视图，以便单击联系人组不会更新整个视图。 相反，单击联系人组只会更新联系人列表。

接下来，我们使用 jQuery 动画效果淡入淡出并淡入联系人列表中。 向 Ajax 应用程序添加动画可用于向应用程序的用户提供等效的浏览器进度栏。

我们还向 Ajax 应用程序添加了浏览器历史记录支持。 我们允许用户单击浏览器"后退"和"前进"按钮以更改"索引"视图的状态。

最后，我们创建了一个支持 HTTP DELETE 操作的删除链接。 通过执行 Ajax 删除，我们允许用户删除数据库记录，而无需用户请求额外的删除确认页。

> [!div class="step-by-step"]
> [上一篇](iteration-6-use-test-driven-development-vb.md)

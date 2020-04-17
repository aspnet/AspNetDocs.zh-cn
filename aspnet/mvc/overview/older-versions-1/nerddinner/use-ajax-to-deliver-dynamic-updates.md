---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 提供动态更新 |微软文档
author: rick-anderson
description: 步骤 10 支持登录用户 RSVP，他们有兴趣参加晚宴，使用基于 Ajax 的方法集成在晚餐详细信息中...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541242"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>使用 AJAX 提供动态更新

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第10步，该教程演示如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。
> 
> 步骤 10 使用在晚餐详细信息页中集成的基于 Ajax 的方法，实现对登录用户的支持，以便 RSVP 让他们对参加晚宴感兴趣。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>神经晚餐步骤 10： AJAX 启用 RSV 接受

现在，让我们对登录用户实施支持，以便 RSVP 对参加晚宴感兴趣。 我们将使用在晚餐详细信息页中集成的基于 AJAX 的方法启用此功能。

### <a name="indicating-whether-the-user-is-rsvpd"></a>指示用户是否为 RSVP'd

用户可以访问 */Dinners/详细信息/[id]* URL 以查看有关特定晚餐的详细信息：

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

详细信息（）操作方法的实现方式是这样的：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

实现 RSVP 支持的第一步是向我们的 Dinner 对象（在之前构建的Dinner.cs部分类中）添加"IsUser 注册（用户名）"帮助器方法。 此帮助程序方法返回 true 或 false，具体取决于用户当前是晚餐的 RSVP d：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

然后，我们可以向 Details.aspx 视图模板添加以下代码，以显示指示用户是否已注册的事件的适当消息：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

现在，当用户访问他们注册的晚餐时，他们会看到此消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

当他们访问晚餐时，他们没有注册，他们会看到以下消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>实现寄存器操作方法

现在，让我们添加必要的功能，使用户能够从详细信息页面到 RSVP 共进晚餐。

为了实现这一点，我们将通过右键单击 \控制器目录并选择"添加控制器&gt;"菜单命令创建新的"RSVPController"类。

我们将在新的 RSVPController 类中实现"注册"操作方法，该方法以 Dinner 的 ID 作为参数，检索相应的 Dinner 对象，检查登录用户当前是否位于已注册的用户列表中，如果没有为其添加 RSVP 对象：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

请注意，我们如何返回一个简单的字符串作为操作方法的输出。 我们本可以将此消息嵌入到视图模板中 ，但由于它非常小，我们只需在控制器基类上使用 Content（） 帮助器方法，并返回如下所示的字符串消息。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>使用 AJAX 调用 RSVPForEvent 操作方法

我们将使用 AJAX 从"详细信息"视图中调用注册操作方法。 实现这一点非常简单。 首先，我们将添加两个脚本库引用：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

第一个库引用 ASP.NET AJAX 客户端脚本库的核心。 此文件的大小约为 24k（压缩），包含核心客户端 AJAX 功能。 第二个库包含与ASP.NET MVC 的内置 AJAX 帮助器方法集成的实用程序函数（我们稍后会使用）。

然后，我们可以更新我们之前添加的视图模板代码，以便我们不是提供"您未注册此事件"消息，而是呈现一个链接，当推送时执行 AJAX 调用时，该链接会调用我们的 RSVPForEvent 操作方法，并在用户中调用 RSVP：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上面使用的Ajax.ActionLink（） 帮助器方法内置于mVCASP.NET，与 Html.ActionLink（） 帮助器方法类似，只不过，在单击链接时，它不是执行标准导航，而是对操作方法发出 AJAX 调用。 上面我们调用"RSVP"控制器上的"注册"操作方法，并将 DinnerID 作为"id"参数传递给它。 我们传递的最终 AjaxOptions 参数表示，我们希望获取从操作方法返回的内容，并更新 ID 为"rsvpmsg"的页面上的 HTML &lt;div&gt;元素。

现在，当用户浏览到尚未注册的晚餐时，他们会看到指向 RSVP 的链接：

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

如果他们单击"此事件的 RSVP"链接，他们将对 RSVP 控制器上的注册操作方法进行 AJAX 调用，并且当它完成后，他们将看到如下更新的消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

进行此 AJAX 调用时所涉及的网络带宽和流量非常轻量。 当用户单击"此事件的 RSVP"链接时，将针对在线路上如下所示的 */Dinners/Register/1* URL 发出小型 HTTP POST 网络请求：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

我们的注册操作方法的响应很简单：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

此轻量级呼叫速度很快，即使在速度较慢的网络上也能正常工作。

### <a name="adding-a-jquery-animation"></a>添加 jQuery 动画

我们实现的AJAX功能工作良好，速度快。 但是，有时发生得如此之快，以至于用户可能没有注意到 RSVP 链接已被新文本替换。 为了使结果更加明显一点，我们可以添加一个简单的动画来吸引对更新消息的注意。

默认ASP.NET MVC 项目模板包括 jQuery - 一个出色的（非常受欢迎的）开源 JavaScript 库，也受 Microsoft 支持。 jQuery 提供了许多功能，包括不错的 HTML DOM 选择和效果库。

要使用 jQuery，我们将首先向其添加脚本引用。 由于我们将在网站内的各种位置使用 jQuery，因此我们将在 Site.master 页面文件中添加脚本引用，以便所有页面都可以使用它。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*提示：请确保您已为 VS 2008 SP1 安装了 JavaScript 智能感知修补程序，从而能够对 JavaScript 文件（包括 jQuery）提供更丰富的对讲义支持。您可以通过以下位置下载：http://tinyurl.com/vs2008javascripthotfix*

使用 JQuery 编写的代码通常使用全局"$（）"JavaScript 方法，该方法使用 CSS 选择器检索一个或多个 HTML 元素。 例如 *，$（"#rsvpmsg"）* 选择任何具有 rsvpmsg ID 的 HTML 元素，而 *$（".某事"）* 将选择具有"某物"CSS 类名称的所有元素。 您还可以使用选择器查询编写更高级的查询，如"返回所有已检查的单选按钮"，例如 *：$（"输入="@type收音机**）"。@checked*

选择元素后，可以调用方法对它们执行操作，例如隐藏它们 *：$（"#rsvpmsg"）。"隐藏";*

对于我们的 RSVP 方案，我们将定义一个名为"AnimateRSVPMessage"的简单 JavaScript 函数，该函数选择"rsvpmsg"div&lt;&gt;并为其文本内容的大小设置动画。 下面的代码将文本启动较小，然后使其在 400 毫秒的时间内增加：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

然后，我们可以通过将其名称传递给我们的Ajax.ActionLink（） 帮助器方法（通过AjaxOptions"OnSuccess"事件属性）来连接此 JavaScript 函数，以在 AJAX 调用成功完成后调用它：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

现在，当单击"此事件的 RSVP"链接并成功完成我们的 AJAX 呼叫时，发回的内容消息将设置动画并变大：

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

除了提供"On成功"事件外，AjaxOptions 对象还公开了您可以处理的 OnBegin、OnOn 失败和 OnComplete 事件（以及各种其他属性和有用的选项）。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>清理 - 重构 RSVP 部分视图

我们的详细信息视图模板开始变得有点长，加班会使它很难理解。 为了帮助提高代码的可读性，让我们通过创建一个部分视图 （ RSVPStatus.ascx） 来完成，该视图封装了我们详细信息页的所有 RSVP 视图代码。

我们可以通过右键单击 [Views_Dinners] 文件夹，然后选择"添加-&gt;视图"菜单命令来执行此操作。 我们将它采用晚餐对象作为其强类型视图模型。 然后，我们可以复制/粘贴从我们的细节.aspx 视图的 RSVP 内容到它。

完成此操作后，我们还要创建另一个部分视图 - EditAndDeleteLinks.ascx - 封装我们的"编辑"和"删除"链接视图代码。 我们还将它将一个 Dinner 对象作为其强类型视图模型，并将"编辑"和"删除"逻辑从"详细信息.aspx"视图中复制/粘贴到该对象中。

然后，我们的详细信息视图模板可以只包括底部的两个 Html.Render 部分（） 方法调用：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

这使得代码的读取和维护更简洁。

### <a name="next-step"></a>下一步

现在，让我们来看看如何进一步使用AJAX，并将交互式映射支持添加到我们的应用程序。

> [!div class="step-by-step"]
> [上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)

---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: 动态填充控件 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到 t 上的目标控件...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 369beea703f84bb787ec132a357f016c2a74e6bd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131227"
---
# <a name="dynamically-populating-a-control-vb"></a>动态填充控件 (VB)

通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。

## <a name="overview"></a>概述

`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。 本教程演示如何对此进行设置。

## <a name="steps"></a>步骤

首先，需要 ASP.NET Web 服务实现的方法调用的`DynamicPopulate`。 Web 服务类需要`ScriptService`中定义的特性`Microsoft.Web.Script.Services`; 否则，ASP.NET AJAX 不能创建又所需的 web 服务客户端的 JavaScript 代理`DynamicPopulate`。

Web 方法必须预料到一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。 以下 web 服务所表示的格式返回当前日期`contextKey`参数：

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

Web 服务然后另存为`DynamicPopulate.vb.asmx`。 或者，可以实现`getDate()`方法与实际的 ASP.NET 页内的页面方法作为`DynamicPopulate`控件。

在下一步，创建新的 ASP.NET 文件。 如往常一样，第一步是包括`ScriptManager`来加载 ASP.NET AJAX 库并使控件工具包工作在当前页中：

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

然后，添加一个 label 控件 (例如使用具有相同名称的 HTML 控件或&lt; `asp:Label`  / &gt; web 控件) 的更高版本将显示 web 服务调用的结果。

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

然后将使用 （作为 HTML 控件，因为我们不需要回发到服务器） 的 HTML 按钮来触发动态填充：

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

最后，我们需要`DynamicPopulateExtender`绑定各项的控件。 将设置以下属性 (显而易见的除了`ID`并`runat` = `"server"`):

- `TargetControlID` 从 web 服务调用放置结果的位置
- `ServicePath` web 服务的路径 （如果你想要使用的页面方法忽略）
- `ServiceMethod` 页面方法的 web 方法的名称
- `ContextKey` 上下文信息发送到 web 服务
- `PopulateTriggerControlID` 这将触发 web 服务调用元素
- `ClearContentsDuringUpdate` 是否要在 web 服务调用期间空目标元素

正如您所看到的该控件所需的一些信息，但将所有内容放入位是相当直接。 下面是针对标记`DynamicPopulateExtender`当前应用场景中的控件：

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

在浏览器中运行 ASP.NET 页并单击按钮;你将收到月-日-年格式的当前日期。

[![单击此按钮从服务器中检索日期](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

单击此按钮从服务器中检索日期 ([单击此项可查看原尺寸图像](dynamically-populating-a-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [下一页](dynamically-populating-a-control-using-javascript-code-vb.md)

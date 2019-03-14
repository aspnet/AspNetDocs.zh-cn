---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: 动态控制 UpdatePanel 动画 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 内容的...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 4de43cca95a37270c752d57f39940339b5bb2e3c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048174"
---
<a name="dynamically-controlling-updatepanel-animations-c"></a>动态控制 UpdatePanel 动画 (C#)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 对于在 UpdatePanel 的内容，一个特殊的扩展程序存在严重依赖于此动画框架：UpdatePanelAnimation。 它还可以与 UpdatePanel 触发器一起工作。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 有关的内容`UpdatePanel`，一个特殊的扩展程序存在的严重依赖于此动画框架： `UpdatePanelAnimation`。 它还可以结合使用`UpdatePanel`触发器。

## <a name="steps"></a>步骤

第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

在此方案中的动画将应用于当前时间的显示。 此信息可以写入到标签使用`Page_Load()`方法，或 （为简单起见） 使用以下的内联代码：


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

此外，创建一个按钮来触发更新的时间：


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

然后将此代码放入`<ContentTemplate>`一部分`UpdatePanel`元素。 在面板`UpdateMode`属性必须设置为`"Conditional"`，因为仅触发器可能会更新面板的内容。 在`<Triggers>`一部分`UpdatePanel`，创建并绑定到异步回发触发器`Click`按钮的事件。 因此，如果用户单击按钮，`UpdatePanel`进行刷新。 下面是针对标记`UpdatePanel`控件：


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

最后，`UpdatePanelAnimationExtender`必须配置：设置`TargetControlID`的面板中，id 属性，定义动画扩展器中的。 在使淡出有意义的这会创建很好的视觉更新时间重点。 然后，扩展器标记可能类似以下形式：


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

在浏览器中运行的文件。 只要单击该按钮时，当前时间显示在面板中，始终为 1 秒的持续时间内淡入。


[![淡入淡出的当前时间](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

淡入淡出的当前时间 ([单击此项可查看原尺寸图像](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](animating-an-updatepanel-control-cs.md)
> [下一页](adding-animation-to-a-control-vb.md)

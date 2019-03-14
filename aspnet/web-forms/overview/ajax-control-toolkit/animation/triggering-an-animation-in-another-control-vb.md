---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 触发另一个控件 (VB) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 通常情况下，启动...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 132f9f85eccabc890308984b9e78ed1d2212c57a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046854"
---
<a name="triggering-an-animation-in-another-control-vb"></a>触发另一控件的动画 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 通常情况下，启动动画时触发用户与相同的控件的交互。 但是也可以与一个控件，然后动画进行交互的另一个控件。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 通常情况下，启动动画时触发用户与相同的控件的交互。 但是也可以与一个控件，然后动画进行交互的另一个控件。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

若要启动对面板进行动画处理，使用一个 HTML 按钮。 请注意， `<input type="button" />` favoured 通过`<asp:Button />`因为我们不希望在回发，当用户单击该按钮。

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`。 务必要设置`TargetControlID`按钮 （触发动画的元素） 的 id 不为面板 （要进行动画处理的元素） 的 ID

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

在`<Animations>`节点，照常位置动画。 才能使这些更改面板，而不是按钮，设置`AnimationTarget`属性中的每个动画元素`AnimationExtender`。 值为`AnimationTarget`当然是在面板的 ID。 这样一来，动画会发生与面板不与触发的按钮。 下面是`AnimationExtender`对于此方案的标记：

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

请注意特殊单个动画的显示的顺序。 首先，在动画运行后，获取停用按钮。 由于没有任何`AnimationTarget`属性中`<EnableAction>`元素，此动画应用于原始控件: 按钮。 接下来两个动画步骤应执行 parallelly (`<Parallel>`元素)。 两者都具有其`AnimationTarget`属性设置为`"Panel1"`，因此对面板中，而不是按钮进行动画处理。


[![按钮上的鼠标单击启动面板动画](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

按钮上的鼠标单击启动面板动画 ([单击此项可查看原尺寸图像](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](disabling-actions-during-animation-vb.md)
> [下一页](modifying-animations-from-the-server-side-vb.md)

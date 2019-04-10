---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 根据条件 (VB) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 无论动画是...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 78140f56184e88fb4dbe29f234aebd5732b69ad9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418867"
---
# <a name="animation-depending-on-a-condition-vb"></a>取决于条件的动画 (VB)

通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画运行还取决于窗体的某些 JavaScript 代码中的条件。


## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画运行还取决于窗体的某些 JavaScript 代码中的条件。

## <a name="steps"></a>步骤

首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

动画将应用于文本的外观如下所示的面板：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。 而不是一个常规的动画，`<Condition>`发挥作用的元素。 作为的值提供的 JavaScript 代码`ConditionScript`属性在运行时执行。 如果其计算结果为 true，动画执行，否则不。 以下标记提供了两个动画，每个正在执行时随机的情况下的 50%中。 因为可能仅在一个动画`<OnLoad>`，这两个`<Condition>`联接在一起使用的动画`<Sequence>`元素：

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

请注意，为小于号 (`<`) 中`ConditionScript`属性必须为转义 （）。 当您运行此脚本，无动画运行或两个空格，或同时执行操作。


[![T他面板淡出而无需调整其大小，因此第二个动画运行第一个未](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

在面板淡出而无需调整大小时，因此第二个动画运行第一个未 ([单击此项可查看原尺寸图像](animation-depending-on-a-condition-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](executing-several-animations-after-each-other-vb.md)
> [下一页](picking-one-animation-out-of-a-list-vb.md)

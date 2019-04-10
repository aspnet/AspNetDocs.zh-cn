---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 选取列表 (C#) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 该框架还允许...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 1cbb60431824ce642625c06cba6b5194aa547b1b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419699"
---
# <a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="b0e60-104">选取列表中的一个动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="b0e60-104">Picking One Animation Out Of a List (C#)</span></span>

<span data-ttu-id="b0e60-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b0e60-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b0e60-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b0e60-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="b0e60-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="b0e60-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b0e60-108">该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。</span><span class="sxs-lookup"><span data-stu-id="b0e60-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="b0e60-109">概述</span><span class="sxs-lookup"><span data-stu-id="b0e60-109">Overview</span></span>

<span data-ttu-id="b0e60-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="b0e60-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b0e60-111">该框架还允许程序员选取一个列表中的动画的动画，具体取决于一些 JavaScript 代码的计算。</span><span class="sxs-lookup"><span data-stu-id="b0e60-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="b0e60-112">步骤</span><span class="sxs-lookup"><span data-stu-id="b0e60-112">Steps</span></span>

<span data-ttu-id="b0e60-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="b0e60-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="b0e60-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="b0e60-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="b0e60-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="b0e60-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="b0e60-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性</span><span class="sxs-lookup"><span data-stu-id="b0e60-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory</span></span> `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="b0e60-117">内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。</span><span class="sxs-lookup"><span data-stu-id="b0e60-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="b0e60-118">而不是一个常规的动画，`<Case>`发挥作用的元素。</span><span class="sxs-lookup"><span data-stu-id="b0e60-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="b0e60-119">对其 SelectScript 属性的值;返回值必须是数字。</span><span class="sxs-lookup"><span data-stu-id="b0e60-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="b0e60-120">具体取决于此编号，其中一个内子动画&lt;用例&gt;执行。</span><span class="sxs-lookup"><span data-stu-id="b0e60-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="b0e60-121">例如，如果 SelectScript 计算结果为 2，控件工具包运行中的第三个动画&lt;用例&gt;（从 0 开始计数）。</span><span class="sxs-lookup"><span data-stu-id="b0e60-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="b0e60-122">以下标记定义了三个子动画：调整大小的宽度调整大小的高度和淡出。JavaScript 代码 (`Math.floor(3 * Math.random())`)，以便三个动画的之一运行，然后选择介于 0 到 2 之间的数字：</span><span class="sxs-lookup"><span data-stu-id="b0e60-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


[![O<span data-ttu-id="b0e60-123">内布拉斯加州的可能的三个动画：在面板变宽时]</span><span class="sxs-lookup"><span data-stu-id="b0e60-123">ne of the possible three animations: The panel gets wider]</span></span>(picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

<span data-ttu-id="b0e60-124">其中一种可能的三个动画：在面板获取更广 ([单击此项可查看原尺寸图像](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b0e60-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0e60-125">[上一页](animation-depending-on-a-condition-cs.md)
> [下一页](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b0e60-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>

---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 在同一时间 (VB) 执行多个动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它允许运行跌落造成的严重...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: f8bb91de9642814a79d0fddd642928c25c58ebfd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59402838"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="cea95-104">在同一时间 (VB) 执行多个动画</span><span class="sxs-lookup"><span data-stu-id="cea95-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="cea95-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cea95-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cea95-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="cea95-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="cea95-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="cea95-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cea95-108">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="cea95-108">It allows to run several animations in a parallel fashion.</span></span>


## <a name="overview"></a><span data-ttu-id="cea95-109">概述</span><span class="sxs-lookup"><span data-stu-id="cea95-109">Overview</span></span>

<span data-ttu-id="cea95-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="cea95-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cea95-111">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="cea95-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="cea95-112">步骤</span><span class="sxs-lookup"><span data-stu-id="cea95-112">Steps</span></span>

<span data-ttu-id="cea95-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="cea95-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="cea95-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="cea95-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="cea95-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="cea95-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="cea95-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="cea95-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="cea95-117">内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。</span><span class="sxs-lookup"><span data-stu-id="cea95-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="cea95-118">通常情况下，`<OnLoad>`只接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="cea95-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="cea95-119">此动画框架允许你联接为一个，并使用多个动画`<Parallel>`元素。</span><span class="sxs-lookup"><span data-stu-id="cea95-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="cea95-120">中的所有动画`<Parallel>`在同一时间执行。</span><span class="sxs-lookup"><span data-stu-id="cea95-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="cea95-121">下面是有关可能的标记`AnimationExtender`控件淡出和调整面板大小在同一时间：</span><span class="sxs-lookup"><span data-stu-id="cea95-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="cea95-122">和确实： 当你运行此脚本，面板会显示，然后调整大小活动 （两个以上倍，以便其宽度和高度的一半来） 和同时淡出。</span><span class="sxs-lookup"><span data-stu-id="cea95-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>


[![T<span data-ttu-id="cea95-123">他面板淡出，调整大小 （包括其内容，得益于浏览器的呈现引擎）]</span><span class="sxs-lookup"><span data-stu-id="cea95-123">he panel is fading out and resizing (including its content, thanks to the browser's rendering engine)]</span></span>(executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

<span data-ttu-id="cea95-124">淡出和调整大小 （包括其内容，得益于浏览器的呈现引擎） 面板 ([单击此项可查看原尺寸图像](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cea95-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cea95-125">[上一页](adding-animation-to-a-control-vb.md)
> [下一页](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cea95-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>

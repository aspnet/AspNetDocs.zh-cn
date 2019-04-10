---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 将动画添加到控件 (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 本教程演示如何...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c55bbeb383b15f4dc9cb95d25905cade1e8c5c29
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418893"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="a4483-104">将动画添加到控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="a4483-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="a4483-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a4483-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a4483-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a4483-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="a4483-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="a4483-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a4483-108">本教程演示如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="a4483-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="a4483-109">概述</span><span class="sxs-lookup"><span data-stu-id="a4483-109">Overview</span></span>

<span data-ttu-id="a4483-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="a4483-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a4483-111">本教程演示如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="a4483-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="a4483-112">步骤</span><span class="sxs-lookup"><span data-stu-id="a4483-112">Steps</span></span>

<span data-ttu-id="a4483-113">第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="a4483-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="a4483-114">在此方案中的动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="a4483-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="a4483-115">面板关联的 CSS 类定义的背景颜色和宽度：</span><span class="sxs-lookup"><span data-stu-id="a4483-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="a4483-116">接下来，我们需要`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="a4483-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="a4483-117">提供后`ID`和常用`runat="server"`，则`TargetControlID`属性必须设置为该控件，要进行动画处理，在本例中，面板：</span><span class="sxs-lookup"><span data-stu-id="a4483-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="a4483-118">使用 XML 语法，遗憾的是当前不完全支持 Visual Studio 的 IntelliSense 以声明方式，应用整个动画。</span><span class="sxs-lookup"><span data-stu-id="a4483-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="a4483-119">根节点是`<Animations>;`在此节点中，这将决定当 animation(s) take(s) 位置允许多个事件：</span><span class="sxs-lookup"><span data-stu-id="a4483-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- `OnClick` <span data-ttu-id="a4483-120">（鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="a4483-120">(mouse click)</span></span>
- `OnHoverOut` <span data-ttu-id="a4483-121">（当鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="a4483-121">(when the mouse leaves a control)</span></span>
- `OnHoverOver` <span data-ttu-id="a4483-122">(当鼠标悬停在控件上，停止`OnHoverOut`动画)</span><span class="sxs-lookup"><span data-stu-id="a4483-122">(when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- `OnLoad` <span data-ttu-id="a4483-123">（如果已加载页）</span><span class="sxs-lookup"><span data-stu-id="a4483-123">(when the page has been loaded)</span></span>
- `OnMouseOut` <span data-ttu-id="a4483-124">（当鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="a4483-124">(when the mouse leaves a control)</span></span>
- `OnMouseOver` <span data-ttu-id="a4483-125">(当鼠标悬停在控件上，不会停止`OnMouseOut`动画)</span><span class="sxs-lookup"><span data-stu-id="a4483-125">(when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="a4483-126">Framework 附带了动画，每个由其自己的 XML 元素表示一组。</span><span class="sxs-lookup"><span data-stu-id="a4483-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="a4483-127">下面是所选内容：</span><span class="sxs-lookup"><span data-stu-id="a4483-127">Here is a selection:</span></span>

- `<Color>` <span data-ttu-id="a4483-128">（更改一种颜色）</span><span class="sxs-lookup"><span data-stu-id="a4483-128">(changing a color)</span></span>
- `<FadeIn>` <span data-ttu-id="a4483-129">（淡入淡出）</span><span class="sxs-lookup"><span data-stu-id="a4483-129">(fading in)</span></span>
- `<FadeOut>` <span data-ttu-id="a4483-130">（淡出）</span><span class="sxs-lookup"><span data-stu-id="a4483-130">(fading out)</span></span>
- `<Property>` <span data-ttu-id="a4483-131">（更改控件的属性）</span><span class="sxs-lookup"><span data-stu-id="a4483-131">(changing a control's property)</span></span>
- `<Pulse>` <span data-ttu-id="a4483-132">(pulsating)</span><span class="sxs-lookup"><span data-stu-id="a4483-132">(pulsating)</span></span>
- `<Resize>` <span data-ttu-id="a4483-133">（更改大小）</span><span class="sxs-lookup"><span data-stu-id="a4483-133">(changing the size)</span></span>
- `<Scale>` <span data-ttu-id="a4483-134">（按比例更改大小）</span><span class="sxs-lookup"><span data-stu-id="a4483-134">(proportionally changing the size)</span></span>

<span data-ttu-id="a4483-135">在此示例中，面板应淡出。该动画应需要 1.5 秒钟的时间 (`Duration`属性)，显示每秒 24 帧 （动画步骤） (`Fps`属性)。</span><span class="sxs-lookup"><span data-stu-id="a4483-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="a4483-136">下面是完整标记`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="a4483-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="a4483-137">当运行此脚本时，面板会显示，并在一个半秒内淡出。</span><span class="sxs-lookup"><span data-stu-id="a4483-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


[![T<span data-ttu-id="a4483-138">他面板淡出]</span><span class="sxs-lookup"><span data-stu-id="a4483-138">he panel is fading out]</span></span>(adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

<span data-ttu-id="a4483-139">在面板淡出 ([单击此项可查看原尺寸图像](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a4483-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4483-140">[上一页](dynamically-controlling-updatepanel-animations-cs.md)
> [下一页](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a4483-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>

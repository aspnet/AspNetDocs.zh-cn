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
ms.openlocfilehash: 29c2673aa7b018cbe8c66eb72c256b69a2193a47
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65134035"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="5e792-104">动态控制 UpdatePanel 动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="5e792-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="5e792-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5e792-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5e792-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5e792-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="5e792-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="5e792-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5e792-108">对于在 UpdatePanel 的内容，一个特殊的扩展程序存在严重依赖于此动画框架：UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="5e792-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="5e792-109">它还可以与 UpdatePanel 触发器一起工作。</span><span class="sxs-lookup"><span data-stu-id="5e792-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="5e792-110">概述</span><span class="sxs-lookup"><span data-stu-id="5e792-110">Overview</span></span>

<span data-ttu-id="5e792-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="5e792-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5e792-112">有关的内容`UpdatePanel`，一个特殊的扩展程序存在的严重依赖于此动画框架： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="5e792-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="5e792-113">它还可以结合使用`UpdatePanel`触发器。</span><span class="sxs-lookup"><span data-stu-id="5e792-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="5e792-114">步骤</span><span class="sxs-lookup"><span data-stu-id="5e792-114">Steps</span></span>

<span data-ttu-id="5e792-115">第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="5e792-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="5e792-116">在此方案中的动画将应用于当前时间的显示。</span><span class="sxs-lookup"><span data-stu-id="5e792-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="5e792-117">此信息可以写入到标签使用`Page_Load()`方法，或 （为简单起见） 使用以下的内联代码：</span><span class="sxs-lookup"><span data-stu-id="5e792-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="5e792-118">此外，创建一个按钮来触发更新的时间：</span><span class="sxs-lookup"><span data-stu-id="5e792-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="5e792-119">然后将此代码放入`<ContentTemplate>`一部分`UpdatePanel`元素。</span><span class="sxs-lookup"><span data-stu-id="5e792-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="5e792-120">在面板`UpdateMode`属性必须设置为`"Conditional"`，因为仅触发器可能会更新面板的内容。</span><span class="sxs-lookup"><span data-stu-id="5e792-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="5e792-121">在`<Triggers>`一部分`UpdatePanel`，创建并绑定到异步回发触发器`Click`按钮的事件。</span><span class="sxs-lookup"><span data-stu-id="5e792-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="5e792-122">因此，如果用户单击按钮，`UpdatePanel`进行刷新。</span><span class="sxs-lookup"><span data-stu-id="5e792-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="5e792-123">下面是针对标记`UpdatePanel`控件：</span><span class="sxs-lookup"><span data-stu-id="5e792-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="5e792-124">最后，`UpdatePanelAnimationExtender`必须配置：设置`TargetControlID`的面板中，id 属性，定义动画扩展器中的。</span><span class="sxs-lookup"><span data-stu-id="5e792-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="5e792-125">在使淡出有意义的这会创建很好的视觉更新时间重点。</span><span class="sxs-lookup"><span data-stu-id="5e792-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="5e792-126">然后，扩展器标记可能类似以下形式：</span><span class="sxs-lookup"><span data-stu-id="5e792-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="5e792-127">在浏览器中运行的文件。</span><span class="sxs-lookup"><span data-stu-id="5e792-127">Run the file in the browser.</span></span> <span data-ttu-id="5e792-128">只要单击该按钮时，当前时间显示在面板中，始终为 1 秒的持续时间内淡入。</span><span class="sxs-lookup"><span data-stu-id="5e792-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="5e792-129">[![淡入淡出的当前时间](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5e792-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="5e792-130">淡入淡出的当前时间 ([单击此项可查看原尺寸图像](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5e792-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5e792-131">[上一页](animating-an-updatepanel-control-cs.md)
> [下一页](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5e792-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>

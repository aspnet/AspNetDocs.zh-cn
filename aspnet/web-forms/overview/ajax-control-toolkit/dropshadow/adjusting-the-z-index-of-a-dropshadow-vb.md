---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 调整 DropShadow (VB) 的 Z-索引 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 但是此卷影有时会与其他控件中，已为冲突...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: a900a074e1507965e7d60e8de4202de57dc6180e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043244"
---
<a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="d7599-104">调整 DropShadow 的 Z-索引 (VB)</span><span class="sxs-lookup"><span data-stu-id="d7599-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>
====================
<span data-ttu-id="d7599-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d7599-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d7599-106">[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d7599-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="d7599-107">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="d7599-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="d7599-108">但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。</span><span class="sxs-lookup"><span data-stu-id="d7599-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="d7599-109">当菜单项会弹出，随即出现之后投影。</span><span class="sxs-lookup"><span data-stu-id="d7599-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="d7599-110">概述</span><span class="sxs-lookup"><span data-stu-id="d7599-110">Overview</span></span>

<span data-ttu-id="d7599-111">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="d7599-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="d7599-112">但是此卷影有时会与其他控件，例如 ASP.NET 菜单控件冲突。</span><span class="sxs-lookup"><span data-stu-id="d7599-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="d7599-113">当菜单项会弹出，随即出现之后投影。</span><span class="sxs-lookup"><span data-stu-id="d7599-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="d7599-114">步骤</span><span class="sxs-lookup"><span data-stu-id="d7599-114">Steps</span></span>

<span data-ttu-id="d7599-115">代码开始与面板本身，以便在面板包含足够多的效果是可见的文本包含足够多的文本：</span><span class="sxs-lookup"><span data-stu-id="d7599-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="d7599-116">紧前面放置另一个面板`panelShadow`面板。</span><span class="sxs-lookup"><span data-stu-id="d7599-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="d7599-117">它包含一个具有水平方向，以便通过显示菜单项 (确切地说： 下)`dropShadow`面板):</span><span class="sxs-lookup"><span data-stu-id="d7599-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="d7599-118">然后，将`DropShadowExtender`添加扩展`panelShadow`面板中的投影效果：</span><span class="sxs-lookup"><span data-stu-id="d7599-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="d7599-119">最后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：</span><span class="sxs-lookup"><span data-stu-id="d7599-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="d7599-120">当运行此脚本时，菜单项显示在面板的下方。</span><span class="sxs-lookup"><span data-stu-id="d7599-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="d7599-121">但是，菜单上使用的 CSS 类`panel`其中只需定义两件事要使元素显示在其他面板：</span><span class="sxs-lookup"><span data-stu-id="d7599-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="d7599-122">相对定位</span><span class="sxs-lookup"><span data-stu-id="d7599-122">Relative positioning</span></span>
- <span data-ttu-id="d7599-123">正 z 索引</span><span class="sxs-lookup"><span data-stu-id="d7599-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="d7599-124">然后，`DropShadowExtender`控件不与菜单控件不再冲突。</span><span class="sxs-lookup"><span data-stu-id="d7599-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


<span data-ttu-id="d7599-125">[![之前：菜单项不可见](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d7599-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)</span></span>

<span data-ttu-id="d7599-126">在此之前:菜单项不可见 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d7599-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>


<span data-ttu-id="d7599-127">[![之后：菜单项显示](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d7599-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)</span></span>

<span data-ttu-id="d7599-128">之后：将显示菜单项 ([单击此项可查看原尺寸图像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d7599-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d7599-129">[上一页](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一页](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d7599-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
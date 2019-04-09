---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 数据绑定滑块控件 (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 就可以将绑定当前 positio...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3f966869c106416886dfa4e9e3c2cf67ee5fe337
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385808"
---
# <a name="databinding-the-slider-control-c"></a><span data-ttu-id="1ce03-104">数据绑定滑块控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="1ce03-104">Databinding the Slider Control (C#)</span></span>

<span data-ttu-id="1ce03-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1ce03-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1ce03-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1ce03-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="1ce03-107">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="1ce03-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="1ce03-108">就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="1ce03-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="1ce03-109">概述</span><span class="sxs-lookup"><span data-stu-id="1ce03-109">Overview</span></span>

<span data-ttu-id="1ce03-110">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="1ce03-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="1ce03-111">就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="1ce03-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="1ce03-112">步骤</span><span class="sxs-lookup"><span data-stu-id="1ce03-112">Steps</span></span>

<span data-ttu-id="1ce03-113">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="1ce03-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1ce03-114">接下来，添加两个`TextBox`到页面的控件。</span><span class="sxs-lookup"><span data-stu-id="1ce03-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="1ce03-115">一个将转换为图形滑块，和另一个将保存的滑块位置。</span><span class="sxs-lookup"><span data-stu-id="1ce03-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1ce03-116">下一步已是最后一步。</span><span class="sxs-lookup"><span data-stu-id="1ce03-116">The next step is already the final step.</span></span> <span data-ttu-id="1ce03-117">`SliderExtender`从 ASP.NET AJAX 控件工具包控件使一个滑块，从第一个文本框和滑块位置更改时，会自动更新第二个文本框。</span><span class="sxs-lookup"><span data-stu-id="1ce03-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="1ce03-118">要使其工作，以便`SliderExtender`的`TargetControlID`属性必须设置为第一个文本框; ID`BoundControlID`属性必须设置为第二个文本框的 ID。</span><span class="sxs-lookup"><span data-stu-id="1ce03-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="1ce03-119">您可以看到在浏览器中，数据绑定的工作在两个方向： 在文本框中输入新值更新滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="1ce03-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="1ce03-120">如果仅读取第二个文本框中，可以这样就更难用户手动更新中有值与文本字段添加较弱的保护。</span><span class="sxs-lookup"><span data-stu-id="1ce03-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


[![S<span data-ttu-id="1ce03-121">lider 和文本框已同步]</span><span class="sxs-lookup"><span data-stu-id="1ce03-121">lider and text box are in sync]</span></span>(databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)

<span data-ttu-id="1ce03-122">滑块和文本框都是同步 ([单击此项可查看原尺寸图像](databinding-the-slider-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1ce03-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ce03-123">[上一页](using-the-slider-control-with-auto-postback-cs.md)
> [下一页](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1ce03-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>

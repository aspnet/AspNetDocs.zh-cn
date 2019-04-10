---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 通过 (VB) 的客户端代码操作 Dropshadow |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。 此外可以使用客户端 JavaScrip 更改此扩展器的属性...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: c9b0946568063b9e5cf1454bd7a57c43304c3543
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59390306"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="adb92-104">通过客户端代码操作 DropShadow 属性 (VB)</span><span class="sxs-lookup"><span data-stu-id="adb92-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="adb92-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="adb92-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="adb92-106">[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="adb92-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="adb92-107">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="adb92-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="adb92-108">此外可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="adb92-108">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="adb92-109">概述</span><span class="sxs-lookup"><span data-stu-id="adb92-109">Overview</span></span>

<span data-ttu-id="adb92-110">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="adb92-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="adb92-111">此外可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="adb92-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="adb92-112">步骤</span><span class="sxs-lookup"><span data-stu-id="adb92-112">Steps</span></span>

<span data-ttu-id="adb92-113">代码开头包含几行文本的面板：</span><span class="sxs-lookup"><span data-stu-id="adb92-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="adb92-114">关联的 CSS 类为面板提供了一种很好的背景色：</span><span class="sxs-lookup"><span data-stu-id="adb92-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="adb92-115">`DropShadowExtender`添加进来以扩展面板中的投影效果，设置为 50%的不透明度：</span><span class="sxs-lookup"><span data-stu-id="adb92-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="adb92-116">然后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：</span><span class="sxs-lookup"><span data-stu-id="adb92-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="adb92-117">另一个面板包含用于设置投影的不透明度的两个 JavaScript 链接： 减号链接会降低阴影的不透明度，加上链接会增加它。</span><span class="sxs-lookup"><span data-stu-id="adb92-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="adb92-118">JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。</span><span class="sxs-lookup"><span data-stu-id="adb92-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="adb92-119">ASP.NET AJAX 定义`$find()`完全该任务的方法。</span><span class="sxs-lookup"><span data-stu-id="adb92-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="adb92-120">然后，将`get_Opacity()`方法检索当前不透明度，`set_Opacity()`方法将其设置。</span><span class="sxs-lookup"><span data-stu-id="adb92-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="adb92-121">JavaScript 代码然后将当前的不透明度值放入`<label>`元素：</span><span class="sxs-lookup"><span data-stu-id="adb92-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


[![T<span data-ttu-id="adb92-122">在客户端上更改他不透明度]</span><span class="sxs-lookup"><span data-stu-id="adb92-122">he opacity is changed on the client side]</span></span>(manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

<span data-ttu-id="adb92-123">在客户端上更改不透明度 ([单击此项可查看原尺寸图像](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="adb92-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="adb92-124">上一个</span><span class="sxs-lookup"><span data-stu-id="adb92-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)

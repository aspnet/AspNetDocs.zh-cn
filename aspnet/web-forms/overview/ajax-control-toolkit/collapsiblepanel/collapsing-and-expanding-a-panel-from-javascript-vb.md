---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: 折叠和展开面板从 JavaScript (VB) |Microsoft Docs
author: wenz
description: CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能以折叠其内容并将其展开...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 1f80a6979966a887db0557b4f1b98570e10b1ab7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032804"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="23ee3-103">通过 JavaScript 折叠和展开面板 (VB)</span><span class="sxs-lookup"><span data-stu-id="23ee3-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>
====================
<span data-ttu-id="23ee3-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="23ee3-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="23ee3-105">[下载代码](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="23ee3-105">[Download Code](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="23ee3-106">CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能折叠其内容，并再次将其展开。</span><span class="sxs-lookup"><span data-stu-id="23ee3-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="23ee3-107">也可以从自定义 JavaScript 代码触发这两个操作。</span><span class="sxs-lookup"><span data-stu-id="23ee3-107">These two actions can also be triggered from custom JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="23ee3-108">概述</span><span class="sxs-lookup"><span data-stu-id="23ee3-108">Overview</span></span>

<span data-ttu-id="23ee3-109">CollapsiblePanel 控件在 ASP.NET AJAX 控件工具包扩展一个面板，并为其提供的功能折叠其内容，并再次将其展开。</span><span class="sxs-lookup"><span data-stu-id="23ee3-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="23ee3-110">也可以从自定义 JavaScript 代码触发这两个操作。</span><span class="sxs-lookup"><span data-stu-id="23ee3-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="23ee3-111">步骤</span><span class="sxs-lookup"><span data-stu-id="23ee3-111">Steps</span></span>

<span data-ttu-id="23ee3-112">首先，创建一个新的 ASP.NET 页面并将包含`ScriptManager`中`<form>`元素。</span><span class="sxs-lookup"><span data-stu-id="23ee3-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="23ee3-113">这将加载 ASP.NET AJAX 库所需控件工具包：</span><span class="sxs-lookup"><span data-stu-id="23ee3-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="23ee3-114">然后，使用一些文本创建一个面板，以便可以看到展开/折叠效果：</span><span class="sxs-lookup"><span data-stu-id="23ee3-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="23ee3-115">正如您所看到的面板将引用的 CSS 类如下所示 （现在基本上是定义背景色和面板的宽度）：</span><span class="sxs-lookup"><span data-stu-id="23ee3-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="23ee3-116">`CollapsiblePanelExtender`控件需要`TargetControlID`属性，以便该工具包知道哪个面板可折叠或展开根据请求：</span><span class="sxs-lookup"><span data-stu-id="23ee3-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="23ee3-117">遗憾的是，扩展器当前不会公开特定 API 的折叠或展开面板，但未记录的一些方法即可。</span><span class="sxs-lookup"><span data-stu-id="23ee3-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="23ee3-118">首先，将三个 HTML 按钮添加到页然后会触发客户端 JavaScript 以折叠或展开面板的内容：</span><span class="sxs-lookup"><span data-stu-id="23ee3-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="23ee3-119">在客户端的 JavaScript 代码 (入门`<script type="text/javascript">`)，则`$find()`方法需要使用访问`CollapsiblePanelExtender`。</span><span class="sxs-lookup"><span data-stu-id="23ee3-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="23ee3-120">`$find("cpe")` 将返回对它的引用。</span><span class="sxs-lookup"><span data-stu-id="23ee3-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="23ee3-121">从此处，特定的方法将解决手头的任务。</span><span class="sxs-lookup"><span data-stu-id="23ee3-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="23ee3-122">该方法用于打开 （扩展） 名控制面板`_doOpen()`; 下面的代码实现`doOpen()`单击第一个按钮时调用的函数：</span><span class="sxs-lookup"><span data-stu-id="23ee3-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="23ee3-123">用于关闭，或折叠面板，`_doClose()`方法需要执行。</span><span class="sxs-lookup"><span data-stu-id="23ee3-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="23ee3-124">因此当用户单击第二个按钮上时，以下 JavaScript 代码调用：</span><span class="sxs-lookup"><span data-stu-id="23ee3-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="23ee3-125">第三个按钮切换面板的状态： 从折叠到已展开，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="23ee3-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="23ee3-126">`CollapsiblePanelExtender`公开`toggle()`做到这一点的方法： 反转面板的状态。</span><span class="sxs-lookup"><span data-stu-id="23ee3-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="23ee3-127">但是还有另一种方法 (这由在内部使用`toggle()`方法):`get_Collapsed()`方法的`CollapsiblePanelExtender()`告诉我们是否折叠面板。</span><span class="sxs-lookup"><span data-stu-id="23ee3-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="23ee3-128">根据此函数的返回值，面板，则可以展开 (`_doOpen()`方法) 或折叠 (`_doClose()`) 方法：</span><span class="sxs-lookup"><span data-stu-id="23ee3-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]


<span data-ttu-id="23ee3-129">[![第三个按钮更改面板的状态： 从折叠到扩展和后端](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23ee3-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="23ee3-130">第三个按钮更改面板的状态： 从折叠到扩展和后端 ([单击此项可查看原尺寸图像](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="23ee3-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="23ee3-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="23ee3-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)

---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: 自动回发使用 CascadingDropDown (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 7c84951691935d9976f961f65f96fa70633ecbce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061324"
---
<a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="55cdd-103">通过 CascadingDropDown 使用自动回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="55cdd-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>
====================
<span data-ttu-id="55cdd-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="55cdd-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="55cdd-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="55cdd-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="55cdd-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="55cdd-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="55cdd-107">但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件自动回发功能不起作用，因为以异步方式将数据加载到列表生成本身 （不必要） 回发。</span><span class="sxs-lookup"><span data-stu-id="55cdd-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="55cdd-108">使用一些 JavaScript 代码，可以避免这种效果。</span><span class="sxs-lookup"><span data-stu-id="55cdd-108">With some JavaScript code, this effect can be avoided.</span></span>


## <a name="overview"></a><span data-ttu-id="55cdd-109">概述</span><span class="sxs-lookup"><span data-stu-id="55cdd-109">Overview</span></span>

<span data-ttu-id="55cdd-110">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="55cdd-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="55cdd-111">（例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件自动回发功能不起作用，因为以异步方式将数据加载到列表生成本身 （不必要） 回发。</span><span class="sxs-lookup"><span data-stu-id="55cdd-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="55cdd-112">使用一些 JavaScript 代码，可以避免这种效果。</span><span class="sxs-lookup"><span data-stu-id="55cdd-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="55cdd-113">步骤</span><span class="sxs-lookup"><span data-stu-id="55cdd-113">Steps</span></span>

<span data-ttu-id="55cdd-114">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (之内&lt; `form` &gt;元素):</span><span class="sxs-lookup"><span data-stu-id="55cdd-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="55cdd-115">然后，DropDownList 控件是必需的：</span><span class="sxs-lookup"><span data-stu-id="55cdd-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="55cdd-116">对于此列表中，添加 CascadingDropDown 扩展程序以提供 web 服务 URL 和方法的信息：</span><span class="sxs-lookup"><span data-stu-id="55cdd-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="55cdd-117">然后 CascadingDropDown 扩展程序以异步方式调用 web 服务使用以下方法签名：</span><span class="sxs-lookup"><span data-stu-id="55cdd-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="55cdd-118">该方法返回类型 CascadingDropDown 值的数组。</span><span class="sxs-lookup"><span data-stu-id="55cdd-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="55cdd-119">类型的构造函数要求第一次列表项的标题和值 (HTML`value`属性)。</span><span class="sxs-lookup"><span data-stu-id="55cdd-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="55cdd-120">加载页面在浏览器中的将填充下拉列表中的与三个供应商，第二个被预先选定状态。</span><span class="sxs-lookup"><span data-stu-id="55cdd-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="55cdd-121">此外，ASP.NET 定义`__doPostBack()`JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="55cdd-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="55cdd-122">页面加载后，此 JavaScript 调用添加到下拉列表中，但仅是否有元素中。</span><span class="sxs-lookup"><span data-stu-id="55cdd-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="55cdd-123">如果在列表中没有元素，控件工具包当前是否正在加载，因此 JavaScript 代码使用超时，并尝试再次在半秒。</span><span class="sxs-lookup"><span data-stu-id="55cdd-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="55cdd-124">这样一来，在列表中存在实际元素，并且用户选择一个条目时，回发才执行。</span><span class="sxs-lookup"><span data-stu-id="55cdd-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>


<span data-ttu-id="55cdd-125">[![选择一个列表元素导致回发](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55cdd-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="55cdd-126">选择一个列表元素导致回发 ([单击此项可查看原尺寸图像](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="55cdd-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="55cdd-127">[上一页](presetting-list-entries-with-cascadingdropdown-cs.md)
> [下一页](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="55cdd-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>

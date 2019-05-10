---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: 动态添加 Accordion 窗格 (C#) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。 面板通常声明 w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 7134c95845ec7f22b5216e10b50ab8f81cd24806
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131255"
---
# <a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="0956b-104">动态添加 Accordion 窗格 (C#)</span><span class="sxs-lookup"><span data-stu-id="0956b-104">Dynamically Adding An Accordion Pane (C#)</span></span>

<span data-ttu-id="0956b-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0956b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0956b-106">[下载代码](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0956b-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="0956b-107">AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="0956b-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="0956b-108">面板通常声明内页面本身，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="0956b-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="overview"></a><span data-ttu-id="0956b-109">概述</span><span class="sxs-lookup"><span data-stu-id="0956b-109">Overview</span></span>

<span data-ttu-id="0956b-110">AJAX 控件工具包中的可折叠面板控件提供了多个窗格，并允许用户一次显示其中一个。</span><span class="sxs-lookup"><span data-stu-id="0956b-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="0956b-111">面板通常声明内页面本身，但可以使用服务器端代码来实现相同的结果。</span><span class="sxs-lookup"><span data-stu-id="0956b-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="0956b-112">步骤</span><span class="sxs-lookup"><span data-stu-id="0956b-112">Steps</span></span>

<span data-ttu-id="0956b-113">可折叠面板控件公开服务器端代码的所有重要属性。</span><span class="sxs-lookup"><span data-stu-id="0956b-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="0956b-114">除此之外，`Panes`属性授予访问权限的窗格组成可折叠面板集合。</span><span class="sxs-lookup"><span data-stu-id="0956b-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="0956b-115">每个窗格中的类型没有`AccordionPane`。</span><span class="sxs-lookup"><span data-stu-id="0956b-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="0956b-116">因此，轻松地创建此类的窗格为：</span><span class="sxs-lookup"><span data-stu-id="0956b-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="0956b-117">`HeaderContainer`的属性`AccordionPane`提供访问的窗格; 标头部分中的 ASP.NET 控件`ContentContainer`属性的`AccordionPane`窗格的内容部分对执行相同操作。</span><span class="sxs-lookup"><span data-stu-id="0956b-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="0956b-118">这使得 ASP.NET 代码，可以将内容添加到窗格：</span><span class="sxs-lookup"><span data-stu-id="0956b-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="0956b-119">最后，必须将窗格添加到`Panes`可折叠面板的集合：</span><span class="sxs-lookup"><span data-stu-id="0956b-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="0956b-120">下面是将两个窗格添加到 Accordion 控件的完整服务器端代码：</span><span class="sxs-lookup"><span data-stu-id="0956b-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="0956b-121">唯一缺少元素是可折叠面板本身，具体取决于是否存在 ASP.NET`ScriptManager`控件：</span><span class="sxs-lookup"><span data-stu-id="0956b-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="0956b-122">若要完成该示例，两个可折叠面板控件中引用的 CSS 类提供浏览器的样式信息：</span><span class="sxs-lookup"><span data-stu-id="0956b-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]

<span data-ttu-id="0956b-123">[![服务器端代码动态添加 accordion 中的数据](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0956b-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="0956b-124">服务器端代码动态添加 accordion 中的数据 ([单击此项可查看原尺寸图像](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0956b-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0956b-125">[上一页](databinding-to-an-accordion-cs.md)
> [下一页](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0956b-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>

---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: 处理回发 ModalPopup (VB) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 Pos 时，必须格外谨慎处理...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f81a2bf1866d026046fdba815fdbae1b162c1dd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047054"
---
<a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="7e1b1-104">通过 ModalPopup 处理回发 (VB)</span><span class="sxs-lookup"><span data-stu-id="7e1b1-104">Handling Postbacks from a ModalPopup (VB)</span></span>
====================
<span data-ttu-id="7e1b1-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7e1b1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7e1b1-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7e1b1-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="7e1b1-107">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7e1b1-108">从弹出窗口中创建一个回发时，必须格外小心。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-108">Special care must be taken when a postback is created from within the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="7e1b1-109">概述</span><span class="sxs-lookup"><span data-stu-id="7e1b1-109">Overview</span></span>

<span data-ttu-id="7e1b1-110">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="7e1b1-111">从弹出窗口中创建一个回发时，必须格外小心。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="7e1b1-112">步骤</span><span class="sxs-lookup"><span data-stu-id="7e1b1-112">Steps</span></span>

<span data-ttu-id="7e1b1-113">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="7e1b1-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="7e1b1-114">接下来，添加一个面板作为模式弹出框。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="7e1b1-115">存在，用户可以输入一个名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="7e1b1-116">一个按钮用于关闭弹出窗口和保存的信息。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="7e1b1-117">请注意，`OnClick`属性设置，以便在回发发生时单击此按钮：</span><span class="sxs-lookup"><span data-stu-id="7e1b1-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="7e1b1-118">页面本身包含两个标签，以便完全相同的信息： 名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="7e1b1-119">一个按钮用于触发模式弹出框：</span><span class="sxs-lookup"><span data-stu-id="7e1b1-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="7e1b1-120">为了使显示的弹出窗口，添加`ModalPopupExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="7e1b1-121">设置`PopupControlID`属性为面板的 ID 和`TargetControlID`到按钮的 ID:</span><span class="sxs-lookup"><span data-stu-id="7e1b1-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="7e1b1-122">现在只要`Save`模式弹出框内单击时，服务器端`SaveData()`执行方法。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="7e1b1-123">您可以在数据存储中保存输入的数据。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="7e1b1-124">为简单起见，只需标签中输出的新数据：</span><span class="sxs-lookup"><span data-stu-id="7e1b1-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="7e1b1-125">此外，应使用当前名称和电子邮件填充模式弹出框中的文本框控件。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="7e1b1-126">但是这是仅有必要不回发发生时。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="7e1b1-127">如果回发，ASP.NET 视图状态功能便会自动填充的文本框使用适当的值。</span><span class="sxs-lookup"><span data-stu-id="7e1b1-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]


<span data-ttu-id="7e1b1-128">[![模式弹出框会导致回发](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7e1b1-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="7e1b1-129">模式弹出框会导致回发 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7e1b1-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e1b1-130">[上一页](using-modalpopup-with-a-repeater-control-vb.md)
> [下一页](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7e1b1-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>

---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 通过验证控件 (C#) 使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中，它我...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: f833868d9dbf51a9714b9bbe6730a24badc169d0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391008"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="04bb2-104">通过验证控件使用 TextBoxWatermark (C#)</span><span class="sxs-lookup"><span data-stu-id="04bb2-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="04bb2-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="04bb2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="04bb2-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="04bb2-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="04bb2-107">AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="04bb2-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="04bb2-108">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="04bb2-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="04bb2-109">如果用户离开而无需输入文本的框中，将重新出现已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="04bb2-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="04bb2-110">这可能与在同一页上，ASP.NET 验证控件发生冲突，但可能会解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="04bb2-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>


## <a name="overview"></a><span data-ttu-id="04bb2-111">概述</span><span class="sxs-lookup"><span data-stu-id="04bb2-111">Overview</span></span>

<span data-ttu-id="04bb2-112">`TextBoxWatermark` AJAX 控件工具包中的控件扩展的文本框中，以便在框中显示文本。</span><span class="sxs-lookup"><span data-stu-id="04bb2-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="04bb2-113">当用户单击到框中时，它将被清空。</span><span class="sxs-lookup"><span data-stu-id="04bb2-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="04bb2-114">如果用户离开而无需输入文本的框中，将重新出现已预先的文本。</span><span class="sxs-lookup"><span data-stu-id="04bb2-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="04bb2-115">这可能与在同一页上，ASP.NET 验证控件发生冲突，但可能会解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="04bb2-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="04bb2-116">步骤</span><span class="sxs-lookup"><span data-stu-id="04bb2-116">Steps</span></span>

<span data-ttu-id="04bb2-117">该示例的基本设置均以下：`TextBox`控件打使用`TextBoxWatermarkExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="04bb2-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="04bb2-118">一个按钮触发回发和更高版本将用于触发页面上的验证控件。</span><span class="sxs-lookup"><span data-stu-id="04bb2-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="04bb2-119">此外，`ScriptManager`初始化 ASP.NET AJAX 所需的控件：</span><span class="sxs-lookup"><span data-stu-id="04bb2-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="04bb2-120">现在，添加`RequiredFieldValidator`会检查是否存在文本字段中时提交窗体的控件。</span><span class="sxs-lookup"><span data-stu-id="04bb2-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="04bb2-121">`InitialValue`验证程序的属性必须设置为相同的值中使用`TextBoxWatermarkExtender`控件：提交表单后，未更改文本框的值是在其中的水印值：</span><span class="sxs-lookup"><span data-stu-id="04bb2-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="04bb2-122">但是没有这种方法的一个问题：如果客户端禁用 JavaScript，则在文本字段会不预先填写好的水印文本，因此`RequiredFieldValidator`不会触发一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="04bb2-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="04bb2-123">因此，第二个`RequiredFieldValidator`该控件是需要检查空文本框 (省略`InitialValue`属性)。</span><span class="sxs-lookup"><span data-stu-id="04bb2-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="04bb2-124">因为这两个验证程序使用`Display` = `"Dynamic"`，最终用户不能将这两个验证程序的已触发的可视外观与区分开来; 相反，它看起来时只有一个。</span><span class="sxs-lookup"><span data-stu-id="04bb2-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="04bb2-125">最后，添加一些服务器端代码来输出字段中的文本，如果没有验证程序发出一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="04bb2-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]


[![T<span data-ttu-id="04bb2-126">他验证程序错误报告的字段中没有的文本]</span><span class="sxs-lookup"><span data-stu-id="04bb2-126">he validator complains that there is no text in the field]</span></span>(using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

<span data-ttu-id="04bb2-127">验证程序错误报告的字段中没有的文本 ([单击此项可查看原尺寸图像](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="04bb2-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04bb2-128">[上一页](using-textboxwatermark-in-a-formview-cs.md)
> [下一页](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="04bb2-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>

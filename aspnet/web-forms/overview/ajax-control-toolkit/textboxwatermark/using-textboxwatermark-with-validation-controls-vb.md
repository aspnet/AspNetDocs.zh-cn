---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 通过验证控件 (VB) 中使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中，它我...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: d83fb53ddb40a31013bc724909fa149ce2e4c713
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59387360"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a>通过验证控件使用 TextBoxWatermark (VB)

通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)

> AJAX 控件工具包中的 TextBoxWatermark 控件扩展的文本框中，使得在框中显示文本。 当用户单击到框中时，它将被清空。 如果用户离开而无需输入文本的框中，将重新出现已预先的文本。 这可能与在同一页上，ASP.NET 验证控件发生冲突，但可能会解决这些问题。


## <a name="overview"></a>概述

`TextBoxWatermark` AJAX 控件工具包中的控件扩展的文本框中，以便在框中显示文本。 当用户单击到框中时，它将被清空。 如果用户离开而无需输入文本的框中，将重新出现已预先的文本。 这可能与在同一页上，ASP.NET 验证控件发生冲突，但可能会解决这些问题。

## <a name="steps"></a>步骤

该示例的基本设置均以下：`TextBox`控件打使用`TextBoxWatermarkExtender`控件。 一个按钮触发回发和更高版本将用于触发页面上的验证控件。 此外，`ScriptManager`初始化 ASP.NET AJAX 所需的控件：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

现在，添加`RequiredFieldValidator`会检查是否存在文本字段中时提交窗体的控件。 `InitialValue`验证程序的属性必须设置为相同的值中使用`TextBoxWatermarkExtender`控件：提交表单后，未更改文本框的值是在其中的水印值：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

但是没有这种方法的一个问题：如果客户端禁用 JavaScript，则在文本字段会不预先填写好的水印文本，因此`RequiredFieldValidator`不会触发一条错误消息。 因此，第二个`RequiredFieldValidator`该控件是需要检查空文本框 (省略`InitialValue`属性)。

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

因为这两个验证程序使用`Display` = `"Dynamic"`，最终用户不能将这两个验证程序的已触发的可视外观与区分开来; 相反，它看起来时只有一个。

最后，添加一些服务器端代码来输出字段中的文本，如果没有验证程序发出一条错误消息：

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]


[![验证程序错误报告的字段中没有的文本](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)

验证程序错误报告的字段中没有的文本 ([单击此项可查看原尺寸图像](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](using-textboxwatermark-in-a-formview-vb.md)

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
<a name="handling-postbacks-from-a-modalpopup-vb"></a>通过 ModalPopup 处理回发 (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 从弹出窗口中创建一个回发时，必须格外小心。


## <a name="overview"></a>概述

在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 从弹出窗口中创建一个回发时，必须格外小心。

## <a name="steps"></a>步骤

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

接下来，添加一个面板作为模式弹出框。 存在，用户可以输入一个名称和电子邮件地址。 一个按钮用于关闭弹出窗口和保存的信息。 请注意，`OnClick`属性设置，以便在回发发生时单击此按钮：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

页面本身包含两个标签，以便完全相同的信息： 名称和电子邮件地址。 一个按钮用于触发模式弹出框：

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

为了使显示的弹出窗口，添加`ModalPopupExtender`控件。 设置`PopupControlID`属性为面板的 ID 和`TargetControlID`到按钮的 ID:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

现在只要`Save`模式弹出框内单击时，服务器端`SaveData()`执行方法。 您可以在数据存储中保存输入的数据。 为简单起见，只需标签中输出的新数据：

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

此外，应使用当前名称和电子邮件填充模式弹出框中的文本框控件。 但是这是仅有必要不回发发生时。 如果回发，ASP.NET 视图状态功能便会自动填充的文本框使用适当的值。

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]


[![模式弹出框会导致回发](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

模式弹出框会导致回发 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一页](using-modalpopup-with-a-repeater-control-vb.md)
> [下一页](positioning-a-modalpopup-vb.md)

---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: 通过使用带 UpdatePanel (VB) 的弹出控件处理回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 特别注意必须为其拍摄...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 3c4b58e864ca99aa30444fbb3244bfa4ffb4c336
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379035"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>使用带 UpdatePanel 的弹出控件处理回发 (VB)

通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 特别留意具有此类弹出窗口中产生的回发时要执行。


## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 特别留意具有此类弹出窗口中产生的回发时要执行。

## <a name="steps"></a>步骤

使用时`PopupControl`带回发，`UpdatePanel`可以防止引起回发页面刷新。 以下标记定义了几个重要的元素：

- 一个`ScriptManager`控件，以使 ASP.NET AJAX Control Toolkit 工作原理
- 两个`TextBox`控件，这将触发一个弹出窗口
- 一个`Panel`将充当弹出窗口的控件
- 在面板内`Calendar`内嵌入控件`UpdatePanel`控件
- 两个`PopupControlExtender`将该面板分配到文本框中的控件

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

请注意，`OnSelectionChanged`属性的`Calendar`控件设置。 因此当用户选择在日历中的日期，产生的回发和服务器端方法`c1_SelectionChanged()`执行。 在该方法中，必须检索和写回文本框中的当前日期。

为此，语法如下所示：首先，代理对象`PopupControlExtender`页面上必须生成。 ASP.NET AJAX 控件工具包提供了`GetProxyForCurrentPopup()`方法。 此方法返回的对象支持`Commit()`方法可将值发送回控件触发的弹出窗口 （不触发方法调用的控件 ！）。 下面的代码提供的参数作为所选的日期`Commit()`方法，从而导致代码以便将所选的日期写回到文本框中：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

现在每当您单击日历日期后，所选的日期将显示在关联的文本框中，创建日期选取器控件的当前可在许多网站上。


[![T当用户单击文本框时显示他日历](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))


[![C单击某个日期上会将其放在文本框中](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

单击某个日期将其放在文本框中 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [上一页](using-multiple-popup-controls-vb.md)
> [下一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)

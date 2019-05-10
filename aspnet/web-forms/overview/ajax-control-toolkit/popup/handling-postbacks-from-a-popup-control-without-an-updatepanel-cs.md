---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 通过使用没有 UpdatePanel (C#) 的弹出控件处理回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 当回发发生时 su...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 05a365e26a1d66c7d4034dbbec2d7f158e0b4164
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132503"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>使用没有 UpdatePanel 的弹出控件处理回发 (C#)

通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 在这样的面板中产生的回发和页面上有多个面板时很难确定单击的面板。

## <a name="overview"></a>概述

AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 在这样的面板中产生的回发和页面上有多个面板时很难确定单击的面板。

## <a name="steps"></a>步骤

使用时`PopupControl`带回发，但无`UpdatePanel`的页上，控件工具包不提供任何方法来确定哪些客户端元素已触发反过来引起回发的弹出窗口。 但是借助一个小技巧对于此方案提供一种解决方法。

首先，下面是基本设置： 这两个触发的同一个弹出窗口中，日历的两个文本框。 两个`PopupControlExtenders`将文本框和弹出项组合在一起。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

基本理念是隐藏的窗体字段中添加&lt; `form` &gt;包含启动弹出项文本框中的元素：

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

加载页面时，JavaScript 代码将事件处理程序添加到两个文本框：每当用户单击文本框时，其名称写入到隐藏窗体字段：

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

在服务器端代码中，必须读取的隐藏字段的值。 由于隐藏的表单字段进行了一些无关紧要操作，一种允许列表方法验证隐藏的值是必需的。 一旦确定正确的文本框中，从日历中的日期写入到它。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[![当用户单击文本框中，将显示日历](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))

[![单击某个日期将其放入文本框](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

单击某个日期将其放在文本框中 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [上一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一页](using-multiple-popup-controls-vb.md)

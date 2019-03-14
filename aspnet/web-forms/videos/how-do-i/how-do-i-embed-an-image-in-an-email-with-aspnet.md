---
uid: web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
title: '[如何实现:]在包含 ASP.NET 的电子邮件中嵌入图像 |Microsoft Docs'
author: rick-anderson
description: Chris Pels 显示了如何使用 ASP.NET 在电子邮件中嵌入图像。 他创建 web 窗体 （带有字段的收件人、 发件人、 主题和正文），然后使用 AlternateView...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: 424788ac-0a43-4063-99e7-db5aa4c66a9d
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-embed-an-image-in-an-email-with-aspnet
msc.type: video
ms.openlocfilehash: d046c988c060580b856fb65c90521c3a2815e760
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059684"
---
<a name="how-do-i-embed-an-image-in-an-email-with-aspnet"></a>[如何实现:]在包含 ASP.NET 的电子邮件中嵌入图像
====================
通过[Chris Pels](https://twitter.com/chrispels)

Chris Pels 显示了如何使用 ASP.NET 在电子邮件中嵌入图像。 他创建 web 窗体 （带有字段的收件人、 发件人、 主题和正文）、 AlternateView 类用于创建文本和 HTML 版本的一封电子邮件、 的 LinkedResource 类实例中存储图像，HTML AlternateView 将其嵌入。 然后，他将这两个版本添加到 MailMessage 对象并将电子邮件发送两次，第一种使用 HTML 接收功能启用，然后作为纯文本。 在 Outlook 中会显示这两个电子邮件消息。 该 HTML 版本显示嵌入的图像;文本版本却没有。

[&#9654;观看视频 （19 分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-embed-an-image-in-an-email-with-aspnet)

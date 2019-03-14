---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: 在 Repeater (VB) 中使用 ConfirmButton |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ConfirmButton 扩展器创建答： 是/没有弹出菜单，用户单击按钮时 （包括 LinkButton 控件）。 仅当是是...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 38ac40776c2fdd14af046b5e13df0701c71a4ad0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044314"
---
<a name="using-a-confirmbutton-in-a-repeater-vb"></a>在 Repeater 中使用 ConfirmButton (VB)
====================
通过[Christian Wenz](https://github.com/wenz)

[下载代码](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> AJAX 控件工具包中的 ConfirmButton 扩展器创建答： 是/没有弹出菜单，用户单击按钮时 （包括 LinkButton 控件）。 仅当单击是，则执行是按钮的操作，否则取消。 这也是可以在 repeater 中。


## <a name="overview"></a>概述

AJAX 控件工具包中的 ConfirmButton 扩展器创建答： 是/没有弹出菜单，用户单击按钮时 （包括 LinkButton 控件）。 仅当单击是，则执行是按钮的操作，否则取消。 这也是可以在 repeater 中。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。 若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。

对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。 如果你的设置不同，您必须调整数据库的连接信息。

若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

然后，数据源是必需的。 为简单起见，检索仅 AdventureWorks 的供应商表中的前五个条目。 请注意，当使用 Visual Studio 向导来创建数据源时，表名 (`Vendors`) 当前不使用正确的前缀与`Purchasing`。 以下标记是正确的订阅：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

然后可以在 repeater 中使用此数据源。 像往常一样，`DataBinder.Eval()`方法从数据源检索数据。 `ConfirmButtonExtender`然后必须将控件放在`<ItemTemplate>`中继器使其显示为数据源中的每个条目的部分。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]


[![数据源的每个项旁边显示确认按钮](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

数据源的每个项旁边显示确认按钮 ([单击此项可查看原尺寸图像](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一篇](using-a-confirmbutton-in-a-repeater-cs.md)

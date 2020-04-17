---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX 控制工具包控制和控制扩展器 （C#） |微软文档
author: rick-anderson
description: 了解如何将 AJAX 控制工具包控件和扩展器添加到ASP.NET页。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543712"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>使用 AJAX 控件工具包控件和控件扩展程序 (C#)

由[微软](https://github.com/microsoft)

> 了解如何将 AJAX 控制工具包控件和扩展器添加到ASP.NET页。

AJAX 控制工具包包含一组控件和控制扩展器。 在本教程中，您将了解如何将控件和控制扩展器添加到ASP.NET页。

> [!NOTE] 
> 
> 有关安装 AJAX 控制工具包并将 AJAX 控制工具包添加到可视化工作室/可视化 Web 开发人员工具包的说明，请参阅[有关 AJAX 控件工具包入门](get-started-with-the-ajax-control-toolkit-cs.md)教程。

## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX 控制工具包控件

AJAX 控制工具包控件的工作方式与普通ASP.NET控件类似。 您可以将控件从工具箱拖到ASP.NET页上。 您可以在"设计"视图或"源"视图中将控件添加到页面。

使用 AJAX 控制工具包中的控件时有一个特殊要求。 该页必须包含脚本管理器控件。 脚本管理器控件负责包括 AJAX 控制工具包控件所需的所有 JavaScript。

例如，AJAX 控件工具包选项卡包括名为编辑器控件的控件。 此控件显示丰富的 HTML 编辑器。 按照以下步骤将编辑器控件添加到页面：

1. 创建新ASP.NET页面名为 ShowEditor.aspx
2. 从工具箱中的 AJAX 扩展选项卡下方选择脚本管理器控件，并将该控件拖到页面上。
3. 从工具箱中的 AJAX 控制工具包选项卡下方选择编辑器控件，并将控件拖到页面上（参见图 1）。 设计器应如图 2 所示。
4. 通过选择菜单选项 **"调试"、"开始调试**"或点击 F5 键来运行网站。
5. 您应该会看到图 3 中的页面。

[![选择 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**图 01**：选择 HTML 编辑器控件（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)）

[![具有脚本管理器和编辑控件的可视化工作室设计器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**图 02**： 具有脚本管理器和编辑控件的可视化工作室设计器（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)）

[![显示编辑器.aspx 页面](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**图 03**： 显示编辑器.aspx 页面（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)）

## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控制工具包控制扩展器

AJAX 控制工具包还包含控制扩展器。 顾名思义，控件扩展器扩展了现有控件的功能。 例如，"确认按钮"控件扩展器扩展了标准ASP.NET按钮控件。 扩展程序更改按钮控件的行为，以便单击按钮时显示确认对话框。

控件扩展器（与 AJAX 控件工具包控件一样）需要脚本管理器控件。 在开始使用页面中的控件扩展器之前，必须将脚本管理器控件添加到页面。

按照以下步骤使用确认按钮控件扩展器：

1. 创建新ASP.NET页面名为"显示确认按钮.aspx"
2. 通过将控件从 AJAX 扩展选项卡下方拖动到页面上，将脚本管理器控件添加到页面。
3. 通过将"按钮"从工具箱中的"标准"选项卡下方拖动到"设计器"图面，将标准按钮控件添加到页面。
4. 单击 **"添加扩展器**"任务选项（参见图 4）。
5. 在"选择扩展器"对话框中，选择"确认按钮扩展器"（参见图 5），然后单击"确定"按钮。
6. 选择设计器中的"按钮"控件并展开"属性"窗口中的\_Button1 确认按钮扩展器节点（参见图 6）。 将值 *"真的？"* 分配给"确认文本"属性。
7. 通过选择菜单选项 **"调试"、"开始调试"** 或点击 F5 键来运行页面。

[![添加扩展器任务选项](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**图 04**： 添加扩展器任务选项（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)）

[![选择确认按钮控制扩展器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**图 05**： 选择确认按钮控件扩展器（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)）

[![设置确认按钮属性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**图 06**： 设置确认按钮属性（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)）

打开页面时，应看到一个按钮。 单击该按钮时，您将获得图 7 中的确认对话框。

[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**图 07**： 显示确认对话框（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)）

请注意，您通常不会将控件扩展器拖动到页面上。 相反，您可以使用 **"添加扩展器**"任务选项将扩展器添加到已添加到页面的控件。 此外，请注意，通过打开要扩展的控件的属性表来设置控件扩展器属性。

单个ASP.NET控件可以通过多个控件扩展器进行扩展。 要扩展的控件的属性表将列出与控件关联的所有控件扩展器。

> [!div class="step-by-step"]
> [上一页](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)

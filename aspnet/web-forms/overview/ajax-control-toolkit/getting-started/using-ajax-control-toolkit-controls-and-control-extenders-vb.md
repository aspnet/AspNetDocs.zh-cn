---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: 使用 AJAX 控件工具包控件和控件扩展程序 (VB) |Microsoft Docs
author: rick-anderson
description: 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 416ee0d4931a3850c1e9bb4ba28db43f5e1647bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044358"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>使用 AJAX 控件工具包控件和控件扩展程序 (VB)

由 [Microsoft](https://github.com/microsoft)

> 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。

AJAX 控件工具包包含一组控件和控件扩展器。 本 brief 教程介绍如何将控件和控件扩展程序添加到 ASP.NET 页。

> [!NOTE] 
> 
> 有关安装 AJAX 控件工具包并将 AJAX 控件工具包添加到 Visual Studio/Visual Web Developer 工具箱的说明，请参阅 [AJAX 控件工具包入门](get-started-with-the-ajax-control-toolkit-vb.md)教程。

## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX 控件工具包控件

AJAX 控件工具包控件的工作方式与常规 ASP.NET 控件的工作方式相同。 可以将控件从 "工具箱" 拖动到 "ASP.NET" 页上。 可以在 "设计视图" 或 "源" 视图中将控件添加到该页。

使用 AJAX 控件工具包中的控件时，有一种特殊要求。 页面必须包含 ScriptManager 控件。 ScriptManager 控件负责包含 AJAX 控件工具包控件所需的所有必需 JavaScript。

例如，"AJAX 控件工具包" 选项卡包含一个名为 "编辑器控件" 的控件。 此控件显示丰富的 HTML 编辑器。 按照以下步骤将编辑器控件添加到页面：

1. 创建名为 ShowEditor 的新 ASP.NET 页
2. 从 "工具箱" 中的 "AJAX 扩展" 选项卡下选择 "ScriptManager" 控件，并将该控件拖到页面上。
3. 从 "工具箱" 中的 "AJAX 控件工具包" 选项卡下选择编辑器控件，并将控件拖到页面上 (参阅图 1) 。 设计器应类似于图2。
4. 通过选择菜单选项 " **调试"、"开始调试"** 或按 F5 键运行网站。
5. 你应会看到图3中的页面。

[![选择 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**图 01**：选择 HTML 编辑器控件 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)) 

[![带有 ScriptManager 和编辑控件的 Visual Studio 设计器](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**图 02**：包含 ScriptManager 和编辑控件的 Visual Studio 设计器 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)) 

[![DisplayEditor 页](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**图 03**： DisplayEditor 页 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png)) 

## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控件工具包控件扩展程序

AJAX 控件工具包还包含控件扩展程序。 顾名思义，控件扩展器扩展了现有控件的功能。 例如，ConfirmButton 控件扩展器扩展了标准 ASP.NET 按钮控件。 扩展器将更改按钮控件的行为，以便在单击按钮时显示确认对话框。

像 AJAX 控件工具包控件一样，控件扩展器需要 ScriptManager 控件。 在开始使用页面中的控件扩展器之前，必须将 ScriptManager 控件添加到页面。

请按照以下步骤使用 ConfirmButton 控件扩展器：

1. 创建名为 ShowConfirmButton 的新 ASP.NET 页
2. 通过将控件从 "AJAX 扩展" 选项卡下拖到页面上，将 ScriptManager 控件添加到页面。
3. 通过从工具箱中的 "标准" 选项卡下将按钮拖到设计器图面上，将标准按钮控件添加到页面。
4. 单击 " **添加扩展** 器任务" 选项 (参阅图 4) 。
5. 在 "选择扩展器" 对话框中，选择 "ConfirmButtonExtender (参阅图 5) 并单击" 确定 "按钮。
6. 在设计器中选择 "Button" 控件，在属性窗口中展开 "Button1"、 \_ "Button1 ConfirmButtonExtender" 节点 (参见图 6) 。 将值 *"真的？"* 到 ConfirmText 属性。
7. 通过选择菜单选项 " **调试"、"开始调试** " 或按 F5 键来运行页面。

[!["添加扩展器任务" 选项](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**图 04**： "添加扩展器任务" 选项 ([单击以查看完全大小的图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)) 

[![选择 ConfirmButton 控件扩展器](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**图 05**：选择 ConfirmButton 控件扩展器 ([单击查看完全大小的图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)) 

[![设置 ConfirmButton 属性](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**图 06**：设置 ConfirmButton 属性 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)) 

当该页打开时，您应该会看到一个按钮。 单击该按钮时，会收到图7所示的确认对话框。

[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**图 07**：显示确认对话框 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)) 

请注意，通常不会将控件扩展器拖到页面上。 相反，可以使用 " **添加扩展** 器任务" 选项将扩展器添加到已添加到页面的控件。 此外，请注意，您可以通过打开要扩展的控件的属性表来设置控件扩展器属性。

多个控件扩展程序可以扩展单个 ASP.NET 控件。 要扩展的控件的属性表将列出与该控件关联的所有控件扩展程序。

> [!div class="step-by-step"]
> [上一页](get-started-with-the-ajax-control-toolkit-vb.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)

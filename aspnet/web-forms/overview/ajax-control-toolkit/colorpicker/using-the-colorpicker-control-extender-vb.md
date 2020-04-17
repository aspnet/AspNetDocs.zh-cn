---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用彩选器控件扩展器 （VB） |微软文档
author: rick-anderson
description: ColorPicker 是一个ASP.NET AJAX 扩展器，在弹出窗口控件中提供客户端选色功能和 UI。 它可以附加到任何ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542841"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>使用彩选器控件扩展器 （VB）

由[微软](https://github.com/microsoft)

> ColorPicker 是一个ASP.NET AJAX 扩展器，在弹出窗口控件中提供客户端选色功能和 UI。 它可以附加到任何ASP.NET文本框控件。 它。

本教程的目的是解释如何使用 AJAX 控件工具包 ColorPicker 控件扩展器。 ColorPicker 控件扩展器显示一个弹出对话框，使您能够选择颜色。 当您要为用户提供直观的用户界面以选择颜色时，ColorPicker 非常有用。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>使用彩选择器控件扩展器扩展文本框控件

例如，假设您想要创建一个网站，使访问者能够创建自定义的名片。 访问者可以输入名片的文本并选择颜色。 清单1中的ASP.NET页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。 提交表单时，将显示所选值（参见图 1）。

[![创建名片的简单表单](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**图01：** 创建名片的简单表单（[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image2.png)）

**清单 1 - 创建卡.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

清单1中的表单有效，但它不能提供出色的用户体验。 用户必须键入文本框中的颜色。 如果用户想要专用颜色（例如，只是豌豆绿色的正确阴影），则用户必须在没有任何帮助的情况下找出 HTML 颜色代码。

您可以使用 ColorPicker 控件扩展器来创建更好的用户体验。 将焦点移动到 TextBox 控件时，颜色选取器将显示颜色对话框（参见图 2）。

[![彩工控制扩展器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**图 02**： 彩选择器控件扩展器 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image4.png)）

您需要完成两个步骤才能将 ColorPicker 控件扩展器与清单 1 中的窗体一起使用：

1. 将脚本管理器控件添加到页面
2. 将彩选择器控件扩展器添加到页面

在使用 ColorPicker 之前，必须向页面添加脚本管理器。 添加脚本管理器的好地方就在打开的服务器端&lt;表单&gt;标记的正下方。 您可以将脚本管理器从工具箱拖到页面上（脚本管理器位于 AJAX 扩展选项卡下）。 或者，您可以在打开服务器端窗体标记下的源视图中键入以下标记：

&lt;asp：脚本管理器 ID="脚本管理器1"运行 at="服务器" /&gt;

将 ColorPicker 控件扩展器添加到页面的最简单方法是在"设计视图"中。 如果将鼠标悬停在 txtCardColor TextBox 上，将显示一个智能任务选项，使您能够添加扩展器（参见图 3）。 如果选择此选项，将显示扩展器向导（参见图 4）。

[![添加扩展器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**图 03**： 添加扩展器 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image6.png)）

[![使用扩展器向导选择控件扩展器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**图 04**：使用扩展器向导选择控件扩展器（[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image8.png)）

您可以选择颜色选取器扩展器，以便使用颜色选取器扩展器扩展 txtCardColor 文本盒。 单击“确定”，关闭对话框。

进行这些更改后，页面的源类似于清单 2。

**清单2 - CreateCard.aspx（带彩选器）**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

请注意，该页面现在包含一个颜色选取器扩展器控件，该控件直接显示在 txtCardColor 文本盒控件的正下方。 颜色选取器扩展器控件扩展 txtCardColor 控件，以便显示颜色选取器对话框。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>使用按钮启动颜色选取器对话框

颜色选取器扩展器支持以下属性：

- 弹出ButtonId - 页面上导致颜色选取器对话框显示的按钮的 ID。
- 弹出位置 - 颜色选取器对话框相对于目标控件的位置。 可能的值是"绝对"、"中心"、"左下"、"右下角"、"左上"、"右"、"左"（默认值为"左下"。
- 示例控制 Id - 显示所选颜色的控件的 ID。
- 选择颜色 - 颜色选取器选择的初始颜色。

您可以使用这些属性自定义颜色选取器对话框的显示方式以及所选颜色的显示方式。 清单3中的页面说明了如何使用其中几个属性。

**清单3 - 创建卡按钮.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

清单3中的页面包括"选取颜色"按钮（参见图 5）。 单击此按钮时，颜色选取器对话框将显示在 TextBox 上方。 如果从对话框中选择颜色，则所选颜色将显示为 lblSample 标签控件的背景颜色。

"颜色选取器弹出按钮ID"属性用于将"拾取颜色"按钮与"颜色选取器"扩展器相关联。 当您提供 PopupButtonID 属性的值时，当目标控件具有焦点时，颜色选取器对话框将不再显示。 您必须单击该按钮才能显示对话框。

SampleControlID 属性用于将显示所选颜色的控件与颜色选取器相关联。 颜色选取器将此控件的背景颜色更改为当前选择的颜色。

[![使用按钮显示颜色选取器对话框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**图 05**： 使用按钮显示颜色选取器对话框 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image10.png)）

## <a name="summary"></a>总结

在本教程中，您学习了如何使用 ColorPicker 控件扩展器来显示弹出颜色选取器对话框。 首先，我们检查了在焦点移动到 TextBox 控件时如何显示对话框。 接下来，您学习了如何在单击该按钮时创建显示颜色选取器对话框的按钮。

> [!div class="step-by-step"]
> [上一篇](using-the-colorpicker-control-extender-cs.md)

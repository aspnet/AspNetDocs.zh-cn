---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 开始使用 AJAX 控制工具包 （C#） |微软文档
author: rick-anderson
description: 了解开始使用 AJAX 控制工具包所需的所有知识。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543582"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>AJAX 控件工具包入门 (C#)

由[微软](https://github.com/microsoft)

> 了解开始使用 AJAX 控制工具包所需的所有知识。

AJAX 控制工具包包含 30 多个免费控件，可用于ASP.NET应用程序中。 在本教程中，您将了解如何下载 AJAX 控件工具包，并将工具包控件添加到可视化工作室/可视化 Web 开发人员快速工具箱。

## <a name="downloading-the-ajax-control-toolkit"></a>下载 AJAX 控制工具包

[AJAX 控制工具包](http://devexpress.com/act)是由ASP.NET社区成员和ASP.NET团队开发的开源项目。 

[![下载 AJAX 控制工具包](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**图 01**： 下载 AJAX 控制工具包（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)）

下载文件后，需要取消阻止该文件。 右键单击文件，选择"属性"，然后单击 **"取消阻止"** 按钮（参见图 2）。

[![取消阻止 AJAX 控制工具包 ZIP 文件](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**图 02**： 取消阻止 AJAX 控制工具包 ZIP 文件（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)）

取消阻止文件后，可以解压缩文件：右键单击该文件并选择 **"全部提取"** 菜单选项。 现在，我们准备将工具包添加到可视化工作室/可视化 Web 开发人员工具箱。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>将 AJAX 控制工具包添加到工具箱

使用 AJAX 控制工具包的最简单方法是将工具包添加到可视化工作室/可视化 Web 开发人员工具箱（参见图 3）。 这样，您只需在要使用工具包控件时将其拖到页面上即可。

[![AJAX 控制工具包显示在工具箱中](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**图 03**： AJAX 控制工具包显示在工具箱中（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)）

首先，您需要向工具箱添加 AJAX 控制工具包选项卡。 执行以下步骤。

1. 通过选择菜单选项"文件，新网站"，创建新ASP.NET网站。 双击解决方案资源管理器窗口中的 Default.aspx 以在编辑器中打开该文件。
2. 右键单击"常规选项卡"下方的工具框，然后选择菜单选项 **"添加选项卡**"（参见图 4）。
3. 输入名为 AJAX 控制工具包的新选项卡。

[![添加新选项卡](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**图 04**：添加新选项卡（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)）

接下来，您需要将 AJAX 控件工具包控件添加到新选项卡中。按照以下步骤操作：

- 右键单击 AJAX 控制工具包选项卡下方，然后选择菜单选项 **"选择项目"（参见图 5）。**
- 浏览到解压缩 AJAX 控制工具包的位置，然后选择 AjaxControlToolkit.dll 程序集。

[![选择要添加到工具箱的项目](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**图 05**： 选择要添加到工具箱的项目（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)）

完成这些步骤后，所有工具包控件都将显示在工具箱中。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>升级到新版本的工具包

如果您使用的是旧版本的工具包，现在需要移动到更高版本，下面是建议的步骤：

- 二进制 - 从您的网站 Bin 文件夹中删除 AjaxControlToolkit.dll 程序集的旧版本。
- 工具箱项目 - 删除 AJAX 控制工具包选项卡，然后按照上述步骤重新创建具有新版本 AjaxControlToolkit.dll 程序集的选项卡。

> [!div class="step-by-step"]
> [下一页](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)

---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: '如何实现使用 ComboBox 控件？  (C # ) |Microsoft Docs'
author: rick-anderson
description: ComboBox 是 ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可从中选择的选项列表组合在一起。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 035bcb2fb6cce246b904c295aba15efd17c2c232
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045060"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>如何实现使用 ComboBox 控件？ (C#)

由 [Microsoft](https://github.com/microsoft)

> ComboBox 是 ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可从中选择的选项列表组合在一起。

本教程的目的是介绍 AJAX 控件工具包组合框控件。 ComboBox 的工作方式类似于标准 ASP.NET DropDownList 控件和 TextBox 控件之间的组合。 您可以从预先存在的项列表中进行选择，也可以输入一个新项。

ComboBox 与自动完成控件扩展器类似，但控件在不同的方案中使用。 自动完成扩展器会查询 web 服务以获取匹配项。 相反，ComboBox 控件用一组项进行了初始化。 使用 "自动完成" 扩展器时，如果使用的是大量的数据 (数百万辆汽车) 部件，则使用 ComboBox 控件在处理一小部分数据 (数十个汽车部件) 时非常有意义。

## <a name="selecting-from-a-static-list-of-items"></a>从静态项列表中选择

让我们从一个简单的示例开始使用组合框控件。 假设您想要在下拉列表中显示项的静态列表。 但是，您仍希望使列表不完整。 您希望允许用户在列表中输入自定义值。

我们将创建一个新的 ASP.NET Web 窗体页，并使用页面中的 ComboBox 控件。 向项目中添加新的 "ASP.NET" 页，并切换到设计视图。

如果要使用页面中的 ComboBox 控件，则必须将 ScriptManager 控件添加到页面。 将 ScriptManager 控件从 "AJAX 扩展" 选项卡下拖到设计器图面上。 应将 ScriptManager 控件添加到页面顶部;可以立即将其添加到 "打开服务器端 &lt; 窗体" &gt; 标记下。

接下来，将 ComboBox 控件拖到页面上。 您可以在工具箱中找到带有其他 AJAX 控件工具包控件和控件扩展器的 ComboBox 控件 (参阅图 1) 。

[![用于创建名片的简单窗体](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**图 01**：从 "工具箱" 中选择 ComboBox 控件 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image2.png)) 

我们将使用 ComboBox 控件显示静态选项列表。 用户可以从以下三个选项的列表中为其食物选择特定级别的 spiciness： "轻度"、"中" 和 "热" (参阅图 2) 。

[![从静态项列表中选择](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**图 02**：从静态项列表中选择 ([单击查看完全大小的图像](how-do-i-use-the-combobox-control-cs/_static/image4.png)) 

可以通过两种方法将这些选项添加到 ComboBox 控件中。 首先，在将鼠标悬停在设计视图的控件上并打开项编辑器 (，选择 "编辑选项" 任务选项，请参见图 3) 。

[![编辑 ComboBox 项](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**图 03**：编辑 ComboBox 项 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image6.png)) 

第二种方法是在 "源" 视图中打开和关闭 &lt; asp： ComboBox 标记之间添加项的列表 &gt; 。 列表1中的页包含已更新的 ComboBox，其中包含项的列表。

**列表 1-Static .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

打开列表1中的页时，可以从组合框中选择一个预先存在的选项。 换言之，组合框的工作方式与 DropDownList 控件的工作方式相同。

但是，您还可以选择输入新的选项 (例如，不在现有列表中的超级 Spicy) 。 因此，组合框的工作方式也类似于 TextBox 控件。

无论你是选取预先存在的项还是输入自定义项，当你提交窗体时，你的选择将显示在 "标签" 控件中。 提交表单时，Btnsubmit.text \_ 单击处理程序将执行并更新标签 (参见图 4) 。

[![显示选定项](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**图 04**：显示选定项 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image8.png)) 

提交窗体后，ComboBox 支持与 DropDownList 控件相同的属性，以便检索选定项：

- SelectedItem-显示所选项目的 "Text" 属性的值。
- SelectedItem-显示所选项目的值属性的值，或显示键入到 ComboBox 中的文本。
- SelectedValue-与 SelectedItem 相同，不同的是，此属性使你能够指定 (初始) 选定项的默认值。

如果在 ComboBox 中键入自定义选项，则会将自定义选择同时分配给 SelectedItem 和 SelectedItem 属性。

## <a name="selecting-the-list-of-items-from-the-database"></a>从数据库中选择项列表

可以从数据库中检索 ComboBox 显示的项的列表。 例如，可以将 ComboBox 绑定到 SqlDataSource 控件、ObjectDataSource 控件、LinqDataSource 或 EntityDataSource。

假设您想要在组合框中显示电影列表。 要从电影数据库表中检索电影列表。 执行以下步骤：

1. 创建名为 "default.aspx" 的页
2. 通过从工具箱中的 "AJAX 扩展" 选项卡下将 ScriptManager 拖到页面上，将 ScriptManager 控件添加到页面。
3. 通过将 ComboBox 拖到页面上，将 combobox 控件添加到页面。
4. 在设计视图中，将鼠标悬停在 ComboBox 控件上，然后选择 " **选择数据源** " 任务选项 (参见图 5) 。 将启动 "数据源配置向导"。
5. 在 " **选择数据源** " 步骤中，选择 " &lt; 新建数据源" &gt; 选项。
6. 在 " **选择数据源类型** " 步骤中，选择 "数据库"。
7. 在 " **选择你的数据连接** " 步骤中，选择你的数据库 (例如 MoviesDB) 。
8. 在 "将 **连接字符串保存到应用程序配置文件** " 步骤中，选择用于保存连接字符串的选项。
9. 在 " **配置 Select 语句** " 步骤中，选择 "电影数据库" 表并选择所有列。
10. 在 **测试查询** 步骤中，单击 "完成" 按钮。
11. 返回 " **选择数据源** " 步骤，选择要显示的字段的 "标题" 列以及 "数据" 字段的 "Id" 列 (参阅图) 。
12. 单击 "确定" 按钮以关闭该向导。

[![选择数据源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**图 05**：选择数据源 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image10.png)) 

[![选择数据文本和值字段](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**图 06**：选择数据文本和值字段 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image12.png)) 

完成上述步骤后，ComboBox 将绑定到表示电影数据库表中的电影的 SqlDataSource 控件。 页面的源如下所示， (我清理了有点) 的格式。

**列表 2-电影 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

请注意，ComboBox 控件具有指向 SqlDataSource 控件的 DataSourceID 属性。 当你在浏览器中打开该页面时，将显示该数据库中的电影列表 (参见图 7) 。 您可以从列表中选择电影，也可以通过在 ComboBox 中键入电影来输入新电影。

[![显示电影列表](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**图 07**：显示电影列表 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image14.png)) 

## <a name="setting-the-dropdownstyle"></a>设置 DropDownStyle

可以使用 ComboBox DropDownStyle 属性更改 ComboBox 的行为。 此属性接受可能的值：

- 下拉列表 (默认值) 在单击箭头时，组合框将显示一个下拉列表，您可以输入自定义值。
- 简单-ComboBox 自动显示下拉列表，你可以输入自定义值。
- DropDownList-ComboBox 的工作方式与 DropDownList 控件的工作方式相同。

下拉列表和简单选项之间的不同之处是显示项列表。 在简单的情况下，当您将焦点移到 ComboBox 上时，列表会立即显示。 对于下拉列表，必须单击箭头才能查看项列表。

DropDownList 值使 ComboBox 控件像标准的 DropDownList 控件一样工作。 但是，这里有一个重要的差异。 较早版本的 Internet Explorer 显示具有无限 z 索引的 DropDownList 控件，因此控件将显示在其前面放置的任何控件之前。 由于组合框会呈现 HTML &lt; div &gt; 标记，而不是 &lt; html &gt; 选择标记，因此 combobox 正确遵从 z 顺序。

## <a name="setting-the-autocompletemode"></a>设置 AutoCompleteMode

使用 ComboBox AutoCompleteMode 属性可以指定有人将文本键入 ComboBox 时所发生的情况。 此属性接受以下可能值：

- 无-ComboBox)  (默认值不提供任何自动完成行为。
- 建议-ComboBox 显示列表并且突出显示列表中的匹配项 (参见图 8) 。
- 追加-ComboBox 不显示列表，它将列表中的匹配项追加到你键入的内容 (参见图 9) 。
- SuggestAppend-ComboBox 显示列表，并将列表中的匹配项追加到你键入的内容 (参阅图 10) 。

[![组合框提出建议](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**图 08**：组合框提出建议 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image16.png)) 

[![ComboBox 追加匹配文本](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**图 09**： ComboBox 将匹配的文本追加 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image18.png)) 

[![ComboBox 建议并追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**图 10**： ComboBox 建议并追加 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image20.png)) 

## <a name="summary"></a>摘要

在本教程中，您学习了如何使用 ComboBox 控件显示一组固定的项。 我们将 ComboBox 控件绑定到一组静态项和一个数据库表。 最后，您学习了如何通过设置组合框的 DropDownStyle 和 AutoCompleteMode 属性来修改其行为。

> [!div class="step-by-step"]
> [下一页](how-do-i-use-the-combobox-control-vb.md)

---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 如何使用组合盒控件？ （C#） |微软文档
author: rick-anderson
description: ComboBox 是一ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可以选择的选项列表相结合。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543800"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>如何使用组合盒控件？ (C#)

由[微软](https://github.com/microsoft)

> ComboBox 是一ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可以选择的选项列表相结合。

本教程的目的是解释 AJAX 控制工具包组合盒控件。 组合框的工作方式类似于标准ASP.NET下拉列表控件和文本框控件之间的组合。 您可以从预先存在的项目列表中选择，也可以输入新项目。

组合盒类似于自动完成控件扩展器，但控件在不同的方案中使用。 自动完成扩展程序查询 Web 服务以获取匹配的条目。 相反，组合框控件使用一组项进行初始化。 使用 AutoComplete 扩展程序在使用大量数据（数百万个汽车零件）时有意义，而使用 ComboBox 控件在使用一小组数据（数十个汽车部件）时是有意义的。

## <a name="selecting-from-a-static-list-of-items"></a>从静态项目列表中选择

让我们从使用组合框控件的简单示例开始。 假设您要在下拉列表中显示项目的静态列表。 但是，您希望保留列表未完成的可能性。 您希望允许用户在列表中输入自定义值。

我们将创建一个新的ASP.NET Web 窗体页，并在该页中使用 ComboBox 控件。 将新的ASP.NET页添加到项目中并切换到"设计"视图。

如果要在页面中使用 ComboBox 控件，则必须向页面添加脚本管理器控件。 将脚本管理器控件从 AJAX 扩展选项卡下方拖动到设计器表面。 应在页面顶部添加脚本管理器控件;但是，在页面顶部，应添加脚本管理器控件。可以将其添加到打开的服务器端&lt;窗体&gt;标记的下方。

接下来，将组合框控件拖到页面上。 您可以在工具箱中找到与其他 AJAX 控制工具包控件和控制扩展器一起的 ComboBox 控件（见图 1）。

[![创建名片的简单表单](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**图 01**： 从工具箱中选择组合框控件 （[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image2.png)）

我们将使用组合框控件来显示静态选项列表。 用户可以从三个选项列表中为其食物选择特定级别的辣度（参见图 2）。

[![从静态项目列表中选择](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**图 02**：从静态项目列表中选择（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image4.png)）

有两种方法可以将这些选项添加到 ComboBox 控件。 首先，在"设计"视图中将鼠标悬停在控件上并打开项目编辑器时，请选择"编辑选项"任务选项（参见图 3）。

[![编辑组合框项目](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**图 03**： 编辑组合盒项目（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image6.png)）

第二个选项是在源视图中的开盘和关闭&lt;asp：ComboBox&gt;标记之间添加项目列表。 清单 1 中的页面包含包含项目列表的更新的 ComboBox。

**清单 1 - 静态.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

在清单 1 中打开页面时，您可以从组合框中选择一个预先存在的选项。 换句话说，组合框的工作方式与下拉列表控件类似。

但是，您还可以选择输入不在现有列表中的新选项（例如，超级辣）。 因此，组合框也像文本框控件一样工作。

无论您选择预先存在的项目还是输入自定义项目，在提交表单时，您的选择都会显示在标签控件中。 提交表单时，btnSubmit\_单击处理程序将执行并更新标签（参见图 4）。

[![显示所选项目](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**图 04**：显示所选项目（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image8.png)）

ComboBox 支持与提交表单后检索所选项的下拉列表控件相同的属性：

- 选定项目.文本 - 显示所选项目的文本属性的值。
- 选定项目.值 - 显示所选项目的值属性的值或显示键入到组合盒中的文本。
- 所选值 - 与选定项目相同。除非此属性允许您指定默认（初始）选定项目。

如果在组合框中键入自定义选项，则自定义选项将分配给"选定项目.文本"和"选定项目"值属性。

## <a name="selecting-the-list-of-items-from-the-database"></a>从数据库中选择项目列表

您可以检索 ComboBox 从数据库中显示的项目列表。 例如，您可以将组合盒绑定到 SqlDataSource 控件、ObjectDataSource 控件、LinqDataSource 或实体数据源。

假设您要在组合盒中显示电影列表。 您希望从"影片"数据库表中检索影片列表。 执行以下步骤:

1. 创建名为"电影.aspx"的页面
2. 通过将脚本管理器从工具箱中的 AJAX 扩展选项卡下拖动到页面，将脚本管理器控件添加到页面。
3. 通过将组合框拖到页面上，将组合框控件添加到页面。
4. 在"设计"视图中，将鼠标悬停在 ComboBox 控件上，然后选择 **"选择数据源**任务"选项（参见图 5）。 启动数据源配置向导。
5. 在 **"选择数据源**"步骤中，选择"&lt;新建数据源"&gt;选项。
6. 在 **"选择数据源类型"步骤中**，选择"数据库"。
7. 在 **"选择数据连接**"步骤中，选择数据库（例如，MoviesDB.mdf）。
8. 在 **"将连接字符串保存到应用程序配置文件"步骤中**，选择保存连接字符串的选项。
9. 在 **"配置选择语句"** 步骤中，选择"影片"数据库表并选择所有列。
10. 在 **"测试查询**"步骤中，单击"完成"按钮。
11. 回到 **"选择数据源**"步骤中，选择要显示的字段的标题列和数据字段的"Id"列（参见图）。
12. 单击"确定"按钮关闭向导。

[![选择数据源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**图 05**： 选择数据源（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image10.png)）

[![选择数据文本和值字段](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**图 06**：选择数据文本和值字段（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image12.png)）

完成上述步骤后，组合Box 将绑定到 SqlDataSource 控件，该控件表示"电影"数据库表中的影片。 页面的源类似于清单 2（我稍微清理了格式）。

**列表 2 - 电影.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

请注意，ComboBox 控件具有指向 SqlDataSource 控件的 DataSourceID 属性。 在浏览器中打开页面时，将显示数据库中的影片列表（参见图 7）。 您可以通过在组合盒中键入影片从列表中选取影片或输入新影片。

[![显示电影列表](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**图 07**： 显示电影列表（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image14.png)）

## <a name="setting-the-dropdownstyle"></a>设置下拉样式

您可以使用组合盒下拉列表样式属性更改组合框的行为。 此属性接受可能存在的值：

- 下拉 - （默认值） 当您单击箭头并且可以输入自定义值时，组合框将显示下拉列表。
- 简单 - 组合框会自动显示下拉列表，您可以输入自定义值。
- 下拉列表 - 组合框的工作方式与下拉列表控件类似。

下拉列表和"简单"之间的不同是显示项目列表时。 在 Simple 的情况下，当您将焦点移动到组合框时，将立即显示列表。 在下拉列表的情况下，必须单击箭头才能看到项目列表。

"下拉列表"值使组合盒控件的工作方式与标准的下拉列表控件类似。 然而，这里有一个重要的区别。 较旧版本的 Internet Explorer 显示具有无限 z 索引的下拉列表控件，因此该控件将显示在放置在其前面的任何控件的前面。 由于组合&lt;框呈现 HTML div&gt;标记而不是 HTML&lt;选择&gt;标记，因此组合框正确尊重 z 排序。

## <a name="setting-the-autocompletemode"></a>设置自动完成模式

您可以使用 ComboBox 自动完成模式属性来指定当有人在组合框中键入文本时会发生什么情况。 此属性接受以下可能的值：

- 无 - （默认值） 组合框不提供任何自动完成行为。
- 建议 - 组合框显示列表，并突出显示列表中的匹配项（参见图 8）。
- 附加 - 组合框不显示列表，它将匹配项从列表中追加到已键入的内容（参见图 9）。
- 建议应用 - 组合框都会显示列表并将匹配项从列表中追加到已键入的内容上（参见图 10）。

[![组合盒提出建议](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**图 08**： 组合框提出建议（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image16.png)）

[![组合盒追加匹配文本](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**图 09**： 组合盒追加匹配文本（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image18.png)）

[![组合框建议和追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**图10**： 组合框建议和追加（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image20.png)）

## <a name="summary"></a>总结

在本教程中，您学习了如何使用 ComboBox 控件来显示一组固定的项目。 我们将组合框控件绑定到静态项集和数据库表。 最后，您学习了如何通过设置其下拉风格和自动完成模式属性来修改组合盒的行为。

> [!div class="step-by-step"]
> [下一页](how-do-i-use-the-combobox-control-vb.md)

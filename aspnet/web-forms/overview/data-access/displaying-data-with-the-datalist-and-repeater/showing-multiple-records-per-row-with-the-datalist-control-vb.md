---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
title: 显示多条记录，每行使用 DataList 控件 (VB) |Microsoft Docs
author: rick-anderson
description: 在本简短教程中，我们将探讨如何自定义 DataList 的布局通过其 RepeatColumns 和 RepeatDirection 属性。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: f555c531-bf33-4699-9987-42dbfef23c1f
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e8b5493694b24e4187ecb69ca8d2eff6a8507985
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421214"
---
<a name="showing-multiple-records-per-row-with-the-datalist-control-vb"></a>使用 DataList 控件每行显示多条记录 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_VB.exe)或[下载 PDF](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/datatutorial31vb1.pdf)

> 在本简短教程中，我们将探讨如何自定义 DataList 的布局通过其 RepeatColumns 和 RepeatDirection 属性。


## <a name="introduction"></a>介绍

DataList 示例我们已在过去的两个教程中看到为单列 HTML 中的行呈现其数据源中的每个记录`<table>`。 虽然这是默认 DataList 行为，是很容易自定义 DataList 显示，以便数据源项分布在多列、 多行的表。 此外，它可能有的所有数据源中的单行、 多列 DataList 显示的项目。

我们可以自定义 DataList 的布局通过其`RepeatColumns`和`RepeatDirection`属性，分别指示呈现的列数和是否这些项的布局垂直或水平。 图 1 中，例如，显示了具有三个列的表中显示产品信息 DataList。


[![DataList 显示每行的三个产品](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image1.png)

**图 1**:DataList 显示了三种产品每行 ([单击此项可查看原尺寸图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image3.png))


通过显示每行的多个数据源项，DataList 可以更有效地利用水平屏幕空间。 在本简短教程中，我们将探讨这两个 DataList 属性。

## <a name="step-1-displaying-product-information-in-a-datalist"></a>步骤 1：在 DataList 中显示的产品信息

我们检查之前`RepeatColumns`和`RepeatDirection`属性，让 s 首次创建 DataList 上我们列出了使用标准的单一列中，多行表布局的产品信息的页面。 对于此示例，让我们来显示产品名称、 类别和价格，使用以下标记：


[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample1.html)]

我们已看到了如何将数据绑定到在上一示例中，DataList，所以我将快速继续执行这些步骤。 首先打开`RepeatColumnAndDirection.aspx`页中`DataListRepeaterBasics`文件夹，然后拖动 DataList 从工具箱拖到设计器。 通过 DataList s 智能标记，选择创建新对象数据源，并将其配置为从其数据提取`ProductsBLL`类的`GetProducts`方法中，选择 （无） 选项向导的插入、 更新和删除选项卡。

创建并绑定到 DataList 的新对象数据源之后, Visual Studio 自动创建`ItemTemplate`的每个产品的数据字段显示的名称和值。 调整`ItemTemplate`直接通过声明性标记或编辑模板从选项中 DataList s 智能标记，以便它使用上面所示，替换的标记*产品名称*，*类别名称*，并*价格*具有使用相应的数据绑定语法将值分配给的标签控件的文本及其`Text`属性。 更新后`ItemTemplate`，页面 + s 声明性标记应如下所示：


[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-vb/samples/sample2.aspx)]

请注意，我已包含中的格式说明符`Eval`数据绑定语法`UnitPrice`，格式设置为货币的返回的值 `Eval("UnitPrice", "{0:C}").`

请花费片刻时间访问你的浏览器中的页面。 如图 2 所示，DataList 将呈现为一个产品中的单列、 多行的表。


[![默认情况下，DataList 将呈现为单个列中，多行表](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image4.png)

**图 2**:默认情况下，DataList 将呈现为单列表，多行表 ([单击此项可查看原尺寸图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image6.png))


## <a name="step-2-changing-the-datalist-s-layout-direction"></a>步骤 2：更改 DataList 的布局方向

默认行为时 DataList 是垂直在单个列中，多行表中，其项进行布局更改此行为可以轻松地通过 DataList s [ `RepeatDirection`属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)。 `RepeatDirection`属性可接受两个可能值之一：`Horizontal`或`Vertical`（默认值）。

通过更改`RepeatDirection`属性从`Vertical`到`Horizontal`，DataList 呈现其记录在单个行中，创建每个数据源项的一列。 为了说明这种效果，DataList 在设计器上单击，然后，从属性窗口中更改`RepeatDirection`属性从`Vertical`到`Horizontal`。 立即时，在设计器调整 DataList 的布局中，创建一个单行、 多列的界面 （参见图 3）。


[![RepeatDirection 属性决定了如何方向 DataList 的项的布局推出](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image7.png)

**图 3**:`RepeatDirection`属性决定了如何列出出将方向 DataList 的项目 ([单击以查看实际尺寸的图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image9.png))


显示较少的数据，单个行时多列的表可能是最大化屏幕空间的理想方法。 但是，对于更大的数据的卷的单个行将需要大量的列，这些项的屏幕上放置关闭状态的向右-无法推送。 图 4 显示了在单行 DataList 中呈现时的产品。 由于有许多产品 (超过 80)，用户必须滚动到右侧以查看有关每个产品的信息远远。


[![对于足够大的数据源，单个列 DataList 需要水平滚动](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image10.png)

**图 4**:对于足够大的数据源，单个列 DataList 将需要水平滚动 ([单击此项可查看原尺寸图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image12.png))


## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>步骤 3：在多列、 多行表中显示数据

若要创建多列、 多行 DataList，我们需要设置[`RepeatColumns`属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx)到要显示的列数。 默认情况下`RepeatColumns`属性设置为 0，这将导致 DataList 要在单个行或列中显示的所有项 (具体取决于值`RepeatDirection`属性)。

对于我们的示例，让我们来显示每个行的三种产品。 因此，设置`RepeatColumns`属性设置为 3。 此更改后，请花费片刻时间浏览器中查看结果。 如图 5 所示，现在是三列中，多行表中列出的产品。


[![每行显示三种产品](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image13.png)

**图 5**:每行显示三种产品 ([单击此项可查看原尺寸图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image15.png))


`RepeatDirection`属性会影响 DataList 中的项的布局方式。图 5 所示的结果`RepeatDirection`属性设置为`Horizontal`。 请注意，从左到右，从上到下布局 Chai、 Chang 和茴香糖浆的前三个产品。 接下来三个产品 （从开始使用 Chef Anton 的 Cajun Seasoning） 出现在下方的前三个行。 更改`RepeatDirection`属性改回`Vertical`，但是，从上到下，这些产品的布局，从左到右，如图 6 所示。


[![在这里，这些产品均列出出垂直](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image16.png)

**图 6**:在这里，这些产品均列出出垂直 ([单击此项可查看原尺寸图像](showing-multiple-records-per-row-with-the-datalist-control-vb/_static/image18.png))


在结果表中显示的行数取决于绑定到 DataList 的总记录数。 确切地说，它的数据源项的总数上限除以的 s`RepeatColumns`属性值。 由于`Products`表目前尚 84 产品，它是被 3 整除，有 28 行。 如果数据源中的项的数目和`RepeatColumns`属性值不是整除，则最后一个行或列将具有空白单元格。 如果`RepeatDirection`设置为`Vertical`，则最后一列将具有空单元格; 如果`RepeatDirection`是`Horizontal`，则最后一行将具有空单元格。

## <a name="summary"></a>总结

DataList，默认情况下，列出了在单个列中，多行表中，模拟使用单一 TemplateField GridView 布局其项目。 可接受此默认布局时，我们可以通过显示每行的多个数据源项来实现屏幕空间最大化。 实现这个目的是只需设置 DataList 的`RepeatColumns`属性设置为要显示每行的列数。 此外，DataList 的`RepeatDirection`属性可以用于指示是否多列、 多行的表的内容应进行布局水平方向从左到右、 从上到下或垂直方向从上到下，从左到右。

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 John Suru。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
> [下一页](nested-data-web-controls-vb.md)

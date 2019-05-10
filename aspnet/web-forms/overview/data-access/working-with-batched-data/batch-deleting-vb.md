---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
title: 删除 (VB) 的批处理 |Microsoft Docs
author: rick-anderson
description: 了解如何删除单个操作中的多个数据库记录。 在用户界面层我们构建在中创建早期 tut 增强 GridView 时...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4fb72f75-32ab-4bf7-a764-be20367be726
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: b9a9b1fb9037a35ea650fdc062abfcaf69999429
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65119550"
---
# <a name="batch-deleting-vb"></a>批量删除 (VB)

通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_VB.zip)或[下载 PDF](batch-deleting-vb/_static/datatutorial65vb1.pdf)

> 了解如何删除单个操作中的多个数据库记录。 在用户界面层我们制作的增强 GridView 中前面的教程中创建。 数据访问层中，我们将以确保所有删除操作成功，或者所有删除操作都将回滚的事务中的多个删除操作。

## <a name="introduction"></a>介绍

[前面的教程](batch-updating-vb.md)探讨了如何创建批处理编辑界面使用完全可编辑的 GridView。 编辑界面一批将在其中用户通常编辑多个记录在一次的情况下，需要回发和键盘鼠标上下文操作远远少于开关，从而提高最终用户的效率。 此技术是同样适用于其中很常见的用户删除一次性许多记录的页面。

已使用的联机电子邮件客户端的任何人已经非常熟悉最常见的批处理删除接口之一： 一个具有对应删除所有选中的项的网格中的每一行中的复选框按钮 （请参见图 1）。 本教程中非常短因为我们已做的所有硬工作在前面的教程中创建基于 web 的界面和要删除的一系列记录作为单个原子操作的方法。 在中[添加 GridView 复选框列](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)教程中，我们创建的列的复选框并在 GridView[包装事务内的数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)教程中，我们创建中的方法将使用事务来删除 BLL`List<T>`的`ProductID`值。 在本教程中，我们将制作的并合并我们以前的体验，以创建工作批删除示例。

[![每个行包含一个复选框](batch-deleting-vb/_static/image1.gif)](batch-deleting-vb/_static/image1.png)

**图 1**:每个行包含一个复选框 ([单击此项可查看原尺寸图像](batch-deleting-vb/_static/image2.png))

## <a name="step-1-creating-the-batch-deleting-interface"></a>步骤 1：创建批处理正在删除接口

由于我们已创建删除接口中的批处理[添加 GridView 复选框列](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)教程中，我们可以只需将其复制到`BatchDelete.aspx`而不是从头开始创建它。 首先打开`BatchDelete.aspx`页中`BatchData`文件夹并`CheckBoxField.aspx`页中`EnhancedGridView`文件夹。 从`CheckBoxField.aspx`页上，请转到源视图并复制之间的标记`<asp:Content>`标记如图 2 中所示。

[![CheckBoxField.aspx 的声明性标记复制到剪贴板](batch-deleting-vb/_static/image2.gif)](batch-deleting-vb/_static/image3.png)

**图 2**:将复制的声明性标记`CheckBoxField.aspx`到剪贴板 ([单击以查看实际尺寸的图像](batch-deleting-vb/_static/image4.png))

接下来，请转到中的源视图`BatchDelete.aspx`并粘贴剪贴板中的内容`<asp:Content>`标记。 再复制和粘贴的代码中的代码隐藏类中`CheckBoxField.aspx.vb`到中的代码隐藏类内`BatchDelete.aspx.vb`(`DeleteSelectedProducts`按钮 s`Click`事件处理程序`ToggleCheckState`方法，和`Click`事件处理程序有关`CheckAll`和`UncheckAll`按钮)。 通过此内容，请在复制后`BatchDelete.aspx`页面 + s 代码隐藏类应包含以下代码：

[!code-vb[Main](batch-deleting-vb/samples/sample1.vb)]

在复制后通过声明性标记和源代码，请花费片刻时间来测试`BatchDelete.aspx`通过查看通过浏览器。 应会看到 GridView 列出每个行，其中列出 s 产品名称、 类别和价格以及一个复选框的 GridView 中的前十个产品。 应该有三个按钮：检查所有，取消选中所有，并删除所选的产品。 单击查看全部按钮可以选择所有复选框，而取消选中所有清除所有复选框。 单击删除所选产品显示一条消息，其中列出了`ProductID`值的所选的产品，但不实际删除产品。

[![从 CheckBoxField.aspx 接口已被移动到 BatchDeleting.aspx](batch-deleting-vb/_static/image3.gif)](batch-deleting-vb/_static/image5.png)

**图 3**:从接口`CheckBoxField.aspx`已移至`BatchDeleting.aspx`([单击以查看实际尺寸的图像](batch-deleting-vb/_static/image6.png))

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>步骤 2：删除选中的产品使用事务

与正在删除已成功复制到的接口的批处理`BatchDeleting.aspx`，则所有剩下是更新代码，以便删除所选产品按钮删除使用的检查的产品`DeleteProductsWithTransaction`中的方法`ProductsBLL`类。 此方法中添加[包装事务内的数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)教程中，接受作为其输入`List(Of T)`的`ProductID`值，并删除每个相应`ProductID`的作用域内事务。

`DeleteSelectedProducts`按钮 s`Click`事件处理程序当前使用以下`For Each`循环来循环访问每个 GridView 行：

[!code-vb[Main](batch-deleting-vb/samples/sample2.vb)]

对于每一行，`ProductSelector`复选框 Web 控件以编程方式引用。 如果选中，行 s`ProductID`从检索`DataKeys`集合并`DeleteResults`标签的`Text`属性更新为包含一个消息，表明为要删除所选行。

上面的代码并不实际与调用删除任何记录`ProductsBLL`类的`Delete`方法已被注释掉。已删除此逻辑应用，该代码将删除产品但不是能在原子操作。 也就是说，如果序列中的第几个删除操作成功，但更高版本 （可能是由于外键约束冲突） 失败，则会引发异常，但已删除这些产品将保持已删除。

为了确保原子性，我们需要改为使用`ProductsBLL`类的`DeleteProductsWithTransaction`方法。 因为此方法接受一系列`ProductID`我们需要首先编译此列表从网格，然后将其作为参数传递值。 我们首先创建的实例`List(Of T)`类型的`Integer`。 内`For Each`我们需要添加所选的产品的循环`ProductID`值与此`List(Of T)`。 循环之后这`List(Of T)`必须将传递给`ProductsBLL`类的`DeleteProductsWithTransaction`方法。 更新`DeleteSelectedProducts`按钮的`Click`事件处理程序使用以下代码：

[!code-vb[Main](batch-deleting-vb/samples/sample3.vb)]

更新的代码创建`List(Of T)`类型的`Integer`(`productIDsToDelete`)，并填充其与`ProductID`要删除的值。 之后`For Each`循环，如果没有选择，至少一个产品`ProductsBLL`类的`DeleteProductsWithTransaction`方法调用并传递此列表。 `DeleteResults`还显示标签和数据重新绑定到 GridView，（以使新已删除的记录不会再显示为网格中的行）。

图 4 显示了 GridView 后的行数已选择要删除。 图 5 显示的屏幕，单击删除所选产品按钮后立即。 请注意，在图 5`ProductID`下面 GridView 的标签中显示的已删除的记录值，这些行不再 GridView。

[![将删除所选的产品](batch-deleting-vb/_static/image4.gif)](batch-deleting-vb/_static/image7.png)

**图 4**:选择产品将被删除 ([单击此项可查看原尺寸图像](batch-deleting-vb/_static/image8.png))

[![删除产品产品 id 值为所列下方的 GridView](batch-deleting-vb/_static/image5.gif)](batch-deleting-vb/_static/image9.png)

**图 5**:删除产品`ProductID`的值为 GridView 下方列出 ([单击以查看实际尺寸的图像](batch-deleting-vb/_static/image10.png))

> [!NOTE]
> 若要测试`DeleteProductsWithTransaction`s 方法原子性，手动添加的产品条目`Order Details`表，然后尝试删除该产品 （以及其他）。 尝试删除与某关联订单的产品，但请注意如何其他所选的产品删除操作都将回滚时，你将收到外键约束冲突。

## <a name="summary"></a>总结

正在删除接口以批处理需要添加 GridView 具有的列的复选框和按钮 Web 控件，当单击时，将删除所有选定的行作为一个原子操作。 在本教程中我们生成此类接口拼凑在两个以前的教程，完成工作[添加 GridView 复选框列](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)并[包装事务内的数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)。 第一个教程中我们创建 GridView 复选框的列和我们在后一种实现 BLL 中的方法，传递时`List(Of T)`的`ProductID`值，已将其删除在事务范围内。

在下一教程中，我们将创建用于执行批处理插入的接口。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton giesenow 为您和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](batch-updating-vb.md)
> [下一页](batch-inserting-vb.md)

---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
title: 处理 BLL 和 DAL 级别的异常 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何巧妙地处理可编辑 DataList 的更新工作流期间引发的异常。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: f8fd58e2-f932-4f08-ab3d-fbf8ff3295d2
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 5714b118a5894731820d8e9775c8f5c8a375856c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59390124"
---
# <a name="handling-bll--and-dal-level-exceptions-c"></a>处理 BLL 和 DAL 级别的异常 (C#)

通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_CS.exe)或[下载 PDF](handling-bll-and-dal-level-exceptions-cs/_static/datatutorial38cs1.pdf)

> 在本教程中，我们将了解如何巧妙地处理可编辑 DataList 的更新工作流期间引发的异常。


## <a name="introduction"></a>介绍

在中[概述的编辑和删除 DataList 中的数据](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)教程中，我们创建了提供简单的编辑和删除功能 DataList。 虽然完全正常运行，它是用户几乎不友好，作为编辑过程中发生任何错误或删除进程导致未经处理的异常。 例如，省略产品的名称或，在编辑某个产品时，输入价格值为非常经济实惠 ！，将引发异常。 在代码中未捕获此异常，因为它冒泡到 ASP.NET 运行，然后在网页中显示异常 s 的详细信息。

中可以看到[处理 BLL-和 DAL 级别 ASP.NET 页面中的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)教程中，如果从业务逻辑或数据访问层的深度中引发的异常的异常详细信息返回到 ObjectDataSource 和然后到 GridView。 我们已了解如何创建适当地处理这些异常`Updated`或`RowUpdated`ObjectDataSource 或 GridView 中后，检查异常，然后，该值指示处理了该异常的事件处理程序。

但是，，我们 DataList 的教程，不用于更新和删除数据使用对象数据源。 相反，我们正在直接对 BLL。 为了检测异常源自 BLL 或 DAL，我们需要实现异常处理代码中我们的 ASP.NET 页面代码隐藏。 在本教程中，我们将了解如何更巧妙地处理在 DataList s 更新工作流的可编辑过程中引发的异常。

> [!NOTE]
> 在中*概述的编辑和删除 DataList 中的数据*教程中我们讨论了用于编辑和删除 DataList 中的数据的不同方法，一些方法涉及使用 ObjectDataSource 用于更新和正在删除。 如果您采用这些技术，你可以处理通过 ObjectDataSource s 从 BLL 或 DAL 的异常`Updated`或`Deleted`事件处理程序。


## <a name="step-1-creating-an-editable-datalist"></a>步骤 1：创建可编辑的 DataList

我们担心如何处理在更新工作流期间发生的异常之前，让我们来首先创建可编辑的 DataList。 打开`ErrorHandling.aspx`页中`EditDeleteDataList`文件夹中，将 DataList 添加到设计器中，设置其`ID`属性设置为`Products`，并添加名为新 ObjectDataSource `ProductsDataSource`。 配置要使用 ObjectDataSource`ProductsBLL`类的`GetProducts()`方法用于选择记录; 在 INSERT、 UPDATE、 设置下拉列表，删除选项卡添加到 （无）。


[![Return 使用 GetProducts() 方法的产品信息](handling-bll-and-dal-level-exceptions-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-cs/_static/image1.png)

**图 1**:返回使用产品信息`GetProducts()`方法 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-cs/_static/image3.png))


完成 ObjectDataSource 向导后，Visual Studio 自动创建`ItemTemplate`的 DataList。 将此替换`ItemTemplate`，显示每个产品的名称和价格，并包括一个编辑按钮。 接下来，创建`EditItemTemplate`与 TextBox Web 控件的名称和价格和更新和取消按钮。 最后，设置 DataList 的`RepeatColumns`属性设置为 2。

更改后，你页面 s 声明性标记应类似于以下。 编辑、 取消，请确保仔细检查和更新按钮都有其`CommandName`属性设置为编辑，取消，并分别更新。


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample1.aspx)]

> [!NOTE]
> 本教程中 DataList 必须启用 s 视图状态。


花点时间查看我们通过浏览器的进度 （见图 2）。


[![E支票产品包括一个编辑按钮](handling-bll-and-dal-level-exceptions-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-cs/_static/image4.png)

**图 2**:每个产品包含一个编辑按钮 ([单击此项可查看原尺寸图像](handling-bll-and-dal-level-exceptions-cs/_static/image6.png))


目前，编辑按钮仅会导致回发它不是 t 尚未使产品可编辑。 若要启用编辑，我们需要创建的事件处理程序 DataList s `EditCommand`， `CancelCommand`，和`UpdateCommand`事件。 `EditCommand`并`CancelCommand`事件只需更新 DataList 的`EditItemIndex`属性和重新绑定到 DataList 数据：


[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample2.cs)]

`UpdateCommand`稍微要复杂事件处理程序。 它需要读取已编辑产品 s`ProductID`从`DataKeys`以及产品的名称和价格中的文本框集合`EditItemTemplate`，然后调用`ProductsBLL`类的`UpdateProduct`方法，然后再返回 DataList为其预编辑状态。

现在，让 s 只需使用完全相同的代码从`UpdateCommand`中的事件处理程序*概述的编辑和删除 DataList 中的数据*教程。 我们将添加代码来妥善处理步骤 2 中的异常。


[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample3.cs)]

在遇到无效的输入时可以是格式不正确的单价、 类似-$5.00，非法的单位价格值或省略，将引发异常的产品 s 名称的窗体中。 由于`UpdateCommand`事件处理程序不包括在此时处理代码的任何异常，异常将归因于 ASP.NET 运行时，其中它将显示给最终用户 （请参见图 3）。


![未经处理的异常时，最终用户会看到一个错误页面](handling-bll-and-dal-level-exceptions-cs/_static/image7.png)

**图 3**:未经处理的异常时，最终用户会看到一个错误页面


## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>步骤 2：适当地处理 UpdateCommand 事件处理程序中的异常

在更新工作流，可能会发生异常中`UpdateCommand`事件处理程序、 BLL 或将 DAL。 例如，如果用户输入过的价格昂贵，`Decimal.Parse`中的语句`UpdateCommand`事件处理程序将引发`FormatException`异常。 如果用户省略产品的名称或价格具有负数值，DAL 将引发异常。

异常发生时，我们想要显示在页面内的信息性消息。 添加标签 Web 页面控件`ID`设置为`ExceptionDetails`。 配置要显示为红色，特别大，通过将分配的粗体和斜体字体的标签的文本及其`CssClass`属性设置为`Warning`中定义的 CSS 类`Styles.css`文件。

出现错误时，我们只想要一次显示的标签。 也就是说，在后续回发，标签的警告消息应会消失。 这可以通过任一清除标签 s`Text`属性或设置其`Visible`属性设置为`False`中`Page_Load`事件处理程序 (正如我们做返回[处理 BLL-和 DAL 级别在 ASP 中的异常.NET 页](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)教程) 或通过禁用标签的视图状态支持。 让我们来使用后一种选择。


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample4.aspx)]

当引发异常时，我们会将分配到的异常的详细信息`ExceptionDetails`标签控件的`Text`属性。 由于其视图状态禁用的可以在后续回发`Text`属性 s 以编程方式更改都将丢失，恢复为默认文本 （空字符串），从而隐藏警告消息。

若要确定在已以在页面上显示帮助消息引发错误时，我们需要添加`Try ... Catch`阻止对`UpdateCommand`事件处理程序。 `Try`部分包含代码，这可能导致异常，尽管`Catch`块包含在遇到异常时执行的代码。 请查看[异常处理基础知识](https://msdn.microsoft.com/library/2w8f0bss.aspx)主题中的详细信息的.NET Framework 文档上`Try ... Catch`块。


[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample5.cs)]

通过中的代码引发任何类型的异常`Try`块中，`Catch`块的代码将开始执行。 引发异常的类型`DbException`， `NoNullAllowedException`， `ArgumentException`，并在依赖于什么，确实如此，第一个位置中引发错误。 如果在数据库级别的那里的问题`DbException`将引发。 如果输入值非法`UnitPrice`， `UnitsInStock`， `UnitsOnOrder`，或`ReorderLevel`字段，`ArgumentException`将引发，随着我们添加代码以验证在这些字段值`ProductsDataTable`类 (请参阅[创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md)教程)。

我们可以通过基于捕获到异常的类型的消息文本对最终用户提供的更多有用的说明。 下面的代码几乎完全相同的窗体中使用该回到[处理 BLL-和 DAL 级别 ASP.NET 页面中的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)教程提供了此级别的详细信息：


[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample6.cs)]

若要完成本教程，只需调用`DisplayExceptionDetails`方法从`Catch`块中已捕获传递`Exception`实例 (`ex`)。

使用`Try ... Catch`就地块中，用户信息更丰富的错误消息，显示为数字 4 和 5 的显示。 请注意，在遇到异常 DataList 时将保留在编辑模式。 这是因为一旦发生异常时，控制流将立即重定向到`Catch`块，从而绕过 DataList 返回其预先编辑状态代码。


[![A如果用户省略了必需的字段，显示 n 个错误消息](handling-bll-and-dal-level-exceptions-cs/_static/image9.png)](handling-bll-and-dal-level-exceptions-cs/_static/image8.png)

**图 4**:如果用户省略了必需的字段显示一条错误消息 ([单击此项可查看原尺寸图像](handling-bll-and-dal-level-exceptions-cs/_static/image10.png))


[![An 错误消息是显示时输入负价格](handling-bll-and-dal-level-exceptions-cs/_static/image12.png)](handling-bll-and-dal-level-exceptions-cs/_static/image11.png)

**图 5**:一条错误消息是显示时输入负价格 ([单击此项可查看原尺寸图像](handling-bll-and-dal-level-exceptions-cs/_static/image13.png))


## <a name="summary"></a>总结

GridView 和对象数据源提供了后续级别事件处理程序，包括任何更新和删除工作流期间引发的异常以及属性，可设置为指示已被异常有关的信息处理。 这些功能，但是，将不可用时使用 DataList 和直接使用 BLL。 相反，我们需负责实现异常处理。

在本教程中我们已了解如何向更新工作流通过添加一个可编辑 DataList s 添加异常处理`Try ... Catch`阻止对`UpdateCommand`事件处理程序。 如果在更新工作流，会引发的异常`Catch`块的代码执行时，显示中的有用信息`ExceptionDetails`标签。

此时，DataList 也不会尝试防止从第一个位置中发生的异常。 即使我们知道，负价格会导致异常，我们尚未尚未添加任何功能来主动防止用户输入此类输入无效。 在我们的下一教程，我们将了解如何帮助减少无效用户输入引起添加验证控件中的异常`EditItemTemplate`。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [异常设计准则](https://msdn.microsoft.com/library/ms298399.aspx)
- [错误日志记录模块和处理程序 (ELMAH)](http://workspaces.gotdotnet.com/elmah) （用于记录错误的开放源代码库）
- [Enterprise Library 的.NET Framework 2.0](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) （包括异常管理应用程序块）

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Ken Pespisa。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](performing-batch-updates-cs.md)
> [下一页](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)

---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: 跨两个页面 (VB) 筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将使用 GridView，若要列出数据库中的供应商实现此模式。 在 GridView 中的每个供应商一行将包含 Vie...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 6903c8c0649f9e4d56962bd36e03448852cfb81a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59395350"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>跨两个页面的母版/详细信息筛选 (VB)

通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe)或[下载 PDF](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> 在本教程中我们将使用 GridView，若要列出数据库中的供应商实现此模式。 在 GridView 中的每个供应商行将包含查看产品链接，当单击时，会将用户转到单独的页面，它为所选的供应商列出的那些产品。


## <a name="introduction"></a>介绍

我们已在前面的两个教程了解如何在单个网页上使用 Dropdownlist 以显示"主"的记录显示母版/详细信息报表和一个[GridView](master-detail-filtering-with-a-dropdownlist-vb.md)或[DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md)控件来显示"详细信息。" 用于主/详细信息报表的另一种常见模式是具有上一个 web 页面，显示在另一台的详细信息的主记录。 论坛网站，例如[ASP.NET 论坛](https://forums.asp.net/)，是此模式在实践中的一个极好示例。 ASP.NET 论坛由各种论坛入门，Web 窗体数据的演示文稿控件组成，依此类推。 每个线程组成的文章数和每个论坛组成的多个线程。 ASP.NET 论坛主页上列出了论坛。 在论坛上单击 whisks 到`ShowForum.aspx`页上，列出该论坛的线程。 同样，单击在线程上转到`ShowPost.aspx`，后者将显示线程被单击的文章。

在本教程中我们将使用 GridView，若要列出数据库中的供应商实现此模式。 在 GridView 中的每个供应商行将包含查看产品链接，当单击时，会将用户转到单独的页面，它为所选的供应商列出的那些产品。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>步骤 1：添加`SupplierListMaster.aspx`并`ProductsForSupplierDetails.aspx`到页`Filtering`文件夹

在第三个教程中定义页面布局时我们添加了大量中的"起始"页`BasicReporting`， `Filtering`，和`CustomFormatting`文件夹。 但是，我们没有添加起始页为本教程在该时间，请花片刻时间添加到两个新页面`Filtering`文件夹：`SupplierListMaster.aspx`和`ProductsForSupplierDetails.aspx`。 `SupplierListMaster.aspx` 将列出时的"主"记录 （供应商）`ProductsForSupplierDetails.aspx`将显示所选的供应商的产品。

当创建这些两个新页一定要将其与相关联`Site.master`母版页。


![将 SupplierListMaster.aspx 和 ProductsForSupplierDetails.aspx 页添加到筛选的文件夹](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**图 1**:添加`SupplierListMaster.aspx`并`ProductsForSupplierDetails.aspx`到页`Filtering`文件夹


此外，当向项目添加新页面，请务必更新站点地图文件， `Web.sitemap`，相应地。 本教程只需添加`SupplierListMaster.aspx`页可以使用以下 XML 内容作为筛选报表的子站点地图`<siteMapNode>`元素：


[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> 可帮助自动执行更新的站点映射文件时添加新的 ASP.NET 页使用的过程[K.Scott Allen](http://odetocode.com/Blogs/scott/)Visual Studio 的免费[站点映射宏](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)。


## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>步骤 2：显示供应商列表中`SupplierListMaster.aspx`

与`SupplierListMaster.aspx`并`ProductsForSupplierDetails.aspx`创建的页面下, 一步是创建中的供应商提供的 GridView `SupplierListMaster.aspx`。 向页添加 GridView 并将其绑定到新对象数据源。 应使用此 ObjectDataSource`SuppliersBLL`类的`GetSuppliers()`方法以返回所有供应商。


[![S选择 SuppliersBLL 类](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**图 2**:选择`SuppliersBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image4.png))


[![C配置对象数据源使用 GetSuppliers() 方法](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**图 3**:配置为使用 ObjectDataSource`GetSuppliers()`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image7.png))


我们需要包含一个链接，标题为查看产品每 GridView 行中，单击，以便用户可以`ProductsForSupplierDetails.aspx`在所选行中传递`SupplierID`通过在查询字符串值。 例如，如果用户单击为全供应商查看产品链接 (其中包含`SupplierID`值为 4)，应将发送到`ProductsForSupplierDetails.aspx?SupplierID=4`。

若要完成此操作，添加[HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx)到 GridView，从而将超链接添加到每个 GridView 行。 通过单击 GridView 的智能标记中的编辑列链接启动。 接下来，从左上角中的列表中选择 HyperLinkField 并单击添加包括 HyperLinkField GridView 的字段列表中。


[![Add 到 GridView HyperLinkField](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**图 4**:添加到 GridView HyperLinkField ([单击此项可查看原尺寸图像](master-detail-filtering-across-two-pages-vb/_static/image10.png))


HyperLinkField 可以配置为使用相同的文本或 URL 值中每个 GridView 行的链接，也可以将这些值基于绑定到每个特定行的数据值。 若要指定静态值所有行使用 HyperLinkField`Text`或`NavigateUrl`属性。 由于我们想要的所有行是相同的链接文本，设置 HyperLinkField`Text`查看产品的属性。


[![Set HyperLinkField 的文本属性设置为查看产品](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**图 5**:设置 HyperLinkField`Text`属性设置为查看产品 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image13.png))


若要设置的文本或 URL 值，以基于基础数据绑定到 GridView 行上，指定数据字段文本或应从在请求 URL 的值`DataTextField`或`DataNavigateUrlFields`属性。 `DataTextField` 仅可设置为单个数据字段;`DataNavigateUrlFields`，但是，可以设置为数据字段的逗号分隔列表。 我们经常需要基于文本或 URL 上的当前行的数据字段值和一些静态标记的组合。 在本教程中，例如，我们希望 HyperLinkField 的链接的 URL 为`ProductsForSupplierDetails.aspx?SupplierID=supplierID`，其中 *`supplierID`* 是每个 GridView 行`SupplierID`值。 请注意，我们需要这两个静态和数据驱动的以下值：`ProductsForSupplierDetails.aspx?SupplierID=`链接的 URL 的部分是静态的而 *`supplierID`* 部分是数据驱动由于其值是每个行自己的`SupplierID`值。

若要指示静态的和数据驱动的值的组合，请使用`DataTextFormatString`和`DataNavigateUrlFormatString`属性。 根据需要则这些属性中输入静态标记，然后使用标记`{0}`想中指定的字段的值`DataTextField`或`DataNavigateUrlFields`属性才会显示。 如果`DataNavigateUrlFields`属性具有多个字段指定的使用`{0}`您期望第一个字段值插入，`{1}`第二个字段值，等等。

我们将此应用到我们的教程，需要设置`DataNavigateUrlFields`属性设置为`SupplierID`，因为它是我们需要在每个行模式中，自定义其值的数据字段和`DataNavigateUrlFormatString`属性设置为`ProductsForSupplierDetails.aspx?SupplierID={0}`。


[![C配置包含正确链接 URL 基于后 SupplierID HyperLinkField](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**图 6**:配置 HyperLinkField 包括正确链接 URL 基于后`SupplierID`([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image16.png))


添加后 HyperLinkField，任意自定义和重新排列 GridView 的字段。 以下标记显示 GridView 后所做的一些最小字段级别自定义。


[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

花点时间查看`SupplierListMaster.aspx`通过浏览器的页。 如图 7 所示，页当前列出所有供应商包括查看产品链接。 单击查看产品链接将转到`ProductsForSupplierDetails.aspx`，并传递供应商的沿`SupplierID`在查询字符串中。


[![E支票供应商行包含视图的产品链接](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**图 7**:每个供应商行包含视图的产品链接 ([单击此项可查看原尺寸图像](master-detail-filtering-across-two-pages-vb/_static/image19.png))


## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>步骤 3：列出了所有供应商的产品中`ProductsForSupplierDetails.aspx`

此时`SupplierListMaster.aspx`页发送到用户`ProductsForSupplierDetails.aspx`，并传递所选供应商的`SupplierID`在查询字符串中。 本教程的最后一步是在 GridView 中显示的产品`ProductsForSupplierDetails.aspx`其`SupplierID`等于`SupplierID`通过在查询字符串中传递。 若要完成本教程通过添加到 GridView`ProductsForSupplierDetails.aspx`页上，使用名为的新对象数据源控件`ProductsBySupplierDataSource`，它调用`GetProductsBySupplierID(supplierID)`方法从`ProductsBLL`类。


[![Add 新对象数据源名为 ProductsBySupplierDataSource](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**图 8**:添加新对象数据源名为`ProductsBySupplierDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image22.png))


[![S选择 ProductsBLL 类](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**图 9**:选择`ProductsBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image25.png))


[![Have ObjectDataSource Invoke GetProductsBySupplierID(supplierID) 方法](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**图 10**:具有 ObjectDataSource 调用`GetProductsBySupplierID(supplierID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image28.png))


配置数据源向导的最后一步会要求我们提供的源`GetProductsBySupplierID(supplierID)`方法的 *`supplierID`* 参数。 若要使用的查询字符串值，设置参数源为查询字符串，并输入要在 QueryStringField 文本框中使用的查询字符串值的名称 (`SupplierID`)。


[![Populate supplierID SupplierID 查询字符串值的参数值](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**图 11**:填充*`supplierID`* 参数值从`SupplierID`查询字符串值 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image31.png))


就这么简单！ 图 12 显示了`ProductsForSupplierDetails.aspx`页上通过单击为全链接进行访问时`SupplierListMaster.aspx`。


[![T他为全由提供的产品显示](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**图 12**:通过为全产品提供显示 ([单击此项可查看原尺寸图像](master-detail-filtering-across-two-pages-vb/_static/image34.png))


## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>显示中的供应商信息`ProductsForSupplierDetails.aspx`

如图 12 所示，`ProductsForSupplierDetails.aspx`页仅列出了由提供的产品`SupplierID`在查询字符串中指定。 人直接发送到此页上，但是，将不知道的图 12 显示为全产品。 若要纠正此我们可以在此页还显示供应商信息。

首先，通过添加上面的产品 GridView FormView。 创建一个名为的新对象数据源控件`SuppliersDataSource`，它调用`SuppliersBLL`类的`GetSupplierBySupplierID(supplierID)`方法。


[![S选择 SuppliersBLL 类](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**图 13**:选择`SuppliersBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image37.png))


[![Have ObjectDataSource Invoke GetSupplierBySupplierID(supplierID) 方法](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**图 14**:具有 ObjectDataSource 调用`GetSupplierBySupplierID(supplierID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image40.png))


如同`ProductsBySupplierDataSource`，具有 *`supplierID`* 参数分配的值`SupplierID`查询字符串值。


[![Populate supplierID SupplierID 查询字符串值的参数值](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**图 15**:填充*`supplierID`* 参数值从`SupplierID`查询字符串值 ([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image43.png))


在绑定到设计视图中的 ObjectDataSource FormView，Visual Studio 会自动创建 FormView `ItemTemplate`， `InsertItemTemplate`，和`EditItemTemplate`与每个返回的数据字段的标签和文本框 Web 控件对象数据源。 由于我们只想显示供应商的信息，可随时删除`InsertItemTemplate`和`EditItemTemplate`。 接下来，编辑 ItemTemplate，使其显示在供应商的公司名称`<h3>`元素的地址、 城市、 国家/地区和公司名称下的电话号码。 或者，可以手动设置 FormView 的`DataSourceID`并创建`ItemTemplate`标记中，正如我们做回到"[显示的数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)"教程。

以后这些编辑 FormView 的声明性标记看起来应类似于下面：


[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

图 16 所示的屏幕截图`ProductsForSupplierDetails.aspx`页后包含了上面详细说明的供应商信息。


[![T他的产品列表包含摘要有关供应商](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**图 16**:产品的列表包括摘要有关供应商 ([单击此项可查看原尺寸图像](master-detail-filtering-across-two-pages-vb/_static/image46.png))


## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>有关应用最后一个涉及`ProductsForSupplierDetails.aspx`UI

以提高用户体验有此报表是添加一些内容，因此应该对进行`ProductsForSupplierDetails.aspx`页。 当前用户可以转化的唯一方法`ProductsForSupplierDetails.aspx`页回发至供应商提供的列表是单击其浏览器的后退按钮。 让我们添加到超链接控件`ProductsForSupplierDetails.aspx`链接回页`SupplierListMaster.aspx`，提供另一种方法为用户返回到主列表。


[![Add 超链接控件以使用户返回到 SupplierListMaster.aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**图 17**:添加超链接控件以将用户返回到`SupplierListMaster.aspx`([单击以查看实际尺寸的图像](master-detail-filtering-across-two-pages-vb/_static/image49.png))


如果用户不具有任何产品的供应商提供的查看产品链接上单击`ProductsBySupplierDataSource`中的 ObjectDataSource`ProductsForSupplierDetails.aspx`不会返回任何结果。 GridView 绑定到对象数据源不会呈现任何标记，从而导致用户的浏览器中的页上的空白区域。 若要更清楚地告知用户是否存在任何与所选的供应商关联的产品，我们可以设置 GridView 的`EmptyDataText`属性设置为这种情况出现时，我们希望显示的消息。 我设置此属性设置为"没有此供应商提供的产品"

默认情况下，罗斯文数据库中的所有供应商提供至少一个产品。 但是，本教程中我手动修改`Products`表，以便供应商 Escargots Nouveaux 不再与任何产品相关联。 图 18 显示了详细信息页 Escargots Nouveaux 在后进行此更改。


[![U供应商不提供任何产品通知 ser](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**图 18**:供应商不提供任何产品通知用户 ([单击此项可查看原尺寸图像](master-detail-filtering-across-two-pages-vb/_static/image52.png))


## <a name="summary"></a>总结

虽然母版/详细信息报告可以在单个页面上显示母版和详细信息记录，很多网站在它们之间用在两个 web 页面。 在本教程中我们介绍了如何通过将"主"网页中的 GridView 中列出的供应商和"详细信息"页中列出的关联的产品实现此类母版/详细信息报告。 主网页中的每个供应商行包含一个指向传递的行的详细信息页`SupplierID`值。 可以使用 GridView 的 HyperLinkField 轻松地添加此类特定于行的链接。

在详细信息页中指定的供应商检索这些产品通过调用完成`ProductsBLL`类的`GetProductsBySupplierID(supplierID)`方法。 *`supplierID`* 以声明方式使用查询字符串作为参数源指定参数值。 我们还了解了如何使用 FormView 的详细信息页中显示的供应商的详细信息。

我们[下一教程](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)是最后一个母版/详细信息报告。 我们将介绍如何在其中的每一行都有一个选择按钮 GridView 中显示的产品的列表。 单击选择按钮将在同一页上的 DetailsView 控件中显示该产品的详细信息。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-two-dropdownlists-vb.md)
> [下一页](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)

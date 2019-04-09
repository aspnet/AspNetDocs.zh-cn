---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: 使用 DataList 和 Repeater 控件 (VB) 显示数据 |Microsoft Docs
author: rick-anderson
description: 在前面的教程中我们使用了 GridView 控件以显示数据。 开始本教程中，我们看一下生成使用的常见报告模式...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e275b552af1348da48937e26012f7625a2bb3b93
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59383887"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a><span data-ttu-id="4bd9c-104">使用 DataList 和 Repeater 控件显示数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-104">Displaying Data with the DataList and Repeater Controls (VB)</span></span>

<span data-ttu-id="4bd9c-105">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="4bd9c-106">[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe)或[下载 PDF](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-106">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe) or [Download PDF](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)</span></span>

> <span data-ttu-id="4bd9c-107">在前面的教程中我们使用了 GridView 控件以显示数据。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-107">In the preceding tutorials we have used the GridView control to display data.</span></span> <span data-ttu-id="4bd9c-108">开始本教程中，我们介绍构建使用 DataList 和 Repeater 控件的常见报告模式从开始使用这些控件显示数据的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-108">Starting with this tutorial, we look at building common reporting patterns with the DataList and Repeater controls, starting with the basics of displaying data with these controls.</span></span>


## <a name="introduction"></a><span data-ttu-id="4bd9c-109">介绍</span><span class="sxs-lookup"><span data-stu-id="4bd9c-109">Introduction</span></span>

<span data-ttu-id="4bd9c-110">在过去的所有示例中的所有 28 教程中，如果我们需要显示我们转向了 GridView 控件的数据源的多个记录。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-110">In all of the examples throughout the past 28 tutorials, if we needed to display multiple records from a data source we turned to the GridView control.</span></span> <span data-ttu-id="4bd9c-111">GridView 呈现在列中显示的记录的数据字段的数据源中的每个记录的行。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-111">The GridView renders a row for each record in the data source, displaying the record s data fields in columns.</span></span> <span data-ttu-id="4bd9c-112">虽然 GridView 可以显示、 分页、 排序、 编辑和删除数据的管理单元，其外观是有点 boxy。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-112">While the GridView makes it a snap to display, page through, sort, edit, and delete data, its appearance is a bit boxy.</span></span> <span data-ttu-id="4bd9c-113">此外，标记负责 GridView 的结构是固定包括对应的 HTML`<table>`与表行 (`<tr>`) 的每个记录和表格单元格 (`<td>`) 的每个字段。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-113">Moreover, the markup responsible for the GridView s structure is fixed it includes an HTML `<table>` with a table row (`<tr>`) for each record and a table cell (`<td>`) for each field.</span></span>

<span data-ttu-id="4bd9c-114">若要提供更高的外观和呈现的标记中的自定义显示多个记录时，ASP.NET 2.0，提供了 DataList 和 Repeater 控件 (这两种也已推出 ASP.NET 版本 1.x)。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-114">To provide a greater degree of customization in the appearance and rendered markup when displaying multiple records, ASP.NET 2.0 offers the DataList and Repeater controls (both of which were also available in ASP.NET version 1.x).</span></span> <span data-ttu-id="4bd9c-115">DataList 和 Repeater 控件呈现其内容使用模板而不是不是 BoundFields，CheckBoxFields，ButtonFields，等等。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-115">The DataList and Repeater controls render their content using templates rather than BoundFields, CheckBoxFields, ButtonFields, and so on.</span></span> <span data-ttu-id="4bd9c-116">如 GridView，DataList 呈现为 HTML `<table>`，但允许多个数据源记录要显示每个行。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-116">Like the GridView, the DataList renders as an HTML `<table>`, but allows for multiple data source records to be displayed per table row.</span></span> <span data-ttu-id="4bd9c-117">Repeater，另一方面，呈现任何其他标记，而不仅仅什么显式指定，并在需要精确控制发出的标记时使用的理想候选项。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-117">The Repeater, on the other hand, renders no additional markup than what you explicitly specify, and is an ideal candidate when you need precise control over the markup emitted.</span></span>

<span data-ttu-id="4bd9c-118">通过接下来几十教程中，我们将介绍在构建使用 DataList 和 Repeater 控件的常见报告模式开始显示与这些控件模板的数据的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-118">Over the next dozen or so tutorials, we'll look at building common reporting patterns with the DataList and Repeater controls, starting with the basics of displaying data with these controls templates.</span></span> <span data-ttu-id="4bd9c-119">我们将了解如何设置这些控件的格式如何更改数据源中的记录 DataList、 常见的母版/详细信息方案、 方式编辑和删除数据，布局如何通过记录页上，依次类推。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-119">We'll see how to format these controls, how to alter the layout of data source records in the DataList, common master/details scenarios, ways to edit and delete data, how to page through records, and so on.</span></span>

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a><span data-ttu-id="4bd9c-120">步骤 1：添加 DataList 和 Repeater 教程 Web 页</span><span class="sxs-lookup"><span data-stu-id="4bd9c-120">Step 1: Adding the DataList and Repeater Tutorial Web Pages</span></span>

<span data-ttu-id="4bd9c-121">在开始本教程之前，让我们来首先请花费片刻时间，将 ASP.NET 页面，我们需要为本教程，并显示使用 DataList 和 Repeater 的数据处理的下一步的几个教程。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-121">Before we start this tutorial, let s first take a moment to add the ASP.NET pages we'll need for this tutorial and the next few tutorials dealing with displaying data using the DataList and Repeater.</span></span> <span data-ttu-id="4bd9c-122">首先，创建一个新的文件夹在项目中名为`DataListRepeaterBasics`。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-122">Start by creating a new folder in the project named `DataListRepeaterBasics`.</span></span> <span data-ttu-id="4bd9c-123">接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:</span><span class="sxs-lookup"><span data-stu-id="4bd9c-123">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`


![创建 DataListRepeaterBasics 文件夹并添加教程 ASP.NET 页面](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

<span data-ttu-id="4bd9c-125">**图 1**:创建`DataListRepeaterBasics`文件夹并添加教程 ASP.NET 页面</span><span class="sxs-lookup"><span data-stu-id="4bd9c-125">**Figure 1**: Create a `DataListRepeaterBasics` Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="4bd9c-126">打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-126">Open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="4bd9c-127">此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并从项目符号列表中的当前部分显示这些教程。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-127">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial, enumerates the site map and displays the tutorials from the current section in a bulleted list.</span></span>


[![A<span data-ttu-id="4bd9c-128">dd SectionLevelTutorialListing.ascx 用户控件到 Default.aspx]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-128">dd the SectionLevelTutorialListing.ascx User Control to Default.aspx]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

<span data-ttu-id="4bd9c-129">**图 2**:添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-129">**Figure 2**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))</span></span>


<span data-ttu-id="4bd9c-130">为了使项目符号列表显示 DataList 和 Repeater 教程中我们将创建，我们需要将它们添加到的站点映射。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-130">In order to have the bulleted list display the DataList and Repeater tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="4bd9c-131">打开`Web.sitemap`文件，并添加自定义按钮站点映射节点标记后添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-131">Open the `Web.sitemap` file and add the following markup after the Adding Custom Buttons site map node markup:</span></span>


[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

<span data-ttu-id="4bd9c-133">**图 3**:更新包括新的 ASP.NET 页面的站点图</span><span class="sxs-lookup"><span data-stu-id="4bd9c-133">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-product-information-with-the-datalist"></a><span data-ttu-id="4bd9c-134">步骤 2：使用 DataList 显示产品信息</span><span class="sxs-lookup"><span data-stu-id="4bd9c-134">Step 2: Displaying Product Information with the DataList</span></span>

<span data-ttu-id="4bd9c-135">类似于 FormView，DataList 控件 s 呈现的输出取决于模板而不是 BoundFields、 CheckBoxFields，等等。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-135">Similar to the FormView, the DataList control s rendered output depends upon templates rather than BoundFields, CheckBoxFields, and so on.</span></span> <span data-ttu-id="4bd9c-136">与 FormView 不同 DataList 旨在显示记录而不是一个孤立的一组。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-136">Unlike the FormView, the DataList is designed to display a set of records rather than a solitary one.</span></span> <span data-ttu-id="4bd9c-137">让我们来开始学习本教程介绍将产品信息绑定到 DataList。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-137">Let s begin this tutorial with a look at binding product information to a DataList.</span></span> <span data-ttu-id="4bd9c-138">首先打开`Basics.aspx`页中`DataListRepeaterBasics`文件夹。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-138">Start by opening the `Basics.aspx` page in the `DataListRepeaterBasics` folder.</span></span> <span data-ttu-id="4bd9c-139">接下来，将从工具箱拖到设计器的 DataList。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-139">Next, drag a DataList from the Toolbox onto the Designer.</span></span> <span data-ttu-id="4bd9c-140">如图 4 所示之前指定 DataList 的模板，, 在设计器会将其显示为灰色框。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-140">As Figure 4 illustrates, before specifying the DataList s templates, the Designer displays it as a gray box.</span></span>


[![D<span data-ttu-id="4bd9c-141">rag DataList 从工具箱拖到设计器]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-141">rag the DataList From the Toolbox Onto the Designer]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

<span data-ttu-id="4bd9c-142">**图 4**:拖动 DataList 从工具箱拖到设计器 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-142">**Figure 4**: Drag the DataList From the Toolbox Onto the Designer ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))</span></span>


<span data-ttu-id="4bd9c-143">DataList s 从智能标记，添加新对象数据源并将其配置为使用`ProductsBLL`类的`GetProducts`方法。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-143">From the DataList s smart tag, add a new ObjectDataSource and configure it to use the `ProductsBLL` class s `GetProducts` method.</span></span> <span data-ttu-id="4bd9c-144">由于我们在本教程中创建只读 DataList 重新设置为 （无） 下拉列表中的向导的插入，更新和删除选项卡。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-144">Since we re creating a read-only DataList in this tutorial, set the drop-down list to (None) in the wizard s INSERT, UPDATE, and DELETE tabs.</span></span>


[![O<span data-ttu-id="4bd9c-145">若要创建新对象数据源的 pt]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-145">pt to Create a New ObjectDataSource]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

<span data-ttu-id="4bd9c-146">**图 5**:选择创建新对象数据源 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-146">**Figure 5**: Opt to Create a New ObjectDataSource ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))</span></span>


[![C<span data-ttu-id="4bd9c-147">配置对象数据源以使用 ProductsBLL 类]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-147">onfigure the ObjectDataSource to Use the ProductsBLL Class]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

<span data-ttu-id="4bd9c-148">**图 6**:配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-148">**Figure 6**: Configure the ObjectDataSource to Use the `ProductsBLL` Class ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))</span></span>


[![R<span data-ttu-id="4bd9c-149">etrieve 信息有关所有使用 GetProducts 方法的产品的]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-149">etrieve Information About All of the Products Using the GetProducts Method]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

<span data-ttu-id="4bd9c-150">**图 7**:检索信息有关所有的产品使用`GetProducts`方法 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-150">**Figure 7**: Retrieve Information About All of the Products Using the `GetProducts` Method ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))</span></span>


<span data-ttu-id="4bd9c-151">配置对象数据源并将其与 DataList 通过其智能标记关联之后, Visual Studio 自动创建`ItemTemplate`DataList 的显示名称和值的数据源返回每个数据字段中 (请参阅下面的标记）。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-151">After configuring the ObjectDataSource and associating it with the DataList through its smart tag, Visual Studio will automatically create an `ItemTemplate` in the DataList that displays the name and value of each data field returned by the data source (see the markup below).</span></span> <span data-ttu-id="4bd9c-152">此默认`ItemTemplate`的外观等同于将数据源绑定到 FormView 通过设计器时自动创建的模板。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-152">This default `ItemTemplate` s appearance is identical to that of the templates automatically created when binding a data source to the FormView through the Designer.</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> <span data-ttu-id="4bd9c-153">回想一下，在将数据源绑定到 FormView 控件通过 FormView s 智能标记，Visual Studio 创建`ItemTemplate`， `InsertItemTemplate`，和`EditItemTemplate`。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-153">Recall that when binding a data source to a FormView control through the FormView s smart tag, Visual Studio created an `ItemTemplate`, `InsertItemTemplate`, and `EditItemTemplate`.</span></span> <span data-ttu-id="4bd9c-154">使用 DataList，但是，仅`ItemTemplate`创建。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-154">With the DataList, however, only an `ItemTemplate` is created.</span></span> <span data-ttu-id="4bd9c-155">这是因为 DataList 不具有相同的内置编辑和插入 FormView 提供支持。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-155">This is because the DataList does not have the same built-in editing and inserting support offered by the FormView.</span></span> <span data-ttu-id="4bd9c-156">DataList 中确实包含编辑和删除相关的事件，且编辑和删除支持可以通过添加少量的代码，但有 s 简单开箱不支持任何作为 FormView。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-156">The DataList does contain edit- and delete-related events, and editing and deleting support can be added with a bit of code, but there s no simple out-of-the-box support as with the FormView.</span></span> <span data-ttu-id="4bd9c-157">我们将了解如何为包含编辑和在以后的教程中使用 DataList 删除支持。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-157">We'll see how to include editing and deleting support with the DataList in a future tutorial.</span></span>


<span data-ttu-id="4bd9c-158">允许 s 请花费片刻时间来提高此模板的外观。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-158">Let s take a moment to improve the appearance of this template.</span></span> <span data-ttu-id="4bd9c-159">而不是显示的所有数据字段，让我们来仅显示产品名称、 供应商、 类别、 每个计价单位和单价数量。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-159">Rather than displaying all of the data fields, let s only display the product s name, supplier, category, quantity per unit, and unit price.</span></span> <span data-ttu-id="4bd9c-160">此外，let s 显示中的名称`<h4>`标题并使用剩余的字段布局`<table>`标题的下面。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-160">Moreover, let s display the name in an `<h4>` heading and lay out the remaining fields using a `<table>` beneath the heading.</span></span>

<span data-ttu-id="4bd9c-161">若要进行这些更改可以是使用模板编辑 DataList s 智能标记单击编辑模板链接，或者可以修改模板页 s 声明性语法通过手动从设计器中的功能。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-161">To make these changes you can either use the template editing features in the Designer from the DataList s smart tag click on the Edit Templates link or you can modify the template manually through the page s declarative syntax.</span></span> <span data-ttu-id="4bd9c-162">如果在设计器中使用编辑模板选项，您生成的标记可能不以下标记完全匹配，但通过查看时浏览器应看起来非常类似于屏幕截图中图 8 所示。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-162">If you use the Edit Templates option in the Designer, your resulting markup may not match the following markup exactly, but when viewed through a browser should look very similar to the screen shot shown in Figure 8.</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> <span data-ttu-id="4bd9c-163">上面的示例使用标签 Web 控制其`Text`属性分配数据绑定语法的值。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-163">The example above uses Label Web controls whose `Text` property is assigned the value of the databinding syntax.</span></span> <span data-ttu-id="4bd9c-164">或者，可以省略了标签，只是数据绑定语法中键入。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-164">Alternatively, we could have omitted the Labels altogether, typing in just the databinding syntax.</span></span> <span data-ttu-id="4bd9c-165">也就是说，而不是使用`<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />`我们也可以改为使用声明性语法`<%# Eval("CategoryName") %>`。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-165">That is, instead of using `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` we could have instead used the declarative syntax `<%# Eval("CategoryName") %>`.</span></span>


<span data-ttu-id="4bd9c-166">在标签 Web 控件保留，但是，提供两个优势。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-166">Leaving in the Label Web controls, however, offer two advantages.</span></span> <span data-ttu-id="4bd9c-167">首先，它提供一种更容易的方法的格式设置数据，所基于的数据，正如我们将在下一教程中看到。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-167">First, it provides an easier means for formatting the data based on the data, as we'll see in the next tutorial.</span></span> <span data-ttu-id="4bd9c-168">其次，设计器不会 t 显示声明性数据绑定语法中的编辑模板选项显示在某些 Web 控件之外。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-168">Second, the Edit Templates option in the Designer doesn t display declarative databinding syntax that appears outside of some Web control.</span></span> <span data-ttu-id="4bd9c-169">相反，编辑模板接口旨在便于处理静态标记和 Web 控件，并假定任何数据绑定将通过编辑数据绑定对话框中，可从 Web 控件的智能标记进行访问。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-169">Instead, the Edit Templates interface is designed to facilitate working with static markup and Web controls and assumes that any databinding will be done through the Edit DataBindings dialog box, which is accessible from the Web controls smart tags.</span></span>

<span data-ttu-id="4bd9c-170">因此，使用 DataList，可选择编辑通过设计器的模板时我更喜欢使用标签 Web 控件，以便可通过编辑模板接口访问的内容。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-170">Therefore, when working with the DataList, which provides the option of editing the templates through the Designer, I prefer to use Label Web controls so that the content is accessible through the Edit Templates interface.</span></span> <span data-ttu-id="4bd9c-171">我们稍后将看到，Repeater 将需要从源视图进行编辑的模板的内容。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-171">As we'll see shortly, the Repeater requires that the template s contents be edited from the Source view.</span></span> <span data-ttu-id="4bd9c-172">因此，如果我不知道我将需要设置的格式编写我通常会忽略标签 Web Repeater 的模板控制数据的外观绑定文本根据编程逻辑。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-172">Consequently, when crafting the Repeater s templates I'll often omit the Label Web controls unless I know I'll need to format the appearance of the data bound text based on programmatic logic.</span></span>


[![E<span data-ttu-id="4bd9c-173">支票产品的输出是呈现使用 DataList 的 ItemTemplate]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-173">ach Product s Output is Rendered Using the DataList s ItemTemplate]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

<span data-ttu-id="4bd9c-174">**图 8**:每个产品 s 输出是呈现使用 DataList s `ItemTemplate` ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-174">**Figure 8**: Each Product s Output is Rendered Using the DataList s `ItemTemplate` ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))</span></span>


## <a name="step-3-improving-the-appearance-of-the-datalist"></a><span data-ttu-id="4bd9c-175">步骤 3：改进 DataList 的外观</span><span class="sxs-lookup"><span data-stu-id="4bd9c-175">Step 3: Improving the Appearance of the DataList</span></span>

<span data-ttu-id="4bd9c-176">如 GridView，DataList 提供了多个与样式有关的属性，如`Font`， `ForeColor`， `BackColor`， `CssClass`， `ItemStyle`， `AlternatingItemStyle`， `SelectedItemStyle`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-176">Like the GridView, the DataList offers a number of style-related properties, such as `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`, and so on.</span></span> <span data-ttu-id="4bd9c-177">当使用 GridView 和 DetailsView 控件时，我们创建外观文件中的`DataWebControls`预定义的主题`CssClass`这两个控件的属性和`CssClass`及其子属性的多个属性 (`RowStyle``HeaderStyle`，依此类推)。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-177">When working with the GridView and DetailsView controls, we created Skin files in the `DataWebControls` Theme that pre-defined the `CssClass` properties for these two controls and the `CssClass` property for several of their subproperties (`RowStyle`, `HeaderStyle`, and so on).</span></span> <span data-ttu-id="4bd9c-178">让我们来执行相同操作的 DataList。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-178">Let s do the same for the DataList.</span></span>

<span data-ttu-id="4bd9c-179">如中所述[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)教程中，将外观文件指定的默认 Web 控件与外观相关属性; 一个主题是定义的外观、 CSS、 图像和 JavaScript 文件的集合网站具有特定外观和风格。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-179">As discussed in the [Displaying Data With the ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) tutorial, a Skin file specifies the default appearance-related properties for a Web control; a Theme is a collection of Skin, CSS, image, and JavaScript files that define a particular look and feel for a website.</span></span> <span data-ttu-id="4bd9c-180">中*显示数据使用 ObjectDataSource*教程中，我们创建`DataWebControls`主题 (这作为一个文件夹内`App_Themes`文件夹) 的有，目前，两个外观文件-`GridView.skin`和`DetailsView.skin`.</span><span class="sxs-lookup"><span data-stu-id="4bd9c-180">In the *Displaying Data With the ObjectDataSource* tutorial, we created a `DataWebControls` Theme (which is implemented as a folder within the `App_Themes` folder) that has, currently, two Skin files - `GridView.skin` and `DetailsView.skin`.</span></span> <span data-ttu-id="4bd9c-181">让我们来添加三个外观文件来指定 DataList 的预定义的样式设置。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-181">Let s add a third Skin file to specify the pre-defined style settings for the DataList.</span></span>

<span data-ttu-id="4bd9c-182">若要添加将外观文件，请右键单击`App_Themes/DataWebControls`文件夹中，选择添加新项，并从列表中选择的外观文件选项。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-182">To add a Skin file, right-click on the `App_Themes/DataWebControls` folder, choose Add a New Item, and select the Skin File option from the list.</span></span> <span data-ttu-id="4bd9c-183">为 `DataList.skin` 文件命名。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-183">Name the file `DataList.skin`.</span></span>


[![C<span data-ttu-id="4bd9c-184">创建新外观文件命名为 DataList.skin]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-184">reate a New Skin File Named DataList.skin]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

<span data-ttu-id="4bd9c-185">**图 9**:创建新的外观文件命名`DataList.skin`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-185">**Figure 9**: Create a New Skin File Named `DataList.skin` ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))</span></span>


<span data-ttu-id="4bd9c-186">使用以下标记为`DataList.skin`文件：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-186">Use the following markup for the `DataList.skin` file:</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="4bd9c-187">这些设置将相同的 CSS 类分配给相应的 DataList 属性，如 GridView 和 DetailsView 控件采用了。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-187">These settings assign the same CSS classes to the appropriate DataList properties as were used with the GridView and DetailsView controls.</span></span> <span data-ttu-id="4bd9c-188">此处使用的 CSS 类`DataWebControlStyle`， `AlternatingRowStyle`， `RowStyle`，依次类推中定义`Styles.css`文件，并已添加在前面的教程。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-188">The CSS classes used here `DataWebControlStyle`, `AlternatingRowStyle`, `RowStyle`, and so on are defined in the `Styles.css` file and were added in previous tutorials.</span></span>

<span data-ttu-id="4bd9c-189">通过此外观文件添加，DataList 的外观会更新在设计器中 （可能需要刷新设计器视图以查看影响新外观文件; 从视图菜单中，选择刷新）。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-189">With the addition of this Skin file, the DataList s appearance is updated in the Designer (you may need to refresh the Designer view to see the effects of the new Skin file; from the View menu, choose Refresh).</span></span> <span data-ttu-id="4bd9c-190">如图 10 所示，每个交替的产品具有浅粉色背景颜色。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-190">As Figure 10 shows, each alternating product has a light pink background color.</span></span>


[![C<span data-ttu-id="4bd9c-191">创建新外观文件命名为 DataList.skin]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-191">reate a New Skin File Named DataList.skin]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

<span data-ttu-id="4bd9c-192">**图 10**:创建新的外观文件命名`DataList.skin`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-192">**Figure 10**: Create a New Skin File Named `DataList.skin` ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))</span></span>


## <a name="step-4-exploring-the-datalist-s-other-templates"></a><span data-ttu-id="4bd9c-193">步骤 4：了解 DataList s 其他模板</span><span class="sxs-lookup"><span data-stu-id="4bd9c-193">Step 4: Exploring the DataList s Other Templates</span></span>

<span data-ttu-id="4bd9c-194">除了`ItemTemplate`，DataList 支持六种其他可选模板：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-194">In addition to the `ItemTemplate`, the DataList supports six other optional templates:</span></span>

- `HeaderTemplate` <span data-ttu-id="4bd9c-195">如果提供，将标题行添加到输出，并用于呈现此行</span><span class="sxs-lookup"><span data-stu-id="4bd9c-195">if provided, adds a header row to the output and is used to render this row</span></span>
- `AlternatingItemTemplate` <span data-ttu-id="4bd9c-196">用于呈现交替项</span><span class="sxs-lookup"><span data-stu-id="4bd9c-196">used to render alternating items</span></span>
- `SelectedItemTemplate` <span data-ttu-id="4bd9c-197">用于呈现所选的项;所选的项是的项的索引对应于 DataList s [ `SelectedIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-197">used to render the selected item; the selected item is the item whose index corresponds to the DataList s [`SelectedIndex` property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)</span></span>
- `EditItemTemplate` <span data-ttu-id="4bd9c-198">用于呈现所编辑的项</span><span class="sxs-lookup"><span data-stu-id="4bd9c-198">used to render the item being edited</span></span>
- `SeparatorTemplate` <span data-ttu-id="4bd9c-199">如果提供，将添加每个项之间的分隔符，并用于呈现此分隔符</span><span class="sxs-lookup"><span data-stu-id="4bd9c-199">if provided, adds a separator between each item and is used to render this separator</span></span>
- `FooterTemplate` <span data-ttu-id="4bd9c-200">-如果提供，将脚注行添加到输出，并用于呈现此行</span><span class="sxs-lookup"><span data-stu-id="4bd9c-200">- if provided, adds a footer row to the output and is used to render this row</span></span>

<span data-ttu-id="4bd9c-201">指定时`HeaderTemplate`或`FooterTemplate`，DataList 将一个附加的页眉或页脚行添加到呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-201">When specifying the `HeaderTemplate` or `FooterTemplate`, the DataList adds an additional header or footer row to the rendered output.</span></span> <span data-ttu-id="4bd9c-202">如 GridView 的页眉和页脚行、 页眉和页脚中 DataList 未绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-202">Like with the GridView s header and footer rows, the header and footer in a DataList are not bound to data.</span></span> <span data-ttu-id="4bd9c-203">因此，在任何数据绑定语法`HeaderTemplate`或`FooterTemplate`尝试访问绑定的数据将返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-203">Therefore, any databinding syntax in the `HeaderTemplate` or `FooterTemplate` that attempts to access bound data will return a blank string.</span></span>

> [!NOTE]
> <span data-ttu-id="4bd9c-204">中可以看到[GridView 的页脚中显示摘要信息](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)教程中，虽然页眉和页脚行不 t 支持数据绑定语法，特定于数据的信息可直接注入中的这些行GridView 的`RowDataBound`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-204">As we saw in the [Displaying Summary Information in the GridView s Footer](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) tutorial, while the header and footer rows don t support databinding syntax, data-specific information can be injected directly into these rows from the GridView s `RowDataBound` event handler.</span></span> <span data-ttu-id="4bd9c-205">此方法可用于同时计算运行总计或来自数据的其他信息绑定到控件，以及将该信息分配给页脚。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-205">This technique can be used to both calculate running totals or other information from the data bound to the control as well as assign that information to the footer.</span></span> <span data-ttu-id="4bd9c-206">此相同的概念可以应用于的 DataList 和 Repeater 控件;唯一的区别是 DataList 和 Repeater 创建的事件处理程序`ItemDataBound`事件 (而不是为`RowDataBound`事件)。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-206">This same concept can be applied to the DataList and Repeater controls; the only difference is that for the DataList and Repeater create an event handler for the `ItemDataBound` event (instead of for the `RowDataBound` event).</span></span>


<span data-ttu-id="4bd9c-207">对于本示例中，let s 具有标题中的 DataList 的结果顶部显示的产品信息`<h3>`标题。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-207">For our example, let s have the title Product Information displayed at the top of the DataList s results in an `<h3>` heading.</span></span> <span data-ttu-id="4bd9c-208">若要完成此操作，将添加`HeaderTemplate`包含相应的标记。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-208">To accomplish this, add a `HeaderTemplate` with the appropriate markup.</span></span> <span data-ttu-id="4bd9c-209">从设计器中，可以通过单击 DataList s 智能标记中的编辑模板链接，选择从下拉列表中，页眉模板并选取样式下拉列表中的标题 3 选项之后的文本中键入列表 （请参阅图 11）。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-209">From the Designer, this can be accomplished by clicking on the Edit Templates link in the DataList s smart tag, choosing the Header Template from the drop-down list, and typing in the text after picking the Heading 3 option from the style drop-down list (see Figure 11).</span></span>


[![A<span data-ttu-id="4bd9c-210">dd HeaderTemplate 与文本产品信息]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-210">dd a HeaderTemplate with the Text Product Information]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

<span data-ttu-id="4bd9c-211">**图 11**:添加`HeaderTemplate`与文本产品信息 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-211">**Figure 11**: Add a `HeaderTemplate` with the Text Product Information ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))</span></span>


<span data-ttu-id="4bd9c-212">或者，可以在添加该声明的方式通过输入中的以下标记`<asp:DataList>`标记：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-212">Alternatively, this can be added declaratively by entering the following markup within the `<asp:DataList>` tags:</span></span>


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

<span data-ttu-id="4bd9c-213">若要添加的每个产品列表之间的空间位，让我们来添加`SeparatorTemplate`包括每个部分之间的直线。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-213">To add a bit of space between each product listing, let s add a `SeparatorTemplate` that includes a line between each section.</span></span> <span data-ttu-id="4bd9c-214">水平标尺标记 (`<hr>`)，将添加一个此类分隔线。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-214">The horizontal rule tag (`<hr>`), adds such a divider.</span></span> <span data-ttu-id="4bd9c-215">创建`SeparatorTemplate`以使其具有以下标记：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-215">Create the `SeparatorTemplate` so that it has the following markup:</span></span>


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> <span data-ttu-id="4bd9c-216">像`HeaderTemplate`并`FooterTemplates`，则`SeparatorTemplate`未绑定到任何记录从数据源，因此不能直接访问的数据源绑定到 DataList 的记录。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-216">Like the `HeaderTemplate` and `FooterTemplates`, the `SeparatorTemplate` is not bound to any record from the data source and therefore cannot directly access the data source records bound to the DataList.</span></span>


<span data-ttu-id="4bd9c-217">进行此添加后, 查看通过浏览器页面时它应类似于图 12。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-217">After making this addition, when viewing the page through a browser it should look similar to Figure 12.</span></span> <span data-ttu-id="4bd9c-218">请注意标题行和每个产品列表之间的线。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-218">Note the header row and the line between each product listing.</span></span>


[![T<span data-ttu-id="4bd9c-219">他 DataList 包括标头行和水平规则之间每个产品清单]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-219">he DataList Includes a Header Row and a Horizontal Rule Between Each Product Listing]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

<span data-ttu-id="4bd9c-220">**图 12**:DataList 包括标头行和水平规则之间每个产品清单 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-220">**Figure 12**: The DataList Includes a Header Row and a Horizontal Rule Between Each Product Listing ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))</span></span>


## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a><span data-ttu-id="4bd9c-221">步骤 5：呈现 Repeater 控件使用的特定标记</span><span class="sxs-lookup"><span data-stu-id="4bd9c-221">Step 5: Rendering Specific Markup with the Repeater Control</span></span>

<span data-ttu-id="4bd9c-222">如果访问图 12 中的 DataList 示例时，可以从你的浏览器执行视图/源代码，您将看到 DataList 发出对应的 HTML `<table>` ，其中包含一个表行 (`<tr>`) 与一个表格单元格 (`<td>`) 为每个项绑定到DataList。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-222">If you do a View/Source from your browser when visiting the DataList example from Figure 12, you'll see that the DataList emits an HTML `<table>` that contains a table row (`<tr>`) with a single table cell (`<td>`) for each item bound to the DataList.</span></span> <span data-ttu-id="4bd9c-223">此输出，事实上，等同于内容将被发送从单个 templatefield 进一步使用 GridView。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-223">This output, in fact, is identical to what would be emitted from a GridView with a single TemplateField.</span></span> <span data-ttu-id="4bd9c-224">我们将在以后的教程中看到的 DataList 允许进一步自定义的输出中，使我们能够显示每个行的多个数据源记录。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-224">As we'll see in a future tutorial, the DataList does allow further customization of the output, enabling us to display multiple data source records per table row.</span></span>

<span data-ttu-id="4bd9c-225">如果您不想要发出对应的 HTML `<table>`，但？</span><span class="sxs-lookup"><span data-stu-id="4bd9c-225">What if you don t want to emit an HTML `<table>`, though?</span></span> <span data-ttu-id="4bd9c-226">生成数据 Web 控件的标记的总计和完全控制，我们必须使用 Repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-226">For total and complete control over the markup generated by a data Web control, we must use the Repeater control.</span></span> <span data-ttu-id="4bd9c-227">如 DataList 和 Repeater 是基于模板构造的。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-227">Like the DataList, the Repeater is constructed based upon templates.</span></span> <span data-ttu-id="4bd9c-228">Repeater，但是，仅提供以下五个模板：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-228">The Repeater, however, only offers the following five templates:</span></span>

- `HeaderTemplate` <span data-ttu-id="4bd9c-229">如果提供，将添加在项的前面指定的标记</span><span class="sxs-lookup"><span data-stu-id="4bd9c-229">if provided, adds the specified markup before the items</span></span>
- `ItemTemplate` <span data-ttu-id="4bd9c-230">用于呈现项</span><span class="sxs-lookup"><span data-stu-id="4bd9c-230">used to render items</span></span>
- `AlternatingItemTemplate` <span data-ttu-id="4bd9c-231">如果提供，，用于呈现交替项</span><span class="sxs-lookup"><span data-stu-id="4bd9c-231">if provided, used to render alternating items</span></span>
- `SeparatorTemplate` <span data-ttu-id="4bd9c-232">如果提供，将添加每个项之间指定的标记</span><span class="sxs-lookup"><span data-stu-id="4bd9c-232">if provided, adds the specified markup between each item</span></span>
- `FooterTemplate` <span data-ttu-id="4bd9c-233">-如果提供，将指定的标记添加的项目之后</span><span class="sxs-lookup"><span data-stu-id="4bd9c-233">- if provided, adds the specified markup after the items</span></span>

<span data-ttu-id="4bd9c-234">在 ASP.NET 1.x 中，Repeater 控件通常用于显示其数据来自某些数据源的项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-234">In ASP.NET 1.x, the Repeater control was commonly used to display a bulleted list whose data came from some data source.</span></span> <span data-ttu-id="4bd9c-235">在这种情况下，`HeaderTemplate`并`FooterTemplates`将包含在开始和结束`<ul>`标记，分别，而`ItemTemplate`将包含`<li>`具有数据绑定语法元素。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-235">In such a case, the `HeaderTemplate` and `FooterTemplates` would contain the opening and closing `<ul>` tags, respectively, while the `ItemTemplate` would contain `<li>` elements with databinding syntax.</span></span> <span data-ttu-id="4bd9c-236">这种方法仍可在 ASP.NET 2.0 中的两个示例中可以看到[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-236">This approach can still be used in ASP.NET 2.0 as we saw in two examples in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial:</span></span>

- <span data-ttu-id="4bd9c-237">在`Site.master`主页面上，Repeater 用于显示顶层站点映射内容 （基本报告、 筛选报表、 自定义格式设置等） 的项目符号列表; 另一个嵌套的 Repeater 用于显示的子部分顶级部分</span><span class="sxs-lookup"><span data-stu-id="4bd9c-237">In the `Site.master` master page, a Repeater was used to display a bulleted list of the top-level site map contents (Basic Reporting, Filtering Reports, Customized Formatting, and so on); another, nested Repeater was used to display the children sections of the top-level sections</span></span>
- <span data-ttu-id="4bd9c-238">在`SectionLevelTutorialListing.ascx`，Repeater 用于显示当前站点映射部分的子部分的项目符号列表</span><span class="sxs-lookup"><span data-stu-id="4bd9c-238">In `SectionLevelTutorialListing.ascx`, a Repeater was used to display a bulleted list of the children sections of the current site map section</span></span>

> [!NOTE]
> <span data-ttu-id="4bd9c-239">ASP.NET 2.0 引入了新[BulletedList 控件](https://msdn.microsoft.com/library/ms228101.aspx)，这可以绑定到数据源控件以显示一个简单的项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-239">ASP.NET 2.0 introduces the new [BulletedList control](https://msdn.microsoft.com/library/ms228101.aspx), which can be bound to a data source control in order to display a simple bulleted list.</span></span> <span data-ttu-id="4bd9c-240">我们不需要与 BulletedList 控件指定任何相关列表的 HTML 中;相反，我们只用于表示要显示为每个列表项的文本的数据字段。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-240">With the BulletedList control we do not need to specify any of the list-related HTML; instead, we simply indicate the data field to display as the text for each list item.</span></span>


<span data-ttu-id="4bd9c-241">Repeater 将所有数据 Web 控件都充当一个问题。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-241">The Repeater serves as a catch all data Web control.</span></span> <span data-ttu-id="4bd9c-242">如果不是生成所需的标记的现有控件，可以使用 Repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-242">If there is not an existing control that generates the needed markup, the Repeater control can be used.</span></span> <span data-ttu-id="4bd9c-243">为了说明使用 Repeater，让 s 已在步骤 2 中创建的产品信息 DataList 上方显示的类别的列表。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-243">To illustrate using the Repeater, let s have the list of categories displayed above the Product Information DataList created in Step 2.</span></span> <span data-ttu-id="4bd9c-244">具体而言，let s 具有类别中的单行 HTML 显示`<table>`每个类别都显示为表中的列。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-244">In particular, let s have the categories displayed in a single-row HTML `<table>` with each category displayed as a column in the table.</span></span>

<span data-ttu-id="4bd9c-245">若要完成此操作，先从工具箱拖到设计器中，上述产品信息 DataList 拖动 Repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-245">To accomplish this, start by dragging a Repeater control from the Toolbox onto the Designer, above the Product Information DataList.</span></span> <span data-ttu-id="4bd9c-246">如同 DataList 和 Repeater 最初显示为灰色框定义它的模板之前。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-246">As with the DataList, the Repeater initially displays as a gray box until its templates have been defined.</span></span>


[![A<span data-ttu-id="4bd9c-247">dd Repeater 到设计器]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-247">dd a Repeater to the Designer]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

<span data-ttu-id="4bd9c-248">**图 13**:将转发器添加到设计器 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-248">**Figure 13**: Add a Repeater to the Designer ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))</span></span>


<span data-ttu-id="4bd9c-249">那里 s s 中继器中的只有一个选项的智能标记：选择数据源。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-249">There s only one option in the Repeater s smart tag: Choose Data Source.</span></span> <span data-ttu-id="4bd9c-250">选择创建新对象数据源，并将其配置为使用`CategoriesBLL`类的`GetCategories`方法。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-250">Opt to create a new ObjectDataSource and configure it to use the `CategoriesBLL` class s `GetCategories` method.</span></span>


[![C<span data-ttu-id="4bd9c-251">创建新对象数据源]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-251">reate a New ObjectDataSource]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

<span data-ttu-id="4bd9c-252">**图 14**:创建新对象数据源 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-252">**Figure 14**: Create a New ObjectDataSource ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))</span></span>


[![C<span data-ttu-id="4bd9c-253">配置对象数据源以使用 CategoriesBLL 类]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-253">onfigure the ObjectDataSource to Use the CategoriesBLL Class]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

<span data-ttu-id="4bd9c-254">**图 15**:配置为使用 ObjectDataSource`CategoriesBLL`类 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-254">**Figure 15**: Configure the ObjectDataSource to Use the `CategoriesBLL` Class ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))</span></span>


[![R<span data-ttu-id="4bd9c-255">etrieve 信息有关所有使用 GetCategories 方法的类别的]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-255">etrieve Information About All of the Categories Using the GetCategories Method]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

<span data-ttu-id="4bd9c-256">**图 16**:检索信息有关所有类别使用的`GetCategories`方法 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-256">**Figure 16**: Retrieve Information About All of the Categories Using the `GetCategories` Method ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))</span></span>


<span data-ttu-id="4bd9c-257">DataList，与 Visual Studio 不自动创建 ItemTemplate 为 Repeater 后将其绑定到数据源。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-257">Unlike the DataList, Visual Studio does not automatically create an ItemTemplate for the Repeater after binding it to a data source.</span></span> <span data-ttu-id="4bd9c-258">此外，Repeater 的模板不能通过设计器配置，并且必须以声明方式指定。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-258">Furthermore, the Repeater s templates cannot be configured through the Designer and must be specified declaratively.</span></span>

<span data-ttu-id="4bd9c-259">若要为单个行中显示的类别`<table>`与每个类别列，我们需要 Repeater 发出标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-259">To display the categories as a single-row `<table>` with a column for each category, we need the Repeater to emit markup similar to the following:</span></span>


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

<span data-ttu-id="4bd9c-260">由于`<td>Category X</td>`文本是重复发生，这会在 Repeater 的 ItemTemplate 中的部分。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-260">Since the `<td>Category X</td>` text is the portion that repeats, this will appear in the Repeater s ItemTemplate.</span></span> <span data-ttu-id="4bd9c-261">将出现在它之前的标记`<table><tr>`-将被放入`HeaderTemplate`时的结束标记- `</tr></table>` -将放入`FooterTemplate`。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-261">The markup that appears before it - `<table><tr>` - will be placed in the `HeaderTemplate` while the ending markup - `</tr></table>` - will placed in the `FooterTemplate`.</span></span> <span data-ttu-id="4bd9c-262">若要输入这些模板设置，请转到 ASP.NET 页面的声明性部分通过单击左下角中的源按钮并键入以下语法：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-262">To enter these template settings, go to the declarative portion of the ASP.NET page by clicking on the Source button in the lower left corner and type in the following syntax:</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

<span data-ttu-id="4bd9c-263">Repeater 发出指定的它的模板，没有其他任何，执行任何操作更少的精确标记。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-263">The Repeater emits the precise markup as specified by its templates, nothing more, nothing less.</span></span> <span data-ttu-id="4bd9c-264">图 17 显示了 Repeater 的输出时的浏览器查看。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-264">Figure 17 shows the Repeater s output when viewed through a browser.</span></span>


[![A <span data-ttu-id="4bd9c-265">只包含一行 HTML&lt;表&gt;在一个单独的列中列出了每个类别]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-265">Single-Row HTML &lt;table&gt; Lists Each Category in a Separate Column]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

<span data-ttu-id="4bd9c-266">**图 17**:只包含一行 HTML`<table>`列出了在一个单独的列中的每个类别 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-266">**Figure 17**: A Single-Row HTML `<table>` Lists Each Category in a Separate Column ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))</span></span>


## <a name="step-6-improving-the-appearance-of-the-repeater"></a><span data-ttu-id="4bd9c-267">步骤 6：提高中继器的外观</span><span class="sxs-lookup"><span data-stu-id="4bd9c-267">Step 6: Improving the Appearance of the Repeater</span></span>

<span data-ttu-id="4bd9c-268">由于 Repeater 发出精确地指定它的模板的标记，它应提供果然不出所料没有为 Repeater 与样式有关的属性。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-268">Since the Repeater emits precisely the markup specified by its templates, it should come as no surprise that there are no style-related properties for the Repeater.</span></span> <span data-ttu-id="4bd9c-269">若要更改生成 Repeater 的内容的外观，我们必须手动添加到 Repeater 的模板直接的所需的 HTML 或 CSS 内容。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-269">To alter the appearance of the content generated by the Repeater, we must manually add the needed HTML or CSS content directly to the Repeater s templates.</span></span>

<span data-ttu-id="4bd9c-270">对于本示例中，让 s 具有备用背景颜色，如使用 DataList 中的交替行的类别列。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-270">For our example, let s have the category columns alternate background colors, like with the alternating rows in the DataList.</span></span> <span data-ttu-id="4bd9c-271">若要实现此目的，我们需要将分配`RowStyle`到 Repeater 中的每个项的 CSS 类和`AlternatingRowStyle`通过每个交替中继器项的 CSS 类`ItemTemplate`和`AlternatingItemTemplate`模板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-271">To accomplish this, we need to assign the `RowStyle` CSS class to each Repeater item and the `AlternatingRowStyle` CSS class to each alternating Repeater item through the `ItemTemplate` and `AlternatingItemTemplate` templates, like so:</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

<span data-ttu-id="4bd9c-272">允许 s 还将标头行添加到包含产品类别的文本的输出。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-272">Let s also add a header row to the output with the text Product Categories.</span></span> <span data-ttu-id="4bd9c-273">因为我们不知道多少列我们从而`<table>`将组成的生成保证跨所有列标题行的最简单方法是使用*两个* `<table>` s。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-273">Since we don t know how many columns our resulting `<table>` will be comprised of, the simplest way to generate a header row that is guaranteed to span all columns is to use *two* `<table>` s.</span></span> <span data-ttu-id="4bd9c-274">第一个`<table>`将包含两行的标头行和将包含第二个，只包含一行的行`<table>`的系统中有一列用于每个类别。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-274">The first `<table>` will contain two rows the header row and a row that will contain the second, single-row `<table>` that has a column for each category in the system.</span></span> <span data-ttu-id="4bd9c-275">也就是说，我们想要发送以下标记：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-275">That is, we want to emit the following markup:</span></span>


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

<span data-ttu-id="4bd9c-276">以下`HeaderTemplate`和`FooterTemplate`产生所需的标记：</span><span class="sxs-lookup"><span data-stu-id="4bd9c-276">The following `HeaderTemplate` and `FooterTemplate` result in the desired markup:</span></span>


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

<span data-ttu-id="4bd9c-277">图 18 显示了 Repeater 后进行了这些更改。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-277">Figure 18 shows the Repeater after these changes have been made.</span></span>


[![T<span data-ttu-id="4bd9c-278">他备用背景色，包括标题行中的列类别]</span><span class="sxs-lookup"><span data-stu-id="4bd9c-278">he Category Columns Alternate in Background Color and Includes a Header Row]</span></span>(displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

<span data-ttu-id="4bd9c-279">**图 18**:类别列备用背景色，包括标题行中 ([单击此项可查看原尺寸图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="4bd9c-279">**Figure 18**: The Category Columns Alternate in Background Color and Includes a Header Row ([Click to view full-size image](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))</span></span>


## <a name="summary"></a><span data-ttu-id="4bd9c-280">总结</span><span class="sxs-lookup"><span data-stu-id="4bd9c-280">Summary</span></span>

<span data-ttu-id="4bd9c-281">虽然 GridView 控件，可以更容易地显示，编辑、 删除、 排序和分页浏览数据，外观是非常 boxy 和类似网格的。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-281">While the GridView control makes it easy to display, edit, delete, sort, and page through data, the appearance is very boxy and grid-like.</span></span> <span data-ttu-id="4bd9c-282">对消息的外观的更多控制，我们需要打开到 DataList 或 Repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-282">For more control over the appearance, we need to turn to either the DataList or Repeater controls.</span></span> <span data-ttu-id="4bd9c-283">这两种控件显示一的组记录使用模板而不 BoundFields、 CheckBoxFields，等等。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-283">Both of these controls display a set of records using templates instead of BoundFields, CheckBoxFields, and so on.</span></span>

<span data-ttu-id="4bd9c-284">DataList 呈现为 HTML `<table>` ，默认情况下，显示每个数据源记录中单个表行，就像使用单个 TemplateField GridView。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-284">The DataList renders as an HTML `<table>` that, by default, displays each data source record in a single table row, just like a GridView with a single TemplateField.</span></span> <span data-ttu-id="4bd9c-285">我们将在以后的教程中看到的但是，DataList 允许多个记录，以显示每个行。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-285">As we will see in a future tutorial, however, the DataList does permit multiple records to be displayed per table row.</span></span> <span data-ttu-id="4bd9c-286">Repeater，但是，严格地发出其模板; 中指定的标记它不会添加任何附加标记并因此通常用于在 HTML 元素而不显示数据`<table>`（如项目符号列表）。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-286">The Repeater, on the other hand, strictly emits the markup specified in its templates; it does not add any additional markup and therefore is commonly used to display data in HTML elements other than a `<table>` (such as in a bulleted list).</span></span>

<span data-ttu-id="4bd9c-287">虽然 DataList 和 Repeater 提供更灵活地呈现的输出，它们没有很多 GridView 中的内置功能。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-287">While the DataList and Repeater offer more flexibility in their rendered output, they lack many of the built-in features found in the GridView.</span></span> <span data-ttu-id="4bd9c-288">因为我们将介绍在即将发布的教程中，其中一些功能可返回插入，而无需太多工作，但不要继续记住，使用 DataList 或 Repeater 代替 GridView 不会限制可使用而无需实现这些功能的功能您自己。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-288">As we'll examine in upcoming tutorials, some of these features can be plugged back in without too much effort, but do keep in mind that using the DataList or Repeater in lieu of the GridView does limit the features you can use without having to implement those features yourself.</span></span>

<span data-ttu-id="4bd9c-289">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="4bd9c-289">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="4bd9c-290">关于作者</span><span class="sxs-lookup"><span data-stu-id="4bd9c-290">About the Author</span></span>

<span data-ttu-id="4bd9c-291">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-291">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="4bd9c-292">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-292">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="4bd9c-293">他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-293">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="4bd9c-294">他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-294">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="4bd9c-295">或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-295">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="4bd9c-296">特别感谢</span><span class="sxs-lookup"><span data-stu-id="4bd9c-296">Special Thanks To</span></span>

<span data-ttu-id="4bd9c-297">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-297">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="4bd9c-298">本教程中的潜在顾客审阅者已 Yaakov Ellis、 Liz Shulok、 Randy Schmidt 和 Stacy Park。</span><span class="sxs-lookup"><span data-stu-id="4bd9c-298">Lead reviewers for this tutorial were Yaakov Ellis, Liz Shulok, Randy Schmidt, and Stacy Park.</span></span> <span data-ttu-id="4bd9c-299">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="4bd9c-299">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="4bd9c-300">如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-300">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4bd9c-301">[上一页](nested-data-web-controls-cs.md)
> [下一页](formatting-the-datalist-and-repeater-based-upon-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4bd9c-301">[Previous](nested-data-web-controls-cs.md)
[Next](formatting-the-datalist-and-repeater-based-upon-data-vb.md)</span></span>

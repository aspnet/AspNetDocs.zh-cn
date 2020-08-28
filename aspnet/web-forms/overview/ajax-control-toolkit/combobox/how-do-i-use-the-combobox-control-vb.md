---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: 如何实现使用 ComboBox 控件？  (VB) |Microsoft Docs
author: rick-anderson
description: ComboBox 是 ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可从中选择的选项列表组合在一起。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a139f00fc2962c159eabed6c1dc2cbb78c94c564
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044618"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="28013-104">如何实现使用 ComboBox 控件？</span><span class="sxs-lookup"><span data-stu-id="28013-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="28013-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="28013-105">(VB)</span></span>

<span data-ttu-id="28013-106">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="28013-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="28013-107">ComboBox 是 ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可从中选择的选项列表组合在一起。</span><span class="sxs-lookup"><span data-stu-id="28013-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="28013-108">本教程的目的是介绍 AJAX 控件工具包组合框控件。</span><span class="sxs-lookup"><span data-stu-id="28013-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="28013-109">ComboBox 的工作方式类似于标准 ASP.NET DropDownList 控件和 TextBox 控件之间的组合。</span><span class="sxs-lookup"><span data-stu-id="28013-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="28013-110">您可以从预先存在的项列表中进行选择，也可以输入一个新项。</span><span class="sxs-lookup"><span data-stu-id="28013-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="28013-111">ComboBox 与自动完成控件扩展器类似，但控件在不同的方案中使用。</span><span class="sxs-lookup"><span data-stu-id="28013-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="28013-112">自动完成扩展器会查询 web 服务以获取匹配项。</span><span class="sxs-lookup"><span data-stu-id="28013-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="28013-113">相反，ComboBox 控件用一组项进行了初始化。</span><span class="sxs-lookup"><span data-stu-id="28013-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="28013-114">使用 "自动完成" 扩展器时，如果使用的是大量的数据 (数百万辆汽车) 部件，则使用 ComboBox 控件在处理一小部分数据 (数十个汽车部件) 时非常有意义。</span><span class="sxs-lookup"><span data-stu-id="28013-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="28013-115">从静态项列表中选择</span><span class="sxs-lookup"><span data-stu-id="28013-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="28013-116">让我们从一个简单的示例开始使用组合框控件。</span><span class="sxs-lookup"><span data-stu-id="28013-116">Let's start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="28013-117">假设您想要在下拉列表中显示项的静态列表。</span><span class="sxs-lookup"><span data-stu-id="28013-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="28013-118">但是，您仍希望使列表不完整。</span><span class="sxs-lookup"><span data-stu-id="28013-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="28013-119">您希望允许用户在列表中输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="28013-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="28013-120">我们将创建一个新的 ASP.NET Web 窗体页，并使用页面中的 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="28013-120">We'll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="28013-121">向项目中添加新的 "ASP.NET" 页，并切换到设计视图。</span><span class="sxs-lookup"><span data-stu-id="28013-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="28013-122">如果要使用页面中的 ComboBox 控件，则必须将 ScriptManager 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="28013-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="28013-123">将 ScriptManager 控件从 "AJAX 扩展" 选项卡下拖到设计器图面上。</span><span class="sxs-lookup"><span data-stu-id="28013-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="28013-124">应将 ScriptManager 控件添加到页面顶部;可以立即将其添加到 "打开服务器端 &lt; 窗体" &gt; 标记下。</span><span class="sxs-lookup"><span data-stu-id="28013-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="28013-125">接下来，将 ComboBox 控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="28013-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="28013-126">您可以在工具箱中找到带有其他 AJAX 控件工具包控件和控件扩展器的 ComboBox 控件 (参阅图 1) 。</span><span class="sxs-lookup"><span data-stu-id="28013-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="28013-127">[![用于创建名片的简单窗体](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28013-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="28013-128">**图 01**：从 "工具箱" 中选择 ComboBox 控件 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="28013-129">我们将使用 ComboBox 控件显示静态选项列表。</span><span class="sxs-lookup"><span data-stu-id="28013-129">We'll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="28013-130">用户可以从以下三个选项的列表中为其食物选择特定级别的 spiciness： "轻度"、"中" 和 "热" (参阅图 2) 。</span><span class="sxs-lookup"><span data-stu-id="28013-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="28013-131">[![从静态项列表中选择](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="28013-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="28013-132">**图 02**：从静态项列表中选择 ([单击查看完全大小的图像](how-do-i-use-the-combobox-control-vb/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="28013-133">可以通过两种方法将这些选项添加到 ComboBox 控件中。</span><span class="sxs-lookup"><span data-stu-id="28013-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="28013-134">首先，在将鼠标悬停在设计视图的控件上并打开项编辑器 (，选择 "编辑选项" 任务选项，请参见图 3) 。</span><span class="sxs-lookup"><span data-stu-id="28013-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="28013-135">[![编辑 ComboBox 项](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="28013-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="28013-136">**图 03**：编辑 ComboBox 项 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="28013-137">第二种方法是在 "源" 视图中打开和关闭 &lt; asp： ComboBox 标记之间添加项的列表 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="28013-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="28013-138">列表1中的页包含已更新的 ComboBox，其中包含项的列表。</span><span class="sxs-lookup"><span data-stu-id="28013-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="28013-139">**列表 1-Static .aspx**</span><span class="sxs-lookup"><span data-stu-id="28013-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="28013-140">打开列表1中的页时，可以从组合框中选择一个预先存在的选项。</span><span class="sxs-lookup"><span data-stu-id="28013-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="28013-141">换言之，组合框的工作方式与 DropDownList 控件的工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="28013-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="28013-142">但是，您还可以选择输入新的选项 (例如，不在现有列表中的超级 Spicy) 。</span><span class="sxs-lookup"><span data-stu-id="28013-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="28013-143">因此，组合框的工作方式也类似于 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="28013-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="28013-144">无论你是选取预先存在的项还是输入自定义项，当你提交窗体时，你的选择将显示在 "标签" 控件中。</span><span class="sxs-lookup"><span data-stu-id="28013-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="28013-145">提交表单时，Btnsubmit.text \_ 单击处理程序将执行并更新标签 (参见图 4) 。</span><span class="sxs-lookup"><span data-stu-id="28013-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="28013-146">[![显示选定项](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="28013-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="28013-147">**图 04**：显示选定项 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="28013-148">提交窗体后，ComboBox 支持与 DropDownList 控件相同的属性，以便检索选定项：</span><span class="sxs-lookup"><span data-stu-id="28013-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="28013-149">SelectedItem-显示所选项目的 "Text" 属性的值。</span><span class="sxs-lookup"><span data-stu-id="28013-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="28013-150">SelectedItem-显示所选项目的值属性的值，或显示键入到 ComboBox 中的文本。</span><span class="sxs-lookup"><span data-stu-id="28013-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="28013-151">SelectedValue-与 SelectedItem 相同，不同的是，此属性使你能够指定 (初始) 选定项的默认值。</span><span class="sxs-lookup"><span data-stu-id="28013-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="28013-152">如果在 ComboBox 中键入自定义选项，则会将自定义选择同时分配给 SelectedItem 和 SelectedItem 属性。</span><span class="sxs-lookup"><span data-stu-id="28013-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="28013-153">从数据库中选择项列表</span><span class="sxs-lookup"><span data-stu-id="28013-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="28013-154">可以从数据库中检索 ComboBox 显示的项的列表。</span><span class="sxs-lookup"><span data-stu-id="28013-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="28013-155">例如，可以将 ComboBox 绑定到 SqlDataSource 控件、ObjectDataSource 控件、LinqDataSource 或 EntityDataSource。</span><span class="sxs-lookup"><span data-stu-id="28013-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="28013-156">假设您想要在组合框中显示电影列表。</span><span class="sxs-lookup"><span data-stu-id="28013-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="28013-157">要从电影数据库表中检索电影列表。</span><span class="sxs-lookup"><span data-stu-id="28013-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="28013-158">执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="28013-158">Follow these steps:</span></span>

1. <span data-ttu-id="28013-159">创建名为 "default.aspx" 的页</span><span class="sxs-lookup"><span data-stu-id="28013-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="28013-160">通过从工具箱中的 "AJAX 扩展" 选项卡下将 ScriptManager 拖到页面上，将 ScriptManager 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="28013-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="28013-161">通过将 ComboBox 拖到页面上，将 combobox 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="28013-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="28013-162">在设计视图中，将鼠标悬停在 ComboBox 控件上，然后选择 " **选择数据源** " 任务选项 (参见图 5) 。</span><span class="sxs-lookup"><span data-stu-id="28013-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="28013-163">将启动 "数据源配置向导"。</span><span class="sxs-lookup"><span data-stu-id="28013-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="28013-164">在 " **选择数据源** " 步骤中，选择 " &lt; 新建数据源" &gt; 选项。</span><span class="sxs-lookup"><span data-stu-id="28013-164">In the **Choose a Data Source** step, select the &lt;New data source&gt; option.</span></span>
6. <span data-ttu-id="28013-165">在 " **选择数据源类型** " 步骤中，选择 "数据库"。</span><span class="sxs-lookup"><span data-stu-id="28013-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="28013-166">在 " **选择你的数据连接** " 步骤中，选择你的数据库 (例如 MoviesDB) 。</span><span class="sxs-lookup"><span data-stu-id="28013-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="28013-167">在 "将 **连接字符串保存到应用程序配置文件** " 步骤中，选择用于保存连接字符串的选项。</span><span class="sxs-lookup"><span data-stu-id="28013-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="28013-168">在 " **配置 Select 语句** " 步骤中，选择 "电影数据库" 表并选择所有列。</span><span class="sxs-lookup"><span data-stu-id="28013-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="28013-169">在 **测试查询** 步骤中，单击 "完成" 按钮。</span><span class="sxs-lookup"><span data-stu-id="28013-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="28013-170">返回 " **选择数据源** " 步骤，选择要显示的字段的 "标题" 列以及 "数据" 字段的 "Id" 列 (参阅图) 。</span><span class="sxs-lookup"><span data-stu-id="28013-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="28013-171">单击 "确定" 按钮以关闭该向导。</span><span class="sxs-lookup"><span data-stu-id="28013-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="28013-172">[![选择数据源](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="28013-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="28013-173">**图 05**：选择数据源 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image10.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="28013-174">[![选择数据文本和值字段](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="28013-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="28013-175">**图 06**：选择数据文本和值字段 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image12.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>

<span data-ttu-id="28013-176">完成上述步骤后，ComboBox 将绑定到表示电影数据库表中的电影的 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="28013-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="28013-177">页面的源如下所示， (我清理了有点) 的格式。</span><span class="sxs-lookup"><span data-stu-id="28013-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="28013-178">**列表 2-电影 .aspx**</span><span class="sxs-lookup"><span data-stu-id="28013-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="28013-179">请注意，ComboBox 控件具有指向 SqlDataSource 控件的 DataSourceID 属性。</span><span class="sxs-lookup"><span data-stu-id="28013-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="28013-180">当你在浏览器中打开该页面时，将显示该数据库中的电影列表 (参见图 7) 。</span><span class="sxs-lookup"><span data-stu-id="28013-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="28013-181">您可以从列表中选择电影，也可以通过在 ComboBox 中键入电影来输入新电影。</span><span class="sxs-lookup"><span data-stu-id="28013-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="28013-182">[![显示电影列表](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="28013-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="28013-183">**图 07**：显示电影列表 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image14.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="28013-184">设置 DropDownStyle</span><span class="sxs-lookup"><span data-stu-id="28013-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="28013-185">可以使用 ComboBox DropDownStyle 属性更改 ComboBox 的行为。</span><span class="sxs-lookup"><span data-stu-id="28013-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="28013-186">此属性接受可能的值：</span><span class="sxs-lookup"><span data-stu-id="28013-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="28013-187">下拉列表 (默认值) 在单击箭头时，组合框将显示一个下拉列表，您可以输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="28013-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="28013-188">简单-ComboBox 自动显示下拉列表，你可以输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="28013-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="28013-189">DropDownList-ComboBox 的工作方式与 DropDownList 控件的工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="28013-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="28013-190">下拉列表和简单选项之间的不同之处是显示项列表。</span><span class="sxs-lookup"><span data-stu-id="28013-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="28013-191">在简单的情况下，当您将焦点移到 ComboBox 上时，列表会立即显示。</span><span class="sxs-lookup"><span data-stu-id="28013-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="28013-192">对于下拉列表，必须单击箭头才能查看项列表。</span><span class="sxs-lookup"><span data-stu-id="28013-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="28013-193">DropDownList 值使 ComboBox 控件像标准的 DropDownList 控件一样工作。</span><span class="sxs-lookup"><span data-stu-id="28013-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="28013-194">但是，这里有一个重要的差异。</span><span class="sxs-lookup"><span data-stu-id="28013-194">However, there is an important difference here.</span></span> <span data-ttu-id="28013-195">较早版本的 Internet Explorer 显示具有无限 z 索引的 DropDownList 控件，因此控件将显示在其前面放置的任何控件之前。</span><span class="sxs-lookup"><span data-stu-id="28013-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="28013-196">由于组合框会呈现 HTML &lt; div &gt; 标记，而不是 &lt; html &gt; 选择标记，因此 combobox 正确遵从 z 顺序。</span><span class="sxs-lookup"><span data-stu-id="28013-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="28013-197">设置 AutoCompleteMode</span><span class="sxs-lookup"><span data-stu-id="28013-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="28013-198">使用 ComboBox AutoCompleteMode 属性可以指定有人将文本键入 ComboBox 时所发生的情况。</span><span class="sxs-lookup"><span data-stu-id="28013-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="28013-199">此属性接受以下可能值：</span><span class="sxs-lookup"><span data-stu-id="28013-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="28013-200">无-ComboBox)  (默认值不提供任何自动完成行为。</span><span class="sxs-lookup"><span data-stu-id="28013-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="28013-201">建议-ComboBox 显示列表并且突出显示列表中的匹配项 (参见图 8) 。</span><span class="sxs-lookup"><span data-stu-id="28013-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="28013-202">追加-ComboBox 不显示列表，它将列表中的匹配项追加到你键入的内容 (参见图 9) 。</span><span class="sxs-lookup"><span data-stu-id="28013-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="28013-203">SuggestAppend-ComboBox 显示列表，并将列表中的匹配项追加到你键入的内容 (参阅图 10) 。</span><span class="sxs-lookup"><span data-stu-id="28013-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="28013-204">[![组合框提出建议](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="28013-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="28013-205">**图 08**：组合框提出建议 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image16.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>

<span data-ttu-id="28013-206">[![ComboBox 追加匹配文本](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="28013-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="28013-207">**图 09**： ComboBox 将匹配的文本追加 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image18.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>

<span data-ttu-id="28013-208">[![ComboBox 建议并追加](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="28013-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="28013-209">**图 10**： ComboBox 建议并追加 ([单击查看全尺寸图像](how-do-i-use-the-combobox-control-vb/_static/image20.png)) </span><span class="sxs-lookup"><span data-stu-id="28013-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="28013-210">摘要</span><span class="sxs-lookup"><span data-stu-id="28013-210">Summary</span></span>

<span data-ttu-id="28013-211">在本教程中，您学习了如何使用 ComboBox 控件显示一组固定的项。</span><span class="sxs-lookup"><span data-stu-id="28013-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="28013-212">我们将 ComboBox 控件绑定到一组静态项和一个数据库表。</span><span class="sxs-lookup"><span data-stu-id="28013-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="28013-213">最后，您学习了如何通过设置组合框的 DropDownStyle 和 AutoCompleteMode 属性来修改其行为。</span><span class="sxs-lookup"><span data-stu-id="28013-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28013-214">上一页</span><span class="sxs-lookup"><span data-stu-id="28013-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)

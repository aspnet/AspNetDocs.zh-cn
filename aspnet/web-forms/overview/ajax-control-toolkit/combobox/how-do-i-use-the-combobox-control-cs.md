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
# <a name="how-do-i-use-the-combobox-control-c"></a><span data-ttu-id="e5741-104">如何使用组合盒控件？</span><span class="sxs-lookup"><span data-stu-id="e5741-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="e5741-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="e5741-105">(C#)</span></span>

<span data-ttu-id="e5741-106">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e5741-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e5741-107">ComboBox 是一ASP.NET AJAX 控件，它将 TextBox 的灵活性与用户可以选择的选项列表相结合。</span><span class="sxs-lookup"><span data-stu-id="e5741-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="e5741-108">本教程的目的是解释 AJAX 控制工具包组合盒控件。</span><span class="sxs-lookup"><span data-stu-id="e5741-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="e5741-109">组合框的工作方式类似于标准ASP.NET下拉列表控件和文本框控件之间的组合。</span><span class="sxs-lookup"><span data-stu-id="e5741-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="e5741-110">您可以从预先存在的项目列表中选择，也可以输入新项目。</span><span class="sxs-lookup"><span data-stu-id="e5741-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="e5741-111">组合盒类似于自动完成控件扩展器，但控件在不同的方案中使用。</span><span class="sxs-lookup"><span data-stu-id="e5741-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="e5741-112">自动完成扩展程序查询 Web 服务以获取匹配的条目。</span><span class="sxs-lookup"><span data-stu-id="e5741-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="e5741-113">相反，组合框控件使用一组项进行初始化。</span><span class="sxs-lookup"><span data-stu-id="e5741-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="e5741-114">使用 AutoComplete 扩展程序在使用大量数据（数百万个汽车零件）时有意义，而使用 ComboBox 控件在使用一小组数据（数十个汽车部件）时是有意义的。</span><span class="sxs-lookup"><span data-stu-id="e5741-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="e5741-115">从静态项目列表中选择</span><span class="sxs-lookup"><span data-stu-id="e5741-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="e5741-116">让我们从使用组合框控件的简单示例开始。</span><span class="sxs-lookup"><span data-stu-id="e5741-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="e5741-117">假设您要在下拉列表中显示项目的静态列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="e5741-118">但是，您希望保留列表未完成的可能性。</span><span class="sxs-lookup"><span data-stu-id="e5741-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="e5741-119">您希望允许用户在列表中输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="e5741-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="e5741-120">我们将创建一个新的ASP.NET Web 窗体页，并在该页中使用 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="e5741-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="e5741-121">将新的ASP.NET页添加到项目中并切换到"设计"视图。</span><span class="sxs-lookup"><span data-stu-id="e5741-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="e5741-122">如果要在页面中使用 ComboBox 控件，则必须向页面添加脚本管理器控件。</span><span class="sxs-lookup"><span data-stu-id="e5741-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="e5741-123">将脚本管理器控件从 AJAX 扩展选项卡下方拖动到设计器表面。</span><span class="sxs-lookup"><span data-stu-id="e5741-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="e5741-124">应在页面顶部添加脚本管理器控件;但是，在页面顶部，应添加脚本管理器控件。可以将其添加到打开的服务器端&lt;窗体&gt;标记的下方。</span><span class="sxs-lookup"><span data-stu-id="e5741-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="e5741-125">接下来，将组合框控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="e5741-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="e5741-126">您可以在工具箱中找到与其他 AJAX 控制工具包控件和控制扩展器一起的 ComboBox 控件（见图 1）。</span><span class="sxs-lookup"><span data-stu-id="e5741-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="e5741-127">[![创建名片的简单表单](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="e5741-128">**图 01**： 从工具箱中选择组合框控件 （[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="e5741-129">我们将使用组合框控件来显示静态选项列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="e5741-130">用户可以从三个选项列表中为其食物选择特定级别的辣度（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="e5741-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="e5741-131">[![从静态项目列表中选择](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="e5741-132">**图 02**：从静态项目列表中选择（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="e5741-133">有两种方法可以将这些选项添加到 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="e5741-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="e5741-134">首先，在"设计"视图中将鼠标悬停在控件上并打开项目编辑器时，请选择"编辑选项"任务选项（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="e5741-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="e5741-135">[![编辑组合框项目](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="e5741-136">**图 03**： 编辑组合盒项目（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="e5741-137">第二个选项是在源视图中的开盘和关闭&lt;asp：ComboBox&gt;标记之间添加项目列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="e5741-138">清单 1 中的页面包含包含项目列表的更新的 ComboBox。</span><span class="sxs-lookup"><span data-stu-id="e5741-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="e5741-139">**清单 1 - 静态.aspx**</span><span class="sxs-lookup"><span data-stu-id="e5741-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

<span data-ttu-id="e5741-140">在清单 1 中打开页面时，您可以从组合框中选择一个预先存在的选项。</span><span class="sxs-lookup"><span data-stu-id="e5741-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="e5741-141">换句话说，组合框的工作方式与下拉列表控件类似。</span><span class="sxs-lookup"><span data-stu-id="e5741-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="e5741-142">但是，您还可以选择输入不在现有列表中的新选项（例如，超级辣）。</span><span class="sxs-lookup"><span data-stu-id="e5741-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="e5741-143">因此，组合框也像文本框控件一样工作。</span><span class="sxs-lookup"><span data-stu-id="e5741-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="e5741-144">无论您选择预先存在的项目还是输入自定义项目，在提交表单时，您的选择都会显示在标签控件中。</span><span class="sxs-lookup"><span data-stu-id="e5741-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="e5741-145">提交表单时，btnSubmit\_单击处理程序将执行并更新标签（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="e5741-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="e5741-146">[![显示所选项目](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="e5741-147">**图 04**：显示所选项目（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="e5741-148">ComboBox 支持与提交表单后检索所选项的下拉列表控件相同的属性：</span><span class="sxs-lookup"><span data-stu-id="e5741-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="e5741-149">选定项目.文本 - 显示所选项目的文本属性的值。</span><span class="sxs-lookup"><span data-stu-id="e5741-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="e5741-150">选定项目.值 - 显示所选项目的值属性的值或显示键入到组合盒中的文本。</span><span class="sxs-lookup"><span data-stu-id="e5741-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="e5741-151">所选值 - 与选定项目相同。除非此属性允许您指定默认（初始）选定项目。</span><span class="sxs-lookup"><span data-stu-id="e5741-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="e5741-152">如果在组合框中键入自定义选项，则自定义选项将分配给"选定项目.文本"和"选定项目"值属性。</span><span class="sxs-lookup"><span data-stu-id="e5741-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="e5741-153">从数据库中选择项目列表</span><span class="sxs-lookup"><span data-stu-id="e5741-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="e5741-154">您可以检索 ComboBox 从数据库中显示的项目列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="e5741-155">例如，您可以将组合盒绑定到 SqlDataSource 控件、ObjectDataSource 控件、LinqDataSource 或实体数据源。</span><span class="sxs-lookup"><span data-stu-id="e5741-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="e5741-156">假设您要在组合盒中显示电影列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="e5741-157">您希望从"影片"数据库表中检索影片列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="e5741-158">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="e5741-158">Follow these steps:</span></span>

1. <span data-ttu-id="e5741-159">创建名为"电影.aspx"的页面</span><span class="sxs-lookup"><span data-stu-id="e5741-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="e5741-160">通过将脚本管理器从工具箱中的 AJAX 扩展选项卡下拖动到页面，将脚本管理器控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="e5741-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="e5741-161">通过将组合框拖到页面上，将组合框控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="e5741-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="e5741-162">在"设计"视图中，将鼠标悬停在 ComboBox 控件上，然后选择 **"选择数据源**任务"选项（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="e5741-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="e5741-163">启动数据源配置向导。</span><span class="sxs-lookup"><span data-stu-id="e5741-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="e5741-164">在 **"选择数据源**"步骤中，选择"&lt;新建数据源"&gt;选项。</span><span class="sxs-lookup"><span data-stu-id="e5741-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="e5741-165">在 **"选择数据源类型"步骤中**，选择"数据库"。</span><span class="sxs-lookup"><span data-stu-id="e5741-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="e5741-166">在 **"选择数据连接**"步骤中，选择数据库（例如，MoviesDB.mdf）。</span><span class="sxs-lookup"><span data-stu-id="e5741-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="e5741-167">在 **"将连接字符串保存到应用程序配置文件"步骤中**，选择保存连接字符串的选项。</span><span class="sxs-lookup"><span data-stu-id="e5741-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="e5741-168">在 **"配置选择语句"** 步骤中，选择"影片"数据库表并选择所有列。</span><span class="sxs-lookup"><span data-stu-id="e5741-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="e5741-169">在 **"测试查询**"步骤中，单击"完成"按钮。</span><span class="sxs-lookup"><span data-stu-id="e5741-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="e5741-170">回到 **"选择数据源**"步骤中，选择要显示的字段的标题列和数据字段的"Id"列（参见图）。</span><span class="sxs-lookup"><span data-stu-id="e5741-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="e5741-171">单击"确定"按钮关闭向导。</span><span class="sxs-lookup"><span data-stu-id="e5741-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="e5741-172">[![选择数据源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-172">[![Choosing a data source](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="e5741-173">**图 05**： 选择数据源（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="e5741-174">[![选择数据文本和值字段](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span></span>

<span data-ttu-id="e5741-175">**图 06**：选择数据文本和值字段（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span></span>

<span data-ttu-id="e5741-176">完成上述步骤后，组合Box 将绑定到 SqlDataSource 控件，该控件表示"电影"数据库表中的影片。</span><span class="sxs-lookup"><span data-stu-id="e5741-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="e5741-177">页面的源类似于清单 2（我稍微清理了格式）。</span><span class="sxs-lookup"><span data-stu-id="e5741-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="e5741-178">**列表 2 - 电影.aspx**</span><span class="sxs-lookup"><span data-stu-id="e5741-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

<span data-ttu-id="e5741-179">请注意，ComboBox 控件具有指向 SqlDataSource 控件的 DataSourceID 属性。</span><span class="sxs-lookup"><span data-stu-id="e5741-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="e5741-180">在浏览器中打开页面时，将显示数据库中的影片列表（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="e5741-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="e5741-181">您可以通过在组合盒中键入影片从列表中选取影片或输入新影片。</span><span class="sxs-lookup"><span data-stu-id="e5741-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="e5741-182">[![显示电影列表](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span></span>

<span data-ttu-id="e5741-183">**图 07**： 显示电影列表（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="e5741-184">设置下拉样式</span><span class="sxs-lookup"><span data-stu-id="e5741-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="e5741-185">您可以使用组合盒下拉列表样式属性更改组合框的行为。</span><span class="sxs-lookup"><span data-stu-id="e5741-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="e5741-186">此属性接受可能存在的值：</span><span class="sxs-lookup"><span data-stu-id="e5741-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="e5741-187">下拉 - （默认值） 当您单击箭头并且可以输入自定义值时，组合框将显示下拉列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="e5741-188">简单 - 组合框会自动显示下拉列表，您可以输入自定义值。</span><span class="sxs-lookup"><span data-stu-id="e5741-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="e5741-189">下拉列表 - 组合框的工作方式与下拉列表控件类似。</span><span class="sxs-lookup"><span data-stu-id="e5741-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="e5741-190">下拉列表和"简单"之间的不同是显示项目列表时。</span><span class="sxs-lookup"><span data-stu-id="e5741-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="e5741-191">在 Simple 的情况下，当您将焦点移动到组合框时，将立即显示列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="e5741-192">在下拉列表的情况下，必须单击箭头才能看到项目列表。</span><span class="sxs-lookup"><span data-stu-id="e5741-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="e5741-193">"下拉列表"值使组合盒控件的工作方式与标准的下拉列表控件类似。</span><span class="sxs-lookup"><span data-stu-id="e5741-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="e5741-194">然而，这里有一个重要的区别。</span><span class="sxs-lookup"><span data-stu-id="e5741-194">However, there is an important difference here.</span></span> <span data-ttu-id="e5741-195">较旧版本的 Internet Explorer 显示具有无限 z 索引的下拉列表控件，因此该控件将显示在放置在其前面的任何控件的前面。</span><span class="sxs-lookup"><span data-stu-id="e5741-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="e5741-196">由于组合&lt;框呈现 HTML div&gt;标记而不是 HTML&lt;选择&gt;标记，因此组合框正确尊重 z 排序。</span><span class="sxs-lookup"><span data-stu-id="e5741-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="e5741-197">设置自动完成模式</span><span class="sxs-lookup"><span data-stu-id="e5741-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="e5741-198">您可以使用 ComboBox 自动完成模式属性来指定当有人在组合框中键入文本时会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="e5741-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="e5741-199">此属性接受以下可能的值：</span><span class="sxs-lookup"><span data-stu-id="e5741-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="e5741-200">无 - （默认值） 组合框不提供任何自动完成行为。</span><span class="sxs-lookup"><span data-stu-id="e5741-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="e5741-201">建议 - 组合框显示列表，并突出显示列表中的匹配项（参见图 8）。</span><span class="sxs-lookup"><span data-stu-id="e5741-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="e5741-202">附加 - 组合框不显示列表，它将匹配项从列表中追加到已键入的内容（参见图 9）。</span><span class="sxs-lookup"><span data-stu-id="e5741-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="e5741-203">建议应用 - 组合框都会显示列表并将匹配项从列表中追加到已键入的内容上（参见图 10）。</span><span class="sxs-lookup"><span data-stu-id="e5741-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="e5741-204">[![组合盒提出建议](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span></span>

<span data-ttu-id="e5741-205">**图 08**： 组合框提出建议（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span></span>

<span data-ttu-id="e5741-206">[![组合盒追加匹配文本](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span></span>

<span data-ttu-id="e5741-207">**图 09**： 组合盒追加匹配文本（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span></span>

<span data-ttu-id="e5741-208">[![组合框建议和追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="e5741-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span></span>

<span data-ttu-id="e5741-209">**图10**： 组合框建议和追加（[单击以查看全尺寸图像](how-do-i-use-the-combobox-control-cs/_static/image20.png)）</span><span class="sxs-lookup"><span data-stu-id="e5741-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="e5741-210">总结</span><span class="sxs-lookup"><span data-stu-id="e5741-210">Summary</span></span>

<span data-ttu-id="e5741-211">在本教程中，您学习了如何使用 ComboBox 控件来显示一组固定的项目。</span><span class="sxs-lookup"><span data-stu-id="e5741-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="e5741-212">我们将组合框控件绑定到静态项集和数据库表。</span><span class="sxs-lookup"><span data-stu-id="e5741-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="e5741-213">最后，您学习了如何通过设置其下拉风格和自动完成模式属性来修改组合盒的行为。</span><span class="sxs-lookup"><span data-stu-id="e5741-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e5741-214">下一页</span><span class="sxs-lookup"><span data-stu-id="e5741-214">Next</span></span>](how-do-i-use-the-combobox-control-vb.md)

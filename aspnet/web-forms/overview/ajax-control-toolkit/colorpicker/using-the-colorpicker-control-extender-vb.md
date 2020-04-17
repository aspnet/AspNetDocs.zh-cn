---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用彩选器控件扩展器 （VB） |微软文档
author: rick-anderson
description: ColorPicker 是一个ASP.NET AJAX 扩展器，在弹出窗口控件中提供客户端选色功能和 UI。 它可以附加到任何ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542841"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="7c481-104">使用彩选器控件扩展器 （VB）</span><span class="sxs-lookup"><span data-stu-id="7c481-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="7c481-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7c481-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7c481-106">ColorPicker 是一个ASP.NET AJAX 扩展器，在弹出窗口控件中提供客户端选色功能和 UI。</span><span class="sxs-lookup"><span data-stu-id="7c481-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="7c481-107">它可以附加到任何ASP.NET文本框控件。</span><span class="sxs-lookup"><span data-stu-id="7c481-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="7c481-108">它。</span><span class="sxs-lookup"><span data-stu-id="7c481-108">It.</span></span>

<span data-ttu-id="7c481-109">本教程的目的是解释如何使用 AJAX 控件工具包 ColorPicker 控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="7c481-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="7c481-110">ColorPicker 控件扩展器显示一个弹出对话框，使您能够选择颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="7c481-111">当您要为用户提供直观的用户界面以选择颜色时，ColorPicker 非常有用。</span><span class="sxs-lookup"><span data-stu-id="7c481-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="7c481-112">使用彩选择器控件扩展器扩展文本框控件</span><span class="sxs-lookup"><span data-stu-id="7c481-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="7c481-113">例如，假设您想要创建一个网站，使访问者能够创建自定义的名片。</span><span class="sxs-lookup"><span data-stu-id="7c481-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="7c481-114">访问者可以输入名片的文本并选择颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="7c481-115">清单1中的ASP.NET页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="7c481-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="7c481-116">提交表单时，将显示所选值（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="7c481-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="7c481-117">[![创建名片的简单表单](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7c481-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="7c481-118">**图01：** 创建名片的简单表单（[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="7c481-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="7c481-119">**清单 1 - 创建卡.aspx**</span><span class="sxs-lookup"><span data-stu-id="7c481-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="7c481-120">清单1中的表单有效，但它不能提供出色的用户体验。</span><span class="sxs-lookup"><span data-stu-id="7c481-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="7c481-121">用户必须键入文本框中的颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="7c481-122">如果用户想要专用颜色（例如，只是豌豆绿色的正确阴影），则用户必须在没有任何帮助的情况下找出 HTML 颜色代码。</span><span class="sxs-lookup"><span data-stu-id="7c481-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="7c481-123">您可以使用 ColorPicker 控件扩展器来创建更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="7c481-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="7c481-124">将焦点移动到 TextBox 控件时，颜色选取器将显示颜色对话框（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="7c481-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="7c481-125">[![彩工控制扩展器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7c481-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="7c481-126">**图 02**： 彩选择器控件扩展器 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="7c481-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="7c481-127">您需要完成两个步骤才能将 ColorPicker 控件扩展器与清单 1 中的窗体一起使用：</span><span class="sxs-lookup"><span data-stu-id="7c481-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="7c481-128">将脚本管理器控件添加到页面</span><span class="sxs-lookup"><span data-stu-id="7c481-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="7c481-129">将彩选择器控件扩展器添加到页面</span><span class="sxs-lookup"><span data-stu-id="7c481-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="7c481-130">在使用 ColorPicker 之前，必须向页面添加脚本管理器。</span><span class="sxs-lookup"><span data-stu-id="7c481-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="7c481-131">添加脚本管理器的好地方就在打开的服务器端&lt;表单&gt;标记的正下方。</span><span class="sxs-lookup"><span data-stu-id="7c481-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="7c481-132">您可以将脚本管理器从工具箱拖到页面上（脚本管理器位于 AJAX 扩展选项卡下）。</span><span class="sxs-lookup"><span data-stu-id="7c481-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="7c481-133">或者，您可以在打开服务器端窗体标记下的源视图中键入以下标记：</span><span class="sxs-lookup"><span data-stu-id="7c481-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="7c481-134">&lt;asp：脚本管理器 ID="脚本管理器1"运行 at="服务器" /&gt;</span><span class="sxs-lookup"><span data-stu-id="7c481-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="7c481-135">将 ColorPicker 控件扩展器添加到页面的最简单方法是在"设计视图"中。</span><span class="sxs-lookup"><span data-stu-id="7c481-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="7c481-136">如果将鼠标悬停在 txtCardColor TextBox 上，将显示一个智能任务选项，使您能够添加扩展器（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="7c481-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="7c481-137">如果选择此选项，将显示扩展器向导（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="7c481-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="7c481-138">[![添加扩展器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7c481-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="7c481-139">**图 03**： 添加扩展器 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="7c481-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="7c481-140">[![使用扩展器向导选择控件扩展器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7c481-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="7c481-141">**图 04**：使用扩展器向导选择控件扩展器（[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="7c481-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="7c481-142">您可以选择颜色选取器扩展器，以便使用颜色选取器扩展器扩展 txtCardColor 文本盒。</span><span class="sxs-lookup"><span data-stu-id="7c481-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="7c481-143">单击“确定”，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="7c481-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="7c481-144">进行这些更改后，页面的源类似于清单 2。</span><span class="sxs-lookup"><span data-stu-id="7c481-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="7c481-145">**清单2 - CreateCard.aspx（带彩选器）**</span><span class="sxs-lookup"><span data-stu-id="7c481-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="7c481-146">请注意，该页面现在包含一个颜色选取器扩展器控件，该控件直接显示在 txtCardColor 文本盒控件的正下方。</span><span class="sxs-lookup"><span data-stu-id="7c481-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="7c481-147">颜色选取器扩展器控件扩展 txtCardColor 控件，以便显示颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="7c481-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="7c481-148">使用按钮启动颜色选取器对话框</span><span class="sxs-lookup"><span data-stu-id="7c481-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="7c481-149">颜色选取器扩展器支持以下属性：</span><span class="sxs-lookup"><span data-stu-id="7c481-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="7c481-150">弹出ButtonId - 页面上导致颜色选取器对话框显示的按钮的 ID。</span><span class="sxs-lookup"><span data-stu-id="7c481-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="7c481-151">弹出位置 - 颜色选取器对话框相对于目标控件的位置。</span><span class="sxs-lookup"><span data-stu-id="7c481-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="7c481-152">可能的值是"绝对"、"中心"、"左下"、"右下角"、"左上"、"右"、"左"（默认值为"左下"。</span><span class="sxs-lookup"><span data-stu-id="7c481-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="7c481-153">示例控制 Id - 显示所选颜色的控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="7c481-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="7c481-154">选择颜色 - 颜色选取器选择的初始颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="7c481-155">您可以使用这些属性自定义颜色选取器对话框的显示方式以及所选颜色的显示方式。</span><span class="sxs-lookup"><span data-stu-id="7c481-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="7c481-156">清单3中的页面说明了如何使用其中几个属性。</span><span class="sxs-lookup"><span data-stu-id="7c481-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="7c481-157">**清单3 - 创建卡按钮.aspx**</span><span class="sxs-lookup"><span data-stu-id="7c481-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="7c481-158">清单3中的页面包括"选取颜色"按钮（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="7c481-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="7c481-159">单击此按钮时，颜色选取器对话框将显示在 TextBox 上方。</span><span class="sxs-lookup"><span data-stu-id="7c481-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="7c481-160">如果从对话框中选择颜色，则所选颜色将显示为 lblSample 标签控件的背景颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="7c481-161">"颜色选取器弹出按钮ID"属性用于将"拾取颜色"按钮与"颜色选取器"扩展器相关联。</span><span class="sxs-lookup"><span data-stu-id="7c481-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="7c481-162">当您提供 PopupButtonID 属性的值时，当目标控件具有焦点时，颜色选取器对话框将不再显示。</span><span class="sxs-lookup"><span data-stu-id="7c481-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="7c481-163">您必须单击该按钮才能显示对话框。</span><span class="sxs-lookup"><span data-stu-id="7c481-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="7c481-164">SampleControlID 属性用于将显示所选颜色的控件与颜色选取器相关联。</span><span class="sxs-lookup"><span data-stu-id="7c481-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="7c481-165">颜色选取器将此控件的背景颜色更改为当前选择的颜色。</span><span class="sxs-lookup"><span data-stu-id="7c481-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="7c481-166">[![使用按钮显示颜色选取器对话框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7c481-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="7c481-167">**图 05**： 使用按钮显示颜色选取器对话框 （[单击以查看全尺寸图像](using-the-colorpicker-control-extender-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="7c481-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="7c481-168">总结</span><span class="sxs-lookup"><span data-stu-id="7c481-168">Summary</span></span>

<span data-ttu-id="7c481-169">在本教程中，您学习了如何使用 ColorPicker 控件扩展器来显示弹出颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="7c481-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="7c481-170">首先，我们检查了在焦点移动到 TextBox 控件时如何显示对话框。</span><span class="sxs-lookup"><span data-stu-id="7c481-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="7c481-171">接下来，您学习了如何在单击该按钮时创建显示颜色选取器对话框的按钮。</span><span class="sxs-lookup"><span data-stu-id="7c481-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7c481-172">上一篇</span><span class="sxs-lookup"><span data-stu-id="7c481-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)

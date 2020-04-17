---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: 使用 AJAX 控制工具包控制和控制扩展器 （VB） |微软文档
author: rick-anderson
description: 了解如何将 AJAX 控制工具包控件和扩展器添加到ASP.NET页。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 129d6841bc4db62ecbe5f26c4830d1ce2f199bff
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540007"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="113c3-103">使用 AJAX 控件工具包控件和控件扩展程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="113c3-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>

<span data-ttu-id="113c3-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="113c3-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="113c3-105">了解如何将 AJAX 控制工具包控件和扩展器添加到ASP.NET页。</span><span class="sxs-lookup"><span data-stu-id="113c3-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="113c3-106">AJAX 控制工具包包含一组控件和控制扩展器。</span><span class="sxs-lookup"><span data-stu-id="113c3-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="113c3-107">在本教程中，您将了解如何将控件和控制扩展器添加到ASP.NET页。</span><span class="sxs-lookup"><span data-stu-id="113c3-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="113c3-108">有关安装 AJAX 控制工具包并将 AJAX 控制工具包添加到可视化工作室/可视化 Web 开发人员工具包的说明，请参阅[有关 AJAX 控件工具包入门](get-started-with-the-ajax-control-toolkit-vb.md)教程。</span><span class="sxs-lookup"><span data-stu-id="113c3-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="113c3-109">使用 AJAX 控制工具包控件</span><span class="sxs-lookup"><span data-stu-id="113c3-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="113c3-110">AJAX 控制工具包控件的工作方式与普通ASP.NET控件类似。</span><span class="sxs-lookup"><span data-stu-id="113c3-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="113c3-111">您可以将控件从工具箱拖到ASP.NET页上。</span><span class="sxs-lookup"><span data-stu-id="113c3-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="113c3-112">您可以在"设计"视图或"源"视图中将控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="113c3-113">使用 AJAX 控制工具包中的控件时有一个特殊要求。</span><span class="sxs-lookup"><span data-stu-id="113c3-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="113c3-114">该页必须包含脚本管理器控件。</span><span class="sxs-lookup"><span data-stu-id="113c3-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="113c3-115">脚本管理器控件负责包括 AJAX 控制工具包控件所需的所有 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="113c3-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="113c3-116">例如，AJAX 控件工具包选项卡包括名为编辑器控件的控件。</span><span class="sxs-lookup"><span data-stu-id="113c3-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="113c3-117">此控件显示丰富的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="113c3-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="113c3-118">按照以下步骤将编辑器控件添加到页面：</span><span class="sxs-lookup"><span data-stu-id="113c3-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="113c3-119">创建新ASP.NET页面名为 ShowEditor.aspx</span><span class="sxs-lookup"><span data-stu-id="113c3-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="113c3-120">从工具箱中的 AJAX 扩展选项卡下方选择脚本管理器控件，并将该控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="113c3-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="113c3-121">从工具箱中的 AJAX 控制工具包选项卡下方选择编辑器控件，并将控件拖到页面上（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="113c3-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="113c3-122">设计器应如图 2 所示。</span><span class="sxs-lookup"><span data-stu-id="113c3-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="113c3-123">通过选择菜单选项 **"调试"、"开始调试**"或点击 F5 键来运行网站。</span><span class="sxs-lookup"><span data-stu-id="113c3-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="113c3-124">您应该会看到图 3 中的页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="113c3-125">[![选择 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span></span>

<span data-ttu-id="113c3-126">**图 01**：选择 HTML 编辑器控件（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>

<span data-ttu-id="113c3-127">[![具有脚本管理器和编辑控件的可视化工作室设计器](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span></span>

<span data-ttu-id="113c3-128">**图 02**： 具有脚本管理器和编辑控件的可视化工作室设计器（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>

<span data-ttu-id="113c3-129">[![显示编辑器.aspx 页面](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span></span>

<span data-ttu-id="113c3-130">**图 03**： 显示编辑器.aspx 页面（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="113c3-131">使用 AJAX 控制工具包控制扩展器</span><span class="sxs-lookup"><span data-stu-id="113c3-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="113c3-132">AJAX 控制工具包还包含控制扩展器。</span><span class="sxs-lookup"><span data-stu-id="113c3-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="113c3-133">顾名思义，控件扩展器扩展了现有控件的功能。</span><span class="sxs-lookup"><span data-stu-id="113c3-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="113c3-134">例如，"确认按钮"控件扩展器扩展了标准ASP.NET按钮控件。</span><span class="sxs-lookup"><span data-stu-id="113c3-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="113c3-135">扩展程序更改按钮控件的行为，以便单击按钮时显示确认对话框。</span><span class="sxs-lookup"><span data-stu-id="113c3-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="113c3-136">控件扩展器（与 AJAX 控件工具包控件一样）需要脚本管理器控件。</span><span class="sxs-lookup"><span data-stu-id="113c3-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="113c3-137">在开始使用页面中的控件扩展器之前，必须将脚本管理器控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="113c3-138">按照以下步骤使用确认按钮控件扩展器：</span><span class="sxs-lookup"><span data-stu-id="113c3-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="113c3-139">创建新ASP.NET页面名为"显示确认按钮.aspx"</span><span class="sxs-lookup"><span data-stu-id="113c3-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="113c3-140">通过将控件从 AJAX 扩展选项卡下方拖动到页面上，将脚本管理器控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="113c3-141">通过将"按钮"从工具箱中的"标准"选项卡下方拖动到"设计器"图面，将标准按钮控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="113c3-142">单击 **"添加扩展器**"任务选项（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="113c3-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="113c3-143">在"选择扩展器"对话框中，选择"确认按钮扩展器"（参见图 5），然后单击"确定"按钮。</span><span class="sxs-lookup"><span data-stu-id="113c3-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="113c3-144">选择设计器中的"按钮"控件并展开"属性"窗口中的\_Button1 确认按钮扩展器节点（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="113c3-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="113c3-145">将值 *"真的？"* 分配给"确认文本"属性。</span><span class="sxs-lookup"><span data-stu-id="113c3-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="113c3-146">通过选择菜单选项 **"调试"、"开始调试"** 或点击 F5 键来运行页面。</span><span class="sxs-lookup"><span data-stu-id="113c3-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="113c3-147">[![添加扩展器任务选项](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span></span>

<span data-ttu-id="113c3-148">**图 04**： 添加扩展器任务选项（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>

<span data-ttu-id="113c3-149">[![选择确认按钮控制扩展器](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span></span>

<span data-ttu-id="113c3-150">**图 05**： 选择确认按钮控件扩展器（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>

<span data-ttu-id="113c3-151">[![设置确认按钮属性](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span></span>

<span data-ttu-id="113c3-152">**图 06**： 设置确认按钮属性（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>

<span data-ttu-id="113c3-153">打开页面时，应看到一个按钮。</span><span class="sxs-lookup"><span data-stu-id="113c3-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="113c3-154">单击该按钮时，您将获得图 7 中的确认对话框。</span><span class="sxs-lookup"><span data-stu-id="113c3-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="113c3-155">[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="113c3-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span></span>

<span data-ttu-id="113c3-156">**图 07**： 显示确认对话框（[单击以查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="113c3-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>

<span data-ttu-id="113c3-157">请注意，您通常不会将控件扩展器拖动到页面上。</span><span class="sxs-lookup"><span data-stu-id="113c3-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="113c3-158">相反，您可以使用 **"添加扩展器**"任务选项将扩展器添加到已添加到页面的控件。</span><span class="sxs-lookup"><span data-stu-id="113c3-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="113c3-159">此外，请注意，通过打开要扩展的控件的属性表来设置控件扩展器属性。</span><span class="sxs-lookup"><span data-stu-id="113c3-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="113c3-160">单个ASP.NET控件可以通过多个控件扩展器进行扩展。</span><span class="sxs-lookup"><span data-stu-id="113c3-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="113c3-161">要扩展的控件的属性表将列出与控件关联的所有控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="113c3-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="113c3-162">[上一页](get-started-with-the-ajax-control-toolkit-vb.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="113c3-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>

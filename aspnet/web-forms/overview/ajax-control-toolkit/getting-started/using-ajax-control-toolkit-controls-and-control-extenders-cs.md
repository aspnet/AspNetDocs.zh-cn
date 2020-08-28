---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: '使用 AJAX 控件工具包控件和控件扩展程序 (c # ) |Microsoft Docs'
author: rick-anderson
description: 了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 48c8479fce6d121b8a4f03d972ac4117ed974958
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044501"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="db6bc-103">使用 AJAX 控件工具包控件和控件扩展程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="db6bc-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="db6bc-104">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="db6bc-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="db6bc-105">了解如何将 AJAX 控件工具包控件和扩展程序添加到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="db6bc-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="db6bc-106">AJAX 控件工具包包含一组控件和控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="db6bc-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="db6bc-107">本 brief 教程介绍如何将控件和控件扩展程序添加到 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="db6bc-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="db6bc-108">有关安装 AJAX 控件工具包并将 AJAX 控件工具包添加到 Visual Studio/Visual Web Developer 工具箱的说明，请参阅 [AJAX 控件工具包入门](get-started-with-the-ajax-control-toolkit-cs.md)教程。</span><span class="sxs-lookup"><span data-stu-id="db6bc-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="db6bc-109">使用 AJAX 控件工具包控件</span><span class="sxs-lookup"><span data-stu-id="db6bc-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="db6bc-110">AJAX 控件工具包控件的工作方式与常规 ASP.NET 控件的工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="db6bc-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="db6bc-111">可以将控件从 "工具箱" 拖动到 "ASP.NET" 页上。</span><span class="sxs-lookup"><span data-stu-id="db6bc-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="db6bc-112">可以在 "设计视图" 或 "源" 视图中将控件添加到该页。</span><span class="sxs-lookup"><span data-stu-id="db6bc-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="db6bc-113">使用 AJAX 控件工具包中的控件时，有一种特殊要求。</span><span class="sxs-lookup"><span data-stu-id="db6bc-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="db6bc-114">页面必须包含 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="db6bc-115">ScriptManager 控件负责包含 AJAX 控件工具包控件所需的所有必需 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="db6bc-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="db6bc-116">例如，"AJAX 控件工具包" 选项卡包含一个名为 "编辑器控件" 的控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="db6bc-117">此控件显示丰富的 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="db6bc-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="db6bc-118">按照以下步骤将编辑器控件添加到页面：</span><span class="sxs-lookup"><span data-stu-id="db6bc-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="db6bc-119">创建名为 ShowEditor 的新 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="db6bc-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="db6bc-120">从 "工具箱" 中的 "AJAX 扩展" 选项卡下选择 "ScriptManager" 控件，并将该控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="db6bc-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="db6bc-121">从 "工具箱" 中的 "AJAX 控件工具包" 选项卡下选择编辑器控件，并将控件拖到页面上 (参阅图 1) 。</span><span class="sxs-lookup"><span data-stu-id="db6bc-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="db6bc-122">设计器应类似于图2。</span><span class="sxs-lookup"><span data-stu-id="db6bc-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="db6bc-123">通过选择菜单选项 " **调试"、"开始调试"** 或按 F5 键运行网站。</span><span class="sxs-lookup"><span data-stu-id="db6bc-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="db6bc-124">你应会看到图3中的页面。</span><span class="sxs-lookup"><span data-stu-id="db6bc-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="db6bc-125">[![选择 HTML 编辑器控件](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="db6bc-126">**图 01**：选择 HTML 编辑器控件 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>

<span data-ttu-id="db6bc-127">[![带有 ScriptManager 和编辑控件的 Visual Studio 设计器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="db6bc-128">**图 02**：包含 ScriptManager 和编辑控件的 Visual Studio 设计器 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>

<span data-ttu-id="db6bc-129">[![DisplayEditor 页](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="db6bc-130">**图 03**： DisplayEditor 页 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="db6bc-131">使用 AJAX 控件工具包控件扩展程序</span><span class="sxs-lookup"><span data-stu-id="db6bc-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="db6bc-132">AJAX 控件工具包还包含控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="db6bc-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="db6bc-133">顾名思义，控件扩展器扩展了现有控件的功能。</span><span class="sxs-lookup"><span data-stu-id="db6bc-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="db6bc-134">例如，ConfirmButton 控件扩展器扩展了标准 ASP.NET 按钮控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="db6bc-135">扩展器将更改按钮控件的行为，以便在单击按钮时显示确认对话框。</span><span class="sxs-lookup"><span data-stu-id="db6bc-135">The extender changes the Button control's behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="db6bc-136">像 AJAX 控件工具包控件一样，控件扩展器需要 ScriptManager 控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="db6bc-137">在开始使用页面中的控件扩展器之前，必须将 ScriptManager 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="db6bc-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="db6bc-138">请按照以下步骤使用 ConfirmButton 控件扩展器：</span><span class="sxs-lookup"><span data-stu-id="db6bc-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="db6bc-139">创建名为 ShowConfirmButton 的新 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="db6bc-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="db6bc-140">通过将控件从 "AJAX 扩展" 选项卡下拖到页面上，将 ScriptManager 控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="db6bc-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="db6bc-141">通过从工具箱中的 "标准" 选项卡下将按钮拖到设计器图面上，将标准按钮控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="db6bc-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="db6bc-142">单击 " **添加扩展** 器任务" 选项 (参阅图 4) 。</span><span class="sxs-lookup"><span data-stu-id="db6bc-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="db6bc-143">在 "选择扩展器" 对话框中，选择 "ConfirmButtonExtender (参阅图 5) 并单击" 确定 "按钮。</span><span class="sxs-lookup"><span data-stu-id="db6bc-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="db6bc-144">在设计器中选择 "Button" 控件，在属性窗口中展开 "Button1"、 \_ "Button1 ConfirmButtonExtender" 节点 (参见图 6) 。</span><span class="sxs-lookup"><span data-stu-id="db6bc-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="db6bc-145">将值 *"真的？"*</span><span class="sxs-lookup"><span data-stu-id="db6bc-145">Assign the value *'Really?'*</span></span> <span data-ttu-id="db6bc-146">到 ConfirmText 属性。</span><span class="sxs-lookup"><span data-stu-id="db6bc-146">to the ConfirmText property.</span></span>
7. <span data-ttu-id="db6bc-147">通过选择菜单选项 " **调试"、"开始调试** " 或按 F5 键来运行页面。</span><span class="sxs-lookup"><span data-stu-id="db6bc-147">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="db6bc-148">[!["添加扩展器任务" 选项](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-148">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="db6bc-149">**图 04**： "添加扩展器任务" 选项 ([单击以查看完全大小的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-149">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>

<span data-ttu-id="db6bc-150">[![选择 ConfirmButton 控件扩展器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-150">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="db6bc-151">**图 05**：选择 ConfirmButton 控件扩展器 ([单击查看完全大小的图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-151">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>

<span data-ttu-id="db6bc-152">[![设置 ConfirmButton 属性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-152">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="db6bc-153">**图 06**：设置 ConfirmButton 属性 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-153">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>

<span data-ttu-id="db6bc-154">当该页打开时，您应该会看到一个按钮。</span><span class="sxs-lookup"><span data-stu-id="db6bc-154">When the page opens, you should see a button.</span></span> <span data-ttu-id="db6bc-155">单击该按钮时，会收到图7所示的确认对话框。</span><span class="sxs-lookup"><span data-stu-id="db6bc-155">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="db6bc-156">[![显示确认对话框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="db6bc-156">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="db6bc-157">**图 07**：显示确认对话框 ([单击查看全尺寸图像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)) </span><span class="sxs-lookup"><span data-stu-id="db6bc-157">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>

<span data-ttu-id="db6bc-158">请注意，通常不会将控件扩展器拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="db6bc-158">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="db6bc-159">相反，可以使用 " **添加扩展** 器任务" 选项将扩展器添加到已添加到页面的控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-159">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="db6bc-160">此外，请注意，您可以通过打开要扩展的控件的属性表来设置控件扩展器属性。</span><span class="sxs-lookup"><span data-stu-id="db6bc-160">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="db6bc-161">多个控件扩展程序可以扩展单个 ASP.NET 控件。</span><span class="sxs-lookup"><span data-stu-id="db6bc-161">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="db6bc-162">要扩展的控件的属性表将列出与该控件关联的所有控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="db6bc-162">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="db6bc-163">[上一页](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="db6bc-163">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>

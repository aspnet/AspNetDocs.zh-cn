---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: 开始使用 AJAX 控制工具包 （VB） |微软文档
author: rick-anderson
description: 了解开始使用 AJAX 控制工具包所需的所有知识。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543556"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="47d70-103">AJAX 控件工具包入门 (VB)</span><span class="sxs-lookup"><span data-stu-id="47d70-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="47d70-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="47d70-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="47d70-105">了解开始使用 AJAX 控制工具包所需的所有知识。</span><span class="sxs-lookup"><span data-stu-id="47d70-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="47d70-106">AJAX 控制工具包包含 30 多个免费控件，可用于ASP.NET应用程序中。</span><span class="sxs-lookup"><span data-stu-id="47d70-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="47d70-107">在本教程中，您将了解如何下载 AJAX 控件工具包，并将工具包控件添加到可视化工作室/可视化 Web 开发人员快速工具箱。</span><span class="sxs-lookup"><span data-stu-id="47d70-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="47d70-108">下载 AJAX 控制工具包</span><span class="sxs-lookup"><span data-stu-id="47d70-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="47d70-109">[AJAX 控制工具包](http://devexpress.com/act)是由ASP.NET社区成员和ASP.NET团队开发的开源项目。</span><span class="sxs-lookup"><span data-stu-id="47d70-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="47d70-110">[![下载 AJAX 控制工具包](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47d70-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="47d70-111">**图 01**： 下载 AJAX 控制工具包（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="47d70-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="47d70-112">下载文件后，需要取消阻止该文件。</span><span class="sxs-lookup"><span data-stu-id="47d70-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="47d70-113">右键单击文件，选择"属性"，然后单击 **"取消阻止"** 按钮（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="47d70-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="47d70-114">[![取消阻止 AJAX 控制工具包 ZIP 文件](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="47d70-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="47d70-115">**图 02**： 取消阻止 AJAX 控制工具包 ZIP 文件（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="47d70-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="47d70-116">取消阻止文件后，可以解压缩文件：右键单击该文件并选择 **"全部提取"** 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="47d70-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="47d70-117">现在，我们准备将工具包添加到可视化工作室/可视化 Web 开发人员工具箱。</span><span class="sxs-lookup"><span data-stu-id="47d70-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="47d70-118">将 AJAX 控制工具包添加到工具箱</span><span class="sxs-lookup"><span data-stu-id="47d70-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="47d70-119">使用 AJAX 控制工具包的最简单方法是将工具包添加到可视化工作室/可视化 Web 开发人员工具箱（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="47d70-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="47d70-120">这样，您只需在要使用工具包控件时将其拖到页面上即可。</span><span class="sxs-lookup"><span data-stu-id="47d70-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="47d70-121">[![AJAX 控制工具包显示在工具箱中](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="47d70-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="47d70-122">**图 03**： AJAX 控制工具包显示在工具箱中（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="47d70-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="47d70-123">首先，您需要向工具箱添加 AJAX 控制工具包选项卡。</span><span class="sxs-lookup"><span data-stu-id="47d70-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="47d70-124">执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="47d70-124">Follow these steps.</span></span>

1. <span data-ttu-id="47d70-125">通过选择菜单选项"文件，新网站"，创建新ASP.NET网站。</span><span class="sxs-lookup"><span data-stu-id="47d70-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="47d70-126">双击解决方案资源管理器窗口中的 Default.aspx 以在编辑器中打开该文件。</span><span class="sxs-lookup"><span data-stu-id="47d70-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="47d70-127">右键单击"常规选项卡"下方的工具框，然后选择菜单选项 **"添加选项卡**"（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="47d70-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="47d70-128">输入名为 AJAX 控制工具包的新选项卡。</span><span class="sxs-lookup"><span data-stu-id="47d70-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="47d70-129">[![添加新选项卡](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="47d70-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="47d70-130">**图 04**：添加新选项卡（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="47d70-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="47d70-131">接下来，您需要将 AJAX 控件工具包控件添加到新选项卡中。按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="47d70-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="47d70-132">右键单击 AJAX 控制工具包选项卡下方，然后选择菜单选项 **"选择项目"（参见图 5）。**</span><span class="sxs-lookup"><span data-stu-id="47d70-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="47d70-133">浏览到解压缩 AJAX 控制工具包的位置，然后选择 AjaxControlToolkit.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="47d70-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="47d70-134">[![选择要添加到工具箱的项目](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="47d70-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="47d70-135">**图 05**： 选择要添加到工具箱的项目（[单击以查看全尺寸图像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="47d70-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="47d70-136">完成这些步骤后，所有工具包控件都将显示在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="47d70-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="47d70-137">升级到新版本的工具包</span><span class="sxs-lookup"><span data-stu-id="47d70-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="47d70-138">如果您使用的是旧版本的工具包，现在需要移动到更高版本，下面是建议的步骤：</span><span class="sxs-lookup"><span data-stu-id="47d70-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="47d70-139">二进制 - 从您的网站 Bin 文件夹中删除 AjaxControlToolkit.dll 程序集的旧版本。</span><span class="sxs-lookup"><span data-stu-id="47d70-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="47d70-140">工具箱项目 - 删除 AJAX 控制工具包选项卡，然后按照上述步骤重新创建具有新版本 AjaxControlToolkit.dll 程序集的选项卡。</span><span class="sxs-lookup"><span data-stu-id="47d70-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="47d70-141">[上一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一页](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="47d70-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>

---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: '创建自定义 AJAX 控件工具包控件扩展器 (c # ) |Microsoft Docs'
author: rick-anderson
description: 自定义扩展程序使你可以自定义和扩展 ASP.NET 控件的功能，而无需创建新类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 2522f22c80ebd34cd5adbb0ada51fd7755029426
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044657"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a><span data-ttu-id="3507b-103">创建自定义 AJAX 控件工具包控件扩展程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="3507b-103">Creating a Custom AJAX Control Toolkit Control Extender (C#)</span></span>

<span data-ttu-id="3507b-104">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3507b-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3507b-105">自定义扩展程序使你可以自定义和扩展 ASP.NET 控件的功能，而无需创建新类。</span><span class="sxs-lookup"><span data-stu-id="3507b-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="3507b-106">在本教程中，将了解如何创建自定义 AJAX 控件工具包控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="3507b-107">我们创建了一个简单但有用的新扩展器，该扩展程序将按钮的状态从 "已禁用" 更改为 "已启用"，以便在文本框中键入文本。</span><span class="sxs-lookup"><span data-stu-id="3507b-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="3507b-108">阅读本教程后，你将能够用自己的控件扩展器扩展 ASP.NET AJAX 工具包。</span><span class="sxs-lookup"><span data-stu-id="3507b-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="3507b-109">你可以使用 Visual Studio 或 Visual Web Developer 创建自定义控件扩展程序 (确保使用最新版本的 Visual Web Developer) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="3507b-110">DisabledButton 扩展器概述</span><span class="sxs-lookup"><span data-stu-id="3507b-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="3507b-111">新的控件扩展器命名为 DisabledButton 扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="3507b-112">此扩展器将有三个属性：</span><span class="sxs-lookup"><span data-stu-id="3507b-112">This extender will have three properties:</span></span>

- <span data-ttu-id="3507b-113">TargetControlID-控件扩展的文本框。</span><span class="sxs-lookup"><span data-stu-id="3507b-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="3507b-114">TargetButtonIID-已禁用或已启用的按钮。</span><span class="sxs-lookup"><span data-stu-id="3507b-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="3507b-115">DisabledText-按钮中最初显示的文本。</span><span class="sxs-lookup"><span data-stu-id="3507b-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="3507b-116">开始键入时，按钮会显示 "按钮文本" 属性的值。</span><span class="sxs-lookup"><span data-stu-id="3507b-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="3507b-117">将 DisabledButton 扩展器挂钩到 TextBox 和 Button 控件。</span><span class="sxs-lookup"><span data-stu-id="3507b-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="3507b-118">键入任何文本之前，按钮将被禁用，文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="3507b-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

<span data-ttu-id="3507b-119"> ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span></span>

<span data-ttu-id="3507b-120">开始键入文本后，按钮将启用，文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="3507b-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

<span data-ttu-id="3507b-121"> ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="3507b-122">若要创建控件扩展器，需要创建以下三个文件：</span><span class="sxs-lookup"><span data-stu-id="3507b-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="3507b-123">DisabledButtonExtender.cs-此文件是服务器端控件类，将管理创建扩展器，并允许您在设计时设置属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-123">DisabledButtonExtender.cs - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="3507b-124">它还定义了可在扩展器上设置的属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="3507b-125">这些属性可通过代码和设计时访问，并与 DisableButtonBehavior.js 文件中定义的属性相匹配。</span><span class="sxs-lookup"><span data-stu-id="3507b-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="3507b-126">DisabledButtonBehavior.js--在此文件中，你将添加所有客户端脚本逻辑。</span><span class="sxs-lookup"><span data-stu-id="3507b-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="3507b-127">DisabledButtonDesigner.cs-此类启用设计时功能。</span><span class="sxs-lookup"><span data-stu-id="3507b-127">DisabledButtonDesigner.cs - This class enables design-time functionality.</span></span> <span data-ttu-id="3507b-128">如果希望控件扩展器能够正常使用 Visual Studio/Visual Web Developer 设计器，则需要此类。</span><span class="sxs-lookup"><span data-stu-id="3507b-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="3507b-129">因此，控件扩展器由服务器端控件、客户端行为和服务器端设计器类组成。</span><span class="sxs-lookup"><span data-stu-id="3507b-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="3507b-130">你将在以下部分中了解如何创建这三个文件。</span><span class="sxs-lookup"><span data-stu-id="3507b-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="3507b-131">创建自定义扩展器网站和项目</span><span class="sxs-lookup"><span data-stu-id="3507b-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="3507b-132">第一步是在 Visual Studio/Visual Web Developer 中创建类库项目和网站。</span><span class="sxs-lookup"><span data-stu-id="3507b-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="3507b-133">我们会在类库项目中创建自定义扩展器，并测试网站中的自定义扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-133">We'll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="3507b-134">让我们从网站开始。</span><span class="sxs-lookup"><span data-stu-id="3507b-134">Let's start with the website.</span></span> <span data-ttu-id="3507b-135">按照以下步骤创建网站：</span><span class="sxs-lookup"><span data-stu-id="3507b-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="3507b-136">选择菜单选项 " **文件" "新建**网站"。</span><span class="sxs-lookup"><span data-stu-id="3507b-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="3507b-137">选择 **ASP.NET** 网站模板。</span><span class="sxs-lookup"><span data-stu-id="3507b-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="3507b-138">将新网站命名为 " *Website1*"。</span><span class="sxs-lookup"><span data-stu-id="3507b-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="3507b-139">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="3507b-139">Click the **OK** button.</span></span>

<span data-ttu-id="3507b-140">接下来，我们需要创建一个类库项目，该项目将包含控件扩展程序的代码：</span><span class="sxs-lookup"><span data-stu-id="3507b-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="3507b-141">选择菜单选项 **文件 "添加" "新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3507b-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="3507b-142">选择 " **类库** " 模板。</span><span class="sxs-lookup"><span data-stu-id="3507b-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="3507b-143">将名为 **CustomExtenders**的新类库命名为。</span><span class="sxs-lookup"><span data-stu-id="3507b-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="3507b-144">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="3507b-144">Click the **OK** button.</span></span>

<span data-ttu-id="3507b-145">完成这些步骤后，"解决方案资源管理器" 窗口应如图1所示。</span><span class="sxs-lookup"><span data-stu-id="3507b-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="3507b-146">[![包含网站和类库项目的解决方案](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="3507b-147">**图 01**：包含网站和类库项目的解决方案 ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span></span>

<span data-ttu-id="3507b-148">接下来，需要将所有必需的程序集引用添加到类库项目中：</span><span class="sxs-lookup"><span data-stu-id="3507b-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="3507b-149">右键单击 "CustomExtenders" 项目，然后选择 " **添加引用**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="3507b-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="3507b-150">选择 .NET 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3507b-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="3507b-151">添加对下列程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="3507b-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="3507b-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="3507b-152">System.Web.dll</span></span>
    2. <span data-ttu-id="3507b-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="3507b-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="3507b-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="3507b-154">System.Design.dll</span></span>
    4. <span data-ttu-id="3507b-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="3507b-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="3507b-156">单击“浏览”选项卡。</span><span class="sxs-lookup"><span data-stu-id="3507b-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="3507b-157">向 AjaxControlToolkit.dll 程序集添加引用。</span><span class="sxs-lookup"><span data-stu-id="3507b-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="3507b-158">此程序集位于下载 AJAX 控件工具包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="3507b-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="3507b-159">完成这些步骤后，类库项目的 "引用" 文件夹应如图2所示。</span><span class="sxs-lookup"><span data-stu-id="3507b-159">After you complete these steps, your class library project References folder should look like Figure 2.</span></span>

<span data-ttu-id="3507b-160">[![引用具有所需引用的文件夹](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span></span>

<span data-ttu-id="3507b-161">**图 02**：引用具有所需引用的文件夹 ([单击查看完全大小的图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="3507b-162">创建自定义控件扩展器</span><span class="sxs-lookup"><span data-stu-id="3507b-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="3507b-163">现在我们有了类库，接下来我们可以开始构建扩展器控件。</span><span class="sxs-lookup"><span data-stu-id="3507b-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="3507b-164">让我们从自定义扩展程序控件类的 bare 骨骼开始 (参阅列出 1) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-164">Let's start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="3507b-165">**列表 1-MyCustomExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="3507b-165">**Listing 1 - MyCustomExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

<span data-ttu-id="3507b-166">有关列表1中的控件扩展器类，有几个方面需要注意。</span><span class="sxs-lookup"><span data-stu-id="3507b-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="3507b-167">首先，请注意该类继承自基 ExtenderControlBase 类。</span><span class="sxs-lookup"><span data-stu-id="3507b-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="3507b-168">所有 AJAX 控件工具包扩展程序控件都从此基类派生。</span><span class="sxs-lookup"><span data-stu-id="3507b-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="3507b-169">例如，基类包含 TargetID 属性，该属性是每个控件扩展器的必需属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="3507b-170">接下来，请注意，类包含以下两个与客户端脚本相关的属性：</span><span class="sxs-lookup"><span data-stu-id="3507b-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="3507b-171">WebResource-使文件作为嵌入资源包含在程序集中。</span><span class="sxs-lookup"><span data-stu-id="3507b-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="3507b-172">ClientScriptResource-导致从程序集检索脚本资源。</span><span class="sxs-lookup"><span data-stu-id="3507b-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="3507b-173">当编译自定义扩展器时，WebResource 属性用于将 MyControlBehavior.js JavaScript 文件嵌入到程序集中。</span><span class="sxs-lookup"><span data-stu-id="3507b-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="3507b-174">当在网页中使用自定义扩展器时，ClientScriptResource 属性用于从程序集中检索 MyControlBehavior.js 脚本。</span><span class="sxs-lookup"><span data-stu-id="3507b-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="3507b-175">为了使 WebResource 和 ClientScriptResource 属性正常工作，必须将 JavaScript 文件编译为嵌入的资源。</span><span class="sxs-lookup"><span data-stu-id="3507b-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="3507b-176">在 "解决方案资源管理器" 窗口中选择文件，打开属性表，并将值 " *嵌入资源* " 分配给 " **生成操作** " 属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="3507b-177">请注意，控件扩展器还包括 TargetControlType 属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="3507b-178">此属性用于指定控件扩展器所扩展的控件类型。</span><span class="sxs-lookup"><span data-stu-id="3507b-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="3507b-179">对于列表1，控件扩展器用于扩展文本框。</span><span class="sxs-lookup"><span data-stu-id="3507b-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="3507b-180">最后请注意，自定义扩展器包含一个名为 T.myproperty 的属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="3507b-181">该属性标记有 ExtenderControlProperty 特性。</span><span class="sxs-lookup"><span data-stu-id="3507b-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="3507b-182">GetPropertyValue ( # A1 和 SetPropertyValue ( # A3 方法用于将属性值从服务器端控件扩展程序传递到客户端行为。</span><span class="sxs-lookup"><span data-stu-id="3507b-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="3507b-183">接下来，实现 DisabledButton 扩展器的代码。</span><span class="sxs-lookup"><span data-stu-id="3507b-183">Let's go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="3507b-184">此扩展器的代码可以在 "清单 2" 中找到。</span><span class="sxs-lookup"><span data-stu-id="3507b-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="3507b-185">**列表 2-DisabledButtonExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="3507b-185">**Listing 2 - DisabledButtonExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

<span data-ttu-id="3507b-186">清单2中的 DisabledButton 扩展器具有两个名为 TargetButtonID 和 DisabledText 的属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="3507b-187">应用于 TargetButtonID 属性的 IDReferenceProperty 阻止你将 Button 控件的 ID 之外的任何内容分配给此属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="3507b-188">WebResource 和 ClientScriptResource 属性将位于名为 DisabledButtonBehavior.js 的文件中的客户端行为与此扩展器相关联。</span><span class="sxs-lookup"><span data-stu-id="3507b-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="3507b-189">我们将在下一节中讨论此 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="3507b-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="3507b-190">创建自定义扩展器行为</span><span class="sxs-lookup"><span data-stu-id="3507b-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="3507b-191">控件扩展器的客户端组件称为行为。</span><span class="sxs-lookup"><span data-stu-id="3507b-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="3507b-192">"禁用" 和 "启用" 按钮的实际逻辑包含在 DisabledButton 行为中。</span><span class="sxs-lookup"><span data-stu-id="3507b-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="3507b-193">此行为的 JavaScript 代码包含在列表3中。</span><span class="sxs-lookup"><span data-stu-id="3507b-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="3507b-194">**列表 3-DisabledButton.js**</span><span class="sxs-lookup"><span data-stu-id="3507b-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

<span data-ttu-id="3507b-195">清单3中的 JavaScript 文件包含名为 DisabledButtonBehavior 的客户端类。</span><span class="sxs-lookup"><span data-stu-id="3507b-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="3507b-196">此类与服务器端克隆类似，它包含两个名为 TargetButtonID 和 DisabledText 的属性，可以使用 get \_ TargetButtonID/set \_ TargetButtonID 和 \_ DisabledText/set \_ DisabledText 来访问这些属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="3507b-197">Initialize ( # A1 方法将一个 keyup 事件处理程序与该行为的目标元素相关联。</span><span class="sxs-lookup"><span data-stu-id="3507b-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="3507b-198">每次在与此行为相关联的文本框中键入字母时，keyup 处理程序都将执行。</span><span class="sxs-lookup"><span data-stu-id="3507b-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="3507b-199">Keyup 处理程序启用或禁用该按钮，具体取决于与该行为关联的文本框是否包含任何文本。</span><span class="sxs-lookup"><span data-stu-id="3507b-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="3507b-200">请记住，你必须将清单3中的 JavaScript 文件编译为嵌入资源。</span><span class="sxs-lookup"><span data-stu-id="3507b-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="3507b-201">在 "解决方案资源管理器" 窗口中选择文件，打开属性表，并将值 " *嵌入资源* " 分配给 " **生成操作** " 属性 (参见图 3) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="3507b-202">Visual Studio 和 Visual Web Developer 中都提供了此选项。</span><span class="sxs-lookup"><span data-stu-id="3507b-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="3507b-203">[![将 JavaScript 文件添加为嵌入资源](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span></span>

<span data-ttu-id="3507b-204">**图 03**：添加作为嵌入资源的 JavaScript 文件 ([单击查看完全大小的图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="3507b-205">创建自定义扩展器设计器</span><span class="sxs-lookup"><span data-stu-id="3507b-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="3507b-206">需要创建一个最后一个类来完成扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="3507b-207">需要在列表4中创建设计器类。</span><span class="sxs-lookup"><span data-stu-id="3507b-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="3507b-208">此类是使扩展程序正确运行 Visual Studio/Visual Web Developer 设计器所必需的。</span><span class="sxs-lookup"><span data-stu-id="3507b-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="3507b-209">**列表 4-DisabledButtonDesigner.cs**</span><span class="sxs-lookup"><span data-stu-id="3507b-209">**Listing 4 - DisabledButtonDesigner.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

<span data-ttu-id="3507b-210">将清单4中的设计器与具有设计器属性的 DisabledButton 扩展器相关联。需要将设计器属性应用于 DisabledButtonExtender 类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3507b-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="3507b-211">使用自定义扩展器</span><span class="sxs-lookup"><span data-stu-id="3507b-211">Using the Custom Extender</span></span>

<span data-ttu-id="3507b-212">现在，我们已完成了 DisabledButton 控件扩展器的创建，接下来可以在我们的 ASP.NET 网站中使用它。</span><span class="sxs-lookup"><span data-stu-id="3507b-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="3507b-213">首先，需要将自定义扩展器添加到 "工具箱"。</span><span class="sxs-lookup"><span data-stu-id="3507b-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="3507b-214">执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3507b-214">Follow these steps:</span></span>

1. <span data-ttu-id="3507b-215">双击 "解决方案资源管理器" 窗口中的页面，打开 "ASP.NET" 页。</span><span class="sxs-lookup"><span data-stu-id="3507b-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="3507b-216">右键单击 "工具箱"，然后选择菜单选项 " **选择项**"。</span><span class="sxs-lookup"><span data-stu-id="3507b-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="3507b-217">在 "选择工具箱项" 对话框中，浏览到 CustomExtenders.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="3507b-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="3507b-218">单击 **"确定"** 按钮关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="3507b-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="3507b-219">完成这些步骤后，DisabledButton 控件扩展器应显示在工具箱中 (参见图 4) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="3507b-220">[![工具箱中的 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span></span>

<span data-ttu-id="3507b-221">**图 04**：工具箱中的 DisabledButton ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span></span>

<span data-ttu-id="3507b-222">接下来，我们需要创建一个新的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="3507b-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="3507b-223">执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3507b-223">Follow these steps:</span></span>

1. <span data-ttu-id="3507b-224">创建名为 ShowDisabledButton 的新 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="3507b-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="3507b-225">将 ScriptManager 拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="3507b-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="3507b-226">将 TextBox 控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="3507b-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="3507b-227">将一个 "按钮" 控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="3507b-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="3507b-228">在属性窗口中，将 "Button ID" 属性更改为值 " <em>btnsave.dock</em> "，并将 "Text" 属性更改为值\*Save \* \*。</span><span class="sxs-lookup"><span data-stu-id="3507b-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="3507b-229">我们创建了一个包含标准 ASP.NET 文本框和按钮控件的页面。</span><span class="sxs-lookup"><span data-stu-id="3507b-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="3507b-230">接下来，我们需要扩展 TextBox 控件和 DisabledButton 扩展器：</span><span class="sxs-lookup"><span data-stu-id="3507b-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="3507b-231">选择 " **添加扩展** 器任务" 选项以打开扩展器向导对话框 (参阅图 5) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="3507b-232">请注意，此对话框包含我们的自定义 DisabledButton 扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="3507b-233">选择 DisabledButton 扩展器，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3507b-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="3507b-234">[![扩展器向导对话框](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span></span>

<span data-ttu-id="3507b-235">**图 05**：扩展器向导对话框 ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span></span>

<span data-ttu-id="3507b-236">最后，我们可以设置 DisabledButton 扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="3507b-237">可以通过修改 TextBox 控件的属性来修改 DisabledButton 扩展器的属性：</span><span class="sxs-lookup"><span data-stu-id="3507b-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="3507b-238">在设计器中选择文本框。</span><span class="sxs-lookup"><span data-stu-id="3507b-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="3507b-239">在属性窗口中，展开 "扩展器" 节点 (参见图 6) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="3507b-240">将值 *Save* 赋给 DisabledText 属性，并将值 *Btnsave.dock* 分配到 TargetButtonID 属性。</span><span class="sxs-lookup"><span data-stu-id="3507b-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="3507b-241">[![设置扩展器属性](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span></span>

<span data-ttu-id="3507b-242">**图 06**：设置扩展器属性 ([单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span></span>

<span data-ttu-id="3507b-243">通过按 F5)  (运行页面时，按钮控件最初处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="3507b-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="3507b-244">开始在文本框中输入文本后，会立即启用 Button 控件 (参见图 7) 。</span><span class="sxs-lookup"><span data-stu-id="3507b-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="3507b-245">[![操作中的 DisabledButton 扩展器](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="3507b-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span></span>

<span data-ttu-id="3507b-246">**图 07**：操作 (中的 DisabledButton 扩展器 [单击查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)) </span><span class="sxs-lookup"><span data-stu-id="3507b-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="3507b-247">摘要</span><span class="sxs-lookup"><span data-stu-id="3507b-247">Summary</span></span>

<span data-ttu-id="3507b-248">本教程的目的是说明如何通过自定义扩展器控件扩展 AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="3507b-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="3507b-249">在本教程中，我们创建了一个简单的 DisabledButton 控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="3507b-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="3507b-250">我们通过创建 DisabledButtonExtender 类、DisabledButtonBehavior JavaScript 行为和 DisabledButtonDesigner 类实现了这种扩展。</span><span class="sxs-lookup"><span data-stu-id="3507b-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="3507b-251">每当创建自定义控件扩展器时，都应遵循一组类似的步骤。</span><span class="sxs-lookup"><span data-stu-id="3507b-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3507b-252">[上一页](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [下一页](get-started-with-the-ajax-control-toolkit-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3507b-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
[Next](get-started-with-the-ajax-control-toolkit-vb.md)</span></span>

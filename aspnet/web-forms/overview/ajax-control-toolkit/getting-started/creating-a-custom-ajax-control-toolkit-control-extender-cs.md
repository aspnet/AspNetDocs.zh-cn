---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 创建自定义 AJAX 控制工具包控制扩展器 （C#） |微软文档
author: rick-anderson
description: 自定义扩展程序使您能够自定义和扩展ASP.NET控件的功能，而无需创建新类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543023"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a><span data-ttu-id="c22d1-103">创建自定义 AJAX 控件工具包控件扩展程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="c22d1-103">Creating a Custom AJAX Control Toolkit Control Extender (C#)</span></span>

<span data-ttu-id="c22d1-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c22d1-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c22d1-105">自定义扩展程序使您能够自定义和扩展ASP.NET控件的功能，而无需创建新类。</span><span class="sxs-lookup"><span data-stu-id="c22d1-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="c22d1-106">在本教程中，您将了解如何创建自定义 AJAX 控件工具包控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="c22d1-107">我们创建一个简单但有用的新扩展器，当您在 TextBox 中键入文本时，将按钮的状态从禁用更改为启用。</span><span class="sxs-lookup"><span data-stu-id="c22d1-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="c22d1-108">阅读本教程后，您将能够使用自己的控件扩展器扩展ASP.NET AJAX 工具包。</span><span class="sxs-lookup"><span data-stu-id="c22d1-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="c22d1-109">您可以使用可视化工作室或可视化 Web 开发人员创建自定义控件扩展器（请确保您具有最新版本的可视化 Web 开发人员）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="c22d1-110">禁用按钮扩展器概述</span><span class="sxs-lookup"><span data-stu-id="c22d1-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="c22d1-111">我们的新控制扩展器被命名为禁用按钮扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="c22d1-112">此扩展器将有三个属性：</span><span class="sxs-lookup"><span data-stu-id="c22d1-112">This extender will have three properties:</span></span>

- <span data-ttu-id="c22d1-113">目标控制ID - 控件扩展的文本框。</span><span class="sxs-lookup"><span data-stu-id="c22d1-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="c22d1-114">目标ButtonIID - 已禁用或启用的按钮。</span><span class="sxs-lookup"><span data-stu-id="c22d1-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="c22d1-115">禁用文本 - 最初显示在按钮中的文本。</span><span class="sxs-lookup"><span data-stu-id="c22d1-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="c22d1-116">开始键入时，按钮将显示按钮文本属性的值。</span><span class="sxs-lookup"><span data-stu-id="c22d1-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="c22d1-117">将"禁用按钮扩展器"挂到文本框和按钮控件。</span><span class="sxs-lookup"><span data-stu-id="c22d1-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="c22d1-118">键入任何文本之前，将禁用"按钮"，文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="c22d1-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

<span data-ttu-id="c22d1-119">（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span></span>

<span data-ttu-id="c22d1-120">开始键入文本后，将启用"按钮"，文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="c22d1-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

<span data-ttu-id="c22d1-121">（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="c22d1-122">要创建我们的控件扩展器，我们需要创建以下三个文件：</span><span class="sxs-lookup"><span data-stu-id="c22d1-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="c22d1-123">DisabledButtonExtender.cs - 此文件是服务器端控制类，用于管理创建扩展器，并允许您在设计时设置属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-123">DisabledButtonExtender.cs - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="c22d1-124">它还定义可以在扩展器上设置的属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="c22d1-125">这些属性可通过代码和设计时间访问，并匹配在禁用ButtonBehavior.js文件中定义的属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="c22d1-126">禁用ButtonBehavior.js -- 此文件是您将添加所有客户端脚本逻辑的位置。</span><span class="sxs-lookup"><span data-stu-id="c22d1-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="c22d1-127">DisabledButtonDesigner.cs - 此类启用设计时功能。</span><span class="sxs-lookup"><span data-stu-id="c22d1-127">DisabledButtonDesigner.cs - This class enables design-time functionality.</span></span> <span data-ttu-id="c22d1-128">如果希望控件扩展器与可视化工作室/可视化 Web 开发人员设计器正确工作，则需要此类。</span><span class="sxs-lookup"><span data-stu-id="c22d1-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="c22d1-129">因此，控件扩展器由服务器端控件、客户端行为和服务器端设计器类组成。</span><span class="sxs-lookup"><span data-stu-id="c22d1-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="c22d1-130">您将在以下部分了解如何创建所有三个这些文件。</span><span class="sxs-lookup"><span data-stu-id="c22d1-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="c22d1-131">创建自定义扩展器网站和项目</span><span class="sxs-lookup"><span data-stu-id="c22d1-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="c22d1-132">第一步是在可视化工作室/可视化 Web 开发人员中创建类库项目和网站。</span><span class="sxs-lookup"><span data-stu-id="c22d1-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="c22d1-133">我们将在类库项目中创建自定义扩展器，并在网站中测试自定义扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="c22d1-134">让我们从网站开始。</span><span class="sxs-lookup"><span data-stu-id="c22d1-134">Let�s start with the website.</span></span> <span data-ttu-id="c22d1-135">按照以下步骤创建网站：</span><span class="sxs-lookup"><span data-stu-id="c22d1-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="c22d1-136">选择菜单选项 **"文件，新建网站**"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="c22d1-137">选择**ASP.NET网站**模板。</span><span class="sxs-lookup"><span data-stu-id="c22d1-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="c22d1-138">命名新的*网站网站1。*</span><span class="sxs-lookup"><span data-stu-id="c22d1-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="c22d1-139">单击“确定”\*\*\*\* 按钮。</span><span class="sxs-lookup"><span data-stu-id="c22d1-139">Click the **OK** button.</span></span>

<span data-ttu-id="c22d1-140">接下来，我们需要创建包含控件扩展器代码的类库项目：</span><span class="sxs-lookup"><span data-stu-id="c22d1-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="c22d1-141">选择菜单选项 **"文件、添加、新项目**"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="c22d1-142">选择**类库**模板。</span><span class="sxs-lookup"><span data-stu-id="c22d1-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="c22d1-143">使用名称 **"自定义扩展器**"为新类库命名。</span><span class="sxs-lookup"><span data-stu-id="c22d1-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="c22d1-144">单击“确定”\*\*\*\* 按钮。</span><span class="sxs-lookup"><span data-stu-id="c22d1-144">Click the **OK** button.</span></span>

<span data-ttu-id="c22d1-145">完成这些步骤后，解决方案资源管理器窗口应类似于图 1。</span><span class="sxs-lookup"><span data-stu-id="c22d1-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="c22d1-146">[![网站和类库项目的解决方案](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="c22d1-147">**图01：** 包含网站和类库项目的解决方案（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span></span>

<span data-ttu-id="c22d1-148">接下来，您需要向类库项目添加所有必要的程序集引用：</span><span class="sxs-lookup"><span data-stu-id="c22d1-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="c22d1-149">右键单击"自定义扩展器"项目并选择菜单选项 **"添加参考**"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="c22d1-150">选择 .NET 选项卡。</span><span class="sxs-lookup"><span data-stu-id="c22d1-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="c22d1-151">添加对下列程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="c22d1-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="c22d1-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="c22d1-152">System.Web.dll</span></span>
    2. <span data-ttu-id="c22d1-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="c22d1-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="c22d1-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="c22d1-154">System.Design.dll</span></span>
    4. <span data-ttu-id="c22d1-155">系统.Web.扩展.设计.dll</span><span class="sxs-lookup"><span data-stu-id="c22d1-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="c22d1-156">选择“浏览”按钮。</span><span class="sxs-lookup"><span data-stu-id="c22d1-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="c22d1-157">添加对 AjaxControlToolkit.dll 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="c22d1-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="c22d1-158">此程序集位于下载 AJAX 控制工具包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="c22d1-159">完成这些步骤后，类库项目参考文件夹应类似于图 2。</span><span class="sxs-lookup"><span data-stu-id="c22d1-159">After you complete these steps, your class library project References folder should look like Figure 2.</span></span>

<span data-ttu-id="c22d1-160">[![具有所需引用的引用文件夹](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span></span>

<span data-ttu-id="c22d1-161">**图 02**：引用具有所需引用的文件夹（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="c22d1-162">创建自定义控件扩展器</span><span class="sxs-lookup"><span data-stu-id="c22d1-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="c22d1-163">现在，我们已经有了类库，我们可以开始构建扩展器控件。</span><span class="sxs-lookup"><span data-stu-id="c22d1-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="c22d1-164">让我们从自定义扩展器控件类的裸骨开始（参见清单 1）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="c22d1-165">**清单 1 - MyCustomExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="c22d1-165">**Listing 1 - MyCustomExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

<span data-ttu-id="c22d1-166">关于清单1中的控件扩展器类，您注意到几件事。</span><span class="sxs-lookup"><span data-stu-id="c22d1-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="c22d1-167">首先，请注意，类从基扩展器控制库类继承。</span><span class="sxs-lookup"><span data-stu-id="c22d1-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="c22d1-168">所有 AJAX 控制工具包扩展器控件都源自此基类。</span><span class="sxs-lookup"><span data-stu-id="c22d1-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="c22d1-169">例如，基类包括作为每个控件扩展器的必需属性的 TargetID 属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="c22d1-170">接下来，请注意，该类包含以下与客户端脚本相关的两个属性：</span><span class="sxs-lookup"><span data-stu-id="c22d1-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="c22d1-171">Web 资源 - 使文件作为嵌入资源包含在程序集中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="c22d1-172">客户端脚本资源 - 导致从程序集检索脚本资源。</span><span class="sxs-lookup"><span data-stu-id="c22d1-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="c22d1-173">WebResource 属性用于在编译自定义扩展器时将 MyControlBehavior.js JavaScript 文件嵌入到程序集中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="c22d1-174">当在网页中使用自定义扩展器时，客户端脚本资源属性用于从程序集中检索 MyControlBehavior.js 脚本。</span><span class="sxs-lookup"><span data-stu-id="c22d1-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="c22d1-175">为了使 Web 资源和客户端脚本资源属性正常工作，必须将 JavaScript 文件编译为嵌入式资源。</span><span class="sxs-lookup"><span data-stu-id="c22d1-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="c22d1-176">在解决方案资源管理器窗口中选择文件，打开属性表，并将值 *"嵌入资源"* 分配给 **"生成操作"** 属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="c22d1-177">请注意，控件扩展器还包括一个 TargetControlType 属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="c22d1-178">此属性用于指定由控件扩展器扩展的控件类型。</span><span class="sxs-lookup"><span data-stu-id="c22d1-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="c22d1-179">在清单 1 中，控件扩展器用于扩展 TextBox。</span><span class="sxs-lookup"><span data-stu-id="c22d1-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="c22d1-180">最后，请注意，自定义扩展器包含名为 MyProperty 的属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="c22d1-181">属性使用扩展器控制属性属性进行标记。</span><span class="sxs-lookup"><span data-stu-id="c22d1-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="c22d1-182">GetPropertyValue（） 和 SetPropertyValue（） 方法用于将属性值从服务器端控件扩展器传递到客户端行为。</span><span class="sxs-lookup"><span data-stu-id="c22d1-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="c22d1-183">让我们继续实现我们的禁用按钮扩展器的代码。</span><span class="sxs-lookup"><span data-stu-id="c22d1-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="c22d1-184">此扩展器的代码可在清单 2 中找到。</span><span class="sxs-lookup"><span data-stu-id="c22d1-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="c22d1-185">**清单2 - DisabledButtonExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="c22d1-185">**Listing 2 - DisabledButtonExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

<span data-ttu-id="c22d1-186">清单2中的"禁用按钮扩展器"具有两个属性，分别命名为 TargetButtonID 和"禁用文本"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="c22d1-187">应用于 TargetButtonID 属性的 IDReference 属性可防止您将 Button 控件 ID 以外的任何内容分配给此属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="c22d1-188">WebResource 和 ClientScriptResource 属性将位于名为"禁用ButtonBehavior.js"的文件中的客户端行为与此扩展器相关联。</span><span class="sxs-lookup"><span data-stu-id="c22d1-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="c22d1-189">我们将在下一节中讨论此 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="c22d1-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="c22d1-190">创建自定义扩展程序行为</span><span class="sxs-lookup"><span data-stu-id="c22d1-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="c22d1-191">控件扩展器的客户端组件称为行为。</span><span class="sxs-lookup"><span data-stu-id="c22d1-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="c22d1-192">禁用和启用按钮的实际逻辑包含在"禁用按钮"行为中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="c22d1-193">该行为的 JavaScript 代码包含在清单 3 中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="c22d1-194">**清单 3 - 禁用Button.js**</span><span class="sxs-lookup"><span data-stu-id="c22d1-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

<span data-ttu-id="c22d1-195">清单3中的 JavaScript 文件包含名为"禁用Button行为"的客户端类。</span><span class="sxs-lookup"><span data-stu-id="c22d1-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="c22d1-196">此类，与其服务器端孪生一样，包括名为 TargetButtonID 和禁用文本的两个属性，您可以使用\_GetTargetButtonID/设置\_TargetButtonID 进行访问，并获得\_禁用文本/集\_禁用文本。</span><span class="sxs-lookup"><span data-stu-id="c22d1-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="c22d1-197">初始化（） 方法将键up事件处理程序与行为的目标元素关联。</span><span class="sxs-lookup"><span data-stu-id="c22d1-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="c22d1-198">每次在与此行为关联的 TextBox 中键入字母时，键 up 处理程序都会执行。</span><span class="sxs-lookup"><span data-stu-id="c22d1-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="c22d1-199">键up 处理程序启用或禁用按钮，具体取决于与该行为关联的 TextBox 是否包含任何文本。</span><span class="sxs-lookup"><span data-stu-id="c22d1-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="c22d1-200">请记住，您必须将清单 3 中的 JavaScript 文件编译为嵌入式资源。</span><span class="sxs-lookup"><span data-stu-id="c22d1-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="c22d1-201">在解决方案资源管理器窗口中选择文件，打开属性表，并将值 *"嵌入资源"* 分配给**生成操作**属性（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="c22d1-202">此选项在可视化工作室和可视化 Web 开发人员中都可用。</span><span class="sxs-lookup"><span data-stu-id="c22d1-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="c22d1-203">[![将 JavaScript 文件添加为嵌入式资源](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span></span>

<span data-ttu-id="c22d1-204">**图 03**： 将 JavaScript 文件添加为嵌入式资源（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="c22d1-205">创建自定义扩展程序设计器</span><span class="sxs-lookup"><span data-stu-id="c22d1-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="c22d1-206">我们需要创建最后一个类来完成扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="c22d1-207">我们需要在清单4中创建设计器类。</span><span class="sxs-lookup"><span data-stu-id="c22d1-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="c22d1-208">此类是使扩展器在可视化工作室/可视化 Web 开发人员设计器中正确运行所必需的。</span><span class="sxs-lookup"><span data-stu-id="c22d1-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="c22d1-209">**清单4 - DisabledButtonDesigner.cs**</span><span class="sxs-lookup"><span data-stu-id="c22d1-209">**Listing 4 - DisabledButtonDesigner.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

<span data-ttu-id="c22d1-210">将清单 4 中的设计器与"已禁用Button 扩展器"与"设计器"属性相关联。您需要将 Designer 属性应用于禁用Button扩展器类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c22d1-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="c22d1-211">使用自定义扩展器</span><span class="sxs-lookup"><span data-stu-id="c22d1-211">Using the Custom Extender</span></span>

<span data-ttu-id="c22d1-212">现在，我们已经完成了创建禁用按钮控件扩展器，是时候在我们的ASP.NET网站使用它了。</span><span class="sxs-lookup"><span data-stu-id="c22d1-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="c22d1-213">首先，我们需要将自定义扩展器添加到工具箱中。</span><span class="sxs-lookup"><span data-stu-id="c22d1-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="c22d1-214">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="c22d1-214">Follow these steps:</span></span>

1. <span data-ttu-id="c22d1-215">通过双击解决方案资源管理器窗口中的页面打开ASP.NET页。</span><span class="sxs-lookup"><span data-stu-id="c22d1-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="c22d1-216">右键单击工具箱并选择菜单选项 **"选择项目**"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="c22d1-217">在"选择工具箱项目"对话框中，浏览到"自定义扩展器.dll"程序集。</span><span class="sxs-lookup"><span data-stu-id="c22d1-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="c22d1-218">单击"**确定"** 按钮关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="c22d1-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="c22d1-219">完成这些步骤后，禁用 Button 控件扩展器应显示在工具箱中（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="c22d1-220">[![工具箱中的禁用按钮](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span></span>

<span data-ttu-id="c22d1-221">**图 04**： 工具箱中的禁用按钮（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span></span>

<span data-ttu-id="c22d1-222">接下来，我们需要创建一个新的ASP.NET页。</span><span class="sxs-lookup"><span data-stu-id="c22d1-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="c22d1-223">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="c22d1-223">Follow these steps:</span></span>

1. <span data-ttu-id="c22d1-224">创建新ASP.NET页面名为"显示禁用按钮.aspx"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="c22d1-225">将脚本管理器拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="c22d1-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="c22d1-226">将文本框控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="c22d1-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="c22d1-227">将"按钮"控件拖到页面上。</span><span class="sxs-lookup"><span data-stu-id="c22d1-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="c22d1-228">在"属性"窗口中，将按钮 ID 属性更改为值<em>btnSave，</em>将文本属性更改为*值\*"保存*"。</span><span class="sxs-lookup"><span data-stu-id="c22d1-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="c22d1-229">我们创建了一个包含标准ASP.NET文本框和按钮控件的页面。</span><span class="sxs-lookup"><span data-stu-id="c22d1-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="c22d1-230">接下来，我们需要使用禁用按钮扩展器扩展 TextBox 控件：</span><span class="sxs-lookup"><span data-stu-id="c22d1-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="c22d1-231">选择 **"添加扩展器**"任务选项以打开扩展程序向导对话框（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="c22d1-232">请注意，该对话框包括我们的自定义禁用按钮扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="c22d1-233">选择"禁用按钮扩展器"，然后单击 **"确定**"按钮。</span><span class="sxs-lookup"><span data-stu-id="c22d1-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="c22d1-234">[![扩展器向导对话框](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span></span>

<span data-ttu-id="c22d1-235">**图 05**： 扩展器向导对话框（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span></span>

<span data-ttu-id="c22d1-236">最后，我们可以设置禁用按钮扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="c22d1-237">您可以通过修改 TextBox 控件的属性来修改禁用Button扩展器的属性：</span><span class="sxs-lookup"><span data-stu-id="c22d1-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="c22d1-238">选择设计器中的文本框。</span><span class="sxs-lookup"><span data-stu-id="c22d1-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="c22d1-239">在"属性"窗口中，展开扩展器节点（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="c22d1-240">将"*保存到*禁用文本"属性的值和值*btnSave*分配给 TargetButtonID 属性。</span><span class="sxs-lookup"><span data-stu-id="c22d1-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="c22d1-241">[![设置扩展器属性](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span></span>

<span data-ttu-id="c22d1-242">**图 06**：设置扩展器属性（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span></span>

<span data-ttu-id="c22d1-243">当您运行页面（通过点击 F5）时，按钮控件最初被禁用。</span><span class="sxs-lookup"><span data-stu-id="c22d1-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="c22d1-244">一旦您开始将文本输入到 TextBox 中，按钮控件即启用（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="c22d1-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="c22d1-245">[![禁用按钮扩展器正在操作中](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="c22d1-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span></span>

<span data-ttu-id="c22d1-246">**图 07**： 禁用按钮扩展器在操作中（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)）</span><span class="sxs-lookup"><span data-stu-id="c22d1-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="c22d1-247">总结</span><span class="sxs-lookup"><span data-stu-id="c22d1-247">Summary</span></span>

<span data-ttu-id="c22d1-248">本教程的目的是说明如何使用自定义扩展器控件扩展 AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="c22d1-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="c22d1-249">在本教程中，我们创建了一个简单的禁用按钮控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="c22d1-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="c22d1-250">我们通过创建禁用Button扩展器类、禁用Button行为 JavaScript 行为和禁用ButtonDesigner类实现了此扩展程序。</span><span class="sxs-lookup"><span data-stu-id="c22d1-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="c22d1-251">每当创建自定义控件扩展器时，都会遵循一组类似的步骤。</span><span class="sxs-lookup"><span data-stu-id="c22d1-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c22d1-252">[上一页](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [下一页](get-started-with-the-ajax-control-toolkit-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c22d1-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
[Next](get-started-with-the-ajax-control-toolkit-vb.md)</span></span>

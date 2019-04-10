---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 创建自定义 AJAX 控件工具包扩展程序控件 (VB) |Microsoft Docs
author: microsoft
description: 自定义扩展程序，可以自定义和扩展的 ASP.NET 控件的功能而无需创建新的类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 8336fecf60296c44ebcf6cbd6010f9d5daed2923
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415955"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="61ec8-103">创建自定义 AJAX 控件工具包控件扩展程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="61ec8-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>

<span data-ttu-id="61ec8-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="61ec8-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="61ec8-105">自定义扩展程序，可以自定义和扩展的 ASP.NET 控件的功能而无需创建新的类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>


<span data-ttu-id="61ec8-106">在本教程中，您将学习如何创建自定义 AJAX 控件工具包控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="61ec8-107">我们创建一个简单，但更改按钮的状态从禁用启用时文本框中键入文本的有用、 新的扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="61ec8-108">阅读本教程之后, 你将能够扩展 ASP.NET AJAX 工具包使用您自己控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="61ec8-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="61ec8-109">您可以创建自定义控件扩展程序使用 Visual Studio 或 Visual Web Developer （请确保具有最新版本的 Visual Web Developer）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="61ec8-110">DisabledButton 扩展程序的概述</span><span class="sxs-lookup"><span data-stu-id="61ec8-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="61ec8-111">我们新的控件扩展程序名称为 DisabledButton 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="61ec8-112">此扩展器将具有三个属性：</span><span class="sxs-lookup"><span data-stu-id="61ec8-112">This extender will have three properties:</span></span>

- <span data-ttu-id="61ec8-113">TargetControlID-控件扩展的文本框。</span><span class="sxs-lookup"><span data-stu-id="61ec8-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="61ec8-114">TargetButtonIID-已禁用或启用的按钮。</span><span class="sxs-lookup"><span data-stu-id="61ec8-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="61ec8-115">DisabledText-最初在按钮中显示的文本。</span><span class="sxs-lookup"><span data-stu-id="61ec8-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="61ec8-116">当您开始键入时，按钮将显示按钮文本属性的值。</span><span class="sxs-lookup"><span data-stu-id="61ec8-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="61ec8-117">可以将挂接到文本框和按钮控件 DisabledButton 扩展器。</span><span class="sxs-lookup"><span data-stu-id="61ec8-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="61ec8-118">键入的任何文本之前，将禁用的按钮和文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="61ec8-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="61ec8-119">([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>


<span data-ttu-id="61ec8-120">开始键入文本后，启用该按钮和文本框和按钮如下所示：</span><span class="sxs-lookup"><span data-stu-id="61ec8-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>


[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="61ec8-121">([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>


<span data-ttu-id="61ec8-122">若要创建我们控件扩展程序，我们需要创建以下三个文件：</span><span class="sxs-lookup"><span data-stu-id="61ec8-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="61ec8-123">DisabledButtonExtender.vb-此文件是将管理创建您的扩展器，并允许您在设计时设置的属性的服务器端控件类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="61ec8-124">它还定义了可以在您的扩展器设置的属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="61ec8-125">这些属性可通过代码和设计时访问和 DisableButtonBehavior.js 文件中定义的属性匹配。</span><span class="sxs-lookup"><span data-stu-id="61ec8-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="61ec8-126">DisabledButtonBehavior.js-此文件是您将添加所有客户端脚本逻辑。</span><span class="sxs-lookup"><span data-stu-id="61ec8-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="61ec8-127">DisabledButtonDesigner.vb-此类使设计时功能。</span><span class="sxs-lookup"><span data-stu-id="61ec8-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="61ec8-128">如果你想要正常使用 Visual Studio/Visual Web Developer 设计器的控件扩展程序，则需要此类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="61ec8-129">因此控件扩展程序包含服务器端控件、 客户端的行为和服务器端设计器类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="61ec8-130">了解如何在以下各节中创建所有这三个这些文件。</span><span class="sxs-lookup"><span data-stu-id="61ec8-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="61ec8-131">创建自定义扩展程序网站和项目</span><span class="sxs-lookup"><span data-stu-id="61ec8-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="61ec8-132">第一步是在 Visual Studio/Visual Web Developer 中创建一个类库项目和网站。</span><span class="sxs-lookup"><span data-stu-id="61ec8-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="61ec8-133">我们将在类库项目中创建自定义扩展程序和网站中测试自定义扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="61ec8-134">让我们来开始与网站。</span><span class="sxs-lookup"><span data-stu-id="61ec8-134">Let�s start with the website.</span></span> <span data-ttu-id="61ec8-135">请按照下列步骤以创建网站：</span><span class="sxs-lookup"><span data-stu-id="61ec8-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="61ec8-136">选择菜单选项**文件，新的 Web 站点**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="61ec8-137">选择**ASP.NET Web 站点**模板。</span><span class="sxs-lookup"><span data-stu-id="61ec8-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="61ec8-138">新网站命名*Website1*。</span><span class="sxs-lookup"><span data-stu-id="61ec8-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="61ec8-139">单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="61ec8-139">Click the **OK** button.</span></span>

<span data-ttu-id="61ec8-140">接下来，我们需要创建将包含控件扩展程序的代码类库项目：</span><span class="sxs-lookup"><span data-stu-id="61ec8-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="61ec8-141">选择菜单选项**文件中，添加新项目**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="61ec8-142">选择**类库**模板。</span><span class="sxs-lookup"><span data-stu-id="61ec8-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="61ec8-143">具有名称命名的新类库**CustomExtenders**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="61ec8-144">单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="61ec8-144">Click the **OK** button.</span></span>

<span data-ttu-id="61ec8-145">完成这些步骤后，在解决方案资源管理器窗口应如图 1 所示。</span><span class="sxs-lookup"><span data-stu-id="61ec8-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>


[![S<span data-ttu-id="61ec8-146">与网站和类的类库项目的解决方案]</span><span class="sxs-lookup"><span data-stu-id="61ec8-146">olution with website and class library project]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

<span data-ttu-id="61ec8-147">**图 01**:与网站和类的类库项目的解决方案 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>


<span data-ttu-id="61ec8-148">接下来，您需要添加所有必要的程序集引用对类库项目：</span><span class="sxs-lookup"><span data-stu-id="61ec8-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="61ec8-149">右键单击 CustomExtenders 项目，然后选择菜单选项**添加引用**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="61ec8-150">选择.NET 选项卡。</span><span class="sxs-lookup"><span data-stu-id="61ec8-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="61ec8-151">添加对下列程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="61ec8-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="61ec8-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="61ec8-152">System.Web.dll</span></span>
    2. <span data-ttu-id="61ec8-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="61ec8-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="61ec8-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="61ec8-154">System.Design.dll</span></span>
    4. <span data-ttu-id="61ec8-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="61ec8-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="61ec8-156">选择浏览选项卡。</span><span class="sxs-lookup"><span data-stu-id="61ec8-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="61ec8-157">添加对 AjaxControlToolkit.dll 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="61ec8-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="61ec8-158">此程序集位于在其中下载 AJAX 控件工具包的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="61ec8-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="61ec8-159">你可以验证，你已添加所有正确引用通过右键单击项目，选择属性，然后单击引用选项卡 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>


[![R<span data-ttu-id="61ec8-160">具有所需的引用 eferences 文件夹]</span><span class="sxs-lookup"><span data-stu-id="61ec8-160">eferences folder with required references]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

<span data-ttu-id="61ec8-161">**图 02**:使用所需的引用引用文件夹 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>


## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="61ec8-162">创建自定义控件扩展程序</span><span class="sxs-lookup"><span data-stu-id="61ec8-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="61ec8-163">现在，我们有我们的类库，我们可以开始构建我们的扩展程序控件。</span><span class="sxs-lookup"><span data-stu-id="61ec8-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="61ec8-164">让我们来开始准系统的自定义扩展程序控件类 （请参阅代码清单 1）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

**<span data-ttu-id="61ec8-165">代码清单 1-MyCustomExtender.vb</span><span class="sxs-lookup"><span data-stu-id="61ec8-165">Listing 1 - MyCustomExtender.vb</span></span>**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="61ec8-166">有几种您注意到有关列表 1 中的控件扩展程序类的方法。</span><span class="sxs-lookup"><span data-stu-id="61ec8-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="61ec8-167">首先，请注意该类继承 ExtenderControlBase 类的基类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="61ec8-168">所有 AJAX 控件工具包扩展程序控件都派生自这个基类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="61ec8-169">例如，基本类包括为每个控件扩展程序的必需的属性的 TargetID 属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="61ec8-170">接下来，请注意，类包含与客户端脚本相关的以下两个属性：</span><span class="sxs-lookup"><span data-stu-id="61ec8-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="61ec8-171">WebResource-导致文件以将其包含在程序集中嵌入的资源。</span><span class="sxs-lookup"><span data-stu-id="61ec8-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="61ec8-172">ClientScriptResource-会导致要从程序集中检索的脚本资源。</span><span class="sxs-lookup"><span data-stu-id="61ec8-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="61ec8-173">WebResource 属性用于编译自定义扩展器时，将 MyControlBehavior.js JavaScript 文件嵌入到程序集。</span><span class="sxs-lookup"><span data-stu-id="61ec8-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="61ec8-174">ClientScriptResource 属性用于在网页中使用自定义扩展器时，从该程序集检索 MyControlBehavior.js 脚本。</span><span class="sxs-lookup"><span data-stu-id="61ec8-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>


<span data-ttu-id="61ec8-175">为了使 WebResource 和 ClientScriptResource 属性，若要运行，必须作为嵌入资源编译 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="61ec8-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="61ec8-176">选择解决方案资源管理器窗口中的文件，打开属性页中，并将该值赋*嵌入的资源*到**生成操作**属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>


<span data-ttu-id="61ec8-177">请注意，控件扩展程序还包含 TargetControlType 属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="61ec8-178">此属性用于指定由扩展程序控件扩展的控件的类型。</span><span class="sxs-lookup"><span data-stu-id="61ec8-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="61ec8-179">列表 1 中，对于控件扩展程序用于扩展一个文本框。</span><span class="sxs-lookup"><span data-stu-id="61ec8-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="61ec8-180">最后，请注意，自定义扩展器包括名为 MyProperty 的属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="61ec8-181">该属性用 ExtenderControlProperty 特性标记。</span><span class="sxs-lookup"><span data-stu-id="61ec8-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="61ec8-182">GetPropertyValue() 和 SetPropertyValue() 方法用于将属性值从服务器端控件扩展程序传递到客户端的行为。</span><span class="sxs-lookup"><span data-stu-id="61ec8-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="61ec8-183">让我们来继续操作并实现我们 DisabledButton 扩展程序的代码。</span><span class="sxs-lookup"><span data-stu-id="61ec8-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="61ec8-184">可以在代码清单 2 中找到此扩展器的代码。</span><span class="sxs-lookup"><span data-stu-id="61ec8-184">The code for this extender can be found in Listing 2.</span></span>

**<span data-ttu-id="61ec8-185">代码清单 2-DisabledButtonExtender.vb</span><span class="sxs-lookup"><span data-stu-id="61ec8-185">Listing 2 - DisabledButtonExtender.vb</span></span>**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="61ec8-186">列表 2 中的 DisabledButton 扩展器具有两个名为 TargetButtonID 和 DisabledText 的属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="61ec8-187">应用于 TargetButtonID 属性 IDReferenceProperty 防止将按钮控件的 ID 以外的任何分配给此属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="61ec8-188">WebResource 和 ClientScriptResource 属性将位于名为 DisabledButtonBehavior.js 此扩展器的文件中的客户端的行为相关联。</span><span class="sxs-lookup"><span data-stu-id="61ec8-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="61ec8-189">我们将讨论下一节中的此 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="61ec8-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="61ec8-190">创建自定义扩展器行为</span><span class="sxs-lookup"><span data-stu-id="61ec8-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="61ec8-191">控件扩展程序的客户端组件称为一种行为。</span><span class="sxs-lookup"><span data-stu-id="61ec8-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="61ec8-192">禁用和启用该按钮的实际逻辑包含在 DisabledButton 行为。</span><span class="sxs-lookup"><span data-stu-id="61ec8-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="61ec8-193">行为的 JavaScript 代码包含在列表 3 中。</span><span class="sxs-lookup"><span data-stu-id="61ec8-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

**<span data-ttu-id="61ec8-194">代码清单 3-DisabledButton.js</span><span class="sxs-lookup"><span data-stu-id="61ec8-194">Listing 3 - DisabledButton.js</span></span>**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="61ec8-195">列表 3 中的 JavaScript 文件包含一个名为 DisabledButtonBehavior 的客户端类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="61ec8-196">此类，如其服务器端孪生，包括两个属性名为 TargetButtonID 并使用户能够使用 DisabledText 获取\_TargetButtonID/set\_TargetButtonID 并获取\_DisabledText/设置\_DisabledText。</span><span class="sxs-lookup"><span data-stu-id="61ec8-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="61ec8-197">Initialize （） 方法的行为的目标元素相关联的 keyup 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="61ec8-198">与此行为关联的文本框中键入字母每次 keyup 处理程序执行。</span><span class="sxs-lookup"><span data-stu-id="61ec8-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="61ec8-199">Keyup 处理程序可以启用或禁用按钮具体取决于是否包含任何文本与该行为关联的文本框。</span><span class="sxs-lookup"><span data-stu-id="61ec8-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="61ec8-200">请记住，必须编译 JavaScript 文件作为嵌入资源清单 3 中。</span><span class="sxs-lookup"><span data-stu-id="61ec8-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="61ec8-201">选择解决方案资源管理器窗口中的文件，打开属性页中，并将该值赋*嵌入的资源*到**生成操作**属性 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="61ec8-202">此选项是在 Visual Studio 和 Visual Web Developer 中可用。</span><span class="sxs-lookup"><span data-stu-id="61ec8-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>


[![A<span data-ttu-id="61ec8-203">dding 作为嵌入资源的 JavaScript 文件]</span><span class="sxs-lookup"><span data-stu-id="61ec8-203">dding a JavaScript file as an embedded resource]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

<span data-ttu-id="61ec8-204">**图 03**:添加一个 JavaScript 文件作为嵌入资源 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>


## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="61ec8-205">创建自定义扩展程序设计器</span><span class="sxs-lookup"><span data-stu-id="61ec8-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="61ec8-206">没有一个我们需要进行创建，以完成我们的扩展程序的最后一个类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="61ec8-207">我们需要在列表 4 中创建设计器类。</span><span class="sxs-lookup"><span data-stu-id="61ec8-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="61ec8-208">此类是使扩展器与 Visual Studio/Visual Web Developer 设计器正常运行所必需的。</span><span class="sxs-lookup"><span data-stu-id="61ec8-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

**<span data-ttu-id="61ec8-209">列表 4-DisabledButtonDesigner.vb</span><span class="sxs-lookup"><span data-stu-id="61ec8-209">Listing 4 - DisabledButtonDesigner.vb</span></span>**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="61ec8-210">将列表 4 中的设计器与使用设计器属性 DisabledButton 扩展程序相关联。需要将设计器特性应用于 DisabledButtonExtender 类如下：</span><span class="sxs-lookup"><span data-stu-id="61ec8-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="61ec8-211">使用自定义扩展程序</span><span class="sxs-lookup"><span data-stu-id="61ec8-211">Using the Custom Extender</span></span>

<span data-ttu-id="61ec8-212">现在，我们已完成创建 DisabledButton 扩展程序控件，就可以在我们的 ASP.NET 网站中使用它。</span><span class="sxs-lookup"><span data-stu-id="61ec8-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="61ec8-213">首先，我们需要向工具箱添加自定义扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="61ec8-214">请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="61ec8-214">Follow these steps:</span></span>

1. <span data-ttu-id="61ec8-215">通过双击解决方案资源管理器窗口中的页中打开 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="61ec8-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="61ec8-216">右键单击工具箱，然后选择菜单选项**选择项**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="61ec8-217">在选择工具箱项对话框中，浏览到 CustomExtenders.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="61ec8-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="61ec8-218">单击**确定**按钮以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="61ec8-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="61ec8-219">完成这些步骤后，DisabledButton 控件扩展程序应显示在工具箱中 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>


[![D<span data-ttu-id="61ec8-220">在工具箱 isabledButton]</span><span class="sxs-lookup"><span data-stu-id="61ec8-220">isabledButton in the toolbox]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

<span data-ttu-id="61ec8-221">**图 04**:在工具箱 DisabledButton ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>


<span data-ttu-id="61ec8-222">接下来，我们需要创建一个新的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="61ec8-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="61ec8-223">请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="61ec8-223">Follow these steps:</span></span>

1. <span data-ttu-id="61ec8-224">创建一个名为 ShowDisabledButton.aspx 的新 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="61ec8-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="61ec8-225">将 ScriptManager 拖到绘图页上。</span><span class="sxs-lookup"><span data-stu-id="61ec8-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="61ec8-226">将 TextBox 控件拖到绘图页上。</span><span class="sxs-lookup"><span data-stu-id="61ec8-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="61ec8-227">将按钮控件拖到绘图页上。</span><span class="sxs-lookup"><span data-stu-id="61ec8-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="61ec8-228">在属性窗口中，将按钮 ID 属性更改为值<em>btnSave</em>的值的 Text 属性*保存\**。</span><span class="sxs-lookup"><span data-stu-id="61ec8-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>
  

<span data-ttu-id="61ec8-229">我们使用标准 ASP.NET 文本框和按钮控件创建一个页面。</span><span class="sxs-lookup"><span data-stu-id="61ec8-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="61ec8-230">接下来，我们需要扩展具有 DisabledButton 扩展程序的文本框控件：</span><span class="sxs-lookup"><span data-stu-id="61ec8-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="61ec8-231">选择**添加扩展程序**任务选项以打开扩展程序向导对话框 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="61ec8-232">请注意，该对话框包含我们自定义 DisabledButton 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="61ec8-233">选择 DisabledButton 扩展器，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="61ec8-233">Select the DisabledButton extender and click the **OK** button.</span></span>


[![T<span data-ttu-id="61ec8-234">他扩展器向导对话框]</span><span class="sxs-lookup"><span data-stu-id="61ec8-234">he Extender Wizard dialog]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

<span data-ttu-id="61ec8-235">**图 05**:扩展程序向导对话框 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>


<span data-ttu-id="61ec8-236">最后，我们可以设置 DisabledButton 扩展程序的属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="61ec8-237">可以通过修改的 TextBox 控件的属性来修改 DisabledButton 扩展程序属性：</span><span class="sxs-lookup"><span data-stu-id="61ec8-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="61ec8-238">在设计器中选择文本框中。</span><span class="sxs-lookup"><span data-stu-id="61ec8-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="61ec8-239">在属性窗口中，展开的扩展程序节点 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="61ec8-240">将该值赋*保存*DisabledText 属性以及值*btnSave* TargetButtonID 属性。</span><span class="sxs-lookup"><span data-stu-id="61ec8-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>


[![S<span data-ttu-id="61ec8-241">etting 扩展程序属性]</span><span class="sxs-lookup"><span data-stu-id="61ec8-241">etting extender properties]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

<span data-ttu-id="61ec8-242">**图 06**:设置扩展程序属性 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>


<span data-ttu-id="61ec8-243">（按 F5） 运行页面时，按钮控件最初处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="61ec8-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="61ec8-244">一旦您开始在文本框中输入文本，则控件被启用的按钮 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="61ec8-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>


[![T<span data-ttu-id="61ec8-245">在操作中他 DisabledButton 扩展器]</span><span class="sxs-lookup"><span data-stu-id="61ec8-245">he DisabledButton extender in action]</span></span>(creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

<span data-ttu-id="61ec8-246">**图 07**:DisabledButton 扩展器操作 ([单击此项可查看原尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="61ec8-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="61ec8-247">总结</span><span class="sxs-lookup"><span data-stu-id="61ec8-247">Summary</span></span>

<span data-ttu-id="61ec8-248">本教程的目的是说明如何扩展 AJAX 控件工具包与自定义扩展程序控件。</span><span class="sxs-lookup"><span data-stu-id="61ec8-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="61ec8-249">在本教程中，我们创建一个简单的 DisabledButton 控件扩展程序。</span><span class="sxs-lookup"><span data-stu-id="61ec8-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="61ec8-250">我们通过创建 DisabledButtonExtender 类、 DisabledButtonBehavior JavaScript 行为和 DisabledButtonDesigner 类实现此扩展器。</span><span class="sxs-lookup"><span data-stu-id="61ec8-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="61ec8-251">每当创建自定义控件扩展程序时遵循一组类似的步骤。</span><span class="sxs-lookup"><span data-stu-id="61ec8-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="61ec8-252">上一个</span><span class="sxs-lookup"><span data-stu-id="61ec8-252">Previous</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)

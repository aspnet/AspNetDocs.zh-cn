---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。 代码隐藏可以使用 Src attr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440708"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="eba46-104">ASP.NET 2.0 页模型</span><span class="sxs-lookup"><span data-stu-id="eba46-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="eba46-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="eba46-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="eba46-106">在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。</span><span class="sxs-lookup"><span data-stu-id="eba46-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="eba46-107">可以使用 Src 特性或 @Page 指令的代码隐藏特性来实现代码隐藏。</span><span class="sxs-lookup"><span data-stu-id="eba46-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="eba46-108">在 ASP.NET 2.0 中，开发人员仍然可以在内联代码和代码隐藏之间做出选择，但对代码隐藏模型进行了重大的改进。</span><span class="sxs-lookup"><span data-stu-id="eba46-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="eba46-109">在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。</span><span class="sxs-lookup"><span data-stu-id="eba46-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="eba46-110">可以使用 Src 特性或 @Page 指令的代码隐藏特性来实现代码隐藏。</span><span class="sxs-lookup"><span data-stu-id="eba46-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="eba46-111">在 ASP.NET 2.0 中，开发人员仍然可以在内联代码和代码隐藏之间做出选择，但对代码隐藏模型进行了重大的改进。</span><span class="sxs-lookup"><span data-stu-id="eba46-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="eba46-112">代码隐藏模型改进</span><span class="sxs-lookup"><span data-stu-id="eba46-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="eba46-113">为了充分了解 ASP.NET 2.0 中代码隐藏模型的更改，最好快速查看 ASP.NET 1.x 中存在的模型。</span><span class="sxs-lookup"><span data-stu-id="eba46-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="eba46-114">ASP.NET 1.x 中的代码隐藏模型</span><span class="sxs-lookup"><span data-stu-id="eba46-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="eba46-115">在 ASP.NET 1.x 中，代码隐藏模型由一个 ASPX 文件（Webform）和一个包含编程代码的代码隐藏文件组成。</span><span class="sxs-lookup"><span data-stu-id="eba46-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="eba46-116">使用 ASPX 文件中的 @Page 指令连接了这两个文件。</span><span class="sxs-lookup"><span data-stu-id="eba46-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="eba46-117">ASPX 页上的每个控件在代码隐藏文件中都有一个对应的声明作为实例变量。</span><span class="sxs-lookup"><span data-stu-id="eba46-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="eba46-118">代码隐藏文件还包含用于事件绑定的代码，以及 Visual Studio 设计器所需的生成代码。</span><span class="sxs-lookup"><span data-stu-id="eba46-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="eba46-119">此模型的工作良好，但由于 ASPX 页中的每个 ASP.NET 元素都需要代码隐藏文件中的相应代码，因此没有真正的代码和内容分离。</span><span class="sxs-lookup"><span data-stu-id="eba46-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="eba46-120">例如，如果设计器将新的服务器控件添加到 Visual Studio IDE 之外的 ASPX 文件中，则该应用程序将因缺少代码隐藏文件中该控件的声明而中断。</span><span class="sxs-lookup"><span data-stu-id="eba46-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="eba46-121">ASP.NET 2.0 中的代码隐藏模型</span><span class="sxs-lookup"><span data-stu-id="eba46-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="eba46-122">ASP.NET 2.0 在此模型上大大改进。</span><span class="sxs-lookup"><span data-stu-id="eba46-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="eba46-123">在 ASP.NET 2.0 中，代码隐藏是使用 ASP.NET 2.0 中提供的新*分部类*实现的。</span><span class="sxs-lookup"><span data-stu-id="eba46-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="eba46-124">ASP.NET 2.0 中的代码隐藏类定义为分部类，这意味着它仅包含类定义的一部分。</span><span class="sxs-lookup"><span data-stu-id="eba46-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="eba46-125">类定义的其余部分是 ASP.NET 2.0 在运行时或在预编译网站时使用 ASPX 页动态生成的。</span><span class="sxs-lookup"><span data-stu-id="eba46-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="eba46-126">代码隐藏文件和 ASPX 页之间的链接仍使用 @ Page 指令建立。</span><span class="sxs-lookup"><span data-stu-id="eba46-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="eba46-127">但是，ASP.NET 2.0 现在使用 CodeFile 属性，而不是代码隐藏或 Src 特性。</span><span class="sxs-lookup"><span data-stu-id="eba46-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="eba46-128">Inherits 特性还用于指定页的类名。</span><span class="sxs-lookup"><span data-stu-id="eba46-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="eba46-129">典型的 @ Page 指令可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="eba46-130">ASP.NET 2.0 代码隐藏文件中的典型类定义可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="eba46-131">C#和 Visual Basic 是当前支持分部类的唯一托管语言。</span><span class="sxs-lookup"><span data-stu-id="eba46-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="eba46-132">因此，使用 j # 的开发人员将不能使用 ASP.NET 2.0 中的代码隐藏模型。</span><span class="sxs-lookup"><span data-stu-id="eba46-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="eba46-133">新模型增强了代码隐藏模型，因为开发人员现在只包含其创建的代码。</span><span class="sxs-lookup"><span data-stu-id="eba46-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="eba46-134">它还提供了代码和内容的真正分离，因为代码隐藏文件中没有实例变量声明。</span><span class="sxs-lookup"><span data-stu-id="eba46-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="eba46-135">由于 ASPX 页的分部类是发生事件绑定的位置，Visual Basic 开发人员可以通过在代码隐藏中使用 Handles 关键字来绑定事件，从而实现略微提高性能。</span><span class="sxs-lookup"><span data-stu-id="eba46-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="eba46-136">C#没有等效关键字。</span><span class="sxs-lookup"><span data-stu-id="eba46-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="eba46-137">新 @ Page 指令特性</span><span class="sxs-lookup"><span data-stu-id="eba46-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="eba46-138">ASP.NET 2.0 将许多新属性添加到 @ Page 指令中。</span><span class="sxs-lookup"><span data-stu-id="eba46-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="eba46-139">以下属性是 ASP.NET 2.0 中的新增属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="eba46-140">Async</span><span class="sxs-lookup"><span data-stu-id="eba46-140">Async</span></span>

<span data-ttu-id="eba46-141">Async 属性允许您配置要异步执行的页。</span><span class="sxs-lookup"><span data-stu-id="eba46-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="eba46-142">本模块稍后部分介绍的异步页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="eba46-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="eba46-143">AsyncTimeout</span></span>

<span data-ttu-id="eba46-144">指定了异步页面的超时时间。</span><span class="sxs-lookup"><span data-stu-id="eba46-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="eba46-145">默认值为45秒。</span><span class="sxs-lookup"><span data-stu-id="eba46-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="eba46-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="eba46-146">CodeFile</span></span>

<span data-ttu-id="eba46-147">CodeFile 特性是 Visual Studio 2002/2003 中的代码隐藏特性的替换项。</span><span class="sxs-lookup"><span data-stu-id="eba46-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="eba46-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="eba46-148">CodeFileBaseClass</span></span>

<span data-ttu-id="eba46-149">如果希望从一个基类派生多个页，则使用 CodeFileBaseClass 特性。</span><span class="sxs-lookup"><span data-stu-id="eba46-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="eba46-150">由于 ASP.NET 中的分部类的实现，如果没有此特性，则使用共享公共字段来引用 ASPX 页中声明的控件的基类将无法正常工作，因为网络编译引擎将基于该页中的控件自动创建新成员。</span><span class="sxs-lookup"><span data-stu-id="eba46-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="eba46-151">因此，如果想要在 ASP.NET 中的两个或更多页面上使用一个公共基类，则需要定义在 CodeFileBaseClass 属性中指定基类，然后从该基类派生每个页面类。</span><span class="sxs-lookup"><span data-stu-id="eba46-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="eba46-152">使用此属性时，CodeFile 属性也是必需的。</span><span class="sxs-lookup"><span data-stu-id="eba46-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="eba46-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="eba46-153">CompilationMode</span></span>

<span data-ttu-id="eba46-154">此特性允许您设置 ASPX 页的 CompilationMode 属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="eba46-155">CompilationMode 属性是一个枚举，其中包含值**Always**、 **Auto**和**Never**。</span><span class="sxs-lookup"><span data-stu-id="eba46-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="eba46-156">默认值**始终**为。</span><span class="sxs-lookup"><span data-stu-id="eba46-156">The default is **Always**.</span></span> <span data-ttu-id="eba46-157">如果可能，**自动**设置将阻止 ASP.NET 动态编译页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="eba46-158">排除动态编译中的页会提高性能。</span><span class="sxs-lookup"><span data-stu-id="eba46-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="eba46-159">但是，如果排除的页包含必须编译的代码，则在浏览该页时会引发错误。</span><span class="sxs-lookup"><span data-stu-id="eba46-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="eba46-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="eba46-160">EnableEventValidation</span></span>

<span data-ttu-id="eba46-161">此特性指定是否验证回发和回调事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="eba46-162">启用此功能后，将检查回发或回调事件的参数，以确保它们源自最初呈现它们的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="eba46-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="eba46-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="eba46-163">EnableTheming</span></span>

<span data-ttu-id="eba46-164">此属性指定页面上是否使用 ASP.NET 主题。</span><span class="sxs-lookup"><span data-stu-id="eba46-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="eba46-165">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="eba46-165">The default is **false**.</span></span> <span data-ttu-id="eba46-166">[模块 10](profiles-themes-and-web-parts.md)中介绍了 ASP.NET 主题。</span><span class="sxs-lookup"><span data-stu-id="eba46-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="eba46-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="eba46-167">LinePragmas</span></span>

<span data-ttu-id="eba46-168">此属性指定在编译期间是否应添加行杂注。</span><span class="sxs-lookup"><span data-stu-id="eba46-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="eba46-169">行杂注是调试器用来标记代码的特定部分的选项。</span><span class="sxs-lookup"><span data-stu-id="eba46-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="eba46-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="eba46-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="eba46-171">此特性指定是否在页中注入 JavaScript 以便维护回发之间的滚动位置。</span><span class="sxs-lookup"><span data-stu-id="eba46-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="eba46-172">默认情况下，此属性为**false** 。</span><span class="sxs-lookup"><span data-stu-id="eba46-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="eba46-173">如果此属性为**true**，则 ASP.NET 将在回发时添加一个 &lt;脚本&gt; 块，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="eba46-174">请注意，此脚本块的源为 WebResource。</span><span class="sxs-lookup"><span data-stu-id="eba46-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="eba46-175">此资源不是物理路径。</span><span class="sxs-lookup"><span data-stu-id="eba46-175">This resource is not a physical path.</span></span> <span data-ttu-id="eba46-176">请求此脚本时，ASP.NET 会动态生成脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="eba46-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="eba46-177">MasterPageFile</span></span>

<span data-ttu-id="eba46-178">此属性指定当前页的母版页文件。</span><span class="sxs-lookup"><span data-stu-id="eba46-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="eba46-179">路径可以是相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="eba46-179">The path can be relative or absolute.</span></span> <span data-ttu-id="eba46-180">主页面在[模块 4](master-pages.md)中介绍。</span><span class="sxs-lookup"><span data-stu-id="eba46-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="eba46-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="eba46-181">StyleSheetTheme</span></span>

<span data-ttu-id="eba46-182">此属性允许你重写 ASP.NET 2.0 主题定义的用户界面外观属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="eba46-183">[模块 10](profiles-themes-and-web-parts.md)中介绍了主题。</span><span class="sxs-lookup"><span data-stu-id="eba46-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="eba46-184">主题</span><span class="sxs-lookup"><span data-stu-id="eba46-184">Theme</span></span>

<span data-ttu-id="eba46-185">指定页面的主题。</span><span class="sxs-lookup"><span data-stu-id="eba46-185">Specifies the theme for the page.</span></span> <span data-ttu-id="eba46-186">如果没有为 StyleSheetTheme 属性指定值，则主题属性将覆盖应用于页面上的控件的所有样式。</span><span class="sxs-lookup"><span data-stu-id="eba46-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="eba46-187">标题</span><span class="sxs-lookup"><span data-stu-id="eba46-187">Title</span></span>

<span data-ttu-id="eba46-188">设置页面的标题。</span><span class="sxs-lookup"><span data-stu-id="eba46-188">Sets the title for the page.</span></span> <span data-ttu-id="eba46-189">此处指定的值将显示在所呈现页面的 &lt;标题&gt; 元素中。</span><span class="sxs-lookup"><span data-stu-id="eba46-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="eba46-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="eba46-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="eba46-191">设置 ViewStateEncryptionMode 枚举的值。</span><span class="sxs-lookup"><span data-stu-id="eba46-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="eba46-192">可用值**始终**为 "**自动**" 和 "**从不**"。</span><span class="sxs-lookup"><span data-stu-id="eba46-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="eba46-193">默认值为 "**自动**"。如果将此属性设置为 "**自动**"，则将对 viewstate 进行加密，这是一个控件通过调用**RegisterRequiresViewStateEncryption**方法发出请求。</span><span class="sxs-lookup"><span data-stu-id="eba46-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="eba46-194">通过 @ Page 指令设置公共属性值</span><span class="sxs-lookup"><span data-stu-id="eba46-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="eba46-195">ASP.NET 2.0 中 @ Page 指令的另一项新功能是能够设置基类的公共属性的初始值。</span><span class="sxs-lookup"><span data-stu-id="eba46-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="eba46-196">例如，假设你在基类中有一个名为**SomeText**的公共属性，并且你希望在加载页面时将其初始化为**Hello** 。</span><span class="sxs-lookup"><span data-stu-id="eba46-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="eba46-197">只需在 @ Page 指令中设置值即可实现此目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="eba46-198">@ Page 指令的**SomeText**属性将基类中 SomeText 属性的初始值设置为*Hello！* 。</span><span class="sxs-lookup"><span data-stu-id="eba46-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="eba46-199">下面的视频介绍如何使用 @ Page 指令在基类中设置公共属性的初始值。</span><span class="sxs-lookup"><span data-stu-id="eba46-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="eba46-200">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="eba46-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="eba46-201">Page 类的新公共属性</span><span class="sxs-lookup"><span data-stu-id="eba46-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="eba46-202">以下公共属性是 ASP.NET 2.0 中的新增属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="eba46-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="eba46-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="eba46-204">返回页面或控件的应用程序相对路径。</span><span class="sxs-lookup"><span data-stu-id="eba46-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="eba46-205">例如，对于位于 http://app/folder/page.aspx的页，属性将返回 ~/folder/。</span><span class="sxs-lookup"><span data-stu-id="eba46-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="eba46-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="eba46-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="eba46-207">返回页面或控件的相对虚拟目录路径。</span><span class="sxs-lookup"><span data-stu-id="eba46-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="eba46-208">例如，对于位于 http://app/folder/page.aspx的页，属性将返回 ~/folder/page.aspx。</span><span class="sxs-lookup"><span data-stu-id="eba46-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="eba46-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="eba46-209">AsyncTimeout</span></span>

<span data-ttu-id="eba46-210">获取或设置用于异步页面处理的超时值。</span><span class="sxs-lookup"><span data-stu-id="eba46-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="eba46-211">（此模块稍后将介绍异步页面。）</span><span class="sxs-lookup"><span data-stu-id="eba46-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="eba46-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="eba46-212">ClientQueryString</span></span>

<span data-ttu-id="eba46-213">一个只读属性，该属性返回所请求 URL 的查询字符串部分。</span><span class="sxs-lookup"><span data-stu-id="eba46-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="eba46-214">此值为 URL 编码。</span><span class="sxs-lookup"><span data-stu-id="eba46-214">This value is URL encoded.</span></span> <span data-ttu-id="eba46-215">可以使用 HttpServerUtility 类的 UrlDecode 方法对其进行解码。</span><span class="sxs-lookup"><span data-stu-id="eba46-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="eba46-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="eba46-216">ClientScript</span></span>

<span data-ttu-id="eba46-217">此属性返回一个 ClientScriptManager 对象，该对象可用于管理客户端脚本的网络辐射。</span><span class="sxs-lookup"><span data-stu-id="eba46-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="eba46-218">（本模块稍后将介绍 ClientScriptManager 类。）</span><span class="sxs-lookup"><span data-stu-id="eba46-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="eba46-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="eba46-219">EnableEventValidation</span></span>

<span data-ttu-id="eba46-220">此属性控制是否为回发和回调事件启用事件验证。</span><span class="sxs-lookup"><span data-stu-id="eba46-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="eba46-221">启用后，将验证回发或回调事件的参数，以确保它们源自最初呈现它们的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="eba46-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="eba46-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="eba46-222">EnableTheming</span></span>

<span data-ttu-id="eba46-223">此属性获取或设置一个布尔值，该值指定是否将 ASP.NET 2.0 主题应用于页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="eba46-224">窗体</span><span class="sxs-lookup"><span data-stu-id="eba46-224">Form</span></span>

<span data-ttu-id="eba46-225">此属性以 HtmlForm 对象的形式返回 ASPX 页上的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="eba46-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="eba46-226">Header</span><span class="sxs-lookup"><span data-stu-id="eba46-226">Header</span></span>

<span data-ttu-id="eba46-227">此属性返回对 HtmlHead 对象的引用，该对象包含页眉。</span><span class="sxs-lookup"><span data-stu-id="eba46-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="eba46-228">可以使用返回的 HtmlHead 对象来获取/设置样式表、Meta 标记等。</span><span class="sxs-lookup"><span data-stu-id="eba46-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="eba46-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="eba46-229">IdSeparator</span></span>

<span data-ttu-id="eba46-230">此只读属性获取 ASP.NET 在为页上的控件生成唯一 ID 时用于分隔控件标识符的字符。</span><span class="sxs-lookup"><span data-stu-id="eba46-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="eba46-231">它不可直接通过代码使用。</span><span class="sxs-lookup"><span data-stu-id="eba46-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="eba46-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="eba46-232">IsAsync</span></span>

<span data-ttu-id="eba46-233">此属性允许异步页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="eba46-234">此模块稍后将讨论异步页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="eba46-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="eba46-235">IsCallback</span></span>

<span data-ttu-id="eba46-236">如果该页是回调的结果，则此只读属性返回**true** 。</span><span class="sxs-lookup"><span data-stu-id="eba46-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="eba46-237">本模块稍后将讨论调用支持。</span><span class="sxs-lookup"><span data-stu-id="eba46-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="eba46-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="eba46-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="eba46-239">如果页面是跨页面回发的一部分，则此只读属性返回**true** 。</span><span class="sxs-lookup"><span data-stu-id="eba46-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="eba46-240">本模块稍后将介绍跨页面回发。</span><span class="sxs-lookup"><span data-stu-id="eba46-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="eba46-241">项</span><span class="sxs-lookup"><span data-stu-id="eba46-241">Items</span></span>

<span data-ttu-id="eba46-242">返回对 IDictionary 实例的引用，该实例包含存储在页上下文中的所有对象。</span><span class="sxs-lookup"><span data-stu-id="eba46-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="eba46-243">可以将项添加到此 IDictionary 对象，它们将在上下文的整个生存期内可用。</span><span class="sxs-lookup"><span data-stu-id="eba46-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="eba46-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="eba46-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="eba46-245">此属性控制是否在发生回发后，ASP.NET 发出用于维护浏览器中的页面滚动位置的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="eba46-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="eba46-246">（此模块前面讨论了此属性的详细信息。）</span><span class="sxs-lookup"><span data-stu-id="eba46-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="eba46-247">主机</span><span class="sxs-lookup"><span data-stu-id="eba46-247">Master</span></span>

<span data-ttu-id="eba46-248">此只读属性返回对已应用母版页的页面的 MasterPage 实例的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="eba46-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="eba46-249">MasterPageFile</span></span>

<span data-ttu-id="eba46-250">获取或设置页面的母版页文件名。</span><span class="sxs-lookup"><span data-stu-id="eba46-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="eba46-251">只能在 PreInit 方法中设置此属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="eba46-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="eba46-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="eba46-253">此属性获取或设置页面状态的最大长度（以字节为单位）。</span><span class="sxs-lookup"><span data-stu-id="eba46-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="eba46-254">如果将属性设置为正数，则页面视图状态将被拆分为多个隐藏字段，以使其不超过指定的字节数。</span><span class="sxs-lookup"><span data-stu-id="eba46-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="eba46-255">如果该属性为负数，则视图状态不会分解为块。</span><span class="sxs-lookup"><span data-stu-id="eba46-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="eba46-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="eba46-256">PageAdapter</span></span>

<span data-ttu-id="eba46-257">返回对 PageAdapter 对象的引用，该对象修改请求浏览器的页。</span><span class="sxs-lookup"><span data-stu-id="eba46-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="eba46-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="eba46-258">PreviousPage</span></span>

<span data-ttu-id="eba46-259">返回对服务器传输或跨页面回发的情况下的上一页的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="eba46-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="eba46-260">SkinID</span></span>

<span data-ttu-id="eba46-261">指定要应用于页面的 ASP.NET 2.0 外观。</span><span class="sxs-lookup"><span data-stu-id="eba46-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="eba46-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="eba46-262">StyleSheetTheme</span></span>

<span data-ttu-id="eba46-263">此属性获取或设置应用于页面的样式表。</span><span class="sxs-lookup"><span data-stu-id="eba46-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="eba46-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="eba46-264">TemplateControl</span></span>

<span data-ttu-id="eba46-265">返回对页的包含控件的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="eba46-266">主题</span><span class="sxs-lookup"><span data-stu-id="eba46-266">Theme</span></span>

<span data-ttu-id="eba46-267">获取或设置应用于页面的 ASP.NET 2.0 主题的名称。</span><span class="sxs-lookup"><span data-stu-id="eba46-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="eba46-268">必须在 PreInit 方法之前设置此值。</span><span class="sxs-lookup"><span data-stu-id="eba46-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="eba46-269">标题</span><span class="sxs-lookup"><span data-stu-id="eba46-269">Title</span></span>

<span data-ttu-id="eba46-270">此属性获取或设置从页面页眉获取的页面的标题。</span><span class="sxs-lookup"><span data-stu-id="eba46-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="eba46-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="eba46-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="eba46-272">获取或设置页的 ViewStateEncryptionMode。</span><span class="sxs-lookup"><span data-stu-id="eba46-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="eba46-273">请参阅此模块前面的此属性的详细讨论。</span><span class="sxs-lookup"><span data-stu-id="eba46-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="eba46-274">页类的新的受保护属性</span><span class="sxs-lookup"><span data-stu-id="eba46-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="eba46-275">下面是 ASP.NET 2.0 中 Page 类的新保护属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="eba46-276">适配器</span><span class="sxs-lookup"><span data-stu-id="eba46-276">Adapter</span></span>

<span data-ttu-id="eba46-277">返回对在请求该页面的设备上呈现页面的 ControlAdapter 的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="eba46-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="eba46-278">AsyncMode</span></span>

<span data-ttu-id="eba46-279">此属性指示是否异步处理页。</span><span class="sxs-lookup"><span data-stu-id="eba46-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="eba46-280">它旨在供运行时使用，而不是直接在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="eba46-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="eba46-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="eba46-281">ClientIDSeparator</span></span>

<span data-ttu-id="eba46-282">此属性返回在为控件创建唯一的客户端 Id 时用作分隔符的字符。</span><span class="sxs-lookup"><span data-stu-id="eba46-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="eba46-283">它旨在供运行时使用，而不是直接在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="eba46-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="eba46-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="eba46-284">PageStatePersister</span></span>

<span data-ttu-id="eba46-285">此属性返回页的 PageStatePersister 对象。</span><span class="sxs-lookup"><span data-stu-id="eba46-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="eba46-286">此属性主要由 ASP.NET 控件开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="eba46-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="eba46-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="eba46-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="eba46-288">此属性返回追加到用于缓存浏览器的文件路径的唯一后缀。</span><span class="sxs-lookup"><span data-stu-id="eba46-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="eba46-289">默认值为 \_\_ufps = 和6位数字。</span><span class="sxs-lookup"><span data-stu-id="eba46-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="eba46-290">Page 类的新公共方法</span><span class="sxs-lookup"><span data-stu-id="eba46-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="eba46-291">以下公共方法是 ASP.NET 2.0 中 Page 类的新方法。</span><span class="sxs-lookup"><span data-stu-id="eba46-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="eba46-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="eba46-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="eba46-293">此方法为异步页执行注册事件处理程序委托。</span><span class="sxs-lookup"><span data-stu-id="eba46-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="eba46-294">此模块稍后将讨论异步页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="eba46-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="eba46-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="eba46-296">将页样式表中的属性应用于页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="eba46-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="eba46-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="eba46-298">此方法是一种异步任务。</span><span class="sxs-lookup"><span data-stu-id="eba46-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="eba46-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="eba46-299">GetValidators</span></span>

<span data-ttu-id="eba46-300">如果未指定，则返回指定验证组的验证程序的集合或默认验证组。</span><span class="sxs-lookup"><span data-stu-id="eba46-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="eba46-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="eba46-301">RegisterAsyncTask</span></span>

<span data-ttu-id="eba46-302">此方法注册新的异步任务。</span><span class="sxs-lookup"><span data-stu-id="eba46-302">This method registers a new async task.</span></span> <span data-ttu-id="eba46-303">此模块的后面部分介绍了异步页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="eba46-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="eba46-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="eba46-305">此方法告诉 ASP.NET，必须保留 pages 控件状态。</span><span class="sxs-lookup"><span data-stu-id="eba46-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="eba46-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="eba46-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="eba46-307">此方法告知 ASP.NET 页面视图状态要求加密。</span><span class="sxs-lookup"><span data-stu-id="eba46-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="eba46-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="eba46-308">ResolveClientUrl</span></span>

<span data-ttu-id="eba46-309">返回一个相对 URL，该 URL 可用于对图像的客户端请求等。</span><span class="sxs-lookup"><span data-stu-id="eba46-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="eba46-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="eba46-310">SetFocus</span></span>

<span data-ttu-id="eba46-311">此方法会将焦点设置到最初加载页面时指定的控件。</span><span class="sxs-lookup"><span data-stu-id="eba46-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="eba46-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="eba46-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="eba46-313">此方法将注销传递给它的控件，而不再需要控件状态持久性。</span><span class="sxs-lookup"><span data-stu-id="eba46-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="eba46-314">对页面生命周期的更改</span><span class="sxs-lookup"><span data-stu-id="eba46-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="eba46-315">ASP.NET 2.0 的页面生命周期未发生明显变化，但你应该注意一些新的方法。</span><span class="sxs-lookup"><span data-stu-id="eba46-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="eba46-316">ASP.NET 2.0 页面生命周期如下所述。</span><span class="sxs-lookup"><span data-stu-id="eba46-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="eba46-317">PreInit （ASP.NET 2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="eba46-318">PreInit 事件是开发人员可以访问的生命周期中的最早阶段。</span><span class="sxs-lookup"><span data-stu-id="eba46-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="eba46-319">添加此事件可以以编程方式更改 ASP.NET 2.0 主题、母版页、ASP.NET 2.0 配置文件的访问属性等。如果处于 "回发" 状态，则必须认识到在生命周期的这一点，视图状态尚未应用于控件。</span><span class="sxs-lookup"><span data-stu-id="eba46-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="eba46-320">因此，如果开发人员在此阶段更改控件的属性，则可能会在稍后的页面生命周期中覆盖该属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="eba46-321">Init</span><span class="sxs-lookup"><span data-stu-id="eba46-321">Init</span></span>

<span data-ttu-id="eba46-322">Init 事件未在 ASP.NET 1.x 中发生更改。</span><span class="sxs-lookup"><span data-stu-id="eba46-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="eba46-323">你需要在此页上读取或初始化控件的属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="eba46-324">在此阶段，母版页、主题等已应用于页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="eba46-325">InitComplete （2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="eba46-326">在页面初始化阶段结束时调用 InitComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="eba46-327">此时，你可以访问页面上的控件，但尚未填充其状态。</span><span class="sxs-lookup"><span data-stu-id="eba46-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="eba46-328">预加载（2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="eba46-329">此事件在所有回发数据已应用并刚好在页面\_负载之前调用。</span><span class="sxs-lookup"><span data-stu-id="eba46-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="eba46-330">Load</span><span class="sxs-lookup"><span data-stu-id="eba46-330">Load</span></span>

<span data-ttu-id="eba46-331">Load 事件未在 ASP.NET 1.x 中发生更改。</span><span class="sxs-lookup"><span data-stu-id="eba46-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="eba46-332">System.web.ui.page.loadcomplete （2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="eba46-333">System.web.ui.page.loadcomplete 事件是页面加载阶段中的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="eba46-334">在此阶段，所有回发和 viewstate 数据都已应用到页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="eba46-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="eba46-335">PreRender</span></span>

<span data-ttu-id="eba46-336">如果希望为动态添加到页面中的控件正确维护视图状态，则预呈现事件是最后添加它们的机会。</span><span class="sxs-lookup"><span data-stu-id="eba46-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="eba46-337">PreRenderComplete （2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="eba46-338">在 PreRenderComplete 阶段，所有控件都已添加到页面中，并且页已准备好进行呈现。</span><span class="sxs-lookup"><span data-stu-id="eba46-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="eba46-339">PreRenderComplete 事件是在保存页面 viewstate 之前引发的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="eba46-340">SaveStateComplete （2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="eba46-341">在保存所有页面视图状态和控件状态之后，会立即调用 SaveStateComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="eba46-342">这是页面实际呈现到浏览器之前的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="eba46-343">Render</span><span class="sxs-lookup"><span data-stu-id="eba46-343">Render</span></span>

<span data-ttu-id="eba46-344">自 ASP.NET 1.x 后，Render 方法尚未更改。</span><span class="sxs-lookup"><span data-stu-id="eba46-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="eba46-345">这是 HtmlTextWriter 的初始化位置，页面呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="eba46-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="eba46-346">ASP.NET 2.0 中的跨页面回发</span><span class="sxs-lookup"><span data-stu-id="eba46-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="eba46-347">在 ASP.NET 1.x 中，回发到相同的页面需要回发。</span><span class="sxs-lookup"><span data-stu-id="eba46-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="eba46-348">不允许跨页面回发。</span><span class="sxs-lookup"><span data-stu-id="eba46-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="eba46-349">ASP.NET 2.0 添加了通过 IButtonControl 接口回发到不同页的功能。</span><span class="sxs-lookup"><span data-stu-id="eba46-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="eba46-350">除了第三方自定义控件以外，任何实现新的 IButtonControl 接口（Button、LinkButton 和 ImageButton）的控件都可以通过使用 PostBackUrl 特性来利用此新功能。</span><span class="sxs-lookup"><span data-stu-id="eba46-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="eba46-351">下面的代码演示了一个按钮控件，该按钮控件回发到第二页。</span><span class="sxs-lookup"><span data-stu-id="eba46-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="eba46-352">页面回发后，可以通过第二页上的 PreviousPage 属性访问启动回发的页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="eba46-353">此功能通过新的 WebForm\_DoPostBackWithOptions 客户端函数实现，当控件回发到其他页时，ASP.NET 2.0 将呈现到页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="eba46-354">此 JavaScript 函数由将脚本发送到客户端的新 WebResource 处理程序提供。</span><span class="sxs-lookup"><span data-stu-id="eba46-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="eba46-355">以下视频是跨页面回发的演练。</span><span class="sxs-lookup"><span data-stu-id="eba46-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="eba46-356">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="eba46-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="eba46-357">跨页面回发的详细信息</span><span class="sxs-lookup"><span data-stu-id="eba46-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="eba46-358">Viewstate</span><span class="sxs-lookup"><span data-stu-id="eba46-358">Viewstate</span></span>

<span data-ttu-id="eba46-359">您可能已就跨页面回发方案的第一页中的视图状态进行了询问。</span><span class="sxs-lookup"><span data-stu-id="eba46-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="eba46-360">毕竟，任何未实现 IPostBackDataHandler 的控件都将通过 viewstate 保持其状态，因此，若要在跨页面回发的第二页上访问该控件的属性，您必须对该页的视图状态具有访问权限。</span><span class="sxs-lookup"><span data-stu-id="eba46-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="eba46-361">ASP.NET 2.0 使用名为 \_\_PREVIOUSPAGE 的第二页中的新隐藏字段来处理这种情况。</span><span class="sxs-lookup"><span data-stu-id="eba46-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="eba46-362">\_\_PREVIOUSPAGE 窗体字段包含第一页的视图状态，以便您可以访问第二页中所有控件的属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="eba46-363">规避 FindControl</span><span class="sxs-lookup"><span data-stu-id="eba46-363">Circumventing FindControl</span></span>

<span data-ttu-id="eba46-364">在跨页面回发的视频演练中，我使用了 FindControl 方法获取对第一页上 TextBox 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="eba46-365">这种方法非常适用于这种用途，但 FindControl 的开销很高，需要编写其他代码。</span><span class="sxs-lookup"><span data-stu-id="eba46-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="eba46-366">幸运的是，在许多情况下，ASP.NET 2.0 为此目的提供了 FindControl 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="eba46-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="eba46-367">使用 PreviousPageType 指令，可以通过使用 TypeName 或 VirtualPath 属性对上一页进行强类型引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="eba46-368">TypeName 属性允许您指定上一页的类型，而 VirtualPath 属性允许您使用虚拟路径引用上一页。</span><span class="sxs-lookup"><span data-stu-id="eba46-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="eba46-369">设置 PreviousPageType 指令后，必须使用公共属性公开要允许其访问的控件等。</span><span class="sxs-lookup"><span data-stu-id="eba46-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="eba46-370">实验室1跨页面回发</span><span class="sxs-lookup"><span data-stu-id="eba46-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="eba46-371">在此实验室中，您将创建一个应用程序，该应用程序使用 ASP.NET 2.0 的新跨页面回发功能。</span><span class="sxs-lookup"><span data-stu-id="eba46-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="eba46-372">打开 Visual Studio 2005 并创建新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="eba46-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="eba46-373">添加一个名为 page2 的新 Webform。</span><span class="sxs-lookup"><span data-stu-id="eba46-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="eba46-374">在设计视图中打开 default.aspx 并添加 "按钮" 控件和 "TextBox" 控件。</span><span class="sxs-lookup"><span data-stu-id="eba46-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="eba46-375">为 "Button" 控件指定 ID " **SubmitButton** "，并在文本框中控制**用户名**的 id。</span><span class="sxs-lookup"><span data-stu-id="eba46-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="eba46-376">将按钮的 PostBackUrl 属性设置为 page2。</span><span class="sxs-lookup"><span data-stu-id="eba46-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="eba46-377">在源视图中打开 page2。</span><span class="sxs-lookup"><span data-stu-id="eba46-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="eba46-378">添加 @ PreviousPageType 指令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="eba46-379">将以下代码添加到 page2 的代码隐藏页\_负载：</span><span class="sxs-lookup"><span data-stu-id="eba46-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="eba46-380">通过单击 "生成" 菜单上的 "生成" 来生成项目。</span><span class="sxs-lookup"><span data-stu-id="eba46-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="eba46-381">将以下代码添加到 default.aspx 的代码隐藏中：</span><span class="sxs-lookup"><span data-stu-id="eba46-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="eba46-382">将 page2 中的页\_负载更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="eba46-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="eba46-383">生成项目。</span><span class="sxs-lookup"><span data-stu-id="eba46-383">Build the project.</span></span>
11. <span data-ttu-id="eba46-384">运行该项目。</span><span class="sxs-lookup"><span data-stu-id="eba46-384">Run the project.</span></span>
12. <span data-ttu-id="eba46-385">在文本框中输入您的姓名，然后单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="eba46-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="eba46-386">结果是什么？</span><span class="sxs-lookup"><span data-stu-id="eba46-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="eba46-387">ASP.NET 2.0 中的异步页面</span><span class="sxs-lookup"><span data-stu-id="eba46-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="eba46-388">ASP.NET 中的许多争用问题都是由外部调用（如 Web 服务或数据库调用）延迟、文件 IO 延迟等引起的。对 ASP.NET 应用程序发出请求时，ASP.NET 会使用其工作线程之一来处理请求。</span><span class="sxs-lookup"><span data-stu-id="eba46-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="eba46-389">请求完成并发送响应之前，该请求拥有该线程。</span><span class="sxs-lookup"><span data-stu-id="eba46-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="eba46-390">ASP.NET 2.0 通过添加以异步方式执行页面的功能，查找解决此类问题的延迟问题。</span><span class="sxs-lookup"><span data-stu-id="eba46-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="eba46-391">这意味着，工作线程可以启动请求，然后将其他执行移交给另一个线程，从而快速返回到可用线程池。</span><span class="sxs-lookup"><span data-stu-id="eba46-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="eba46-392">文件 IO、数据库调用等完成后，将从线程池中获取一个新线程来完成请求。</span><span class="sxs-lookup"><span data-stu-id="eba46-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="eba46-393">使页面异步执行的第一步是设置页面指令的**Async**属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="eba46-394">此属性告知 ASP.NET 实现页面的 IHttpAsyncHandler。</span><span class="sxs-lookup"><span data-stu-id="eba46-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="eba46-395">下一步是在页面生命周期中的某个时间点调用 AddOnPreRenderCompleteAsync 方法，然后再开始呈现。</span><span class="sxs-lookup"><span data-stu-id="eba46-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="eba46-396">（此方法通常在页\_负载中调用。）AddOnPreRenderCompleteAsync 方法采用两个参数;一个来和一个 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="eba46-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="eba46-397">来返回 IAsyncResult，然后将其作为参数传递给 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="eba46-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="eba46-398">以下视频是异步页面请求的演练。</span><span class="sxs-lookup"><span data-stu-id="eba46-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="eba46-399">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="eba46-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="eba46-400">在 EndEventHandler 完成之前，async page 不会呈现给浏览器。</span><span class="sxs-lookup"><span data-stu-id="eba46-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="eba46-401">毫无疑问，但某些开发人员会将异步请求视为类似于异步回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="eba46-402">请注意，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="eba46-402">It's important to realize that they are not.</span></span> <span data-ttu-id="eba46-403">异步请求的好处是，第一个工作线程可以返回给线程池以处理新请求，从而减少由于 IO 绑定等原因导致的争用。</span><span class="sxs-lookup"><span data-stu-id="eba46-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="eba46-404">ASP.NET 2.0 中的脚本回调</span><span class="sxs-lookup"><span data-stu-id="eba46-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="eba46-405">Web 开发人员一直在寻找阻止与回叫关联的闪烁的方式。</span><span class="sxs-lookup"><span data-stu-id="eba46-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="eba46-406">在 ASP.NET 1.x 中，SmartNavigation 是避免闪烁的最常见方法，但 SmartNavigation 为某些开发人员带来了问题，因为它在客户端上的实现复杂度很高。</span><span class="sxs-lookup"><span data-stu-id="eba46-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="eba46-407">ASP.NET 2.0 解决了脚本回调的这一问题。</span><span class="sxs-lookup"><span data-stu-id="eba46-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="eba46-408">脚本回调利用 XMLHttp 通过 JavaScript 向 Web 服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="eba46-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="eba46-409">XMLHttp 请求返回可通过浏览器的 DOM 操作的 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="eba46-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="eba46-410">新的 WebResource 处理程序对用户隐藏了 XMLHttp 代码。</span><span class="sxs-lookup"><span data-stu-id="eba46-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="eba46-411">在 ASP.NET 2.0 中配置脚本回叫需要几个步骤。</span><span class="sxs-lookup"><span data-stu-id="eba46-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="eba46-412">步骤1：实现 ICallbackEventHandler 接口</span><span class="sxs-lookup"><span data-stu-id="eba46-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="eba46-413">为了使 ASP.NET 能够将页面视为参与脚本回调，必须实现 ICallbackEventHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="eba46-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="eba46-414">可在代码隐藏文件中执行此操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="eba46-415">还可以使用 @ Implements 指令执行此操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="eba46-416">使用内联 ASP.NET 代码时，通常使用 @ Implements 指令。</span><span class="sxs-lookup"><span data-stu-id="eba46-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="eba46-417">步骤2：调用 GetCallbackEventReference</span><span class="sxs-lookup"><span data-stu-id="eba46-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="eba46-418">如前所述，XMLHttp 调用封装在 WebResource 处理程序中。</span><span class="sxs-lookup"><span data-stu-id="eba46-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="eba46-419">呈现页面时，ASP.NET 将添加对 WebForm\_DoCallback 的调用，该脚本是由 WebResource 提供的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="eba46-420">WebForm\_DoCallback 函数将替换回调的 \_\_doPostBack 函数。</span><span class="sxs-lookup"><span data-stu-id="eba46-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="eba46-421">请记住，\_\_doPostBack 以编程方式在页面上提交窗体。</span><span class="sxs-lookup"><span data-stu-id="eba46-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="eba46-422">在回调方案中，您想要阻止回发，因此 \_\_doPostBack 将无法满足要求。</span><span class="sxs-lookup"><span data-stu-id="eba46-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="eba46-423">\_\_doPostBack 仍在客户端脚本回调方案中呈现给页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="eba46-424">但是，它不用于回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="eba46-425">WebForm\_DoCallback 客户端函数的参数是通过服务器端函数 GetCallbackEventReference 提供的，该函数通常会在页面\_负载中调用。</span><span class="sxs-lookup"><span data-stu-id="eba46-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="eba46-426">典型的 GetCallbackEventReference 调用可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="eba46-427">在这种情况下，cm 是 ClientScriptManager 的实例。</span><span class="sxs-lookup"><span data-stu-id="eba46-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="eba46-428">本模块稍后将介绍 ClientScriptManager 类。</span><span class="sxs-lookup"><span data-stu-id="eba46-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="eba46-429">GetCallbackEventReference 有几个重载版本。</span><span class="sxs-lookup"><span data-stu-id="eba46-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="eba46-430">在这种情况下，参数如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="eba46-431">对在其中调用 GetCallbackEventReference 的控件的引用。</span><span class="sxs-lookup"><span data-stu-id="eba46-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="eba46-432">在这种情况下，它是页面本身。</span><span class="sxs-lookup"><span data-stu-id="eba46-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="eba46-433">将从客户端代码传递到服务器端事件的字符串参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="eba46-434">在这种情况下，Im 传递名为 ddlCompany 的下拉列表的值。</span><span class="sxs-lookup"><span data-stu-id="eba46-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="eba46-435">将接受来自服务器端回调事件的返回值（字符串）的客户端函数的名称。</span><span class="sxs-lookup"><span data-stu-id="eba46-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="eba46-436">只有服务器端回调成功时，才会调用此函数。</span><span class="sxs-lookup"><span data-stu-id="eba46-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="eba46-437">因此，为实现稳定性，通常建议使用 GetCallbackEventReference 的重载版本，该版本使用额外的字符串参数指定在发生错误时要执行的客户端函数的名称。</span><span class="sxs-lookup"><span data-stu-id="eba46-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="eba46-438">表示它在回调服务器之前启动的客户端函数的字符串。</span><span class="sxs-lookup"><span data-stu-id="eba46-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="eba46-439">在这种情况下，没有这样的脚本，因此参数为 null。</span><span class="sxs-lookup"><span data-stu-id="eba46-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="eba46-440">指定是否异步执行回调的布尔值。</span><span class="sxs-lookup"><span data-stu-id="eba46-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="eba46-441">对客户端上的 WebForm\_DoCallback 的调用将传递这些参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="eba46-442">因此，当在客户端上呈现此页时，该代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="eba46-443">请注意，客户端上函数的签名有点不同。</span><span class="sxs-lookup"><span data-stu-id="eba46-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="eba46-444">客户端函数传递5个字符串和一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="eba46-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="eba46-445">附加字符串（在上面的示例中为 null）包含将处理服务器端回调中的任何错误的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="eba46-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="eba46-446">步骤3：挂钩客户端控件事件</span><span class="sxs-lookup"><span data-stu-id="eba46-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="eba46-447">请注意，上面 GetCallbackEventReference 的返回值已分配给字符串变量。</span><span class="sxs-lookup"><span data-stu-id="eba46-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="eba46-448">该字符串用于挂钩启动回调的控件的客户端事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="eba46-449">在此示例中，回调由页面上的下拉列表启动，因此我想要挂钩*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="eba46-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="eba46-450">若要挂钩客户端事件，只需按如下所示将处理程序添加到客户端标记：</span><span class="sxs-lookup"><span data-stu-id="eba46-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="eba46-451">请记住， *cbRef*是对 GetCallbackEventReference 的调用的返回值。</span><span class="sxs-lookup"><span data-stu-id="eba46-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="eba46-452">它包含上面所示的对 WebForm\_DoCallback 的调用。</span><span class="sxs-lookup"><span data-stu-id="eba46-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="eba46-453">步骤4：注册客户端脚本</span><span class="sxs-lookup"><span data-stu-id="eba46-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="eba46-454">请注意，调用 GetCallbackEventReference 指定了服务器端回调成功时，将执行名为**ShowCompanyName**的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="eba46-455">该脚本需要使用 ClientScriptManager 实例添加到页面。</span><span class="sxs-lookup"><span data-stu-id="eba46-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="eba46-456">（本模块稍后将讨论 ClientScriptManager 类。）如下所示：</span><span class="sxs-lookup"><span data-stu-id="eba46-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="eba46-457">步骤5：调用 ICallbackEventHandler 接口的方法</span><span class="sxs-lookup"><span data-stu-id="eba46-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="eba46-458">ICallbackEventHandler 包含两个需要在代码中实现的方法。</span><span class="sxs-lookup"><span data-stu-id="eba46-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="eba46-459">它们分别是**RaiseCallbackEvent**和**GetCallbackEvent**。</span><span class="sxs-lookup"><span data-stu-id="eba46-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="eba46-460">**RaiseCallbackEvent**采用字符串作为参数，并且不返回任何内容。</span><span class="sxs-lookup"><span data-stu-id="eba46-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="eba46-461">字符串自变量将从客户端对 WebForm\_DoCallback 的调用传递。</span><span class="sxs-lookup"><span data-stu-id="eba46-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="eba46-462">在这种情况下，该值是名为 ddlCompany 的 dropdown 的*value*属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="eba46-463">服务器端代码应放置在 RaiseCallbackEvent 方法中。</span><span class="sxs-lookup"><span data-stu-id="eba46-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="eba46-464">例如，如果你的回调正在对外部资源进行 WebRequest，则该代码应放置在 RaiseCallbackEvent 中。</span><span class="sxs-lookup"><span data-stu-id="eba46-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="eba46-465">**GetCallbackEvent**负责处理返回给客户端的回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="eba46-466">它不采用任何参数并返回字符串。</span><span class="sxs-lookup"><span data-stu-id="eba46-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="eba46-467">它返回的字符串将作为参数传递到客户端函数（在本例中为*ShowCompanyName*）。</span><span class="sxs-lookup"><span data-stu-id="eba46-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="eba46-468">完成上述步骤后，即可在 ASP.NET 2.0 中执行脚本回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="eba46-469">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="eba46-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="eba46-470">支持发出 XMLHttp 调用的任何浏览器都支持 ASP.NET 中的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="eba46-471">这包括目前正在使用的所有新式浏览器。</span><span class="sxs-lookup"><span data-stu-id="eba46-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="eba46-472">Internet Explorer 使用 XMLHttp ActiveX 对象，而其他新式浏览器（包括即将推出的 IE 7）使用内部 XMLHttp 对象。</span><span class="sxs-lookup"><span data-stu-id="eba46-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="eba46-473">若要以编程方式确定浏览器是否支持回调，可以使用**SupportCallback**属性。</span><span class="sxs-lookup"><span data-stu-id="eba46-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="eba46-474">如果请求的客户端支持脚本回调，则此属性将返回**true** 。</span><span class="sxs-lookup"><span data-stu-id="eba46-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="eba46-475">在 ASP.NET 2.0 中使用客户端脚本</span><span class="sxs-lookup"><span data-stu-id="eba46-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="eba46-476">ASP.NET 2.0 中的客户端脚本通过使用 ClientScriptManager 类进行管理。</span><span class="sxs-lookup"><span data-stu-id="eba46-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="eba46-477">ClientScriptManager 类跟踪使用类型和名称的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="eba46-478">这可以防止在页上以编程方式多次插入同一脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="eba46-479">在页面上成功注册了脚本后，任何以后注册同一个脚本的尝试都将导致脚本不会第二次注册。</span><span class="sxs-lookup"><span data-stu-id="eba46-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="eba46-480">不会添加重复的脚本，也不会发生任何异常。</span><span class="sxs-lookup"><span data-stu-id="eba46-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="eba46-481">若要避免不必要的计算，可以使用一些方法来确定脚本是否已注册，以便不会多次尝试注册。</span><span class="sxs-lookup"><span data-stu-id="eba46-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="eba46-482">所有当前 ASP.NET 开发人员都应该熟悉 ClientScriptManager 的方法：</span><span class="sxs-lookup"><span data-stu-id="eba46-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="eba46-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="eba46-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="eba46-484">此方法将脚本添加到呈现的页面的顶部。</span><span class="sxs-lookup"><span data-stu-id="eba46-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="eba46-485">这对于添加将在客户端上显式调用的函数很有用。</span><span class="sxs-lookup"><span data-stu-id="eba46-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="eba46-486">此方法有两个重载版本。</span><span class="sxs-lookup"><span data-stu-id="eba46-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="eba46-487">其中有三个参数共同。</span><span class="sxs-lookup"><span data-stu-id="eba46-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="eba46-488">它们是：</span><span class="sxs-lookup"><span data-stu-id="eba46-488">They are:</span></span>

`type (string)`

<span data-ttu-id="eba46-489">***类型***参数标识脚本的类型。</span><span class="sxs-lookup"><span data-stu-id="eba46-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="eba46-490">通常最好使用页面的类型（此为。类型的 GetType （））。</span><span class="sxs-lookup"><span data-stu-id="eba46-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="eba46-491">***Key***参数是该脚本的用户定义的键。</span><span class="sxs-lookup"><span data-stu-id="eba46-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="eba46-492">对于每个脚本，这应该是唯一的。</span><span class="sxs-lookup"><span data-stu-id="eba46-492">This should be unique for each script.</span></span> <span data-ttu-id="eba46-493">如果尝试添加的脚本的键和类型与已添加的脚本的类型相同，则不会添加该脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="eba46-494">***脚本***参数是包含要添加的实际脚本的字符串。</span><span class="sxs-lookup"><span data-stu-id="eba46-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="eba46-495">建议使用 StringBuilder 创建脚本，然后对 StringBuilder 使用 ToString （）方法以分配***脚本***参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="eba46-496">如果使用只使用三个参数的重载 Page.clientscript.registerclientscriptblock，则必须在脚本中包含 script 元素（&lt;script&gt; 和 &lt;/script&gt;）。</span><span class="sxs-lookup"><span data-stu-id="eba46-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="eba46-497">您可以选择使用 Page.clientscript.registerclientscriptblock 的重载，该重载采用第四个参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="eba46-498">第四个参数是一个布尔值，该值指定 ASP.NET 是否应为您添加脚本元素。</span><span class="sxs-lookup"><span data-stu-id="eba46-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="eba46-499">如果此参数为**true**，则脚本不应显式包含脚本元素。</span><span class="sxs-lookup"><span data-stu-id="eba46-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="eba46-500">使用 IsClientScriptBlockRegistered 方法来确定脚本是否已注册。</span><span class="sxs-lookup"><span data-stu-id="eba46-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="eba46-501">这使你可以避免尝试重新注册已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="eba46-502">RegisterClientScriptInclude （2.0 中的新增项）</span><span class="sxs-lookup"><span data-stu-id="eba46-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="eba46-503">RegisterClientScriptInclude 标记创建链接到外部脚本文件的脚本块。</span><span class="sxs-lookup"><span data-stu-id="eba46-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="eba46-504">它有两个重载。</span><span class="sxs-lookup"><span data-stu-id="eba46-504">It has two overloads.</span></span> <span data-ttu-id="eba46-505">一个使用密钥和 URL。</span><span class="sxs-lookup"><span data-stu-id="eba46-505">One takes a key and a URL.</span></span> <span data-ttu-id="eba46-506">第二个添加指定类型的第三个参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="eba46-507">例如，下面的代码生成一个脚本块，该脚本块链接到应用程序的 scripts 文件夹的根目录中的 jsfunctions：</span><span class="sxs-lookup"><span data-stu-id="eba46-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="eba46-508">此代码在呈现的页中生成以下代码：</span><span class="sxs-lookup"><span data-stu-id="eba46-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="eba46-509">脚本块呈现在页面的底部。</span><span class="sxs-lookup"><span data-stu-id="eba46-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="eba46-510">使用 IsClientScriptIncludeRegistered 方法来确定脚本是否已注册。</span><span class="sxs-lookup"><span data-stu-id="eba46-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="eba46-511">这样可以避免尝试重新注册脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="eba46-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="eba46-512">RegisterStartupScript</span></span>

<span data-ttu-id="eba46-513">Page.clientscript.registerstartupscript 方法采用与 Page.clientscript.registerclientscriptblock 方法相同的参数。</span><span class="sxs-lookup"><span data-stu-id="eba46-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="eba46-514">使用 Page.clientscript.registerstartupscript 注册的脚本在页面加载后，但在 OnLoad 客户端事件之前执行。</span><span class="sxs-lookup"><span data-stu-id="eba46-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="eba46-515">在1.x 中，向 Page.clientscript.registerstartupscript 注册的脚本放置在结束 &lt;/form&gt; 标记之前，而向 Page.clientscript.registerclientscriptblock 注册的脚本则紧靠在开始 &lt;窗体&gt; 标记之后。</span><span class="sxs-lookup"><span data-stu-id="eba46-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="eba46-516">在 ASP.NET 2.0 中，两者紧靠在结束 &lt;/form&gt; 标记之前。</span><span class="sxs-lookup"><span data-stu-id="eba46-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="eba46-517">如果向 Page.clientscript.registerstartupscript 注册一个函数，则在客户端代码中显式调用该函数之前，该函数将不会执行。</span><span class="sxs-lookup"><span data-stu-id="eba46-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="eba46-518">使用 IsStartupScriptRegistered 方法来确定脚本是否已注册，并避免尝试重新注册脚本。</span><span class="sxs-lookup"><span data-stu-id="eba46-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="eba46-519">其他 ClientScriptManager 方法</span><span class="sxs-lookup"><span data-stu-id="eba46-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="eba46-520">下面是 ClientScriptManager 类的一些其他有用方法。</span><span class="sxs-lookup"><span data-stu-id="eba46-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="eba46-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="eba46-522">请参阅此模块前面的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="eba46-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="eba46-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="eba46-524">获取可用于从客户端事件回发的 JavaScript 引用（javascript：&lt;调用&gt;）。</span><span class="sxs-lookup"><span data-stu-id="eba46-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="eba46-525"><strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="eba46-526">获取一个字符串，该字符串可用于从客户端启动回发。</span><span class="sxs-lookup"><span data-stu-id="eba46-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="eba46-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="eba46-528">返回嵌入到程序集中的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="eba46-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="eba46-529">必须与<strong>RegisterClientScriptResource</strong>结合使用。</span><span class="sxs-lookup"><span data-stu-id="eba46-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="eba46-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="eba46-531">向页注册 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="eba46-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="eba46-532">这些资源嵌入在程序集中，并由新的 WebResource 处理程序进行处理。</span><span class="sxs-lookup"><span data-stu-id="eba46-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="eba46-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="eba46-534">向页面注册一个隐藏的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="eba46-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="eba46-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="eba46-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="eba46-536">注册在提交 HTML 窗体时执行的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="eba46-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |

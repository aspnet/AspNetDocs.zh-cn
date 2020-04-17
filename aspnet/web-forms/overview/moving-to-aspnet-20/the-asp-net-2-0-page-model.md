---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页型号 |微软文档
author: rick-anderson
description: 在ASP.NET 1.x 中，开发人员可以选择内联代码模型和代码背后的代码模型。 代码后面可以使用 Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542854"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="1112a-104">ASP.NET 2.0 页型号</span><span class="sxs-lookup"><span data-stu-id="1112a-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="1112a-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1112a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1112a-106">在ASP.NET 1.x 中，开发人员可以选择内联代码模型和代码背后的代码模型。</span><span class="sxs-lookup"><span data-stu-id="1112a-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="1112a-107">可以使用 Src 属性或@Page指令的 Code 背后属性实现代码后面。</span><span class="sxs-lookup"><span data-stu-id="1112a-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="1112a-108">在ASP.NET 2.0 中，开发人员在内联代码和代码后面之间仍有选择，但代码背后的模型有显著的增强功能。</span><span class="sxs-lookup"><span data-stu-id="1112a-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="1112a-109">在ASP.NET 1.x 中，开发人员可以选择内联代码模型和代码背后的代码模型。</span><span class="sxs-lookup"><span data-stu-id="1112a-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="1112a-110">可以使用 Src 属性或@Page指令的 Code 背后属性实现代码后面。</span><span class="sxs-lookup"><span data-stu-id="1112a-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="1112a-111">在ASP.NET 2.0 中，开发人员在内联代码和代码后面之间仍有选择，但代码背后的模型有显著的增强功能。</span><span class="sxs-lookup"><span data-stu-id="1112a-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="1112a-112">代码后模型的改进</span><span class="sxs-lookup"><span data-stu-id="1112a-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="1112a-113">为了充分理解ASP.NET 2.0 中代码背后的更改，最好快速查看模型，因为它存在于ASP.NET 1.x 中。</span><span class="sxs-lookup"><span data-stu-id="1112a-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="1112a-114">ASP.NET 1.x 中的代码后模型</span><span class="sxs-lookup"><span data-stu-id="1112a-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="1112a-115">在ASP.NET 1.x 中，代码后面模型由 ASPX 文件（Webform）和包含编程代码的代码后文件组成。</span><span class="sxs-lookup"><span data-stu-id="1112a-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="1112a-116">两个文件使用 ASPX@Page文件中的指令连接。</span><span class="sxs-lookup"><span data-stu-id="1112a-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="1112a-117">ASPX 页面上的每个控件在代码后面的文件中都有相应的声明作为实例变量。</span><span class="sxs-lookup"><span data-stu-id="1112a-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="1112a-118">代码背后的文件还包含事件绑定的代码和 Visual Studio 设计器所需的生成代码。</span><span class="sxs-lookup"><span data-stu-id="1112a-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="1112a-119">此模型工作相当良好，但由于 ASPX 页中的每个ASP.NET元素都需要代码背后的文件中的相应代码，因此代码和内容没有真正的分离。</span><span class="sxs-lookup"><span data-stu-id="1112a-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="1112a-120">例如，如果设计器向 Visual Studio IDE 外部的 ASPX 文件添加了新的服务器控件，则应用程序将由于代码背后的文件中缺少该控件的声明而中断。</span><span class="sxs-lookup"><span data-stu-id="1112a-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="1112a-121">ASP.NET 2.0 中的代码后模型</span><span class="sxs-lookup"><span data-stu-id="1112a-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="1112a-122">ASP.NET 2.0 大大改进了此模型。</span><span class="sxs-lookup"><span data-stu-id="1112a-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="1112a-123">在 ASP.NET 2.0 中，使用 ASP.NET 2.0 中提供的新*部分类*实现代码后面。</span><span class="sxs-lookup"><span data-stu-id="1112a-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="1112a-124">ASP.NET 2.0 中的代码后面类定义为部分类，这意味着它只包含类定义的一部分。</span><span class="sxs-lookup"><span data-stu-id="1112a-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="1112a-125">类定义的其余部分由 ASP.NET 2.0 在运行时或使用 ASPX 页或预编译网站时动态生成。</span><span class="sxs-lookup"><span data-stu-id="1112a-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="1112a-126">代码背后的文件和 ASPX 页之间的链接仍使用 @ Page 指令建立。</span><span class="sxs-lookup"><span data-stu-id="1112a-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="1112a-127">但是，ASP.NET 2.0 现在使用 CodeFile 属性，而不是代码背后或 Src 属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="1112a-128">继承属性还用于指定页面的类名称。</span><span class="sxs-lookup"><span data-stu-id="1112a-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="1112a-129">典型的 @ 页面指令可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="1112a-130">ASP.NET 2.0 代码背后的文件中的典型类定义可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="1112a-131">C# 和 Visual Basic 是当前支持部分类的唯一托管语言。</span><span class="sxs-lookup"><span data-stu-id="1112a-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="1112a-132">因此，使用 J# 的开发人员将无法在 ASP.NET 2.0 中使用代码后面模型。</span><span class="sxs-lookup"><span data-stu-id="1112a-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="1112a-133">新模型增强了代码背后的模型，因为开发人员现在将具有仅包含他们创建的代码的代码文件。</span><span class="sxs-lookup"><span data-stu-id="1112a-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="1112a-134">它还提供了代码和内容的真正分离，因为代码后面的文件中没有实例变量声明。</span><span class="sxs-lookup"><span data-stu-id="1112a-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="1112a-135">由于 ASPX 页的部分类是事件绑定发生的位置，因此 Visual Basic 开发人员可以通过在代码后面中使用 Handles 关键字绑定事件来实现轻微的性能提升。</span><span class="sxs-lookup"><span data-stu-id="1112a-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="1112a-136">C# 没有等效关键字。</span><span class="sxs-lookup"><span data-stu-id="1112a-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="1112a-137">新建 = 页面指令属性</span><span class="sxs-lookup"><span data-stu-id="1112a-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="1112a-138">ASP.NET 2.0 向 @ Page 指令添加了许多新属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="1112a-139">以下属性在 ASP.NET 2.0 中是新的。</span><span class="sxs-lookup"><span data-stu-id="1112a-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="1112a-140">Async</span><span class="sxs-lookup"><span data-stu-id="1112a-140">Async</span></span>

<span data-ttu-id="1112a-141">Async 属性允许您配置要异步执行的页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="1112a-142">本模块稍后将介绍异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="1112a-143">同步超时</span><span class="sxs-lookup"><span data-stu-id="1112a-143">AsyncTimeout</span></span>

<span data-ttu-id="1112a-144">指定异步页面的超时。</span><span class="sxs-lookup"><span data-stu-id="1112a-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="1112a-145">默认值为 45 秒。</span><span class="sxs-lookup"><span data-stu-id="1112a-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="1112a-146">代码文件</span><span class="sxs-lookup"><span data-stu-id="1112a-146">CodeFile</span></span>

<span data-ttu-id="1112a-147">CodeFile 属性是 Visual Studio 2002/2003 中 CodeForin 属性的替换。</span><span class="sxs-lookup"><span data-stu-id="1112a-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="1112a-148">代码文件基础类</span><span class="sxs-lookup"><span data-stu-id="1112a-148">CodeFileBaseClass</span></span>

<span data-ttu-id="1112a-149">在希望多个页面从单个基类派生的情况下，使用 CodeFileBaseClass 属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="1112a-150">由于在ASP.NET中实现部分类，如果没有此属性，使用共享公共字段引用在 ASPX 页中声明的控件的基类将无法正常工作，因为 ASP.NETs 编译引擎将根据页面中的控件自动创建新成员。</span><span class="sxs-lookup"><span data-stu-id="1112a-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="1112a-151">因此，如果要在ASP.NET中为两个或多个页面定义一个公共基类，则需要在 CodeFileBaseClass 属性中定义指定基类，然后从该基类派生每个页面类。</span><span class="sxs-lookup"><span data-stu-id="1112a-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="1112a-152">使用此属性时，也需要 CodeFile 属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="1112a-153">编译模式</span><span class="sxs-lookup"><span data-stu-id="1112a-153">CompilationMode</span></span>

<span data-ttu-id="1112a-154">此属性允许您设置 ASPX 页的编译模式属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="1112a-155">"编译模式"属性是包含值 **"始终**、**自动**"和 **"从不"** 的枚举。</span><span class="sxs-lookup"><span data-stu-id="1112a-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="1112a-156">默认值为 **"始终**"。</span><span class="sxs-lookup"><span data-stu-id="1112a-156">The default is **Always**.</span></span> <span data-ttu-id="1112a-157">如果可能，**自动**设置将阻止ASP.NET动态编译页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="1112a-158">从动态编译中排除页面可提高性能。</span><span class="sxs-lookup"><span data-stu-id="1112a-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="1112a-159">但是，如果排除的页面包含必须编译的代码，则在浏览页面时将引发错误。</span><span class="sxs-lookup"><span data-stu-id="1112a-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="1112a-160">启用事件验证</span><span class="sxs-lookup"><span data-stu-id="1112a-160">EnableEventValidation</span></span>

<span data-ttu-id="1112a-161">此属性指定是否验证回退和回调事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="1112a-162">启用此功能后，将检查用于回退或回调事件的参数，以确保它们源自最初呈现这些事件的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="1112a-163">启用"启用"</span><span class="sxs-lookup"><span data-stu-id="1112a-163">EnableTheming</span></span>

<span data-ttu-id="1112a-164">此属性指定ASP.NET主题是否在页面上使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="1112a-165">默认值为**false**。</span><span class="sxs-lookup"><span data-stu-id="1112a-165">The default is **false**.</span></span> <span data-ttu-id="1112a-166">ASP.NET主题在第[10单元](profiles-themes-and-web-parts.md)中介绍。</span><span class="sxs-lookup"><span data-stu-id="1112a-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="1112a-167">线普拉格玛斯</span><span class="sxs-lookup"><span data-stu-id="1112a-167">LinePragmas</span></span>

<span data-ttu-id="1112a-168">此属性指定是否应在编译期间添加行杂注。</span><span class="sxs-lookup"><span data-stu-id="1112a-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="1112a-169">行杂注是调试器用于标记代码特定部分的选项。</span><span class="sxs-lookup"><span data-stu-id="1112a-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="1112a-170">保持滚动位置后回</span><span class="sxs-lookup"><span data-stu-id="1112a-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="1112a-171">此属性指定是否将 JavaScript 注入页面以保持回退之间的滚动位置。</span><span class="sxs-lookup"><span data-stu-id="1112a-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="1112a-172">默认情况下，此属性**为 false。**</span><span class="sxs-lookup"><span data-stu-id="1112a-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="1112a-173">当此属性为**true**时，ASP.NET&lt;将在&gt;回退后添加如下所示的脚本块：</span><span class="sxs-lookup"><span data-stu-id="1112a-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="1112a-174">请注意，此脚本块的 src 是 WebResource.axd。</span><span class="sxs-lookup"><span data-stu-id="1112a-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="1112a-175">此资源不是物理路径。</span><span class="sxs-lookup"><span data-stu-id="1112a-175">This resource is not a physical path.</span></span> <span data-ttu-id="1112a-176">请求此脚本时，ASP.NET动态生成脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="1112a-177">母版页面文件</span><span class="sxs-lookup"><span data-stu-id="1112a-177">MasterPageFile</span></span>

<span data-ttu-id="1112a-178">此属性指定当前页面的主页文件。</span><span class="sxs-lookup"><span data-stu-id="1112a-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="1112a-179">路径可以是相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="1112a-179">The path can be relative or absolute.</span></span> <span data-ttu-id="1112a-180">母版页在[单元 4](master-pages.md)中介绍。</span><span class="sxs-lookup"><span data-stu-id="1112a-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="1112a-181">样式表主题</span><span class="sxs-lookup"><span data-stu-id="1112a-181">StyleSheetTheme</span></span>

<span data-ttu-id="1112a-182">此属性允许您覆盖由ASP.NET 2.0 主题定义的用户界面外观属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="1112a-183">主题在第[10 单元](profiles-themes-and-web-parts.md)中介绍。</span><span class="sxs-lookup"><span data-stu-id="1112a-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="1112a-184">主题</span><span class="sxs-lookup"><span data-stu-id="1112a-184">Theme</span></span>

<span data-ttu-id="1112a-185">指定页面的主题。</span><span class="sxs-lookup"><span data-stu-id="1112a-185">Specifies the theme for the page.</span></span> <span data-ttu-id="1112a-186">如果未为 StyleSheetTheme 属性指定值，则主题属性将覆盖应用于页面上控件的所有样式。</span><span class="sxs-lookup"><span data-stu-id="1112a-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="1112a-187">标题</span><span class="sxs-lookup"><span data-stu-id="1112a-187">Title</span></span>

<span data-ttu-id="1112a-188">设置页面的标题。</span><span class="sxs-lookup"><span data-stu-id="1112a-188">Sets the title for the page.</span></span> <span data-ttu-id="1112a-189">此处指定的值将显示在呈现页面&lt;的标题&gt;元素中。</span><span class="sxs-lookup"><span data-stu-id="1112a-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="1112a-190">查看状态加密模式</span><span class="sxs-lookup"><span data-stu-id="1112a-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="1112a-191">设置视图状态加密模式枚举的值。</span><span class="sxs-lookup"><span data-stu-id="1112a-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="1112a-192">可用值为 **"始终**、**自动**"和 **"从不**"。</span><span class="sxs-lookup"><span data-stu-id="1112a-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="1112a-193">默认值为 **"自动**"。当此属性设置为 **"自动"** 的值时，视图状态被加密是控件通过调用**注册需求视点状态加密**方法请求它。</span><span class="sxs-lookup"><span data-stu-id="1112a-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="1112a-194">通过 @ 页面指令设置公共财产值</span><span class="sxs-lookup"><span data-stu-id="1112a-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="1112a-195">ASP.NET 2.0 中 @ Page 指令的另一个新功能是设置基类公共属性的初始值的能力。</span><span class="sxs-lookup"><span data-stu-id="1112a-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="1112a-196">例如，假设您的基类中具有名为 **"SomeText"** 的公共属性，并且您希望在加载页面时将其初始化为**Hello。**</span><span class="sxs-lookup"><span data-stu-id="1112a-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="1112a-197">只需在 @ Page 指令中设置值即可实现此目的：</span><span class="sxs-lookup"><span data-stu-id="1112a-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="1112a-198">@Page 指令的 **"一些文本"** 属性将基类中的"SomeText"属性的初始值设置为*Hello！*。</span><span class="sxs-lookup"><span data-stu-id="1112a-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="1112a-199">以下视频是使用 @ Page 指令设置基类中公共属性的初始值的演练。</span><span class="sxs-lookup"><span data-stu-id="1112a-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="1112a-200">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="1112a-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="1112a-201">页面类的新公共属性</span><span class="sxs-lookup"><span data-stu-id="1112a-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="1112a-202">以下公共属性是 ASP.NET 2.0 中的新属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="1112a-203">应用相关模板源目录</span><span class="sxs-lookup"><span data-stu-id="1112a-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="1112a-204">返回与应用程序相关的路径到页面或控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="1112a-205">例如，对于 位于 的http://app/folder/page.aspx页面，属性返回 \*/文件夹/。</span><span class="sxs-lookup"><span data-stu-id="1112a-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="1112a-206">应用相对虚拟路径</span><span class="sxs-lookup"><span data-stu-id="1112a-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="1112a-207">将相对虚拟目录路径返回到页面或控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="1112a-208">例如，对于 位于 的http://app/folder/page.aspx页面，属性返回 \*/文件夹/页.aspx。</span><span class="sxs-lookup"><span data-stu-id="1112a-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="1112a-209">同步超时</span><span class="sxs-lookup"><span data-stu-id="1112a-209">AsyncTimeout</span></span>

<span data-ttu-id="1112a-210">获取或设置用于异步页面处理的超时。</span><span class="sxs-lookup"><span data-stu-id="1112a-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="1112a-211">（此模块稍后将介绍异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="1112a-212">客户端查询字符串</span><span class="sxs-lookup"><span data-stu-id="1112a-212">ClientQueryString</span></span>

<span data-ttu-id="1112a-213">返回请求 URL 的查询字符串部分的只读属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="1112a-214">此值是 URL 编码的。</span><span class="sxs-lookup"><span data-stu-id="1112a-214">This value is URL encoded.</span></span> <span data-ttu-id="1112a-215">您可以使用 HttpServer 实用程序类的 Url 解码方法对其进行解码。</span><span class="sxs-lookup"><span data-stu-id="1112a-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="1112a-216">客户端脚本</span><span class="sxs-lookup"><span data-stu-id="1112a-216">ClientScript</span></span>

<span data-ttu-id="1112a-217">此属性返回一个客户端ScriptManager对象，该对象可用于管理客户端脚本的 ASP.NET 发射。</span><span class="sxs-lookup"><span data-stu-id="1112a-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="1112a-218">（本模块稍后将介绍客户端脚本管理器类。</span><span class="sxs-lookup"><span data-stu-id="1112a-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="1112a-219">启用事件验证</span><span class="sxs-lookup"><span data-stu-id="1112a-219">EnableEventValidation</span></span>

<span data-ttu-id="1112a-220">此属性控制是否为回退和回调事件启用事件验证。</span><span class="sxs-lookup"><span data-stu-id="1112a-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="1112a-221">启用后，将验证用于回退或回调事件的参数，以确保它们源自最初呈现这些事件的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="1112a-222">启用"启用"</span><span class="sxs-lookup"><span data-stu-id="1112a-222">EnableTheming</span></span>

<span data-ttu-id="1112a-223">此属性获取或设置布尔，用于指定 ASP.NET 2.0 主题是否应用于页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="1112a-224">Form</span><span class="sxs-lookup"><span data-stu-id="1112a-224">Form</span></span>

<span data-ttu-id="1112a-225">此属性将 ASPX 页上的 HTML 窗体作为 HtmlForm 对象返回。</span><span class="sxs-lookup"><span data-stu-id="1112a-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="1112a-226">标头</span><span class="sxs-lookup"><span data-stu-id="1112a-226">Header</span></span>

<span data-ttu-id="1112a-227">此属性返回对包含页面标题的 HtmlHead 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="1112a-228">您可以使用返回的 HtmlHead 对象获取/设置样式表、元标记等。</span><span class="sxs-lookup"><span data-stu-id="1112a-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="1112a-229">IdSe参数</span><span class="sxs-lookup"><span data-stu-id="1112a-229">IdSeparator</span></span>

<span data-ttu-id="1112a-230">当ASP.NET为页面上的控件构建唯一 ID 时，此只读属性获取用于分隔控件标识符的字符。</span><span class="sxs-lookup"><span data-stu-id="1112a-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="1112a-231">它不可直接通过代码使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="1112a-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="1112a-232">IsAsync</span></span>

<span data-ttu-id="1112a-233">此属性允许异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="1112a-234">本模块稍后将讨论异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="1112a-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="1112a-235">IsCallback</span></span>

<span data-ttu-id="1112a-236">如果页面是回电的结果，则此只读属性将**返回 true。**</span><span class="sxs-lookup"><span data-stu-id="1112a-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="1112a-237">本模块稍后将讨论回电。</span><span class="sxs-lookup"><span data-stu-id="1112a-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="1112a-238">是交叉页面后返回</span><span class="sxs-lookup"><span data-stu-id="1112a-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="1112a-239">如果页面是跨页回邮的一部分，则此只读属性将**返回 true。**</span><span class="sxs-lookup"><span data-stu-id="1112a-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="1112a-240">本模块稍后将介绍跨页回邮。</span><span class="sxs-lookup"><span data-stu-id="1112a-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="1112a-241">Items</span><span class="sxs-lookup"><span data-stu-id="1112a-241">Items</span></span>

<span data-ttu-id="1112a-242">返回对 I字典实例的引用，该实例包含存储在页面上下文中的所有对象。</span><span class="sxs-lookup"><span data-stu-id="1112a-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="1112a-243">您可以将项添加到此 I字典对象，它们将在上下文的整个生存期内可供您使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="1112a-244">保持滚动位置后回</span><span class="sxs-lookup"><span data-stu-id="1112a-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="1112a-245">此属性控制ASP.NET是否发出 JavaScript，该 JavaScript 在回退后在浏览器中维护页面滚动位置。</span><span class="sxs-lookup"><span data-stu-id="1112a-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="1112a-246">（本模块前面讨论了此属性的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1112a-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="1112a-247">主设备</span><span class="sxs-lookup"><span data-stu-id="1112a-247">Master</span></span>

<span data-ttu-id="1112a-248">此只读属性返回对已应用母版页的页面的 MasterPage 实例的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="1112a-249">母版页面文件</span><span class="sxs-lookup"><span data-stu-id="1112a-249">MasterPageFile</span></span>

<span data-ttu-id="1112a-250">获取或设置页面的主页文件名。</span><span class="sxs-lookup"><span data-stu-id="1112a-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="1112a-251">此属性只能在 PreInit 方法中设置。</span><span class="sxs-lookup"><span data-stu-id="1112a-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="1112a-252">最大页面状态长度</span><span class="sxs-lookup"><span data-stu-id="1112a-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="1112a-253">此属性获取或设置以字节为单位的页面状态的最大长度。</span><span class="sxs-lookup"><span data-stu-id="1112a-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="1112a-254">如果属性设置为正数，则页面视图状态将分解为多个隐藏字段，以便不超过指定的字节数。</span><span class="sxs-lookup"><span data-stu-id="1112a-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="1112a-255">如果属性为负数，则视图状态不会分解为块。</span><span class="sxs-lookup"><span data-stu-id="1112a-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="1112a-256">页面适配器</span><span class="sxs-lookup"><span data-stu-id="1112a-256">PageAdapter</span></span>

<span data-ttu-id="1112a-257">返回对 PageAdapter 对象的引用，该对象修改请求浏览器的页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="1112a-258">上一页</span><span class="sxs-lookup"><span data-stu-id="1112a-258">PreviousPage</span></span>

<span data-ttu-id="1112a-259">在服务器.传输或跨页回发的情况下返回对上一页的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="1112a-260">皮肤ID</span><span class="sxs-lookup"><span data-stu-id="1112a-260">SkinID</span></span>

<span data-ttu-id="1112a-261">指定要应用于页面的ASP.NET 2.0 外观。</span><span class="sxs-lookup"><span data-stu-id="1112a-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="1112a-262">样式表主题</span><span class="sxs-lookup"><span data-stu-id="1112a-262">StyleSheetTheme</span></span>

<span data-ttu-id="1112a-263">此属性获取或设置应用于页面的样式表。</span><span class="sxs-lookup"><span data-stu-id="1112a-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="1112a-264">模板控制</span><span class="sxs-lookup"><span data-stu-id="1112a-264">TemplateControl</span></span>

<span data-ttu-id="1112a-265">返回对页面的包含控件的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="1112a-266">主题</span><span class="sxs-lookup"><span data-stu-id="1112a-266">Theme</span></span>

<span data-ttu-id="1112a-267">获取或设置应用于页面的ASP.NET 2.0 主题的名称。</span><span class="sxs-lookup"><span data-stu-id="1112a-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="1112a-268">此值必须在 PreInit 方法之前设置。</span><span class="sxs-lookup"><span data-stu-id="1112a-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="1112a-269">标题</span><span class="sxs-lookup"><span data-stu-id="1112a-269">Title</span></span>

<span data-ttu-id="1112a-270">此属性获取或设置从页眉获取的页面的标题。</span><span class="sxs-lookup"><span data-stu-id="1112a-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="1112a-271">查看状态加密模式</span><span class="sxs-lookup"><span data-stu-id="1112a-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="1112a-272">获取或设置页面的 ViewState 加密模式。</span><span class="sxs-lookup"><span data-stu-id="1112a-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="1112a-273">在本模块前面查看对此属性的详细讨论。</span><span class="sxs-lookup"><span data-stu-id="1112a-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="1112a-274">页面类的新受保护属性</span><span class="sxs-lookup"><span data-stu-id="1112a-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="1112a-275">以下是 ASP.NET 2.0 中 Page 类的新受保护属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="1112a-276">适配器</span><span class="sxs-lookup"><span data-stu-id="1112a-276">Adapter</span></span>

<span data-ttu-id="1112a-277">返回对在请求该页面的设备上呈现该页的 ControlAdapter 的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="1112a-278">异步模式</span><span class="sxs-lookup"><span data-stu-id="1112a-278">AsyncMode</span></span>

<span data-ttu-id="1112a-279">此属性指示页面是否异步处理。</span><span class="sxs-lookup"><span data-stu-id="1112a-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="1112a-280">它供运行时使用，而不是直接在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="1112a-281">客户端 ID 分离器</span><span class="sxs-lookup"><span data-stu-id="1112a-281">ClientIDSeparator</span></span>

<span data-ttu-id="1112a-282">此属性返回在为控件创建唯一客户端 ID 时用作分隔符的字符。</span><span class="sxs-lookup"><span data-stu-id="1112a-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="1112a-283">它供运行时使用，而不是直接在代码中使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="1112a-284">佩奇·邦斯特</span><span class="sxs-lookup"><span data-stu-id="1112a-284">PageStatePersister</span></span>

<span data-ttu-id="1112a-285">此属性返回页面的 PageStatePersister 对象。</span><span class="sxs-lookup"><span data-stu-id="1112a-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="1112a-286">此属性主要由ASP.NET控件开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="1112a-287">唯一的文件路径修复</span><span class="sxs-lookup"><span data-stu-id="1112a-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="1112a-288">此属性返回一个唯一的后缀，该后缀追加到缓存浏览器的文件路径上。</span><span class="sxs-lookup"><span data-stu-id="1112a-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="1112a-289">默认值为\_\_ufps\* 和 6 位数字。</span><span class="sxs-lookup"><span data-stu-id="1112a-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="1112a-290">页面类的新公共方法</span><span class="sxs-lookup"><span data-stu-id="1112a-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="1112a-291">以下公共方法是 ASP.NET 2.0 中的 Page 类的新增方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="1112a-292">附加预渲染完成同步</span><span class="sxs-lookup"><span data-stu-id="1112a-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="1112a-293">此方法注册事件处理程序委托以进行异步页面执行。</span><span class="sxs-lookup"><span data-stu-id="1112a-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="1112a-294">本模块稍后将讨论异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="1112a-295">应用样式表外观</span><span class="sxs-lookup"><span data-stu-id="1112a-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="1112a-296">将页面样式表中的属性应用于页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="1112a-297">执行已注册的同步任务</span><span class="sxs-lookup"><span data-stu-id="1112a-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="1112a-298">此方法是异步任务。</span><span class="sxs-lookup"><span data-stu-id="1112a-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="1112a-299">获取验证器</span><span class="sxs-lookup"><span data-stu-id="1112a-299">GetValidators</span></span>

<span data-ttu-id="1112a-300">如果未指定任何验证组或默认验证组，则返回验证器的集合。</span><span class="sxs-lookup"><span data-stu-id="1112a-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="1112a-301">注册同步任务</span><span class="sxs-lookup"><span data-stu-id="1112a-301">RegisterAsyncTask</span></span>

<span data-ttu-id="1112a-302">此方法注册新的异步任务。</span><span class="sxs-lookup"><span data-stu-id="1112a-302">This method registers a new async task.</span></span> <span data-ttu-id="1112a-303">本模块稍后将介绍异步页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="1112a-304">注册需要控制状态</span><span class="sxs-lookup"><span data-stu-id="1112a-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="1112a-305">此方法告诉ASP.NET必须保留页面控件状态。</span><span class="sxs-lookup"><span data-stu-id="1112a-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="1112a-306">注册需要查看状态加密</span><span class="sxs-lookup"><span data-stu-id="1112a-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="1112a-307">此方法告诉ASP.NET页面视图状态需要加密。</span><span class="sxs-lookup"><span data-stu-id="1112a-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="1112a-308">解析客户端</span><span class="sxs-lookup"><span data-stu-id="1112a-308">ResolveClientUrl</span></span>

<span data-ttu-id="1112a-309">返回可用于图像等客户端请求的相对 URL。</span><span class="sxs-lookup"><span data-stu-id="1112a-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="1112a-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="1112a-310">SetFocus</span></span>

<span data-ttu-id="1112a-311">此方法将焦点设置为最初加载页面时指定的控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="1112a-312">取消注册需要控制状态</span><span class="sxs-lookup"><span data-stu-id="1112a-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="1112a-313">此方法将取消注册传递给它的控件，因为不再需要控件状态持久性。</span><span class="sxs-lookup"><span data-stu-id="1112a-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="1112a-314">对页面生命周期的更改</span><span class="sxs-lookup"><span data-stu-id="1112a-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="1112a-315">ASP.NET 2.0 中的页面生命周期没有显著变化，但您应该知道一些新方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="1112a-316">下面概述了ASP.NET 2.0 页生命周期。</span><span class="sxs-lookup"><span data-stu-id="1112a-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="1112a-317">PreInit（ASP.NET 2.0 中的新增功能）</span><span class="sxs-lookup"><span data-stu-id="1112a-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="1112a-318">PreInit 事件是开发人员可以访问的生命周期中最早的阶段。</span><span class="sxs-lookup"><span data-stu-id="1112a-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="1112a-319">通过添加此事件，可以以编程方式更改ASP.NET 2.0 主题、母版页、ASP.NET 2.0 配置文件的访问属性等。如果您处于后回状态，则实现 Viewstate 尚未应用于生命周期的此时控件非常重要。</span><span class="sxs-lookup"><span data-stu-id="1112a-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="1112a-320">因此，如果开发人员在此阶段更改控件的属性，则在页面生命周期的稍后版本中可能会覆盖该控件的属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="1112a-321">Init</span><span class="sxs-lookup"><span data-stu-id="1112a-321">Init</span></span>

<span data-ttu-id="1112a-322">Init 事件未从 ASP.NET 1.x 更改。</span><span class="sxs-lookup"><span data-stu-id="1112a-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="1112a-323">这是您希望读取或初始化页面上控件属性的位置。</span><span class="sxs-lookup"><span data-stu-id="1112a-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="1112a-324">在此阶段，母版页、主题等已应用于该页。</span><span class="sxs-lookup"><span data-stu-id="1112a-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="1112a-325">InitComplete（2.0 中新增）</span><span class="sxs-lookup"><span data-stu-id="1112a-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="1112a-326">InitComplete 事件在页面初始化阶段结束时调用。</span><span class="sxs-lookup"><span data-stu-id="1112a-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="1112a-327">在生命周期的此时，可以访问页面上的控件，但尚未填充其状态。</span><span class="sxs-lookup"><span data-stu-id="1112a-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="1112a-328">预加载（2.0 中新增）</span><span class="sxs-lookup"><span data-stu-id="1112a-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="1112a-329">此事件是在应用所有回邮数据后，并在页面\_加载之前调用的。</span><span class="sxs-lookup"><span data-stu-id="1112a-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="1112a-330">加载</span><span class="sxs-lookup"><span data-stu-id="1112a-330">Load</span></span>

<span data-ttu-id="1112a-331">加载事件未从 ASP.NET 1.x 更改。</span><span class="sxs-lookup"><span data-stu-id="1112a-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="1112a-332">加载完成（2.0 中新增）</span><span class="sxs-lookup"><span data-stu-id="1112a-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="1112a-333">LoadComplete 事件是页面加载阶段的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="1112a-334">在此阶段，所有回退和视图状态数据已应用于页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="1112a-335">预渲染</span><span class="sxs-lookup"><span data-stu-id="1112a-335">PreRender</span></span>

<span data-ttu-id="1112a-336">如果希望对动态添加到页面的控件正确维护视图状态，则 PreRender 事件是添加它们的最后机会。</span><span class="sxs-lookup"><span data-stu-id="1112a-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="1112a-337">预渲染完成（2.0 中新增）</span><span class="sxs-lookup"><span data-stu-id="1112a-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="1112a-338">在预渲染完成阶段，所有控件都已添加到页面，并且页面已准备好呈现。</span><span class="sxs-lookup"><span data-stu-id="1112a-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="1112a-339">预渲染完成事件是保存页面视图状态之前引发的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="1112a-340">保存状态完成（2.0 中的新增功能）</span><span class="sxs-lookup"><span data-stu-id="1112a-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="1112a-341">保存所有页面视图状态和控制状态后，将立即调用"保存状态完成"事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="1112a-342">这是页面实际呈现到浏览器之前的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="1112a-343">呈现</span><span class="sxs-lookup"><span data-stu-id="1112a-343">Render</span></span>

<span data-ttu-id="1112a-344">自 1.x ASP.NET以来，渲染方法未更改。</span><span class="sxs-lookup"><span data-stu-id="1112a-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="1112a-345">这是 HtmlTextWriter 初始化并将页面呈现到浏览器的位置。</span><span class="sxs-lookup"><span data-stu-id="1112a-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="1112a-346">ASP.NET 2.0 中的跨页回邮</span><span class="sxs-lookup"><span data-stu-id="1112a-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="1112a-347">在ASP.NET 1.x 中，需要回邮后贴到同一页。</span><span class="sxs-lookup"><span data-stu-id="1112a-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="1112a-348">不允许进行跨页回邮。</span><span class="sxs-lookup"><span data-stu-id="1112a-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="1112a-349">ASP.NET 2.0 添加了通过 IButtonControl 界面发回其他页面的功能。</span><span class="sxs-lookup"><span data-stu-id="1112a-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="1112a-350">实现新的 IButtonControl 界面的任何控件（除了第三方自定义控件之外，还可以利用此新功能，使用 PostBackUrl 属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="1112a-351">以下代码显示将回发回第二页的 Button 控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="1112a-352">当页面被发回时，启动回邮的页面可通过第二页上的"上页"属性访问。</span><span class="sxs-lookup"><span data-stu-id="1112a-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="1112a-353">此功能通过新的 WebForm\_DoPostBackOptions 客户端功能实现，该功能ASP.NET 2.0 在控件回退回其他页面时呈现到页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="1112a-354">此 JavaScript 函数由向客户端发出脚本的新 WebResource.axd 处理程序提供。</span><span class="sxs-lookup"><span data-stu-id="1112a-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="1112a-355">下面的视频是跨页回帖的演练。</span><span class="sxs-lookup"><span data-stu-id="1112a-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="1112a-356">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="1112a-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="1112a-357">有关跨页回邮的更多详细信息</span><span class="sxs-lookup"><span data-stu-id="1112a-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="1112a-358">视图状态</span><span class="sxs-lookup"><span data-stu-id="1112a-358">Viewstate</span></span>

<span data-ttu-id="1112a-359">您可能已经问自己，在跨页回退方案中，从第一页中查看状态会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="1112a-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="1112a-360">毕竟，任何不实现 IPostBackDataHandler 的控件都将通过视图状态保持其状态，因此，要访问跨页后回的第二页上该控件的属性，您必须有权访问该页的视图状态。</span><span class="sxs-lookup"><span data-stu-id="1112a-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="1112a-361">ASP.NET 2.0 使用第二页中称为\_\_"上页"的新隐藏字段处理此方案。</span><span class="sxs-lookup"><span data-stu-id="1112a-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="1112a-362">"\_\_上一页"窗体字段包含第一页的视图状态，以便您可以访问第二页中所有控件的属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="1112a-363">绕过查找控制</span><span class="sxs-lookup"><span data-stu-id="1112a-363">Circumventing FindControl</span></span>

<span data-ttu-id="1112a-364">在跨页回发的视频演练中，我使用 FindControl 方法获取对第一页上的 TextBox 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="1112a-365">该方法适用于此目的，但 FindControl 成本高昂，需要编写其他代码。</span><span class="sxs-lookup"><span data-stu-id="1112a-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="1112a-366">幸运的是，ASP.NET 2.0 为此提供了 FindControl 的替代方法，这在很多方案中都不起作用。</span><span class="sxs-lookup"><span data-stu-id="1112a-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="1112a-367">使用"上一页类型"指令允许您使用 TypeName 或 VirtualPath 属性对上一页进行强类型引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="1112a-368">TypeName 属性允许您指定上一页的类型，而 VirtualPath 属性允许您使用虚拟路径引用上一页。</span><span class="sxs-lookup"><span data-stu-id="1112a-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="1112a-369">设置上一页类型指令后，必须公开要允许使用公共属性访问的控件等。</span><span class="sxs-lookup"><span data-stu-id="1112a-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="1112a-370">实验室 1 跨页回邮</span><span class="sxs-lookup"><span data-stu-id="1112a-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="1112a-371">在本实验中，您将创建一个应用程序，该应用程序使用 ASP.NET 2.0 的新跨页回邮功能。</span><span class="sxs-lookup"><span data-stu-id="1112a-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="1112a-372">打开 Visual Studio 2005 并创建新ASP.NET网站。</span><span class="sxs-lookup"><span data-stu-id="1112a-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="1112a-373">添加新的 Web 表单，称为页 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="1112a-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="1112a-374">在"设计"视图中打开默认.aspx 并添加按钮控件和 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="1112a-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="1112a-375">为按钮控件指定 **"提交按钮**"的 ID，而文本框控件为**用户名**ID。</span><span class="sxs-lookup"><span data-stu-id="1112a-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="1112a-376">将按钮的 PostBackUrl 属性设置为页 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="1112a-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="1112a-377">在源视图中打开页面 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="1112a-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="1112a-378">添加 # 上一页类型指令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="1112a-379">将以下代码添加到页 2.aspx 的代码后面的页面\_加载：</span><span class="sxs-lookup"><span data-stu-id="1112a-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="1112a-380">单击"生成"菜单上的"生成"菜单生成项目。</span><span class="sxs-lookup"><span data-stu-id="1112a-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="1112a-381">将以下代码添加到 Default.aspx 的代码后面：</span><span class="sxs-lookup"><span data-stu-id="1112a-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="1112a-382">将页\_2.aspx 中的页面加载更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="1112a-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="1112a-383">生成项目。</span><span class="sxs-lookup"><span data-stu-id="1112a-383">Build the project.</span></span>
11. <span data-ttu-id="1112a-384">运行该项目。</span><span class="sxs-lookup"><span data-stu-id="1112a-384">Run the project.</span></span>
12. <span data-ttu-id="1112a-385">在文本框中输入您的姓名，然后单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="1112a-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="1112a-386">结果如何？</span><span class="sxs-lookup"><span data-stu-id="1112a-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="1112a-387">ASP.NET 2.0 中的异步页面</span><span class="sxs-lookup"><span data-stu-id="1112a-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="1112a-388">ASP.NET中的许多争用问题是由外部调用（如 Web 服务或数据库调用）的延迟、文件 IO 延迟等引起的。当针对ASP.NET应用程序发出请求时，ASP.NET使用其工作线程之一来为该请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="1112a-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="1112a-389">该请求拥有该线程，直到请求完成并发送响应。</span><span class="sxs-lookup"><span data-stu-id="1112a-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="1112a-390">ASP.NET 2.0 寻求通过添加异步执行页面的功能来解决此类问题的延迟问题。</span><span class="sxs-lookup"><span data-stu-id="1112a-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="1112a-391">这意味着工作线程可以启动请求，然后将其他执行交给另一个线程，从而快速返回到可用的线程池。</span><span class="sxs-lookup"><span data-stu-id="1112a-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="1112a-392">当文件 IO、数据库调用等完成时，将从线程池获取一个新线程以完成请求。</span><span class="sxs-lookup"><span data-stu-id="1112a-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="1112a-393">使页面异步执行的第一步是设置页面指令的**Async**属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="1112a-394">此属性告诉ASP.NET实现页面的 IHttpAsyncHandler。</span><span class="sxs-lookup"><span data-stu-id="1112a-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="1112a-395">下一步是在预渲染之前在页面生命周期的某一点调用 AddOnPreRenderCompleteAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="1112a-396">（此方法通常在页面\_加载中调用。AddOnPreRenderCompleteasync方法采用两个参数;a BeginEventHandler 和 endEventHandler。</span><span class="sxs-lookup"><span data-stu-id="1112a-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="1112a-397">BeginEventHandler 返回一个 IAsyncResult，然后将该结果作为参数传递给 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="1112a-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="1112a-398">下面的视频是异步页面请求的演练。</span><span class="sxs-lookup"><span data-stu-id="1112a-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="1112a-399">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="1112a-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="1112a-400">在结束事件处理程序完成之前，异步页面不会呈现给浏览器。</span><span class="sxs-lookup"><span data-stu-id="1112a-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="1112a-401">毫无疑问，但一些开发人员会认为异步请求类似于异步回调。</span><span class="sxs-lookup"><span data-stu-id="1112a-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="1112a-402">重要的是要意识到他们不是。</span><span class="sxs-lookup"><span data-stu-id="1112a-402">It's important to realize that they are not.</span></span> <span data-ttu-id="1112a-403">异步请求的好处是，可以将第一个辅助线程返回到线程池以服务新请求，从而减少由于受 IO 绑定等原因引起的争用。</span><span class="sxs-lookup"><span data-stu-id="1112a-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="1112a-404">ASP.NET 2.0 中的脚本回调</span><span class="sxs-lookup"><span data-stu-id="1112a-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="1112a-405">Web 开发人员一直在寻找防止与回调关联的闪烁的方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="1112a-406">在 ASP.NET 1.x 中，智能导航是避免闪烁的最常见方法，但智能导航由于在客户端上实现的复杂性而给一些开发人员带来了问题。</span><span class="sxs-lookup"><span data-stu-id="1112a-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="1112a-407">ASP.NET 2.0 使用脚本回调解决此问题。</span><span class="sxs-lookup"><span data-stu-id="1112a-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="1112a-408">脚本回调利用 XMLHttp 通过 JavaScript 对 Web 服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="1112a-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="1112a-409">XMLHttp 请求返回 XML 数据，然后可以通过浏览器的 DOM 进行操作。</span><span class="sxs-lookup"><span data-stu-id="1112a-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="1112a-410">XMLHttp 代码由新的 WebResource.axd 处理程序对用户隐藏。</span><span class="sxs-lookup"><span data-stu-id="1112a-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="1112a-411">为了在 2.0 ASP.NET配置脚本回调，需要执行几个步骤。</span><span class="sxs-lookup"><span data-stu-id="1112a-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="1112a-412">步骤 1 ： 实现 IcallbackEventHandler 接口</span><span class="sxs-lookup"><span data-stu-id="1112a-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="1112a-413">为了ASP.NET识别您的页面参与脚本回调，必须实现 ICallbackEventHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="1112a-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="1112a-414">您可以在代码后面的文件中执行此操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="1112a-415">您还可以使用 # 实现指令执行此操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="1112a-416">在使用内联ASP.NET代码时，通常可以使用 @ 实现指令。</span><span class="sxs-lookup"><span data-stu-id="1112a-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="1112a-417">第 2 步 ： 调用返回事件引用</span><span class="sxs-lookup"><span data-stu-id="1112a-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="1112a-418">如前所述，XMLHttp 调用封装在 WebResource.axd 处理程序中。</span><span class="sxs-lookup"><span data-stu-id="1112a-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="1112a-419">呈现页面时，ASP.NET将添加对 WebForm DoCallback\_的调用，WebForm DoCallback 是 WebResource.axd 提供的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="1112a-420">WebForm\_DoCallback 函数将替换\_\_回调的 doPostBack 函数。</span><span class="sxs-lookup"><span data-stu-id="1112a-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="1112a-421">请记住，\_\_以编程方式提交页面上的表单。</span><span class="sxs-lookup"><span data-stu-id="1112a-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="1112a-422">在回调方案中，您希望防止回退，因此\_\_PostBack 是不够的。</span><span class="sxs-lookup"><span data-stu-id="1112a-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="1112a-423">\_\_doPostBack 仍呈现在客户端脚本回调方案中的页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="1112a-424">但是，它不用于回调。</span><span class="sxs-lookup"><span data-stu-id="1112a-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="1112a-425">WebForm\_DoCallback 客户端函数的参数通过服务器端函数 GetCallbackEventReference 提供，该函数通常在页面\_加载中调用。</span><span class="sxs-lookup"><span data-stu-id="1112a-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="1112a-426">对 GetbackEvent 参考的典型调用可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="1112a-427">在这种情况下，cm 是客户端脚本管理器的实例。</span><span class="sxs-lookup"><span data-stu-id="1112a-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="1112a-428">本模块稍后将介绍客户端脚本管理器类。</span><span class="sxs-lookup"><span data-stu-id="1112a-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="1112a-429">有几个重载版本的 GetbackEvent 参考。</span><span class="sxs-lookup"><span data-stu-id="1112a-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="1112a-430">在这种情况下，参数如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="1112a-431">对调用 GetbackEvent参照的控件的引用。</span><span class="sxs-lookup"><span data-stu-id="1112a-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="1112a-432">在这种情况下，它是页面本身。</span><span class="sxs-lookup"><span data-stu-id="1112a-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="1112a-433">将从客户端代码传递到服务器端事件的字符串参数。</span><span class="sxs-lookup"><span data-stu-id="1112a-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="1112a-434">在这种情况下，我传递名为 ddlCompany 的下拉的值。</span><span class="sxs-lookup"><span data-stu-id="1112a-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="1112a-435">客户端函数的名称，该函数将接受服务器端回调事件的返回值（作为字符串）。</span><span class="sxs-lookup"><span data-stu-id="1112a-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="1112a-436">仅当服务器端回调成功时，才会调用此功能。</span><span class="sxs-lookup"><span data-stu-id="1112a-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="1112a-437">因此，为了鲁棒性，通常建议使用重载版本的 GetCallbackEventReference，该版本需要一个额外的字符串参数，指定客户端函数的名称，在发生错误时执行。</span><span class="sxs-lookup"><span data-stu-id="1112a-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="1112a-438">表示在回调到服务器之前启动的客户端函数的字符串。</span><span class="sxs-lookup"><span data-stu-id="1112a-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="1112a-439">在这种情况下，没有这样的脚本，因此参数为 null。</span><span class="sxs-lookup"><span data-stu-id="1112a-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="1112a-440">指定是否异步执行回调的布尔。</span><span class="sxs-lookup"><span data-stu-id="1112a-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="1112a-441">客户端上对 WebForm\_DoCallback 的调用将传递这些参数。</span><span class="sxs-lookup"><span data-stu-id="1112a-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="1112a-442">因此，在客户端上呈现此页面时，该代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="1112a-443">请注意，客户端上函数的签名有点不同。</span><span class="sxs-lookup"><span data-stu-id="1112a-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="1112a-444">客户端函数传递 5 个字符串和一个布尔。</span><span class="sxs-lookup"><span data-stu-id="1112a-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="1112a-445">附加字符串（在上例中为空）包含客户端函数，该函数将处理来自服务器端回调的任何错误。</span><span class="sxs-lookup"><span data-stu-id="1112a-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="1112a-446">步骤 3 ： 钩客户端控制事件</span><span class="sxs-lookup"><span data-stu-id="1112a-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="1112a-447">请注意，上面 GetCallbackEventReference 的返回值已分配给字符串变量。</span><span class="sxs-lookup"><span data-stu-id="1112a-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="1112a-448">该字符串用于钩接启动回调的控件的客户端事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="1112a-449">在此示例中，回调由页面上的下拉展开，因此我想挂接*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="1112a-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="1112a-450">要挂接客户端事件，只需将处理程序添加到客户端标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1112a-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="1112a-451">回想一下*cbRef*是从调用 GetbackEvent 参考的返回值。</span><span class="sxs-lookup"><span data-stu-id="1112a-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="1112a-452">它包含上面显示的对 WebForm\_DoCallback 的调用。</span><span class="sxs-lookup"><span data-stu-id="1112a-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="1112a-453">步骤 4 ： 注册客户端脚本</span><span class="sxs-lookup"><span data-stu-id="1112a-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="1112a-454">回想一下，对 GetCallbackEventReference 的调用指定在服务器端回调成功时将执行名为**ShowCompanyName**的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="1112a-455">需要使用 ClientScriptManager 实例将该脚本添加到页面。</span><span class="sxs-lookup"><span data-stu-id="1112a-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="1112a-456">（本模块稍后将讨论客户端脚本管理器类。你这样做，像这样：</span><span class="sxs-lookup"><span data-stu-id="1112a-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="1112a-457">步骤 5 ： 调用 ICallbackEventHandler 接口的方法</span><span class="sxs-lookup"><span data-stu-id="1112a-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="1112a-458">ICallbackEventHandler 包含需要在代码中实现的两种方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="1112a-459">它们是 **"提高回调事件**"和 **"获取回调事件**"。</span><span class="sxs-lookup"><span data-stu-id="1112a-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="1112a-460">**RaiseCallbackEvent**将字符串作为参数，不返回任何内容。</span><span class="sxs-lookup"><span data-stu-id="1112a-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="1112a-461">字符串参数从客户端调用传递到 WebForm\_DoCallback。</span><span class="sxs-lookup"><span data-stu-id="1112a-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="1112a-462">在这种情况下，该值是名为 ddlCompany 的下拉*的值*属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="1112a-463">服务器端代码应放在"提高回调事件"方法中。</span><span class="sxs-lookup"><span data-stu-id="1112a-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="1112a-464">例如，如果您的回调针对外部资源发出 Web 请求，则应将该代码放在"提高回调事件"中。</span><span class="sxs-lookup"><span data-stu-id="1112a-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="1112a-465">**GetCallbackEvent**负责处理回调返回给客户端的问题。</span><span class="sxs-lookup"><span data-stu-id="1112a-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="1112a-466">它不需要参数并返回字符串。</span><span class="sxs-lookup"><span data-stu-id="1112a-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="1112a-467">它返回的字符串将作为参数传递给客户端函数，在本例中*为 ShowCompanyName*。</span><span class="sxs-lookup"><span data-stu-id="1112a-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="1112a-468">完成上述步骤后，即可在 2.0 ASP.NET执行脚本回调。</span><span class="sxs-lookup"><span data-stu-id="1112a-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="1112a-469">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="1112a-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="1112a-470">ASP.NET脚本回调在支持进行 XMLHttp 调用的任何浏览器中都受支持。</span><span class="sxs-lookup"><span data-stu-id="1112a-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="1112a-471">这包括当今使用的所有现代浏览器。</span><span class="sxs-lookup"><span data-stu-id="1112a-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="1112a-472">Internet Explorer 使用 XMLHttp ActiveX 对象，而其他现代浏览器（包括即将推出的 IE 7）使用内部 XMLHttp 对象。</span><span class="sxs-lookup"><span data-stu-id="1112a-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="1112a-473">要以编程方式确定浏览器是否支持回调，可以使用 **"请求.Browser.支持回拨"** 属性。</span><span class="sxs-lookup"><span data-stu-id="1112a-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="1112a-474">如果请求的客户端支持脚本回调，则此属性将返回**true。**</span><span class="sxs-lookup"><span data-stu-id="1112a-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="1112a-475">在 ASP.NET 2.0 中使用客户端脚本</span><span class="sxs-lookup"><span data-stu-id="1112a-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="1112a-476">ASP.NET 2.0 中的客户端脚本是使用客户端脚本管理器类管理的。</span><span class="sxs-lookup"><span data-stu-id="1112a-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="1112a-477">客户端脚本管理器类使用类型和名称跟踪客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="1112a-478">这样可以防止同一脚本多次以编程方式插入到页面上。</span><span class="sxs-lookup"><span data-stu-id="1112a-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="1112a-479">在页面上成功注册脚本后，任何后续注册同一脚本的尝试都将导致脚本无法第二次注册。</span><span class="sxs-lookup"><span data-stu-id="1112a-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="1112a-480">不添加重复的脚本，也不会发生异常。</span><span class="sxs-lookup"><span data-stu-id="1112a-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="1112a-481">为了避免不必要的计算，可以使用一些方法来确定脚本是否已注册，以便不要尝试多次注册脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="1112a-482">客户端脚本管理器的方法应对所有当前ASP.NET开发人员都熟悉：</span><span class="sxs-lookup"><span data-stu-id="1112a-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="1112a-483">注册客户端脚本块</span><span class="sxs-lookup"><span data-stu-id="1112a-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="1112a-484">此方法将脚本添加到呈现页面的顶部。</span><span class="sxs-lookup"><span data-stu-id="1112a-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="1112a-485">这对于添加将在客户端上显式调用的函数非常有用。</span><span class="sxs-lookup"><span data-stu-id="1112a-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="1112a-486">此方法有两个重载版本。</span><span class="sxs-lookup"><span data-stu-id="1112a-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="1112a-487">四个参数中有三个在它们中很常见。</span><span class="sxs-lookup"><span data-stu-id="1112a-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="1112a-488">它们分别是：</span><span class="sxs-lookup"><span data-stu-id="1112a-488">They are:</span></span>

`type (string)`

<span data-ttu-id="1112a-489">***类型***参数标识脚本的类型。</span><span class="sxs-lookup"><span data-stu-id="1112a-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="1112a-490">通常最好使用页面的类型（这。获取类型的类型。</span><span class="sxs-lookup"><span data-stu-id="1112a-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="1112a-491">***键***参数是脚本的用户定义的密钥。</span><span class="sxs-lookup"><span data-stu-id="1112a-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="1112a-492">对于每个脚本来说，这应该是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1112a-492">This should be unique for each script.</span></span> <span data-ttu-id="1112a-493">如果尝试添加具有相同键和已添加脚本类型的脚本，则不会添加该脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="1112a-494">***脚本***参数是包含要添加的实际脚本的字符串。</span><span class="sxs-lookup"><span data-stu-id="1112a-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="1112a-495">建议使用 StringBuilder 创建脚本，然后在 StringBuilder 上使用 ToString（） 方法分配***脚本***参数。</span><span class="sxs-lookup"><span data-stu-id="1112a-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="1112a-496">如果使用加载的注册客户端脚本块，该参数仅包含三个参数，则必须在脚本中包含脚本元素&lt;（&gt;脚本&lt;和&gt;/脚本）。</span><span class="sxs-lookup"><span data-stu-id="1112a-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="1112a-497">您可以选择使用采用第四个参数的注册客户端脚本块的重载。</span><span class="sxs-lookup"><span data-stu-id="1112a-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="1112a-498">第四个参数是布尔，它指定ASP.NET是否应该为您添加脚本元素。</span><span class="sxs-lookup"><span data-stu-id="1112a-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="1112a-499">如果此参数**为 true，** 则脚本不应显式包含脚本元素。</span><span class="sxs-lookup"><span data-stu-id="1112a-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="1112a-500">使用 IsClientScriptBlock 注册方法确定脚本是否已注册。</span><span class="sxs-lookup"><span data-stu-id="1112a-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="1112a-501">这允许您避免尝试重新注册已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="1112a-502">注册客户端脚本包括（2.0 中的新增功能）</span><span class="sxs-lookup"><span data-stu-id="1112a-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="1112a-503">注册客户端脚本包含标记创建链接到外部脚本文件的脚本块。</span><span class="sxs-lookup"><span data-stu-id="1112a-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="1112a-504">它有两个过载。</span><span class="sxs-lookup"><span data-stu-id="1112a-504">It has two overloads.</span></span> <span data-ttu-id="1112a-505">一个需要一个键和一个URL。</span><span class="sxs-lookup"><span data-stu-id="1112a-505">One takes a key and a URL.</span></span> <span data-ttu-id="1112a-506">第二个参数添加第三个参数，指定类型。</span><span class="sxs-lookup"><span data-stu-id="1112a-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="1112a-507">例如，以下代码生成一个脚本块，该脚本块链接到应用程序脚本文件夹的根目录中的 js 函数.js：</span><span class="sxs-lookup"><span data-stu-id="1112a-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="1112a-508">此代码在呈现的页面中生成以下代码：</span><span class="sxs-lookup"><span data-stu-id="1112a-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="1112a-509">脚本块呈现在页面底部。</span><span class="sxs-lookup"><span data-stu-id="1112a-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="1112a-510">使用 IsClientScript 包括注册方法确定脚本是否已注册。</span><span class="sxs-lookup"><span data-stu-id="1112a-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="1112a-511">这允许您避免尝试重新注册脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="1112a-512">注册启动脚本</span><span class="sxs-lookup"><span data-stu-id="1112a-512">RegisterStartupScript</span></span>

<span data-ttu-id="1112a-513">注册启动脚本方法采用与注册客户端脚本块方法相同的参数。</span><span class="sxs-lookup"><span data-stu-id="1112a-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="1112a-514">注册到注册启动脚本的脚本在页面加载后在 OnLoad 客户端事件之前执行。</span><span class="sxs-lookup"><span data-stu-id="1112a-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="1112a-515">在 1.X 中，注册到的&lt;脚本位于关闭 /窗体&gt;标记之前，而注册到 RegisterClientScriptBlock 的脚本则紧随打开&lt;表单&gt;标记之后放置。</span><span class="sxs-lookup"><span data-stu-id="1112a-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="1112a-516">在 ASP.NET 2.0 中，两者都放在&lt;关闭&gt;/窗体标记之前。</span><span class="sxs-lookup"><span data-stu-id="1112a-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="1112a-517">如果向注册启动脚本注册函数，则在客户端代码中显式调用该函数之前，该函数不会执行。</span><span class="sxs-lookup"><span data-stu-id="1112a-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="1112a-518">使用 IsStartupScript 注册方法确定脚本是否已注册，并避免尝试重新注册脚本。</span><span class="sxs-lookup"><span data-stu-id="1112a-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="1112a-519">其他客户端脚本管理器方法</span><span class="sxs-lookup"><span data-stu-id="1112a-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="1112a-520">下面是客户端ScriptManager 类的其他一些有用方法。</span><span class="sxs-lookup"><span data-stu-id="1112a-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="1112a-521"><strong>获取回拨事件引用</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="1112a-522">请参阅本模块前面的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="1112a-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="1112a-523"><strong>获取后回客户端超链接</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="1112a-524">获取可用于从客户端事件发回的 JavaScript 引用（javascript：&lt;调用&gt;）。</span><span class="sxs-lookup"><span data-stu-id="1112a-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="1112a-525"><strong>获取后回活动参考</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="1112a-526">获取可用于从客户端发起回帖子的字符串。</span><span class="sxs-lookup"><span data-stu-id="1112a-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="1112a-527"><strong>获取Web资源Url</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="1112a-528">返回嵌入在程序集中的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="1112a-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="1112a-529">必须与<strong>注册客户端脚本资源</strong>结合使用。</span><span class="sxs-lookup"><span data-stu-id="1112a-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="1112a-530"><strong>注册客户端脚本资源</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="1112a-531">将 Web 资源注册到该页。</span><span class="sxs-lookup"><span data-stu-id="1112a-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="1112a-532">这些资源嵌入到程序集中并由新的 WebResource.axd 处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="1112a-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="1112a-533"><strong>注册隐藏字段</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="1112a-534">将隐藏的表单字段与页面注册。</span><span class="sxs-lookup"><span data-stu-id="1112a-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="1112a-535"><strong>注册提交声明</strong></span><span class="sxs-lookup"><span data-stu-id="1112a-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="1112a-536">注册提交 HTML 窗体时执行的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="1112a-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |

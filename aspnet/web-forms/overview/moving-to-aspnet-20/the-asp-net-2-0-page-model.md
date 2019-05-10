---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页面模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。 无法使用任一 Src attr 实现代码隐藏...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127921"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="8a6b1-104">ASP.NET 2.0 页面模型</span><span class="sxs-lookup"><span data-stu-id="8a6b1-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="8a6b1-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8a6b1-106">在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="8a6b1-107">可以使用 Src 属性或代码隐藏文件属性的实现代码隐藏@Page指令。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="8a6b1-108">在 ASP.NET 2.0 中，开发人员仍然可以内联代码和代码隐藏之间进行选择，但有了显著改进代码隐藏模型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="8a6b1-109">在 ASP.NET 1.x 中，开发人员必须使用内联代码模型和代码隐藏代码模型之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="8a6b1-110">可以使用 Src 属性或代码隐藏文件属性的实现代码隐藏@Page指令。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="8a6b1-111">在 ASP.NET 2.0 中，开发人员仍然可以内联代码和代码隐藏之间进行选择，但有了显著改进代码隐藏模型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="8a6b1-112">在代码隐藏模型中的改进</span><span class="sxs-lookup"><span data-stu-id="8a6b1-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="8a6b1-113">以全面了解 ASP.NET 2.0 中的代码隐藏模型中的更改，其最大努力来快速查看模型作为它存在于 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="8a6b1-114">在 ASP.NET 中的代码隐藏模型 1.x</span><span class="sxs-lookup"><span data-stu-id="8a6b1-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="8a6b1-115">在 ASP.NET 1.x 中，代码隐藏模型组成一个 ASPX 文件 （web 窗体） 和包含编程代码的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="8a6b1-116">两个文件连接使用@Page指令 ASPX 文件中。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="8a6b1-117">ASPX 页的每个控件实例变量作为代码隐藏文件中有相应的声明。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="8a6b1-118">代码隐藏文件还包含有关事件绑定的代码和生成的 Visual Studio 设计器所需的代码。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="8a6b1-119">此模型的效果非常好，但由于 ASPX 页中的每个 ASP.NET 元素所需的代码隐藏文件中的相应代码，有没有真正分离的代码和内容。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="8a6b1-120">例如，如果设计器添加到 Visual Studio IDE 外部 ASPX 文件新的服务器控件，该应用程序将会破坏由于没有为该控件声明的代码隐藏文件中。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="8a6b1-121">ASP.NET 2.0 中的代码隐藏模型</span><span class="sxs-lookup"><span data-stu-id="8a6b1-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="8a6b1-122">ASP.NET 2.0 可大大提高了此模型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="8a6b1-123">在 ASP.NET 2.0 中，代码隐藏实现使用新*分部类*ASP.NET 2.0 中提供。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="8a6b1-124">ASP.NET 2.0 中的代码隐藏类定义为分部类，这意味着它包含仅的类定义的一部分。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="8a6b1-125">类定义的剩余部分是动态生成的 ASP.NET 2.0 在运行时或在预编译网站时使用的 ASPX 页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="8a6b1-126">使用 @ Page 指令仍建立的代码隐藏文件和 ASPX 页面之间的链接。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="8a6b1-127">但是，而不是代码隐藏文件或 Src 属性中，ASP.NET 2.0 现在使用 CodeFile 属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="8a6b1-128">Inherits 特性也用于指定页面的类名称。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="8a6b1-129">典型的 @ Page 指令可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="8a6b1-130">ASP.NET 2.0 代码隐藏文件中的典型类定义可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="8a6b1-131">C# 和 Visual Basic 是目前支持分部类的唯一托管的语言。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="8a6b1-132">因此，使用 J# 开发人员将不能使用 ASP.NET 2.0 中的代码隐藏模型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="8a6b1-133">新模型增强了代码隐藏模型，因为开发人员现在可以包含用户创建的代码的代码文件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="8a6b1-134">它还提供的则返回 true 的代码和内容分隔由于没有任何实例变量声明中的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6b1-135">ASPX 页的分部类是事件绑定发生的地方，因为 Visual Basic 开发人员可以通过使用在代码隐藏中的句柄关键字将事件绑定实现性能稍有提升。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="8a6b1-136">C# 具有任何等效的关键字。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="8a6b1-137">新的 @ Page 指令属性</span><span class="sxs-lookup"><span data-stu-id="8a6b1-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="8a6b1-138">ASP.NET 2.0 将多个新属性添加到 @ Page 指令。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="8a6b1-139">以下属性是 ASP.NET 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="8a6b1-140">Async</span><span class="sxs-lookup"><span data-stu-id="8a6b1-140">Async</span></span>

<span data-ttu-id="8a6b1-141">在 Async 属性允许您配置页后，可以以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="8a6b1-142">我们将介绍更高版本在此模块中的异步页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="8a6b1-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="8a6b1-143">AsyncTimeout</span></span>

<span data-ttu-id="8a6b1-144">指定异步页面的超时时间。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="8a6b1-145">默认值为 45 秒。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="8a6b1-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="8a6b1-146">CodeFile</span></span>

<span data-ttu-id="8a6b1-147">CodeFile 特性将取代 Visual Studio 2002/2003 中的代码隐藏特性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="8a6b1-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="8a6b1-148">CodeFileBaseClass</span></span>

<span data-ttu-id="8a6b1-149">在想要从一个基类派生的多个页的情况下使用 CodeFileBaseClass 属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="8a6b1-150">由于在 ASP.NET 中，如果不使用此属性的分部类的实现使用共享的常见字段来引用在 ASPX 页面中声明的控件的基类将不能正常工作因为 ASP。网络编译引擎将自动创建基于页面中控件的新成员。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="8a6b1-151">因此，如果想在 ASP.NET 中的两个或多个页面的一个公共基类，您将需要定义 CodeFileBaseClass 属性中指定基类，然后从该基类派生的每个页面类。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="8a6b1-152">CodeFile 特性，还需要使用此属性时。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="8a6b1-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="8a6b1-153">CompilationMode</span></span>

<span data-ttu-id="8a6b1-154">此属性可以设置 ASPX 页的 CompilationMode 属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="8a6b1-155">CompilationMode 属性是一个枚举，包含的值**Always**，**自动**，并**从不**。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="8a6b1-156">默认值是**始终为**。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-156">The default is **Always**.</span></span> <span data-ttu-id="8a6b1-157">**自动**设置将阻止 ASP.NET 动态编译页面在可能的情况。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="8a6b1-158">从动态编译中排除页面可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="8a6b1-159">但是，如果排除的页面包含必须编译该代码，浏览页时将会引发错误。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="8a6b1-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="8a6b1-160">EnableEventValidation</span></span>

<span data-ttu-id="8a6b1-161">此属性指定验证回发和回调事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="8a6b1-162">启用此功能后，要回发参数或回调事件就会检查以确保它们源自最初呈现它们的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="8a6b1-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="8a6b1-163">EnableTheming</span></span>

<span data-ttu-id="8a6b1-164">此属性指定在页面上使用 ASP.NET 主题。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="8a6b1-165">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-165">The default is **false**.</span></span> <span data-ttu-id="8a6b1-166">中介绍了 ASP.NET 主题[模块 10](profiles-themes-and-web-parts.md)。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="8a6b1-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="8a6b1-167">LinePragmas</span></span>

<span data-ttu-id="8a6b1-168">此属性指定是否应在编译期间添加行杂注。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="8a6b1-169">行杂注是调试器用于标记代码的特定部分的选项。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="8a6b1-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="8a6b1-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="8a6b1-171">此属性指定 JavaScript 注入到页面以维护回发之间滚动位置。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="8a6b1-172">此属性是**false**默认情况下。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="8a6b1-173">当此属性是 **，则返回 true**，ASP.NET 将添加&lt;脚本&gt;块在回发时的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="8a6b1-174">请注意，此脚本块的 src WebResource.axd。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="8a6b1-175">此资源不是物理路径。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-175">This resource is not a physical path.</span></span> <span data-ttu-id="8a6b1-176">当请求此脚本时，ASP.NET 动态生成脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="8a6b1-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="8a6b1-177">MasterPageFile</span></span>

<span data-ttu-id="8a6b1-178">此属性指定当前页的主控页文件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="8a6b1-179">路径可以是相对值还是绝对值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-179">The path can be relative or absolute.</span></span> <span data-ttu-id="8a6b1-180">中介绍了母版页[模块 4](master-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="8a6b1-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="8a6b1-181">StyleSheetTheme</span></span>

<span data-ttu-id="8a6b1-182">此属性允许你重写由 ASP.NET 2.0 主题定义的用户界面外观属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="8a6b1-183">主题中介绍[模块 10](profiles-themes-and-web-parts.md)。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="8a6b1-184">主题</span><span class="sxs-lookup"><span data-stu-id="8a6b1-184">Theme</span></span>

<span data-ttu-id="8a6b1-185">指定的页面的主题。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-185">Specifies the theme for the page.</span></span> <span data-ttu-id="8a6b1-186">如果没有为 StyleSheetTheme 属性指定一个值，在 Theme 特性重写应用于控件的页上的所有样式。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="8a6b1-187">标题</span><span class="sxs-lookup"><span data-stu-id="8a6b1-187">Title</span></span>

<span data-ttu-id="8a6b1-188">设置页面标题。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-188">Sets the title for the page.</span></span> <span data-ttu-id="8a6b1-189">此处指定的值将出现在&lt;标题&gt;呈现页面上的元素。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="8a6b1-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="8a6b1-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="8a6b1-191">设置 ViewStateEncryptionMode 枚举的值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="8a6b1-192">可用值为**Always**，**自动**，并**从不**。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="8a6b1-193">默认值是**自动**。如果此属性设置为值**自动**，加密视图状态是控件请求通过调用**RegisterRequiresViewStateEncryption**方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="8a6b1-194">设置公共属性的值通过 @ Page 指令</span><span class="sxs-lookup"><span data-stu-id="8a6b1-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="8a6b1-195">ASP.NET 2.0 中的 @ Page 指令的另一新功能是能够设置基类的公共属性的初始值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="8a6b1-196">假设，例如，具有公共属性称为**SomeText**基类还意愿它初始化为**Hello**加载页时。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="8a6b1-197">您可以完成此操作通过只需在 @ Page 指令中设置的值如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="8a6b1-198">**SomeText** @ Page 指令的特性设置到基类中 SomeText 属性的初始值*Hello ！*。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="8a6b1-199">下面的视频是使用 @ Page 指令的基类中设置的公共属性的初始值的演练。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="8a6b1-200">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="8a6b1-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="8a6b1-201">页类的新的公共属性</span><span class="sxs-lookup"><span data-stu-id="8a6b1-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="8a6b1-202">以下公共属性是 ASP.NET 2.0 中新增的。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="8a6b1-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="8a6b1-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="8a6b1-204">返回到页或控件的应用程序相对路径。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="8a6b1-205">例如，对于位于一个页面 http://app/folder/page.aspx，该属性返回 ~ / 文件夹 /。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="8a6b1-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="8a6b1-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="8a6b1-207">返回的页或控件的相对虚拟目录路径。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="8a6b1-208">例如对于位于一个页面 http://app/folder/page.aspx，该属性返回 ~ / folder/page.aspx。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="8a6b1-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="8a6b1-209">AsyncTimeout</span></span>

<span data-ttu-id="8a6b1-210">获取或设置用于异步页处理的超时值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="8a6b1-211">（异步页面将在后面进行介绍此模块。）</span><span class="sxs-lookup"><span data-stu-id="8a6b1-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="8a6b1-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="8a6b1-212">ClientQueryString</span></span>

<span data-ttu-id="8a6b1-213">返回所请求的 URL 的查询字符串部分的只读属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="8a6b1-214">此值进行 URL 编码。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-214">This value is URL encoded.</span></span> <span data-ttu-id="8a6b1-215">HttpServerUtility 类的 UrlDecode 方法可用于对其进行解码。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="8a6b1-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="8a6b1-216">ClientScript</span></span>

<span data-ttu-id="8a6b1-217">此属性返回可用于管理 ASP.NETs 句子的客户端脚本的 ClientScriptManager 对象。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="8a6b1-218">（ClientScriptManager 类介绍此模块中的更高版本中）。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="8a6b1-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="8a6b1-219">EnableEventValidation</span></span>

<span data-ttu-id="8a6b1-220">此属性控制启用事件验证回发和回调事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="8a6b1-221">启用时，要回发参数或回调事件进行验证以确保它们源自最初呈现它们的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="8a6b1-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="8a6b1-222">EnableTheming</span></span>

<span data-ttu-id="8a6b1-223">此属性获取或设置一个布尔值，指定 ASP.NET 2.0 主题应用于页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="8a6b1-224">窗体</span><span class="sxs-lookup"><span data-stu-id="8a6b1-224">Form</span></span>

<span data-ttu-id="8a6b1-225">此属性为 HtmlForm 对象返回 ASPX 页上的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="8a6b1-226">Header</span><span class="sxs-lookup"><span data-stu-id="8a6b1-226">Header</span></span>

<span data-ttu-id="8a6b1-227">此属性返回对包含页眉的 HtmlHead 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="8a6b1-228">可以使用返回的 HtmlHead 对象来获取或设置样式表、 Meta 标记，等等。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="8a6b1-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="8a6b1-229">IdSeparator</span></span>

<span data-ttu-id="8a6b1-230">此只读属性获取用于分隔控件标识符，当 ASP.NET 在生成的唯一 ID 的页面上的控件时的字符。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="8a6b1-231">它不可直接通过代码使用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="8a6b1-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="8a6b1-232">IsAsync</span></span>

<span data-ttu-id="8a6b1-233">此属性允许异步页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="8a6b1-234">更高版本中此模块讨论了异步页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="8a6b1-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="8a6b1-235">IsCallback</span></span>

<span data-ttu-id="8a6b1-236">此只读属性返回 **，则返回 true**如果页是调用返回的结果。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="8a6b1-237">更高版本中此模块讨论了回拨。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="8a6b1-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="8a6b1-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="8a6b1-239">此只读属性返回 **，则返回 true**如果页是跨页回发的一部分。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="8a6b1-240">此模块中稍后介绍跨页回发。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="8a6b1-241">项</span><span class="sxs-lookup"><span data-stu-id="8a6b1-241">Items</span></span>

<span data-ttu-id="8a6b1-242">返回到 IDictionary 实例，其中包含存储在页上下文中的所有对象的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="8a6b1-243">可以将项添加到此 IDictionary 对象以及他们将在上下文的整个生存期内可用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="8a6b1-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="8a6b1-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="8a6b1-245">此属性控制 ASP.NET 发出保持页滚动位置，在浏览器中的，为在回发发生后的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="8a6b1-246">（此属性的详细信息讨论了之前在此模块中。）</span><span class="sxs-lookup"><span data-stu-id="8a6b1-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="8a6b1-247">Master</span><span class="sxs-lookup"><span data-stu-id="8a6b1-247">Master</span></span>

<span data-ttu-id="8a6b1-248">此只读属性返回对已应用主页面的页面 MasterPage 实例的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="8a6b1-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="8a6b1-249">MasterPageFile</span></span>

<span data-ttu-id="8a6b1-250">获取或设置页面的母版页文件名。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="8a6b1-251">仅可以 PreInit 方法中设置此属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="8a6b1-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="8a6b1-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="8a6b1-253">此属性获取或设置页状态的最大长度以字节为单位。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="8a6b1-254">如果该属性设置为正数，页面视图状态将分解为多个隐藏字段，以便它不会超过指定的字节数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="8a6b1-255">如果该属性为一个负数，视图状态将不会划分为区块。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="8a6b1-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="8a6b1-256">PageAdapter</span></span>

<span data-ttu-id="8a6b1-257">返回对修改的页请求的浏览器的 PageAdapter 对象的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="8a6b1-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="8a6b1-258">PreviousPage</span></span>

<span data-ttu-id="8a6b1-259">在 Server.Transfer 或跨页回发的情况下返回到前一页的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="8a6b1-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="8a6b1-260">SkinID</span></span>

<span data-ttu-id="8a6b1-261">指定要应用于页的 ASP.NET 2.0 外观。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="8a6b1-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="8a6b1-262">StyleSheetTheme</span></span>

<span data-ttu-id="8a6b1-263">此属性获取或设置应用于页的样式表。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="8a6b1-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="8a6b1-264">TemplateControl</span></span>

<span data-ttu-id="8a6b1-265">返回到页包含的控件的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="8a6b1-266">主题</span><span class="sxs-lookup"><span data-stu-id="8a6b1-266">Theme</span></span>

<span data-ttu-id="8a6b1-267">获取或设置应用于页面的 ASP.NET 2.0 主题的名称。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="8a6b1-268">必须在 PreInit 方法之前设置此值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="8a6b1-269">标题</span><span class="sxs-lookup"><span data-stu-id="8a6b1-269">Title</span></span>

<span data-ttu-id="8a6b1-270">此属性获取或设置页面标题，从页面标头中获得。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="8a6b1-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="8a6b1-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="8a6b1-272">获取或设置页面的 ViewStateEncryptionMode。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="8a6b1-273">请参阅本模块前面的此属性的详细的讨论。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="8a6b1-274">页类的新的受保护的属性</span><span class="sxs-lookup"><span data-stu-id="8a6b1-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="8a6b1-275">以下是 ASP.NET 2.0 中的页类的新的受保护的属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="8a6b1-276">适配器</span><span class="sxs-lookup"><span data-stu-id="8a6b1-276">Adapter</span></span>

<span data-ttu-id="8a6b1-277">返回的引用将在设备上的页呈现了 ControlAdapter 请求它。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="8a6b1-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="8a6b1-278">AsyncMode</span></span>

<span data-ttu-id="8a6b1-279">此属性指示以异步方式处理页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="8a6b1-280">由运行时并不是直接在代码中，它被供使用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="8a6b1-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="8a6b1-281">ClientIDSeparator</span></span>

<span data-ttu-id="8a6b1-282">此属性返回时为控件创建唯一的客户端 Id，用作分隔符的字符。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="8a6b1-283">由运行时并不是直接在代码中，它被供使用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="8a6b1-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="8a6b1-284">PageStatePersister</span></span>

<span data-ttu-id="8a6b1-285">此属性返回页面的 PageStatePersister 对象。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="8a6b1-286">此属性主要由 ASP.NET 控件开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="8a6b1-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="8a6b1-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="8a6b1-288">此属性返回的唯一后缀追加到用于缓存浏览器的文件路径。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="8a6b1-289">默认值是\_ \_ufps = 和一个 6 位数字。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="8a6b1-290">用于 Page 类的新公共方法</span><span class="sxs-lookup"><span data-stu-id="8a6b1-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="8a6b1-291">以下公共方法不熟悉 ASP.NET 2.0 中的页类。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="8a6b1-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="8a6b1-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="8a6b1-293">此方法注册为异步页执行的事件处理程序委托。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="8a6b1-294">更高版本中此模块讨论了异步页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="8a6b1-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="8a6b1-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="8a6b1-296">适用于页的页样式表中的属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="8a6b1-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="8a6b1-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="8a6b1-298">此方法才会异步任务。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="8a6b1-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="8a6b1-299">GetValidators</span></span>

<span data-ttu-id="8a6b1-300">如果未指定，则返回的验证程序指定的验证组或默认验证组的集合。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="8a6b1-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="8a6b1-301">RegisterAsyncTask</span></span>

<span data-ttu-id="8a6b1-302">此方法注册一个新的异步任务。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-302">This method registers a new async task.</span></span> <span data-ttu-id="8a6b1-303">此模块中稍后介绍异步页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="8a6b1-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="8a6b1-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="8a6b1-305">此方法告诉 ASP.NET，必须将页控件状态保存。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="8a6b1-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="8a6b1-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="8a6b1-307">此方法会告知 ASP.NET 页视图状态，需要加密。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="8a6b1-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="8a6b1-308">ResolveClientUrl</span></span>

<span data-ttu-id="8a6b1-309">返回可用于图像等的客户端请求的相对 URL。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="8a6b1-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="8a6b1-310">SetFocus</span></span>

<span data-ttu-id="8a6b1-311">此方法会将焦点设置到最初加载页面时指定的控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="8a6b1-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="8a6b1-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="8a6b1-313">此方法将取消注册为不再需要控件状态持久性传递给它的控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="8a6b1-314">对页面生命周期的更改</span><span class="sxs-lookup"><span data-stu-id="8a6b1-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="8a6b1-315">在 ASP.NET 2.0 中的页面生命周期尚未发生显著变化，但应注意的一些新方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="8a6b1-316">下面列出了在 ASP.NET 2.0 页面生命周期。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="8a6b1-317">PreInit （中 ASP.NET 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="8a6b1-318">PreInit 事件是一名开发人员可以访问的生命周期中的最早阶段。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="8a6b1-319">此事件添加会使可能要以编程方式更改 ASP.NET 2.0 主题，主页面，请访问 ASP.NET 2.0 配置文件等的属性。如果您是在回发状态下，一定要认识到，视图状态具有尚未应用到控件此时生命周期中。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="8a6b1-320">因此，如果在此阶段，开发人员更改控件的属性，它将可能覆盖页面生命周期中更高版本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="8a6b1-321">Init</span><span class="sxs-lookup"><span data-stu-id="8a6b1-321">Init</span></span>

<span data-ttu-id="8a6b1-322">Init 事件未更改从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="8a6b1-323">这是你想要读取或初始化您的页面上的控件的属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="8a6b1-324">在此阶段、 母版页、 主题等已应用到的页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="8a6b1-325">InitComplete （中 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-326">在页初始化阶段结束时，调用 InitComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="8a6b1-327">此时在生命周期中，可以访问控件的页上，但尚未填充其状态。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="8a6b1-328">预加载 （2.0 中的新增功能）</span><span class="sxs-lookup"><span data-stu-id="8a6b1-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-329">已应用所有回发数据后，只需在页之前调用此事件\_负载。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="8a6b1-330">Load</span><span class="sxs-lookup"><span data-stu-id="8a6b1-330">Load</span></span>

<span data-ttu-id="8a6b1-331">加载事件未更改从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="8a6b1-332">LoadComplete （中 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-333">LoadComplete 事件是在页加载阶段中的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="8a6b1-334">在此阶段，回发和视图状态的所有数据已都应用到的页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="8a6b1-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="8a6b1-335">PreRender</span></span>

<span data-ttu-id="8a6b1-336">如果您要用于视图状态的控件的动态添加到页面中正确维护，PreRender 事件是将其添加的最后机会。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="8a6b1-337">PreRenderComplete （中 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-338">在 PreRenderComplete 阶段中，所有控件已都添加到页和页已准备好呈现。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="8a6b1-339">PreRenderComplete 事件是页面视图状态保存之前引发的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="8a6b1-340">SaveStateComplete （中 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-341">已保存所有页面视图状态和控件状态后立即调用 SaveStateComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="8a6b1-342">这是页面实际上呈现到浏览器之前的最后一个事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="8a6b1-343">呈现</span><span class="sxs-lookup"><span data-stu-id="8a6b1-343">Render</span></span>

<span data-ttu-id="8a6b1-344">Render 方法未更改以来 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="8a6b1-345">这是初始化 HtmlTextWriter 和页呈现到浏览器的位置。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="8a6b1-346">ASP.NET 2.0 中的跨页回发</span><span class="sxs-lookup"><span data-stu-id="8a6b1-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="8a6b1-347">在 ASP.NET 1.x 中，回发所需发布到相同的页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="8a6b1-348">不允许跨页回发。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="8a6b1-349">ASP.NET 2.0 添加了回发到不同的页通过 IButtonControl 接口的功能。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="8a6b1-350">实现新 IButtonControl 接口 （按钮、 LinkButton 和第三方自定义控件除了 ImageButton） 的任何控件可以充分利用这一新功能通过 PostBackUrl 属性的使用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="8a6b1-351">下面的代码显示回发到第二个页的按钮控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="8a6b1-352">页面回发，启动回发页面时，可通过第二个页面的 PreviousPage 属性进行访问。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="8a6b1-353">通过新的 web 窗体中实现此功能\_DoPostBackWithOptions 控件回发到不同的页时，ASP.NET 2.0 将呈现给页的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="8a6b1-354">此 JavaScript 函数提供的新的 WebResource.axd 处理程序用来发出到客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="8a6b1-355">下面的视频是跨页回发的演练。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="8a6b1-356">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="8a6b1-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="8a6b1-357">在跨页回发的更多详细信息</span><span class="sxs-lookup"><span data-stu-id="8a6b1-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="8a6b1-358">视图状态</span><span class="sxs-lookup"><span data-stu-id="8a6b1-358">Viewstate</span></span>

<span data-ttu-id="8a6b1-359">您可能已要求自己已发生视图状态从跨页回发方案中的第一页有关。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="8a6b1-360">毕竟，不实现 IPostBackDataHandler 任何控件将其状态保存通过视图状态，因此有权访问该控件在跨页回发的第二页上的属性，必须具有对页面视图状态的访问。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="8a6b1-361">ASP.NET 2.0 负责这种情况下，使用名为的第二个页中的新的隐藏的字段\_ \_PREVIOUSPAGE。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="8a6b1-362">\_ \_PREVIOUSPAGE 窗体字段包含的第一页的视图状态，以便您可以在第二页中有权访问所有控件的属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="8a6b1-363">绕过 FindControl</span><span class="sxs-lookup"><span data-stu-id="8a6b1-363">Circumventing FindControl</span></span>

<span data-ttu-id="8a6b1-364">在跨页回发的视频演练中，我使用的 FindControl 方法来获取对第一页上的文本框控件的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="8a6b1-365">该方法非常适用于此目的，但 FindControl 很高，它需要编写附加代码。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="8a6b1-366">幸运的是，ASP.NET 2.0 提供了实现此目的，可以在许多方案的 FindControl 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="8a6b1-367">PreviousPageType 指令，可通过使用类型名称或 VirtualPath 属性具有对前一页的强类型引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="8a6b1-368">TypeName 特性，可指定前一页的类型，但 VirtualPath 特性，您可以使用虚拟路径的上一页，请参阅。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="8a6b1-369">设置 PreviousPageType 指令后，则必须公开控件，你想要允许使用公共属性的访问等。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="8a6b1-370">实验室 1 跨页回发</span><span class="sxs-lookup"><span data-stu-id="8a6b1-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="8a6b1-371">在此实验中，将创建使用新的 ASP.NET 2.0 跨页回发的功能的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="8a6b1-372">打开 Visual Studio 2005 并创建新的 ASP.NET Web 站点。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="8a6b1-373">添加名为 page2.aspx 的新 web 窗体。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="8a6b1-374">在设计视图中打开 Default.aspx 并添加一个按钮控件和文本框控件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="8a6b1-375">提供的 ID 的按钮控件**SubmitButton**和 TextBox 控件的 ID**用户名**。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="8a6b1-376">将按钮的 PostBackUrl 属性设置为 page2.aspx。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="8a6b1-377">在源视图中打开 page2.aspx。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="8a6b1-378">添加一个 @ PreviousPageType 指令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="8a6b1-379">将以下代码添加到页\_page2.aspx 的代码隐藏的负载：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="8a6b1-380">通过单击生成菜单上生成中生成项目。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="8a6b1-381">将以下代码添加到 Default.aspx 代码隐藏：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="8a6b1-382">更改的页\_中所示的 page2.aspx 负载：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="8a6b1-383">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-383">Build the project.</span></span>
11. <span data-ttu-id="8a6b1-384">运行该项目。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-384">Run the project.</span></span>
12. <span data-ttu-id="8a6b1-385">在文本框中输入你的名称，然后单击按钮。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="8a6b1-386">结果是什么？</span><span class="sxs-lookup"><span data-stu-id="8a6b1-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="8a6b1-387">ASP.NET 2.0 中异步页面</span><span class="sxs-lookup"><span data-stu-id="8a6b1-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="8a6b1-388">在 ASP.NET 中的很多争用问题所引起的延迟的外部调用 （例如 Web 服务或数据库调用），文件 IO 延迟，等等。当针对 ASP.NET 应用程序发出请求时，ASP.NET 将使用其工作线程之一来该请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="8a6b1-389">该请求拥有该线程，直到完成该请求并发送响应。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="8a6b1-390">ASP.NET 2.0 致力于通过添加以异步方式执行页的功能来解决这些类型的问题的延迟问题。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="8a6b1-391">这意味着工作线程可以启动请求，然后移交到另一个线程，从而快速返回到可用的线程池的其他执行。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="8a6b1-392">完成后的文件 IO、 数据库调用等，请从线程池，以完成请求获取新的线程。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="8a6b1-393">进行异步执行的页的第一步是设置**异步**页指令的特性如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="8a6b1-394">此属性告知 ASP.NET 实现 IHttpAsyncHandler 页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="8a6b1-395">下一步是在之前 PreRender 页生命周期中的点调用 AddOnPreRenderCompleteAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="8a6b1-396">(此方法通常在页面中调用\_负载。)AddOnPreRenderCompleteAsync 方法采用两个参数;来和 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="8a6b1-397">来返回到 EndEventHandler 然后作为参数传递的 IAsyncResult。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="8a6b1-398">以下视频是异步页请求的演练。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="8a6b1-399">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="8a6b1-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="8a6b1-400">直到完成 EndEventHandler 某个异步页面不呈现到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="8a6b1-401">毫无疑问，但某些开发人员将认为视作类似于异步回调的异步请求。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="8a6b1-402">请务必认识到它们不是。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-402">It's important to realize that they are not.</span></span> <span data-ttu-id="8a6b1-403">异步请求的好处是，第一个工作线程可以返回到线程池来支持新请求，从而减少了由于 IO 绑定的争用，等等。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="8a6b1-404">ASP.NET 2.0 中的脚本回调</span><span class="sxs-lookup"><span data-stu-id="8a6b1-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="8a6b1-405">Web 开发人员一直查找有关如何防止闪烁与回调相关联。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="8a6b1-406">在 ASP.NET 1.x 中，SmartNavigation 避免闪烁，最常用方法但 SmartNavigation 导致问题的一些开发人员由于其在客户端上实现的复杂性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="8a6b1-407">ASP.NET 2.0 解决了这一问题的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="8a6b1-408">脚本回调使用 XMLHttp 针对通过 JavaScript 的 Web 服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="8a6b1-409">XMLHttp 请求返回 XML 数据，然后可以操作通过浏览器的 dom。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="8a6b1-410">XMLHttp 代码是对用户隐藏的新 WebResource.axd 处理程序。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="8a6b1-411">有几个步骤所需以便配置 ASP.NET 2.0 中的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="8a6b1-412">步骤 1:实现 ICallbackEventHandler 接口</span><span class="sxs-lookup"><span data-stu-id="8a6b1-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="8a6b1-413">为了使 ASP.NET 可以识别您的页面为参与的脚本回调，您必须实现 ICallbackEventHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="8a6b1-414">您可以执行此操作在代码隐藏文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="8a6b1-415">您也可以这样做因此使用 @ Implements 指令类似于：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="8a6b1-416">使用内联 ASP.NET 代码时，通常会使用 @ Implements 指令。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="8a6b1-417">步骤 2:调用 GetCallbackEventReference</span><span class="sxs-lookup"><span data-stu-id="8a6b1-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="8a6b1-418">正如前面提到，XMLHttp 调用被封装在 WebResource.axd 处理程序。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="8a6b1-419">ASP.NET 呈现页面时，将添加对 web 窗体的调用\_DoCallback，WebResource.axd 的支持提供的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="8a6b1-420">该 web 窗体\_DoCallback 函数将替换\_ \_doPostBack 回调函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="8a6b1-421">请记住， \_ \_doPostBack 以编程方式提交窗体页上的。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="8a6b1-422">在回调方案中，你想要防止在回发，因此\_ \_doPostBack 将无法满足需要。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6b1-423">\_\_doPostBack 仍呈现到客户端脚本回调情形中的页。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="8a6b1-424">但是，它不用于回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="8a6b1-425">该 web 窗体的自变量\_DoCallback 客户端函数提供通过服务器端函数通常会在页面中调用的 GetCallbackEventReference\_负载。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="8a6b1-426">对 GetCallbackEventReference 的典型调用如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="8a6b1-427">在这种情况下，cm 是 ClientScriptManager 实例。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="8a6b1-428">ClientScriptManager 类将在此模块的后面进行介绍。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="8a6b1-429">有多个重载的版本的 GetCallbackEventReference。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="8a6b1-430">在这种情况下，参数是按如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="8a6b1-431">对调用 GetCallbackEventReference 控件的引用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="8a6b1-432">在这种情况下，它是页面本身。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="8a6b1-433">服务器端事件将从客户端代码中传递一个字符串参数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="8a6b1-434">在这种情况下，将下拉列表中的值传递的 Im 调用 ddlCompany。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="8a6b1-435">将接受的返回值 （作为字符串） 从服务器端的回调事件的客户端函数的名称。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="8a6b1-436">服务器端的回调成功后，将仅调用此函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="8a6b1-437">因此，为了可靠性，通常建议使用 GetCallbackEventReference 使用指定的要发生错误时执行的客户端的函数名称的其他字符串参数的重载的版本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="8a6b1-438">一个表示它在回调到服务器之前启动的客户端函数的字符串。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="8a6b1-439">在这种情况下，没有任何此类脚本，因此该参数为 null。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="8a6b1-440">一个布尔值，指定以异步方式执行回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="8a6b1-441">对 web 窗体调用\_DoCallback 客户端上的会将这些参数传递。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="8a6b1-442">因此，在客户端上呈现此页面时，该代码看起来如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="8a6b1-443">请注意，在客户端上函数的签名稍有不同。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="8a6b1-444">5 个字符串和布尔值，将传递客户端函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="8a6b1-445">（这是 null，在上面的示例中） 的附加字符串包含将处理服务器端的回调中的所有错误的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="8a6b1-446">步骤 3:挂接的客户端的控件事件</span><span class="sxs-lookup"><span data-stu-id="8a6b1-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="8a6b1-447">请注意，上述 GetCallbackEventReference 的返回值分配给字符串变量。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="8a6b1-448">该字符串用于挂接启动回调的控件的客户端的事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="8a6b1-449">在此示例中，该回调由启动下拉列表中的页上，我想要挂接*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="8a6b1-450">若要挂接客户端事件中，只需将一个处理程序添加到客户端的标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="8a6b1-451">请记住， *cbRef* GetCallbackEventReference 调用的返回值。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="8a6b1-452">它包含对 web 窗体调用\_DoCallback 上面所示。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="8a6b1-453">步骤 4:注册客户端脚本</span><span class="sxs-lookup"><span data-stu-id="8a6b1-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="8a6b1-454">回想一下，对 GetCallbackEventReference 调用指定客户端脚本调用**ShowCompanyName**服务器端的回调成功时将执行。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="8a6b1-455">该脚本需要添加到使用 ClientScriptManager 实例的页面。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="8a6b1-456">（ClientScriptManager 类将讨论此模块中更高版本。）因此执行操作，类似于：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="8a6b1-457">步骤 5:调用 ICallbackEventHandler 接口的方法</span><span class="sxs-lookup"><span data-stu-id="8a6b1-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="8a6b1-458">ICallbackEventHandler 包含你需要在代码中实现的两个方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="8a6b1-459">它们是**RaiseCallbackEvent**并**GetCallbackEvent**。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="8a6b1-460">**RaiseCallbackEvent**采用字符串作为参数并不返回任何内容。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="8a6b1-461">字符串参数传递到 web 窗体客户端调用\_DoCallback。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="8a6b1-462">在这种情况下，此值是*值*调用 ddlCompany 下拉列表中的属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="8a6b1-463">服务器端代码应置于 RaiseCallbackEvent 方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="8a6b1-464">例如，如果您的回调正在对外部资源 WebRequest，该代码应放置在 RaiseCallbackEvent。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="8a6b1-465">**GetCallbackEvent**负责处理回调的返回到客户端。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="8a6b1-466">它不采用任何参数并返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="8a6b1-467">它将返回的字符串将被作为参数传递给客户端的函数，在这种情况下*ShowCompanyName*。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="8a6b1-468">完成上述步骤后，你现可在 ASP.NET 2.0 中执行的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="8a6b1-469">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="8a6b1-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="8a6b1-470">在 ASP.NET 中的脚本回调中支持使 XMLHttp 调用任何浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="8a6b1-471">中包括的所有新式浏览器中使用今天。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="8a6b1-472">Internet Explorer 使用 XMLHttp ActiveX 对象，而其他现代浏览器 （包括即将推出的 IE 7） 使用的内部的 XMLHttp 对象。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="8a6b1-473">若要以编程方式确定是否浏览器支持回调，则可以使用**Request.Browser.SupportCallback**属性。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="8a6b1-474">此属性将返回 **，则返回 true**如果请求的客户端支持的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="8a6b1-475">使用 ASP.NET 2.0 中的客户端脚本</span><span class="sxs-lookup"><span data-stu-id="8a6b1-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="8a6b1-476">在 ASP.NET 2.0 中的客户端脚本通过 ClientScriptManager 类的使用进行管理。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="8a6b1-477">跟踪客户端脚本使用一种类型和名称的 ClientScriptManager 类。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="8a6b1-478">这可以防止同一个脚本以编程方式插入页面上一次以上。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6b1-479">脚本已成功注册页面上后，任何后续尝试注册相同的脚本只需将导致未注册第二次该脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="8a6b1-480">添加任何重复的脚本，并且没有发生异常。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="8a6b1-481">若要避免不必要的计算，有可用于确定脚本是否已注册，以便不尝试超过一次注册的方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="8a6b1-482">Clientscriptmanager 处理的方法应为所有当前的 ASP.NET 开发人员所熟悉:</span><span class="sxs-lookup"><span data-stu-id="8a6b1-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="8a6b1-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="8a6b1-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="8a6b1-484">此方法将脚本添加到呈现的页的顶部。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="8a6b1-485">这可用于添加将在客户端显式调用的函数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="8a6b1-486">有两个重载的版本，此方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="8a6b1-487">三个四个参数是在它们之间通用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="8a6b1-488">它们是：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-488">They are:</span></span>

`type (string)`

<span data-ttu-id="8a6b1-489">***类型***参数标识脚本的类型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="8a6b1-490">它通常是一个好办法，请使用页面的类型 （这。GetType()) 的类型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="8a6b1-491">***密钥***参数是该脚本的用户定义键。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="8a6b1-492">这应该是唯一的每个脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-492">This should be unique for each script.</span></span> <span data-ttu-id="8a6b1-493">如果尝试添加具有相同的密钥和已添加了脚本的类型的脚本，将不会添加它。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="8a6b1-494">***脚本***参数是一个包含要添加的实际脚本的字符串。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="8a6b1-495">建议使用 StringBuilder 创建脚本，然后使用 StringBuilder 上的 tostring （） 方法来分配***脚本***参数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="8a6b1-496">如果使用重载的 RegisterClientScriptBlock 只使用三个参数，则必须包括脚本元素 (&lt;脚本&gt;并&lt;/script&gt;) 在脚本中。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="8a6b1-497">您可以选择使用 RegisterClientScriptBlock 第四个自变量的重载。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="8a6b1-498">第四个参数是一个布尔值，指定 ASP.NET 应为您添加脚本元素。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="8a6b1-499">如果此参数，则 **，则返回 true**，您的脚本不应包含的脚本元素显式。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="8a6b1-500">IsClientScriptBlockRegistered 方法用于确定是否已注册脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="8a6b1-501">这可以避免尝试重新注册已注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="8a6b1-502">RegisterClientScriptInclude （中 2.0)</span><span class="sxs-lookup"><span data-stu-id="8a6b1-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="8a6b1-503">RegisterClientScriptInclude 标记创建一个脚本块链接到外部脚本文件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="8a6b1-504">它有两个重载。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-504">It has two overloads.</span></span> <span data-ttu-id="8a6b1-505">一种采用密钥和 URL。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-505">One takes a key and a URL.</span></span> <span data-ttu-id="8a6b1-506">第二个将添加第三个参数指定的类型。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="8a6b1-507">例如，下面的代码的脚本块链接到 jsfunctions.js 根目录中生成的应用程序的 scripts 文件夹：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="8a6b1-508">此代码生成呈现的页面中的以下代码：</span><span class="sxs-lookup"><span data-stu-id="8a6b1-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="8a6b1-509">脚本块呈现在页面底部。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="8a6b1-510">IsClientScriptIncludeRegistered 方法用于确定是否已注册脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="8a6b1-511">这可以避免尝试重新注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="8a6b1-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="8a6b1-512">RegisterStartupScript</span></span>

<span data-ttu-id="8a6b1-513">RegisterStartupScript 方法采用与 RegisterClientScriptBlock 方法相同的参数。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="8a6b1-514">RegisterStartupScript 中注册的脚本执行在页面加载之后、 但在 OnLoad 客户端的事件。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="8a6b1-515">在 1.X 中，使用 RegisterStartupScript 已注册的脚本已放恰好在关闭之前&lt;/形成&gt;标记而 RegisterClientScriptBlock 与已注册的脚本已被放在打开后立即&lt;窗体&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="8a6b1-516">在 ASP.NET 2.0 中，同时位于结束之前立即&lt;/&gt;标记。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="8a6b1-517">如果对 RegisterStartupScript 注册了一个函数，该函数不会执行，直到显式需在客户端代码中调用它即可。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="8a6b1-518">IsStartupScriptRegistered 方法用于确定是否已注册一个脚本，从而避免尝试重新注册的脚本。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="8a6b1-519">其他 ClientScriptManager 方法</span><span class="sxs-lookup"><span data-stu-id="8a6b1-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="8a6b1-520">以下是一些其他有用的 ClientScriptManager 类方法。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="8a6b1-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="8a6b1-522">请参阅本模块前面的脚本回调。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="8a6b1-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="8a6b1-524">获取 JavaScript 参考 (javascript:&lt;调用&gt;) 可用于从客户端事件重新发布。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="8a6b1-525"><strong>GetPostBackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="8a6b1-526">获取一个字符串，可用来发起从客户端返回 post 调用。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="8a6b1-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="8a6b1-528">返回到程序集内嵌入的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="8a6b1-529">必须与结合使用<strong>RegisterClientScriptResource</strong>。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="8a6b1-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="8a6b1-531">向页注册的 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="8a6b1-532">以下是资源嵌入程序集中并由新的 WebResource.axd 处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="8a6b1-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="8a6b1-534">向页注册隐藏窗体字段。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="8a6b1-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="8a6b1-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="8a6b1-536">注册客户端代码执行时提交的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="8a6b1-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |

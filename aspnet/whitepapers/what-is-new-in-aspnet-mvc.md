---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2 的新增功能 |Microsoft Docs
author: rick-anderson
description: 本文档介绍 ASP.NET MVC 2 中引入的新功能和改进。 此文档也可以下载。
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045034"
---
# <a name="whats-new-in-aspnet-mvc-2"></a><span data-ttu-id="cfe12-104">ASP.NET MVC 2 的新增功能</span><span class="sxs-lookup"><span data-stu-id="cfe12-104">What's New in ASP.NET MVC 2</span></span>

> <span data-ttu-id="cfe12-105">本文档介绍 ASP.NET MVC 2 中引入的新功能和改进。</span><span class="sxs-lookup"><span data-stu-id="cfe12-105">This document describes new features and improvements introduced in ASP.NET MVC 2.</span></span> <span data-ttu-id="cfe12-106">此文档还可供 [下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)</span><span class="sxs-lookup"><span data-stu-id="cfe12-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)</span></span>

<span data-ttu-id="cfe12-107">[产品介绍](#_TOC1) </span><span class="sxs-lookup"><span data-stu-id="cfe12-107">[Introduction](#_TOC1) </span></span>  
<span data-ttu-id="cfe12-108">[将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2](#_TOC2) </span><span class="sxs-lookup"><span data-stu-id="cfe12-108">[Upgrading an ASP.NET MVC 1.0 Project to ASP.NET MVC 2](#_TOC2) </span></span>  
<span data-ttu-id="cfe12-109">[新功能](#_TOC3) </span><span class="sxs-lookup"><span data-stu-id="cfe12-109">[New Features](#_TOC3) </span></span>  
<span data-ttu-id="cfe12-110">[模板化帮助器](#_TOC3_1) </span><span class="sxs-lookup"><span data-stu-id="cfe12-110">[Templated Helpers](#_TOC3_1) </span></span>  
<span data-ttu-id="cfe12-111">[区域](#_TOC3_2) </span><span class="sxs-lookup"><span data-stu-id="cfe12-111">[Areas](#_TOC3_2) </span></span>  
<span data-ttu-id="cfe12-112">[支持异步控制器](#_TOC3_3) </span><span class="sxs-lookup"><span data-stu-id="cfe12-112">[Support for Asynchronous Controllers](#_TOC3_3) </span></span>  
<span data-ttu-id="cfe12-113">[在操作方法参数中对 DefaultValueAttribute 的支持](#_TOC3_4) </span><span class="sxs-lookup"><span data-stu-id="cfe12-113">[Support for DefaultValueAttribute in Action-Method Parameters](#_TOC3_4) </span></span>  
<span data-ttu-id="cfe12-114">[支持在模型联编程序中绑定二进制数据](#_TOC3_5) </span><span class="sxs-lookup"><span data-stu-id="cfe12-114">[Support for Binding Binary Data with Model Binders](#_TOC3_5) </span></span>  
<span data-ttu-id="cfe12-115">[ModelMetadata 和 ModelMetadataProvider 类](#_TOC3_6) </span><span class="sxs-lookup"><span data-stu-id="cfe12-115">[ModelMetadata and ModelMetadataProvider Classes](#_TOC3_6) </span></span>  
<span data-ttu-id="cfe12-116">[支持 DataAnnotations 属性](#_TOC3_7) </span><span class="sxs-lookup"><span data-stu-id="cfe12-116">[Support for DataAnnotations Attributes](#_TOC3_7) </span></span>  
<span data-ttu-id="cfe12-117">[模型验证程序提供程序](#_TOC3_8) </span><span class="sxs-lookup"><span data-stu-id="cfe12-117">[Model-Validator Providers](#_TOC3_8) </span></span>  
<span data-ttu-id="cfe12-118">[客户端验证](#_TOC3_9) </span><span class="sxs-lookup"><span data-stu-id="cfe12-118">[Client-Side Validation](#_TOC3_9) </span></span>  
<span data-ttu-id="cfe12-119">[Visual Studio 2010 的新代码段](#_TOC3_10) </span><span class="sxs-lookup"><span data-stu-id="cfe12-119">[New Code Snippets for Visual Studio 2010](#_TOC3_10) </span></span>  
<span data-ttu-id="cfe12-120">[新建 RequireHttpsAttribute 操作筛选器](#_TOC3_11) </span><span class="sxs-lookup"><span data-stu-id="cfe12-120">[New RequireHttpsAttribute Action Filter](#_TOC3_11) </span></span>  
<span data-ttu-id="cfe12-121">[重写 HTTP 方法谓词](#_TOC3_12) </span><span class="sxs-lookup"><span data-stu-id="cfe12-121">[Overriding the HTTP Method Verb](#_TOC3_12) </span></span>  
<span data-ttu-id="cfe12-122">[模板化帮助器的新 HiddenInputAttribute 类](#_TOC3_13) </span><span class="sxs-lookup"><span data-stu-id="cfe12-122">[New HiddenInputAttribute Class for Templated Helpers](#_TOC3_13) </span></span>  
<span data-ttu-id="cfe12-123">[ValidationSummary Helper 方法可以显示模型级别错误](#_TOC3_14) </span><span class="sxs-lookup"><span data-stu-id="cfe12-123">[Html.ValidationSummary Helper Method Can Display Model-Level Errors](#_TOC3_14) </span></span>  
<span data-ttu-id="cfe12-124">[Visual Studio 中的 T4 模板生成特定于 .NET Framework](#_TOC3_15)[API 改进](#_TOC4)目标版本的代码</span><span class="sxs-lookup"><span data-stu-id="cfe12-124">[T4 Templates in Visual Studio Generate Code that is Specific to the Target Version of the .NET Framework](#_TOC3_15)[API Improvements](#_TOC4)</span></span>  
[<span data-ttu-id="cfe12-125">重大更改</span><span class="sxs-lookup"><span data-stu-id="cfe12-125">Breaking Changes</span></span>](#_TOC5)  
[<span data-ttu-id="cfe12-126">免责声明</span><span class="sxs-lookup"><span data-stu-id="cfe12-126">Disclaimer</span></span>](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  <span data-ttu-id="cfe12-127">产品介绍</span><span class="sxs-lookup"><span data-stu-id="cfe12-127">Introduction</span></span>

<span data-ttu-id="cfe12-128">ASP.NET MVC 2 在 ASP.NET MVC 1.0 上构建，引入了大量的增强功能和功能，重点提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="cfe12-128">ASP.NET MVC 2 builds on ASP.NET MVC 1.0 and introduces a large set of enhancements and features that are focused on increasing productivity.</span></span> <span data-ttu-id="cfe12-129">此版本与 ASP.NET MVC 1.0 兼容，因此，ASP.NET MVC 1.0 的所有知识、技能、代码和扩展仍适用。</span><span class="sxs-lookup"><span data-stu-id="cfe12-129">This release is compatible with ASP.NET MVC 1.0, so all your knowledge, skills, code, and extensions for ASP.NET MVC 1.0 continue to apply.</span></span>

<span data-ttu-id="cfe12-130">有关 ASP.NET MVC 的详细信息，请访问以下资源：</span><span class="sxs-lookup"><span data-stu-id="cfe12-130">For more information about ASP.NET MVC, visit the following resources:</span></span>

- [<span data-ttu-id="cfe12-131">MSDN 上的 ASP.NET MVC 文档</span><span class="sxs-lookup"><span data-stu-id="cfe12-131">ASP.NET MVC documentation on MSDN</span></span>](https://go.microsoft.com/fwlink/?LinkId=159758)
- [<span data-ttu-id="cfe12-132">ASP.NET MVC 网站</span><span class="sxs-lookup"><span data-stu-id="cfe12-132">The ASP.NET MVC Web site</span></span>](https://asp.net/mvc/)
- [<span data-ttu-id="cfe12-133">ASP.NET MVC 论坛</span><span class="sxs-lookup"><span data-stu-id="cfe12-133">The ASP.NET MVC forums</span></span>](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  <span data-ttu-id="cfe12-134">将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2</span><span class="sxs-lookup"><span data-stu-id="cfe12-134">Upgrading an ASP.NET MVC 1.0 Project to ASP.NET MVC 2</span></span>

<span data-ttu-id="cfe12-135">ASP.NET MVC 2 可以与同一服务器上的 ASP.NET MVC 1.0 并行安装，这使应用程序开发人员可以灵活选择何时将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="cfe12-135">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server, which gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span> <span data-ttu-id="cfe12-136">有关如何升级的信息，请参阅将 [ASP.NET mvc 1.0 应用程序升级到 ASP.NET mvc 2](https://go.microsoft.com/fwlink/?LinkID=185459)的文档。</span><span class="sxs-lookup"><span data-stu-id="cfe12-136">For information on how to upgrade, see the document [Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).</span></span>

## <a name="new-features"></a><a id="_TOC3"></a>  <span data-ttu-id="cfe12-137">新功能</span><span class="sxs-lookup"><span data-stu-id="cfe12-137">New Features</span></span>

<span data-ttu-id="cfe12-138">本部分介绍了在 MVC 2 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="cfe12-138">This section describes features that have been introduced in the MVC 2 release.</span></span>

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  <span data-ttu-id="cfe12-139">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="cfe12-139">Templated Helpers</span></span>

<span data-ttu-id="cfe12-140">模板化帮助器允许您自动将用于编辑和显示的 HTML 元素与数据类型相关联。</span><span class="sxs-lookup"><span data-stu-id="cfe12-140">Templated helpers let you automatically associate HTML elements for edit and display with data types.</span></span> <span data-ttu-id="cfe12-141">例如，当视图中显示类型为 system.string 的数据时，可以自动呈现日期选取器 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="cfe12-141">For example, when data of type System.DateTime is displayed in a view, a date-picker UI element can be automatically rendered.</span></span> <span data-ttu-id="cfe12-142">这类似于字段模板在 ASP.NET 动态数据中的工作方式。</span><span class="sxs-lookup"><span data-stu-id="cfe12-142">This is similar to how field templates work in ASP.NET Dynamic Data.</span></span> <span data-ttu-id="cfe12-143">有关详细信息，请参阅 MSDN 网站上的 [使用模板化帮助器显示数据](https://go.microsoft.com/fwlink/?LinkId=159062) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-143">For more information, see [Using Templated Helpers to Display Data](https://go.microsoft.com/fwlink/?LinkId=159062) on the MSDN Web site.</span></span>

### <a name="areas"></a><a id="_TOC3_2"></a>  <span data-ttu-id="cfe12-144">区域</span><span class="sxs-lookup"><span data-stu-id="cfe12-144">Areas</span></span>

<span data-ttu-id="cfe12-145">使用区域可以将大型项目组织为多个较小的分区，以便管理大型 Web 应用程序的复杂性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-145">Areas let you organize a large project into multiple smaller sections in order to manage the complexity of a large Web application.</span></span> <span data-ttu-id="cfe12-146"> ( "area" ) 的每个部分通常代表一个大型网站的单独部分，并用于对相关的控制器和视图集进行分组。</span><span class="sxs-lookup"><span data-stu-id="cfe12-146">Each section ("area") typically represents a separate section of a large Web site and is used to group related sets of controllers and views.</span></span> <span data-ttu-id="cfe12-147">有关详细信息，请参阅 MSDN 网站上的 [演练：按区域组织 ASP.NET MVC 应用程序](https://go.microsoft.com/fwlink/?LinkId=158978) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-147">For more information, see [Walkthrough: Organizing an ASP.NET MVC Application by Areas](https://go.microsoft.com/fwlink/?LinkId=158978) on the MSDN Web site.</span></span>

<span data-ttu-id="cfe12-148">若要创建新区域，请在解决方案资源管理器中右键单击该项目，单击 "添加"，然后单击 "区域"。</span><span class="sxs-lookup"><span data-stu-id="cfe12-148">To create a new area, in Solution Explorer, right-click the project, click Add, and then click Area.</span></span> <span data-ttu-id="cfe12-149">此时将显示一个对话框，提示您输入区域名称。</span><span class="sxs-lookup"><span data-stu-id="cfe12-149">This displays a dialog box that prompts you for the area name.</span></span> <span data-ttu-id="cfe12-150">输入区域名称后，Visual Studio 会向项目中添加一个新区域。</span><span class="sxs-lookup"><span data-stu-id="cfe12-150">After you enter the area name, Visual Studio adds a new area to the project.</span></span>

<span data-ttu-id="cfe12-151">下图显示了项目的示例布局，其中包含两个区域：管理员和博客。</span><span class="sxs-lookup"><span data-stu-id="cfe12-151">The following figure shows an example layout for a project with two areas, Admin and Blogs.</span></span>

![](what-is-new-in-aspnet-mvc/_static/image1.png)

<span data-ttu-id="cfe12-152">创建区域时，Visual Studio 会将从 AreaRegistration 派生的类添加到每个区域。</span><span class="sxs-lookup"><span data-stu-id="cfe12-152">When you create an area, Visual Studio adds a class that derives from AreaRegistration to each area.</span></span> <span data-ttu-id="cfe12-153">若要注册区域及其路由，需要此类，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-153">This class is required in order to register the area and its routes, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

<span data-ttu-id="cfe12-154">ASP.NET MVC 2 的默认项目模板在 global.asax 文件的代码中包含对 RegisterAllAreas 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="cfe12-154">The default project template for ASP.NET MVC 2 includes a call to the RegisterAllAreas method in the code for the Global.asax file.</span></span> <span data-ttu-id="cfe12-155">此方法通过查找派生自 AreaRegistration 类的所有类型、实例化类型的实例，然后对实例调用 RegisterArea 方法来注册项目中的每个区域。</span><span class="sxs-lookup"><span data-stu-id="cfe12-155">This method registers each area in the project by looking for all types that derive from the AreaRegistration class, instantiating an instance of the type, and then calling the RegisterArea method on the instance.</span></span> <span data-ttu-id="cfe12-156">下面的示例演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cfe12-156">The following example shows how this is done.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

<span data-ttu-id="cfe12-157">如果未通过调用上下文来指定 RegisterArea 方法中的命名空间，则为。命名空间. Add 方法，默认情况下使用注册类的命名空间。</span><span class="sxs-lookup"><span data-stu-id="cfe12-157">If you do not specify the namespace in the RegisterArea method by calling the context.Namespaces.Add method, the namespace of the registration class is used by default.</span></span>

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  <span data-ttu-id="cfe12-158">支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="cfe12-158">Support for Asynchronous Controllers</span></span>

<span data-ttu-id="cfe12-159">ASP.NET MVC 2 现在允许控制器异步处理请求。</span><span class="sxs-lookup"><span data-stu-id="cfe12-159">ASP.NET MVC 2 now allows controllers to process requests asynchronously.</span></span> <span data-ttu-id="cfe12-160">这可以通过允许频繁调用阻止操作 (如网络请求) 的服务器而不是调用非阻塞对等项，从而提高性能。</span><span class="sxs-lookup"><span data-stu-id="cfe12-160">This can lead to performance gains by allowing servers which frequently call blocking operations (like network requests) to call non-blocking counterparts instead.</span></span> <span data-ttu-id="cfe12-161">有关详细信息，请参阅 MSDN 上的在 [ASP.NET MVC 中使用异步控制器](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) 主题。</span><span class="sxs-lookup"><span data-stu-id="cfe12-161">For more information, see the [Using an Asynchronous Controller in ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) topic on MSDN.</span></span>

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  <span data-ttu-id="cfe12-162">在操作方法参数中对 DefaultValueAttribute 的支持</span><span class="sxs-lookup"><span data-stu-id="cfe12-162">Support for DefaultValueAttribute in Action-Method Parameters</span></span>

<span data-ttu-id="cfe12-163">System.componentmodel. DefaultValueAttribute 类允许将默认值提供给操作方法的参数参数。</span><span class="sxs-lookup"><span data-stu-id="cfe12-163">The System.ComponentModel.DefaultValueAttribute class allows a default value to be supplied for the argument parameter to an action method.</span></span> <span data-ttu-id="cfe12-164">例如，假设定义了以下默认路由：</span><span class="sxs-lookup"><span data-stu-id="cfe12-164">For example, assume that the following default route is defined:</span></span>

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

<span data-ttu-id="cfe12-165">还假定定义了以下控制器和操作方法：</span><span class="sxs-lookup"><span data-stu-id="cfe12-165">Also assume that the following controller and action method is defined:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

<span data-ttu-id="cfe12-166">以下任何请求 Url 都将调用在前面的示例中定义的视图操作方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-166">Any of the following request URLs will invoke the View action method that is defined in the preceding example.</span></span>

- <span data-ttu-id="cfe12-167">/Article/View/123</span><span class="sxs-lookup"><span data-stu-id="cfe12-167">/Article/View/123</span></span>
- <span data-ttu-id="cfe12-168">/Article/View/123？ page = 1 (与以前的请求有效) </span><span class="sxs-lookup"><span data-stu-id="cfe12-168">/Article/View/123?page=1 (Effectively the same as the previous request)</span></span>
- <span data-ttu-id="cfe12-169">/Article/View/123？页 = 2</span><span class="sxs-lookup"><span data-stu-id="cfe12-169">/Article/View/123?page=2</span></span>

<span data-ttu-id="cfe12-170">如果没有 DefaultValueAttribute 属性，则前面的列表中的第一个 URL 将不起作用，因为页参数是不可以为 null 的值类型，其值尚未提供。</span><span class="sxs-lookup"><span data-stu-id="cfe12-170">Without the DefaultValueAttribute attribute, the first URL from the preceding list would not work, because the page argument is a non-nullable value type whose value has not been provided.</span></span>

<span data-ttu-id="cfe12-171">如果代码是用 Visual Basic 2010 或 Visual c # 2010 编写的，则可以使用可选参数，而不是 DefaultValueAttribute 属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-171">If your code is written in Visual Basic 2010 or Visual C# 2010, you can use optional parameters instead of the DefaultValueAttribute attribute, as shown in the following example:</span></span>

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  <span data-ttu-id="cfe12-172">支持在模型联编程序中绑定二进制数据</span><span class="sxs-lookup"><span data-stu-id="cfe12-172">Support for Binding Binary Data with Model Binders</span></span>

<span data-ttu-id="cfe12-173">Html 的隐藏帮助程序有两个新的重载，这些重载将二进制值编码为64编码的字符串：</span><span class="sxs-lookup"><span data-stu-id="cfe12-173">There are two new overloads of the Html.Hidden helper that encode binary values as base-64-encoded strings:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

<span data-ttu-id="cfe12-174">典型用途是在视图中嵌入对象的时间戳。</span><span class="sxs-lookup"><span data-stu-id="cfe12-174">A typical use is to embed a timestamp for an object in the view.</span></span> <span data-ttu-id="cfe12-175">例如，你的应用程序可能包含以下 Product 对象：</span><span class="sxs-lookup"><span data-stu-id="cfe12-175">For example, your application might include the following Product object:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

<span data-ttu-id="cfe12-176">编辑窗体可以在窗体中呈现时间戳属性，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-176">An edit form can render the TimeStamp property in the form as shown in the following example:</span></span>

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

<span data-ttu-id="cfe12-177">此标记会将时间戳值为的隐藏输入元素呈现为以64编码的字符串，类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="cfe12-177">This markup renders a hidden input element with the timestamp value as a base-64-encoded string that resembles the following example:</span></span>

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

<span data-ttu-id="cfe12-178">此窗体可能会发布到具有类型为 Product 的参数的操作方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-178">This form might be posted to an action method that has an argument of type Product, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

<span data-ttu-id="cfe12-179">在操作方法中，TimeStamp 属性会正确填充，因为已发布的64编码字符串将转换为字节数组。</span><span class="sxs-lookup"><span data-stu-id="cfe12-179">In the action method, the TimeStamp property is populated correctly because the posted base-64-encoded string is converted to a byte array.</span></span>

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  <span data-ttu-id="cfe12-180">ModelMetadata 和 ModelMetadataProvider 类</span><span class="sxs-lookup"><span data-stu-id="cfe12-180">ModelMetadata and ModelMetadataProvider Classes</span></span>

<span data-ttu-id="cfe12-181">ModelMetadataProvider 类提供了一个抽象，用于获取视图中模型的元数据。</span><span class="sxs-lookup"><span data-stu-id="cfe12-181">The ModelMetadataProvider class provides an abstraction for obtaining metadata for the model within a view.</span></span> <span data-ttu-id="cfe12-182">MVC 2 包含一个默认提供程序，该提供程序使 System.componentmodel. DataAnnotations 命名空间中的属性公开的元数据可用。</span><span class="sxs-lookup"><span data-stu-id="cfe12-182">MVC 2 includes a default provider that makes available the metadata that is exposed by the attributes in the System.ComponentModel.DataAnnotations namespace.</span></span> <span data-ttu-id="cfe12-183">可以创建从其他数据存储（如数据库或 XML 文件）提供元数据的元数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="cfe12-183">It is possible to create metadata providers that provide metadata from other data stores, such as databases or XML files.</span></span>

<span data-ttu-id="cfe12-184">ViewDataDictionary 类公开 ModelMetadata 对象，该对象包含 ModelMetadataProvider 类从模型中提取的元数据。</span><span class="sxs-lookup"><span data-stu-id="cfe12-184">The ViewDataDictionary class exposes a ModelMetadata object that contains the metadata that is extracted from the model by the ModelMetadataProvider class.</span></span> <span data-ttu-id="cfe12-185">这使模板化帮助器可以使用此元数据，并相应地调整它们的输出。</span><span class="sxs-lookup"><span data-stu-id="cfe12-185">This enables the templated helpers to consume this metadata and adjust their output accordingly.</span></span>

<span data-ttu-id="cfe12-186">有关详细信息，请参阅 [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 和 [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 类的文档。</span><span class="sxs-lookup"><span data-stu-id="cfe12-186">For more information, see the documentation for the [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) and [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) classes.</span></span>

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  <span data-ttu-id="cfe12-187">支持 DataAnnotations 属性</span><span class="sxs-lookup"><span data-stu-id="cfe12-187">Support for DataAnnotations Attributes</span></span>

<span data-ttu-id="cfe12-188">当您绑定到某一模型以提供输入验证时，ASP.NET MVC 2 支持使用 RegexAttribute) 命名空间中定义的 RangeAttribute、有 requiredattribute、StringLengthAttribute 和 System.componentmodel 验证特性 (。</span><span class="sxs-lookup"><span data-stu-id="cfe12-188">ASP.NET MVC 2 supports using the RangeAttribute, RequiredAttribute, StringLengthAttribute, and RegexAttribute validation attributes (defined in the System.ComponentModel.DataAnnotations namespace) when you bind to a model in order to provide input validation.</span></span>

<span data-ttu-id="cfe12-189">有关详细信息，请参阅 MSDN 网站上的 [如何：使用 DataAnnotations 属性验证模型数据](https://go.microsoft.com/fwlink/?LinkId=159063) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-189">For more information, see [How to: Validate Model Data Using DataAnnotations Attributes](https://go.microsoft.com/fwlink/?LinkId=159063) on the MSDN Web site.</span></span> <span data-ttu-id="cfe12-190">演示如何使用这些属性的示例项目可从下载 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-190">A sample project that illustrates the use of these attributes is available for download at [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753).</span></span>

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  <span data-ttu-id="cfe12-191">模型验证程序提供程序</span><span class="sxs-lookup"><span data-stu-id="cfe12-191">Model-Validator Providers</span></span>

<span data-ttu-id="cfe12-192">模型验证提供程序类表示为模型提供验证逻辑的抽象。</span><span class="sxs-lookup"><span data-stu-id="cfe12-192">The model-validation provider class represents an abstraction that provides validation logic for the model.</span></span> <span data-ttu-id="cfe12-193">ASP.NET MVC 包含基于 System.componentmodel. DataAnnotations 命名空间中包含的验证属性的默认提供程序。</span><span class="sxs-lookup"><span data-stu-id="cfe12-193">ASP.NET MVC includes a default provider based on validation attributes that are included in the System.ComponentModel.DataAnnotations namespace.</span></span> <span data-ttu-id="cfe12-194">您还可以创建自己的验证提供程序，用于定义自定义验证规则以及验证规则到模型的自定义映射。</span><span class="sxs-lookup"><span data-stu-id="cfe12-194">You can also create your own validation providers that define custom validation rules and custom mappings of validation rules to the model.</span></span> <span data-ttu-id="cfe12-195">有关详细信息，请参阅 [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) 类的文档。</span><span class="sxs-lookup"><span data-stu-id="cfe12-195">For more information, see the documentation for the [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) class.</span></span>

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  <span data-ttu-id="cfe12-196">客户端验证</span><span class="sxs-lookup"><span data-stu-id="cfe12-196">Client-Side Validation</span></span>

<span data-ttu-id="cfe12-197">模型验证程序提供程序类将验证元数据以 JSON 序列化数据（可由客户端验证库使用）的形式公开给浏览器。</span><span class="sxs-lookup"><span data-stu-id="cfe12-197">The model-validator provider class exposes validation metadata to the browser in the form of JSON-serialized data that can be consumed by a client-side validation library.</span></span> <span data-ttu-id="cfe12-198">ASP.NET MVC 2 包括客户端验证库和支持前面提到的 DataAnnotations 命名空间验证特性的适配器。</span><span class="sxs-lookup"><span data-stu-id="cfe12-198">ASP.NET MVC 2 includes a client validation library and adapter that supports the DataAnnotations namespace validation attributes noted earlier.</span></span> <span data-ttu-id="cfe12-199">提供程序类还允许您通过编写处理 JSON 数据并调入到备用库的适配器来使用其他客户端验证库。</span><span class="sxs-lookup"><span data-stu-id="cfe12-199">The provider class also enables you to use other client-validation libraries by writing an adapter that processes the JSON data and calls into the alternate library.</span></span>

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  <span data-ttu-id="cfe12-200">Visual Studio 2010 的新代码段</span><span class="sxs-lookup"><span data-stu-id="cfe12-200">New Code Snippets for Visual Studio 2010</span></span>

<span data-ttu-id="cfe12-201">随 Visual Studio 2010 一起安装了一组适用于 ASP.NET MVC 2 的 HTML 代码段。</span><span class="sxs-lookup"><span data-stu-id="cfe12-201">A set of HTML code snippets for ASP.NET MVC 2 is installed with Visual Studio 2010.</span></span> <span data-ttu-id="cfe12-202">若要查看这些代码段的列表，请在 "工具" 菜单中选择 "代码片段管理器"。</span><span class="sxs-lookup"><span data-stu-id="cfe12-202">To view a list of these snippets, in the Tools menu, select Code Snippets Manager.</span></span> <span data-ttu-id="cfe12-203">对于 "语言"，选择 "HTML"，对于 "位置"，选择 "ASP.NET MVC 2"。</span><span class="sxs-lookup"><span data-stu-id="cfe12-203">For the language, select HTML, and for location, select ASP.NET MVC 2.</span></span> <span data-ttu-id="cfe12-204">有关如何使用代码片段的详细信息，请参阅 Visual Studio 文档。</span><span class="sxs-lookup"><span data-stu-id="cfe12-204">For more information about how to use code snippets, see the Visual Studio documentation.</span></span>

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  <span data-ttu-id="cfe12-205">新建 RequireHttpsAttribute 操作筛选器</span><span class="sxs-lookup"><span data-stu-id="cfe12-205">New RequireHttpsAttribute Action Filter</span></span>

<span data-ttu-id="cfe12-206">ASP.NET MVC 2 包含可应用于操作方法和控制器的新 RequireHttpsAttribute 类。</span><span class="sxs-lookup"><span data-stu-id="cfe12-206">ASP.NET MVC 2 includes a new RequireHttpsAttribute class that can be applied to action methods and controllers.</span></span> <span data-ttu-id="cfe12-207">默认情况下，筛选器会将非 SSL (HTTP) 请求重定向到启用 SSL 的 (HTTPS) 等效项。</span><span class="sxs-lookup"><span data-stu-id="cfe12-207">By default, the filter redirects a non-SSL (HTTP) request to the SSL-enabled (HTTPS) equivalent.</span></span>

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  <span data-ttu-id="cfe12-208">重写 HTTP 方法谓词</span><span class="sxs-lookup"><span data-stu-id="cfe12-208">Overriding the HTTP Method Verb</span></span>

<span data-ttu-id="cfe12-209">使用 REST 体系结构样式构建网站时，会使用 HTTP 谓词来确定要对资源执行的操作。</span><span class="sxs-lookup"><span data-stu-id="cfe12-209">When you build a Web site by using the REST architectural style, HTTP verbs are used to determine which action to perform for a resource.</span></span> <span data-ttu-id="cfe12-210">REST 要求应用程序支持各种公共 HTTP 谓词，包括 GET、PUT、POST 和 DELETE。</span><span class="sxs-lookup"><span data-stu-id="cfe12-210">REST requires that applications support the full range of common HTTP verbs, including GET, PUT, POST, and DELETE.</span></span>

<span data-ttu-id="cfe12-211">ASP.NET MVC 2 包含可应用于操作方法的新属性和该功能压缩语法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-211">ASP.NET MVC 2 includes new attributes that you can apply to action methods and that feature compact syntax.</span></span> <span data-ttu-id="cfe12-212">通过这些属性，ASP.NET MVC 可以根据 HTTP 谓词选择操作方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-212">These attributes enable ASP.NET MVC to select an action method based on the HTTP verb.</span></span> <span data-ttu-id="cfe12-213">在下面的示例中，POST 请求将调用第一个操作方法，PUT 请求将调用第二个操作方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-213">In the following example, a POST request will call the first action method and a PUT request will call the second action method.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

<span data-ttu-id="cfe12-214">在 ASP.NET MVC 的早期版本中，这些操作方法需要更详细的语法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-214">In earlier versions of ASP.NET MVC, these action methods required more verbose syntax, as shown in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

<span data-ttu-id="cfe12-215">由于浏览器仅支持 GET 和 POST HTTP 谓词，因此不能发布到需要不同谓词的操作。</span><span class="sxs-lookup"><span data-stu-id="cfe12-215">Because browsers support only the GET and POST HTTP verbs, it is not possible to post to an action that requires a different verb.</span></span> <span data-ttu-id="cfe12-216">因此，不能以本机方式支持所有 RESTful 请求。</span><span class="sxs-lookup"><span data-stu-id="cfe12-216">Thus it is not possible to natively support all RESTful requests.</span></span>

<span data-ttu-id="cfe12-217">但是，若要在 POST 操作期间支持 RESTful 请求，ASP.NET MVC 2 引入了新的 HttpMethodOverride HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-217">However, to support RESTful requests during POST operations, ASP.NET MVC 2 introduces a new HttpMethodOverride HTML helper method.</span></span> <span data-ttu-id="cfe12-218">此方法将呈现隐藏的 input 元素，该元素导致窗体有效模拟任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-218">This method renders a hidden input element that causes the form to effectively emulate any HTTP method.</span></span> <span data-ttu-id="cfe12-219">例如，通过使用 HttpMethodOverride HTML 帮助器方法，你可以将窗体提交作为 PUT 或 DELETE 请求出现。</span><span class="sxs-lookup"><span data-stu-id="cfe12-219">For example, by using the HttpMethodOverride HTML helper method, you can have a form submission appear be a PUT or DELETE request.</span></span> <span data-ttu-id="cfe12-220">HttpMethodOverride 的行为会影响以下属性：</span><span class="sxs-lookup"><span data-stu-id="cfe12-220">The behavior of HttpMethodOverride affects the following attributes:</span></span>

- <span data-ttu-id="cfe12-221">HttpPostAttribute</span><span class="sxs-lookup"><span data-stu-id="cfe12-221">HttpPostAttribute</span></span>
- <span data-ttu-id="cfe12-222">HttpPutAttribute</span><span class="sxs-lookup"><span data-stu-id="cfe12-222">HttpPutAttribute</span></span>
- <span data-ttu-id="cfe12-223">HttpGetAttribute</span><span class="sxs-lookup"><span data-stu-id="cfe12-223">HttpGetAttribute</span></span>
- <span data-ttu-id="cfe12-224">HttpDeleteAttribute</span><span class="sxs-lookup"><span data-stu-id="cfe12-224">HttpDeleteAttribute</span></span>
- <span data-ttu-id="cfe12-225">AcceptVerbsAttribute</span><span class="sxs-lookup"><span data-stu-id="cfe12-225">AcceptVerbsAttribute</span></span>

<span data-ttu-id="cfe12-226">隐藏的 input 元素的名称为 X HTTP 方法重写，其值设置为要模拟的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="cfe12-226">The hidden input element has its name X-HTTP-Method-Override and its value set to the HTTP verb to emulate.</span></span> <span data-ttu-id="cfe12-227">还可以在 HTTP 标头中或在查询字符串值中指定替代值作为名称/值对。</span><span class="sxs-lookup"><span data-stu-id="cfe12-227">The override value can also be specified in an HTTP header or in a query string value as a name/value pair.</span></span>

<span data-ttu-id="cfe12-228">仅当实际请求是 POST 请求时，才可以使用该重写。</span><span class="sxs-lookup"><span data-stu-id="cfe12-228">The override can only be used when the real request is a POST request.</span></span> <span data-ttu-id="cfe12-229">对于使用其他任何 HTTP 谓词的请求，将忽略替代值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-229">The override value will be ignored for requests that use any other HTTP verb.</span></span>

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  <span data-ttu-id="cfe12-230">模板化帮助器的新 HiddenInputAttribute 类</span><span class="sxs-lookup"><span data-stu-id="cfe12-230">New HiddenInputAttribute Class for Templated Helpers</span></span>

<span data-ttu-id="cfe12-231">您可以将新的 HiddenInputAttribute 属性应用于模型属性，以指示在编辑器模板中显示模型时是否应呈现隐藏的 input 元素。</span><span class="sxs-lookup"><span data-stu-id="cfe12-231">You can apply the new HiddenInputAttribute attribute to a model property to indicate whether a hidden input element should be rendered when displaying the model in an editor template.</span></span> <span data-ttu-id="cfe12-232"> (属性设置 HiddenInput) 的隐式 UIHint 值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-232">(The attribute sets an implicit UIHint value of HiddenInput).</span></span> <span data-ttu-id="cfe12-233">利用属性的 DisplayValue 属性，您可以指定是否在编辑器和显示模式下显示值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-233">The attribute's DisplayValue property lets you specify whether the value is displayed in editor and display modes.</span></span> <span data-ttu-id="cfe12-234">如果将 DisplayValue 设置为 false，则不会显示任何内容，甚至是通常环绕字段的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="cfe12-234">When DisplayValue is set to false, nothing is displayed, not even the HTML markup that normally surrounds a field.</span></span> <span data-ttu-id="cfe12-235">DisplayValue 的默认值为 true。</span><span class="sxs-lookup"><span data-stu-id="cfe12-235">The default value for DisplayValue is true.</span></span>

<span data-ttu-id="cfe12-236">你可以在以下方案中使用 HiddenInputAttribute 属性：</span><span class="sxs-lookup"><span data-stu-id="cfe12-236">You might use HiddenInputAttribute attribute in the following scenarios:</span></span>

- <span data-ttu-id="cfe12-237">当视图允许用户编辑对象的 ID 并且需要显示值并提供隐藏输入元素（该元素包含旧 ID，以便将其传递回控制器）时，可以使用视图。</span><span class="sxs-lookup"><span data-stu-id="cfe12-237">When a view lets users edit the ID of an object and it is necessary to display the value as well as to provide a hidden input element that contains the old ID so that it can be passed back to the controller.</span></span>
- <span data-ttu-id="cfe12-238">当视图允许用户编辑绝不应显示的二进制属性时，如时间戳属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-238">When a view lets users edit a binary property that should never be displayed, such as a timestamp property.</span></span> <span data-ttu-id="cfe12-239">在这种情况下，不会显示值和周围的 HTML 标记 (如标签和值) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-239">In that case, the value and surrounding HTML markup (such as the label and value) are not displayed.</span></span>

<span data-ttu-id="cfe12-240">下面的示例演示如何使用 HiddenInputAttribute 类。</span><span class="sxs-lookup"><span data-stu-id="cfe12-240">The following example shows how to use the HiddenInputAttribute class.</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

<span data-ttu-id="cfe12-241">如果该特性设置为 true (或未) 指定参数，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="cfe12-241">When the attribute is set to true (or no parameter is specified), the following occurs:</span></span>

- <span data-ttu-id="cfe12-242">在显示模板中，将呈现一个标签，并向用户显示值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-242">In display templates, a label is rendered and the value is displayed to the user.</span></span>
- <span data-ttu-id="cfe12-243">在编辑器模板中，将呈现标签，并在隐藏的输入元素中呈现值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-243">In editor templates, a label is rendered and the value is rendered in a hidden input element.</span></span>

<span data-ttu-id="cfe12-244">当特性设置为 false 时，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="cfe12-244">When the attribute is set to false, the following occurs:</span></span>

- <span data-ttu-id="cfe12-245">在显示模板中，不会为该字段呈现任何内容。</span><span class="sxs-lookup"><span data-stu-id="cfe12-245">In display templates, nothing is rendered for that field.</span></span>
- <span data-ttu-id="cfe12-246">在编辑器模板中，不呈现标签，并且值在隐藏的输入元素中呈现。</span><span class="sxs-lookup"><span data-stu-id="cfe12-246">In editor templates, no label is rendered and the value is rendered in a hidden input element.</span></span>

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  <span data-ttu-id="cfe12-247">ValidationSummary Helper 方法可以显示模型级别错误</span><span class="sxs-lookup"><span data-stu-id="cfe12-247">Html.ValidationSummary Helper Method Can Display Model-Level Errors</span></span>

<span data-ttu-id="cfe12-248">ValidationSummary helper 方法只显示模型级错误，而不是始终显示所有验证错误。</span><span class="sxs-lookup"><span data-stu-id="cfe12-248">Instead of always displaying all validation errors, the Html.ValidationSummary helper method has a new option to display only model-level errors.</span></span> <span data-ttu-id="cfe12-249">这使得在验证摘要和特定于字段的错误中显示要显示在每个字段旁边的模型级错误。</span><span class="sxs-lookup"><span data-stu-id="cfe12-249">This enables model-level errors to be displayed in the validation summary and field-specific errors to be displayed next to each field.</span></span>

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  <span data-ttu-id="cfe12-250">Visual Studio 中的 T4 模板生成特定于 .NET Framework 目标版本的代码</span><span class="sxs-lookup"><span data-stu-id="cfe12-250">T4 Templates in Visual Studio Generate Code that is Specific to the Target Version of the .NET Framework</span></span>

<span data-ttu-id="cfe12-251">新属性可用于来自 ASP.NET MVC T4 主机的 T4 文件，该文件指定应用程序使用的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="cfe12-251">A new property is available to T4 files from the ASP.NET MVC T4 host that specifies the version of the .NET Framework that is used by the application.</span></span> <span data-ttu-id="cfe12-252">这使 T4 模板能够生成特定于 .NET Framework 版本的代码和标记。</span><span class="sxs-lookup"><span data-stu-id="cfe12-252">This enables T4 templates to generate code and markup that is specific to a version of the .NET Framework.</span></span> <span data-ttu-id="cfe12-253">在 Visual Studio 2008 中，值始终为 .NET 3.5。</span><span class="sxs-lookup"><span data-stu-id="cfe12-253">In Visual Studio 2008, the value is always .NET 3.5.</span></span> <span data-ttu-id="cfe12-254">在 Visual Studio 2010 中，此值为 .NET 3.5 或 .NET 4。</span><span class="sxs-lookup"><span data-stu-id="cfe12-254">In Visual Studio 2010, the value is either .NET 3.5 or .NET 4.</span></span>

## <a name="api-improvements"></a><a id="_TOC4"></a>  <span data-ttu-id="cfe12-255">API 改进</span><span class="sxs-lookup"><span data-stu-id="cfe12-255">API Improvements</span></span>

<span data-ttu-id="cfe12-256">本部分介绍对现有 ASP.NET MVC 类型和成员所做的更改。</span><span class="sxs-lookup"><span data-stu-id="cfe12-256">This section describes changes to existing ASP.NET MVC types and members.</span></span>

- <span data-ttu-id="cfe12-257">在 Controller 类中添加了受保护的虚拟 CreateActionInvoker 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-257">Added a protected virtual CreateActionInvoker method in the Controller class.</span></span> <span data-ttu-id="cfe12-258">此方法由控制器的 ActionInvoker 属性调用，如果尚未设置任何调用程序，则允许调用程序的迟缓实例化。</span><span class="sxs-lookup"><span data-stu-id="cfe12-258">This method is invoked by the ActionInvoker property of Controller and allows for lazy instantiation of the invoker if no invoker is already set.</span></span>
- <span data-ttu-id="cfe12-259">在 AuthorizeAttribute 类中添加了受保护的 virtual HandleUnauthorizedRequest 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-259">Added a protected virtual HandleUnauthorizedRequest method in the AuthorizeAttribute class.</span></span> <span data-ttu-id="cfe12-260">这将启用从 AuthorizeAttribute 派生的筛选器，以控制在授权失败时的行为。</span><span class="sxs-lookup"><span data-stu-id="cfe12-260">This enables filters that derive from AuthorizeAttribute to control the behavior when authorization fails.</span></span>
- <span data-ttu-id="cfe12-261">在 ValueProviderDictionary 类中添加了一个添加 (字符串键、对象值) 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-261">Added an Add(string key, object value) method in the ValueProviderDictionary class.</span></span> <span data-ttu-id="cfe12-262">这使你可以使用 ValueProviderDictionary 的字典初始值设定项语法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="cfe12-262">This enables you to use the dictionary initializer syntax for ValueProviderDictionary, as in the following example:</span></span>

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- <span data-ttu-id="cfe12-263">\_在 AjaxContext 类中添加了 get object 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-263">Added a get\_object method in the Sys.Mvc.AjaxContext class.</span></span> <span data-ttu-id="cfe12-264">这是一种与 get data 方法类似的 JavaScript 方法 \_ ，但如果响应的内容类型为 application/json，则 get 对象将 \_ 返回 json 对象。</span><span class="sxs-lookup"><span data-stu-id="cfe12-264">This is a JavaScript method that is similar to the get\_data method, but if the content type of the response is application/json, get\_object returns the JSON object.</span></span>
- <span data-ttu-id="cfe12-265">在 AuthorizationContext 类中添加了一个 ActionDescriptor 属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-265">Added an ActionDescriptor property in the AuthorizationContext class.</span></span>
- <span data-ttu-id="cfe12-266">添加了 UrlParameter 标记，可用于在窗体发布时绑定到包含 ID 属性的模型时解决问题。</span><span class="sxs-lookup"><span data-stu-id="cfe12-266">Added a UrlParameter.Optional token that can be used to work around problems when binding to a model that contains an ID property when the property is absent in a form post.</span></span> <span data-ttu-id="cfe12-267">有关更多详细信息，请参阅 Phil Haack 的博客上的 [ASP.NET MVC 2 可选 URL 参数](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) 条目。</span><span class="sxs-lookup"><span data-stu-id="cfe12-267">For more detail, see the entry [ASP.NET MVC 2 Optional URL Parameters](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) on Phil Haack's blog.</span></span>

## <a name="breaking-changes"></a><a id="_TOC5"></a>  <span data-ttu-id="cfe12-268">重大更改</span><span class="sxs-lookup"><span data-stu-id="cfe12-268">Breaking Changes</span></span>

<span data-ttu-id="cfe12-269">在现有的 ASP.NET MVC 1.0 应用程序中，以下更改可能会导致错误。</span><span class="sxs-lookup"><span data-stu-id="cfe12-269">The following changes might cause errors in existing ASP.NET MVC 1.0 applications.</span></span>

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a><span data-ttu-id="cfe12-270">用于实现 IDataErrorInfo 的类的属性验证行为更改</span><span class="sxs-lookup"><span data-stu-id="cfe12-270">Change in property validation behavior for classes that implement IDataErrorInfo</span></span>

<span data-ttu-id="cfe12-271">对于使用 IDataErrorInfo 执行验证的模型对象，无论是否设置了新值，都会验证每个属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-271">For model objects that use IDataErrorInfo to perform validation, every property is validated, regardless of whether a new value was set.</span></span> <span data-ttu-id="cfe12-272">在 ASP.NET MVC 1.0 中，只验证具有新值集的属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-272">In ASP.NET MVC 1.0, only properties that had new values set were validated.</span></span> <span data-ttu-id="cfe12-273">在 ASP.NET MVC 2 中，仅当所有属性验证程序都成功时，才会调用 IDataErrorInfo 的 Error 属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-273">In ASP.NET MVC 2, the Error property of IDataErrorInfo is called only if all the property validators were successful.</span></span>

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a><span data-ttu-id="cfe12-274">安装程序中的 IIS 脚本映射脚本不再可用</span><span class="sxs-lookup"><span data-stu-id="cfe12-274">IIS script mapping script is no longer available in the installer</span></span>

<span data-ttu-id="cfe12-275">IIS 脚本映射脚本是一个命令行脚本，用于在经典模式下配置 IIS 6 和 IIS 7 的脚本映射。</span><span class="sxs-lookup"><span data-stu-id="cfe12-275">The IIS script-mapping script is a command-line script that is used to configure script maps for IIS 6 and for IIS 7 in Classic mode.</span></span> <span data-ttu-id="cfe12-276">如果使用 Visual Studio 开发服务器或者使用集成模式下的 IIS 7，则不需要脚本映射脚本。</span><span class="sxs-lookup"><span data-stu-id="cfe12-276">The script-mapping script is not needed if you use the Visual Studio Development Server or if you use IIS 7 in Integrated mode.</span></span> <span data-ttu-id="cfe12-277">在 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)上，这些脚本可作为单独的不受支持的下载。</span><span class="sxs-lookup"><span data-stu-id="cfe12-277">The scripts are available as a separate unsupported download on the [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a><span data-ttu-id="cfe12-278">MVC 先期中的替代 helper 方法不再可用</span><span class="sxs-lookup"><span data-stu-id="cfe12-278">The Html.Substitute helper method in MVC Futures is no longer available</span></span>

<span data-ttu-id="cfe12-279">由于 MVC 视图引擎的呈现行为发生了变化，因此，替代 helper 方法不起作用，已被删除。</span><span class="sxs-lookup"><span data-stu-id="cfe12-279">Due to changes in the rendering behavior of MVC view engines, the Html.Substitute helper method does not work and has been removed.</span></span>

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a><span data-ttu-id="cfe12-280">Ivalueprovider 必需接口取代了 IDictionary 的所有使用</span><span class="sxs-lookup"><span data-stu-id="cfe12-280">The IValueProvider interface replaces all uses of IDictionary</span></span>

<span data-ttu-id="cfe12-281">在 MVC 1.0 中接受的 IDictionary 的每个属性或方法参数现在都接受 Ivalueprovider 必需。</span><span class="sxs-lookup"><span data-stu-id="cfe12-281">Every property or method argument that accepted IDictionary in MVC 1.0 now accepts IValueProvider.</span></span> <span data-ttu-id="cfe12-282">此更改仅影响包括自定义值提供程序或自定义模型联编程序的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cfe12-282">This change affects only applications that include custom value providers or custom model binders.</span></span> <span data-ttu-id="cfe12-283">受此更改影响的属性和方法的示例包括以下各项：</span><span class="sxs-lookup"><span data-stu-id="cfe12-283">Examples of properties and methods that are affected by this change include the following:</span></span>

- <span data-ttu-id="cfe12-284">ControllerBase 和 ModelBindingContext 类的 ValueProvider 属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-284">The ValueProvider property of the ControllerBase and ModelBindingContext classes.</span></span>
- <span data-ttu-id="cfe12-285">控制器类的 TryUpdateModel 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-285">The TryUpdateModel methods of the Controller class.</span></span>

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a><span data-ttu-id="cfe12-286">在 web.config 文件中添加了新的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="cfe12-286">New CSS classes were added in the Site.css file</span></span>

<span data-ttu-id="cfe12-287">ASP.NET MVC 项目模板中的 web.config 文件已更新，包括验证功能使用的新样式和模板化帮助器。</span><span class="sxs-lookup"><span data-stu-id="cfe12-287">The Site.css file in the ASP.NET MVC project templates has been updated to include new styles used by the validation functionality and by the templated helpers.</span></span>

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a><span data-ttu-id="cfe12-288">助手现在返回 MvcHtmlString 对象</span><span class="sxs-lookup"><span data-stu-id="cfe12-288">Helpers now return an MvcHtmlString object</span></span>

<span data-ttu-id="cfe12-289">为了充分利用 ASP.NET 4 中的新 HTML 编码表达式语法，HTML 帮助器的返回类型现在为 MvcHtmlString 而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="cfe12-289">In order to take advantage of the new HTML-encoding expression syntax in ASP.NET 4, the return type for HTML helpers is now MvcHtmlString instead of a string.</span></span> <span data-ttu-id="cfe12-290">如果你使用 ASP.NET MVC 2 和 ASP.NET 3.5 上的新帮助器，你将无法利用 HTML 编码语法;只有在运行 ASP.NET 4 上的 ASP.NET MVC 2 时，新语法才可用。</span><span class="sxs-lookup"><span data-stu-id="cfe12-290">If you use ASP.NET MVC 2 and the new helpers on ASP.NET 3.5, you will not be able to take advantage of the HTML-encoding syntax; the new syntax is available only when you run ASP.NET MVC 2 on ASP.NET 4.</span></span>

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a><span data-ttu-id="cfe12-291">JsonResult 现在仅响应 HTTP POST 请求</span><span class="sxs-lookup"><span data-stu-id="cfe12-291">JsonResult now responds only to HTTP POST requests</span></span>

<span data-ttu-id="cfe12-292">为了缓解可能泄露信息的 JSON 劫持攻击，默认情况下，JsonResult 类现在仅响应 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="cfe12-292">In order to mitigate JSON hijacking attacks that have the potential for information disclosure, by default, the JsonResult class now responds only to HTTP POST requests.</span></span> <span data-ttu-id="cfe12-293">对于返回 JsonResult 对象的操作方法，Ajax GET 调用应改为使用 POST。</span><span class="sxs-lookup"><span data-stu-id="cfe12-293">Ajax GET calls to action methods that return a JsonResult object should be changed to use POST instead.</span></span> <span data-ttu-id="cfe12-294">如有必要，可以通过设置 JsonResult 的新 JsonRequestBehavior 属性来重写此行为。</span><span class="sxs-lookup"><span data-stu-id="cfe12-294">If necessary, you can override this behavior by setting the new JsonRequestBehavior property of JsonResult.</span></span> <span data-ttu-id="cfe12-295">有关潜在攻击的详细信息，请参阅博客文章 Phil Haack 的博客上的 [JSON 劫持](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="cfe12-295">For more information about the potential exploit, see the blog post [JSON Hijacking](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) on Phil Haack's blog.</span></span>

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a><span data-ttu-id="cfe12-296">ModelBindingContext 上的模型和 ModelType 属性资源库已过时</span><span class="sxs-lookup"><span data-stu-id="cfe12-296">Model and ModelType property setters on ModelBindingContext are obsolete</span></span>

<span data-ttu-id="cfe12-297">新的可设置 ModelMetadata 属性已添加到 ModelBindingContext 类。</span><span class="sxs-lookup"><span data-stu-id="cfe12-297">A new settable ModelMetadata property has been added to the ModelBindingContext class.</span></span> <span data-ttu-id="cfe12-298">新属性将封装模型和 ModelType 属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-298">The new property encapsulates both the Model and the ModelType properties.</span></span> <span data-ttu-id="cfe12-299">尽管 Model 和 ModelType 属性已过时，但对于向后兼容性，属性 getter 仍有效;它们委托给 ModelMetadata 属性以检索值。</span><span class="sxs-lookup"><span data-stu-id="cfe12-299">Although the Model and ModelType properties are obsolete, for backward compatibility the property getters still work; they delegate to the ModelMetadata property to retrieve the value.</span></span>

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a><span data-ttu-id="cfe12-300">对 DefaultControllerFactory 类的更改将从其派生的自定义控制器工厂中断</span><span class="sxs-lookup"><span data-stu-id="cfe12-300">Changes to the DefaultControllerFactory class break custom controller factories that derive from it</span></span>

<span data-ttu-id="cfe12-301">DefaultControllerFactory 类是通过删除 RequestContext 属性修复的。</span><span class="sxs-lookup"><span data-stu-id="cfe12-301">The DefaultControllerFactory class was fixed by removing the RequestContext property.</span></span> <span data-ttu-id="cfe12-302">为替代此属性，请求上下文实例会传递到受保护的虚拟 GetControllerInstance 和 GetControllerType 方法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-302">In place of this property, the request context instance is passed to the protected virtual GetControllerInstance and GetControllerType methods.</span></span> <span data-ttu-id="cfe12-303">此更改会影响派生自 DefaultControllerFactory 的自定义控制器工厂。</span><span class="sxs-lookup"><span data-stu-id="cfe12-303">This change affects custom controller factories that derive from DefaultControllerFactory.</span></span>

<span data-ttu-id="cfe12-304">自定义控制器工厂通常用于提供 ASP.NET MVC 应用程序的依赖项注入。</span><span class="sxs-lookup"><span data-stu-id="cfe12-304">Custom controller factories are often used to provide dependency injection for ASP.NET MVC applications.</span></span> <span data-ttu-id="cfe12-305">若要更新自定义控制器工厂以支持 ASP.NET MVC 2，请更改方法签名或签名以匹配新的签名，并使用请求上下文参数而不是属性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-305">To update the custom controller factories to support ASP.NET MVC 2, change the method signature or signatures to match the new signatures, and use the request context parameter instead of the property.</span></span>

#### <a name="area-is-a-now-a-reserved-route-value-key"></a><span data-ttu-id="cfe12-306">"Area" 是一个保留的路由值键</span><span class="sxs-lookup"><span data-stu-id="cfe12-306">"Area" is a now a reserved route-value key</span></span>

<span data-ttu-id="cfe12-307">路由值中的字符串 "area" 现在在 ASP.NET MVC 中具有特殊含义，其方式与 "控制器" 和 "操作" 的操作方式相同。</span><span class="sxs-lookup"><span data-stu-id="cfe12-307">The string "area" in Route values now has special meaning in ASP.NET MVC, in the same way that "controller" and "action" do.</span></span> <span data-ttu-id="cfe12-308">其中一个含义是，如果使用包含 "area" 的路由值字典提供 HTML 帮助器，帮助程序将不再在查询字符串中追加 "area"。</span><span class="sxs-lookup"><span data-stu-id="cfe12-308">One implication is that if HTML helpers are supplied with a route-value dictionary containing "area", the helpers will no longer append "area" in the query string.</span></span>

<span data-ttu-id="cfe12-309">如果使用的是 "区域" 功能，请确保不要将 {area} 用作路由 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="cfe12-309">If you are using the Areas feature, make sure to not use {area} as part of your route URL.</span></span>

## <a name="disclaimer"></a><a id="_TOC6"></a>  <span data-ttu-id="cfe12-310">否认</span><span class="sxs-lookup"><span data-stu-id="cfe12-310">Disclaimer</span></span>

<span data-ttu-id="cfe12-311">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="cfe12-311">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="cfe12-312">本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。</span><span class="sxs-lookup"><span data-stu-id="cfe12-312">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="cfe12-313">由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。</span><span class="sxs-lookup"><span data-stu-id="cfe12-313">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="cfe12-314">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="cfe12-314">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="cfe12-315">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="cfe12-315">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="cfe12-316">用户有责任遵守所有适用的版权法/著作权法。</span><span class="sxs-lookup"><span data-stu-id="cfe12-316">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="cfe12-317">在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。</span><span class="sxs-lookup"><span data-stu-id="cfe12-317">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="cfe12-318">Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="cfe12-318">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="cfe12-319">除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。</span><span class="sxs-lookup"><span data-stu-id="cfe12-319">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="cfe12-320">除非另有说明，否则，本文档中提及的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件没有任何关联。</span><span class="sxs-lookup"><span data-stu-id="cfe12-320">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="cfe12-321">© 2010 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="cfe12-321">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="cfe12-322">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="cfe12-322">All rights reserved.</span></span>

<span data-ttu-id="cfe12-323">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="cfe12-323">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="cfe12-324">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="cfe12-324">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>

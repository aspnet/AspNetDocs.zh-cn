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
ms.openlocfilehash: 1a0a29241d8afecd295b11013b27621b21c9ed52
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162694"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2 的新增功能

> 本文档介绍 ASP.NET MVC 2 中引入的新功能和改进。 此文档还可供[下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)

[产品介绍](#_TOC1)   
[将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2](#_TOC2)   
[新功能](#_TOC3)   
[模板化帮助器](#_TOC3_1)   
[区域](#_TOC3_2)   
[支持异步控制器](#_TOC3_3)   
[在操作方法参数中对 DefaultValueAttribute 的支持](#_TOC3_4)   
[支持在模型联编程序中绑定二进制数据](#_TOC3_5)   
[ModelMetadata 和 ModelMetadataProvider 类](#_TOC3_6)   
[支持 DataAnnotations 属性](#_TOC3_7)   
[模型验证程序提供程序](#_TOC3_8)   
[客户端验证](#_TOC3_9)   
[Visual Studio 2010 的新代码段](#_TOC3_10)   
[新建 RequireHttpsAttribute 操作筛选器](#_TOC3_11)   
[重写 HTTP 方法谓词](#_TOC3_12)   
[模板化帮助器的新 HiddenInputAttribute 类](#_TOC3_13)   
[ValidationSummary Helper 方法可以显示模型级别错误](#_TOC3_14)   
[Visual Studio 中的 T4 模板生成特定于 .NET Framework](#_TOC3_15)[API 改进](#_TOC4)目标版本的代码  
[重大更改](#_TOC5)  
[免责声明](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>产品介绍

ASP.NET MVC 2 在 ASP.NET MVC 1.0 上构建，引入了大量的增强功能和功能，重点提高工作效率。 此版本与 ASP.NET MVC 1.0 兼容，因此，ASP.NET MVC 1.0 的所有知识、技能、代码和扩展仍适用。

有关 ASP.NET MVC 的详细信息，请访问以下资源：

- [MSDN 上的 ASP.NET MVC 文档](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC 网站](https://asp.net/mvc/)
- [ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>将 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2

ASP.NET MVC 2 可以与同一服务器上的 ASP.NET MVC 1.0 并行安装，这使应用程序开发人员可以灵活选择何时将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2。 有关如何升级的信息，请参阅将[ASP.NET mvc 1.0 应用程序升级到 ASP.NET mvc 2](https://go.microsoft.com/fwlink/?LinkID=185459)的文档。

## <a name="new-features"></a><a id="_TOC3"></a>新功能

本部分介绍了在 MVC 2 版本中引入的功能。

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>模板化帮助器

模板化帮助器允许您自动将用于编辑和显示的 HTML 元素与数据类型相关联。 例如，当视图中显示类型为 system.string 的数据时，可以自动呈现日期选取器 UI 元素。 这类似于字段模板在 ASP.NET 动态数据中的工作方式。 有关详细信息，请参阅 MSDN 网站上的[使用模板化帮助器显示数据](https://go.microsoft.com/fwlink/?LinkId=159062)。

### <a name="areas"></a><a id="_TOC3_2"></a>区域

使用区域可以将大型项目组织为多个较小的分区，以便管理大型 Web 应用程序的复杂性。  ( "area" ) 的每个部分通常代表一个大型网站的单独部分，并用于对相关的控制器和视图集进行分组。 有关详细信息，请参阅 MSDN 网站上的[演练：按区域组织 ASP.NET MVC 应用程序](https://go.microsoft.com/fwlink/?LinkId=158978)。

若要创建新区域，请在解决方案资源管理器中右键单击该项目，单击 "添加"，然后单击 "区域"。 此时将显示一个对话框，提示您输入区域名称。 输入区域名称后，Visual Studio 会向项目中添加一个新区域。

下图显示了项目的示例布局，其中包含两个区域：管理员和博客。

![](what-is-new-in-aspnet-mvc/_static/image1.png)

创建区域时，Visual Studio 会将从 AreaRegistration 派生的类添加到每个区域。 若要注册区域及其路由，需要此类，如下面的示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2 的默认项目模板在 global.asax 文件的代码中包含对 RegisterAllAreas 方法的调用。 此方法通过查找派生自 AreaRegistration 类的所有类型、实例化类型的实例，然后对实例调用 RegisterArea 方法来注册项目中的每个区域。 下面的示例演示如何执行此操作。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

如果未通过调用上下文来指定 RegisterArea 方法中的命名空间，则为。命名空间. Add 方法，默认情况下使用注册类的命名空间。

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>支持异步控制器

ASP.NET MVC 2 现在允许控制器异步处理请求。 这可以通过允许频繁调用阻止操作 (如网络请求) 的服务器而不是调用非阻塞对等项，从而提高性能。 有关详细信息，请参阅 MSDN 上的在[ASP.NET MVC 中使用异步控制器](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx)主题。

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>在操作方法参数中对 DefaultValueAttribute 的支持

System.componentmodel. DefaultValueAttribute 类允许将默认值提供给操作方法的参数参数。 例如，假设定义了以下默认路由：

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

还假定定义了以下控制器和操作方法：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

以下任何请求 Url 都将调用在前面的示例中定义的视图操作方法。

- /Article/View/123
- /Article/View/123？ page = 1 (与以前的请求有效) 
- /Article/View/123？页 = 2

如果没有 DefaultValueAttribute 属性，则前面的列表中的第一个 URL 将不起作用，因为页参数是不可以为 null 的值类型，其值尚未提供。

如果代码是用 Visual Basic 2010 或 Visual c # 2010 编写的，则可以使用可选参数，而不是 DefaultValueAttribute 属性，如以下示例中所示：

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>支持在模型联编程序中绑定二进制数据

Html 的隐藏帮助程序有两个新的重载，这些重载将二进制值编码为64编码的字符串：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

典型用途是在视图中嵌入对象的时间戳。 例如，你的应用程序可能包含以下 Product 对象：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

编辑窗体可以在窗体中呈现时间戳属性，如以下示例中所示：

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

此标记会将时间戳值为的隐藏输入元素呈现为以64编码的字符串，类似于以下示例：

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

此窗体可能会发布到具有类型为 Product 的参数的操作方法，如以下示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

在操作方法中，TimeStamp 属性会正确填充，因为已发布的64编码字符串将转换为字节数组。

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>ModelMetadata 和 ModelMetadataProvider 类

ModelMetadataProvider 类提供了一个抽象，用于获取视图中模型的元数据。 MVC 2 包含一个默认提供程序，该提供程序使 System.componentmodel. DataAnnotations 命名空间中的属性公开的元数据可用。 可以创建从其他数据存储（如数据库或 XML 文件）提供元数据的元数据提供程序。

ViewDataDictionary 类公开 ModelMetadata 对象，该对象包含 ModelMetadataProvider 类从模型中提取的元数据。 这使模板化帮助器可以使用此元数据，并相应地调整它们的输出。

有关详细信息，请参阅[ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx)和[ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx)类的文档。

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>支持 DataAnnotations 属性

当您绑定到某一模型以提供输入验证时，ASP.NET MVC 2 支持使用 RegexAttribute) 命名空间中定义的 RangeAttribute、有 requiredattribute、StringLengthAttribute 和 System.componentmodel 验证特性 (。

有关详细信息，请参阅 MSDN 网站上的[如何：使用 DataAnnotations 属性验证模型数据](https://go.microsoft.com/fwlink/?LinkId=159063)。 演示如何使用这些属性的示例项目可从下载 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) 。

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>模型验证程序提供程序

模型验证提供程序类表示为模型提供验证逻辑的抽象。 ASP.NET MVC 包含基于 System.componentmodel. DataAnnotations 命名空间中包含的验证属性的默认提供程序。 您还可以创建自己的验证提供程序，用于定义自定义验证规则以及验证规则到模型的自定义映射。 有关详细信息，请参阅[ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx)类的文档。

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>客户端验证

模型验证程序提供程序类将验证元数据以 JSON 序列化数据（可由客户端验证库使用）的形式公开给浏览器。 ASP.NET MVC 2 包括客户端验证库和支持前面提到的 DataAnnotations 命名空间验证特性的适配器。 提供程序类还允许您通过编写处理 JSON 数据并调入到备用库的适配器来使用其他客户端验证库。

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>Visual Studio 2010 的新代码段

随 Visual Studio 2010 一起安装了一组适用于 ASP.NET MVC 2 的 HTML 代码段。 若要查看这些代码段的列表，请在 "工具" 菜单中选择 "代码片段管理器"。 对于 "语言"，选择 "HTML"，对于 "位置"，选择 "ASP.NET MVC 2"。 有关如何使用代码片段的详细信息，请参阅 Visual Studio 文档。

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>新建 RequireHttpsAttribute 操作筛选器

ASP.NET MVC 2 包含可应用于操作方法和控制器的新 RequireHttpsAttribute 类。 默认情况下，筛选器会将非 SSL (HTTP) 请求重定向到启用 SSL 的 (HTTPS) 等效项。

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>重写 HTTP 方法谓词

使用 REST 体系结构样式构建网站时，会使用 HTTP 谓词来确定要对资源执行的操作。 REST 要求应用程序支持各种公共 HTTP 谓词，包括 GET、PUT、POST 和 DELETE。

ASP.NET MVC 2 包含可应用于操作方法的新属性和该功能压缩语法。 通过这些属性，ASP.NET MVC 可以根据 HTTP 谓词选择操作方法。 在下面的示例中，POST 请求将调用第一个操作方法，PUT 请求将调用第二个操作方法。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

在 ASP.NET MVC 的早期版本中，这些操作方法需要更详细的语法，如以下示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

由于浏览器仅支持 GET 和 POST HTTP 谓词，因此不能发布到需要不同谓词的操作。 因此，不能以本机方式支持所有 RESTful 请求。

但是，若要在 POST 操作期间支持 RESTful 请求，ASP.NET MVC 2 引入了新的 HttpMethodOverride HTML 帮助器方法。 此方法将呈现隐藏的 input 元素，该元素导致窗体有效模拟任何 HTTP 方法。 例如，通过使用 HttpMethodOverride HTML 帮助器方法，你可以将窗体提交作为 PUT 或 DELETE 请求出现。 HttpMethodOverride 的行为会影响以下属性：

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

隐藏的 input 元素的名称为 X HTTP 方法重写，其值设置为要模拟的 HTTP 谓词。 还可以在 HTTP 标头中或在查询字符串值中指定替代值作为名称/值对。

仅当实际请求是 POST 请求时，才可以使用该重写。 对于使用其他任何 HTTP 谓词的请求，将忽略替代值。

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>模板化帮助器的新 HiddenInputAttribute 类

您可以将新的 HiddenInputAttribute 属性应用于模型属性，以指示在编辑器模板中显示模型时是否应呈现隐藏的 input 元素。  (属性设置 HiddenInput) 的隐式 UIHint 值。 利用属性的 DisplayValue 属性，您可以指定是否在编辑器和显示模式下显示值。 如果将 DisplayValue 设置为 false，则不会显示任何内容，甚至是通常环绕字段的 HTML 标记。 DisplayValue 的默认值为 true。

你可以在以下方案中使用 HiddenInputAttribute 属性：

- 当视图允许用户编辑对象的 ID 并且需要显示值并提供隐藏输入元素（该元素包含旧 ID，以便将其传递回控制器）时，可以使用视图。
- 当视图允许用户编辑绝不应显示的二进制属性时，如时间戳属性。 在这种情况下，不会显示值和周围的 HTML 标记 (如标签和值) 。

下面的示例演示如何使用 HiddenInputAttribute 类。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

如果该特性设置为 true (或未) 指定参数，将发生以下情况：

- 在显示模板中，将呈现一个标签，并向用户显示值。
- 在编辑器模板中，将呈现标签，并在隐藏的输入元素中呈现值。

当特性设置为 false 时，将发生以下情况：

- 在显示模板中，不会为该字段呈现任何内容。
- 在编辑器模板中，不呈现标签，并且值在隐藏的输入元素中呈现。

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>ValidationSummary Helper 方法可以显示模型级别错误

ValidationSummary helper 方法只显示模型级错误，而不是始终显示所有验证错误。 这使得在验证摘要和特定于字段的错误中显示要显示在每个字段旁边的模型级错误。

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>Visual Studio 中的 T4 模板生成特定于 .NET Framework 目标版本的代码

新属性可用于来自 ASP.NET MVC T4 主机的 T4 文件，该文件指定应用程序使用的 .NET Framework 版本。 这使 T4 模板能够生成特定于 .NET Framework 版本的代码和标记。 在 Visual Studio 2008 中，值始终为 .NET 3.5。 在 Visual Studio 2010 中，此值为 .NET 3.5 或 .NET 4。

## <a name="api-improvements"></a><a id="_TOC4"></a>API 改进

本部分介绍对现有 ASP.NET MVC 类型和成员所做的更改。

- 在 Controller 类中添加了受保护的虚拟 CreateActionInvoker 方法。 此方法由控制器的 ActionInvoker 属性调用，如果尚未设置任何调用程序，则允许调用程序的迟缓实例化。
- 在 AuthorizeAttribute 类中添加了受保护的 virtual HandleUnauthorizedRequest 方法。 这将启用从 AuthorizeAttribute 派生的筛选器，以控制在授权失败时的行为。
- 在 ValueProviderDictionary 类中添加了一个添加 (字符串键、对象值) 方法。 这使你可以使用 ValueProviderDictionary 的字典初始值设定项语法，如以下示例中所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- \_在 AjaxContext 类中添加了 get object 方法。 这是一种与 get data 方法类似的 JavaScript 方法 \_ ，但如果响应的内容类型为 application/json，则 get 对象将 \_ 返回 json 对象。
- 在 AuthorizationContext 类中添加了一个 ActionDescriptor 属性。
- 添加了 UrlParameter 标记，可用于在窗体发布时绑定到包含 ID 属性的模型时解决问题。 有关更多详细信息，请参阅 Phil Haack 的博客上的[ASP.NET MVC 2 可选 URL 参数](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx)条目。

## <a name="breaking-changes"></a><a id="_TOC5"></a>重大更改

在现有的 ASP.NET MVC 1.0 应用程序中，以下更改可能会导致错误。

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>用于实现 IDataErrorInfo 的类的属性验证行为更改

对于使用 IDataErrorInfo 执行验证的模型对象，无论是否设置了新值，都会验证每个属性。 在 ASP.NET MVC 1.0 中，只验证具有新值集的属性。 在 ASP.NET MVC 2 中，仅当所有属性验证程序都成功时，才会调用 IDataErrorInfo 的 Error 属性。

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>安装程序中的 IIS 脚本映射脚本不再可用

IIS 脚本映射脚本是一个命令行脚本，用于在经典模式下配置 IIS 6 和 IIS 7 的脚本映射。 如果使用 Visual Studio 开发服务器或者使用集成模式下的 IIS 7，则不需要脚本映射脚本。 在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)上，这些脚本可作为单独的不受支持的下载。

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>MVC 先期中的替代 helper 方法不再可用

由于 MVC 视图引擎的呈现行为发生了变化，因此，替代 helper 方法不起作用，已被删除。

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>Ivalueprovider 必需接口取代了 IDictionary 的所有使用

在 MVC 1.0 中接受的 IDictionary 的每个属性或方法参数现在都接受 Ivalueprovider 必需。 此更改仅影响包括自定义值提供程序或自定义模型联编程序的应用程序。 受此更改影响的属性和方法的示例包括以下各项：

- ControllerBase 和 ModelBindingContext 类的 ValueProvider 属性。
- 控制器类的 TryUpdateModel 方法。

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>在 web.config 文件中添加了新的 CSS 类

ASP.NET MVC 项目模板中的 web.config 文件已更新，包括验证功能使用的新样式和模板化帮助器。

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>助手现在返回 MvcHtmlString 对象

为了充分利用 ASP.NET 4 中的新 HTML 编码表达式语法，HTML 帮助器的返回类型现在为 MvcHtmlString 而不是字符串。 如果你使用 ASP.NET MVC 2 和 ASP.NET 3.5 上的新帮助器，你将无法利用 HTML 编码语法;只有在运行 ASP.NET 4 上的 ASP.NET MVC 2 时，新语法才可用。

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult 现在仅响应 HTTP POST 请求

为了缓解可能泄露信息的 JSON 劫持攻击，默认情况下，JsonResult 类现在仅响应 HTTP POST 请求。 对于返回 JsonResult 对象的操作方法，Ajax GET 调用应改为使用 POST。 如有必要，可以通过设置 JsonResult 的新 JsonRequestBehavior 属性来重写此行为。 有关潜在攻击的详细信息，请参阅博客文章 Phil Haack 的博客上的[JSON 劫持](http://haacked.com/archive/2009/06/25/json-hijacking.aspx)。

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>ModelBindingContext 上的模型和 ModelType 属性资源库已过时

新的可设置 ModelMetadata 属性已添加到 ModelBindingContext 类。 新属性将封装模型和 ModelType 属性。 尽管 Model 和 ModelType 属性已过时，但对于向后兼容性，属性 getter 仍有效;它们委托给 ModelMetadata 属性以检索值。

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>对 DefaultControllerFactory 类的更改将从其派生的自定义控制器工厂中断

DefaultControllerFactory 类是通过删除 RequestContext 属性修复的。 为替代此属性，请求上下文实例会传递到受保护的虚拟 GetControllerInstance 和 GetControllerType 方法。 此更改会影响派生自 DefaultControllerFactory 的自定义控制器工厂。

自定义控制器工厂通常用于提供 ASP.NET MVC 应用程序的依赖项注入。 若要更新自定义控制器工厂以支持 ASP.NET MVC 2，请更改方法签名或签名以匹配新的签名，并使用请求上下文参数而不是属性。

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Area" 是一个保留的路由值键

路由值中的字符串 "area" 现在在 ASP.NET MVC 中具有特殊含义，其方式与 "控制器" 和 "操作" 的操作方式相同。 其中一个含义是，如果使用包含 "area" 的路由值字典提供 HTML 帮助器，帮助程序将不再在查询字符串中追加 "area"。

如果使用的是 "区域" 功能，请确保不要将 {area} 用作路由 URL 的一部分。

## <a name="disclaimer"></a><a id="_TOC6"></a>否认

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。 由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

用户有责任遵守所有适用的版权法/著作权法。 在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。

Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。

除非另有说明，否则，本文档中提及的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件没有任何关联。

© 2010 Microsoft Corporation。 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。

---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: （包括 2011 年 4 月工具更新）ASP.NET MVC 3 是一个框架，用于使用成熟的设计模式构建可扩展的、基于标准的 Web 应用程序...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675141"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *（包括 2011 年 4 月工具更新）*
> 
> ASP.NET MVC 3 是一个框架，用于使用成熟的设计模式以及 ASP.NET 和 .NET 框架的强大功能构建可扩展的、基于标准的 Web 应用程序。
> 
> 它与mVC ASP.NET并行安装，所以立即开始使用它！
> 
> 在此处下载[安装程序](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>热门功能

- 集成脚手架系统可通过 NuGet 进行扩展
- 启用 HTML 5 的项目模板
- 表现性视图，包括新的剃刀视图引擎
- 具有依赖项注入和全局操作筛选器的强大挂钩
- 具有不显眼的 JavaScript、jQuery 验证和 JSON 绑定的丰富 JavaScript 支持
- *阅读[下面的](#overview)完整功能列表*

## <a name="top-links"></a>热门链接

ASP.NET MVC 3 中的新增功能

- 菲尔·哈克[：ASP.NET MVC 3 发布](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- 斯科特·汉塞尔曼[：ASP.NET MVC3、WebMatrix、NuGet、IIS 快递和果园发布 - 微软 1 月 Web 发布上下文](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- 斯科特·古斯里：[宣布发布ASP.NET MVC 3，IIS 快递，SQL CE 4，网络农场框架，果园，WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 的发行说明](../whitepapers/mvc3-release-notes.md)

安装和帮助

- 使用 Web 平台安装程序安装ASP.NET MVC [3（建议）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- 使用[安装程序可执行文件](https://go.microsoft.com/fwlink/?LinkID=208140)安装ASP.NET MVC 3
- 安装[ASP.NET MVC 3 用于可视化工作室 11 开发人员预览](https://go.microsoft.com/fwlink/?LinkID=208140)
- 阅读[简介以ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- 在[论坛](https://forums.asp.net/1146.aspx)中获取有关 MVC 3 ASP.NET帮助和讨论

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview（ASP.NET MVC 3 概述）

ASP.NET MVC 3 建立在 ASP.NET MVC 1 和 2 的基础上，增加了既简化了代码又允许更深度扩展性的伟大功能。 本主题概述了此版本中包括的许多新功能，这些功能分为以下各节：

- [通过 Mvc Scaffold 集成扩展脚手架](#BM_MvcScaffolding)
- [启用 HTML 5 的项目模板](#BM_HTML5)
- [剃刀视图引擎](#BM_TheRazorViewEngine)
- [支持多视图引擎](#BM_Support_for_Multiple_View_Engines)
- [控制器改进](#BM_Controller_Improvements)
- [JavaScript 和 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [模型验证改进](#BM_Model_Validation_Improvements)
- [依赖项注入改进](#BM_Dependency_Injection_Improvements)
- [其他新功能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>通过 Mvc Scaffold 集成扩展脚手架

新的 Scaffoldsing 系统使您能够更轻松地拿起并开始高效使用，如果您是框架的完全新，并且如果您经验丰富且已经知道正在做什么，则自动执行常见开发任务。

这是由新的NuGet*脚手架*包支持，称为**Mvc脚手架**。 许多软件技术使用术语"Scaffolding"表示"快速生成软件的基本大纲，然后您可以编辑和自定义"。 我们为ASP.NET MVC 创建的脚手架包在几个方案中非常有用：

- **如果你第一次学习ASP.NETMVC，** 因为它为您提供了一种快速的方式来获得一些有用的工作代码，然后你可以根据您的需要进行编辑和调整。 它为您从看着空白页面的创伤中拯救，并且不知道从哪里开始！
- **如果您对 MVC ASP.NET非常了解，并且正在探索一些新的附加技术**，如对象关系映射器、视图引擎、测试库等，因为该技术的创建者可能也为它创建了一个基架包。
- **如果工作涉及重复创建类似类或某种文件**，因为您可以创建自定义基架，以输出测试夹具、部署脚本或其他任何需要。 团队中的每个人都可以使用自定义脚手架。

MvcScaffoldsing 中的其他功能包括：

- 支持 C# 和 VB 项目
- 支持剃刀和 ASPX 视图引擎
- 支持将脚手架放入ASP.NET MVC 区域并使用自定义视图布局/主机
- 您可以通过编辑 T4 模板轻松自定义输出
- 您可以使用自定义 PowerShell 逻辑和自定义 T4 模板添加全新的基架。 这些参数（以及您提供给它们的任何自定义参数）会自动显示在控制台选项卡完成列表中。
- 您可以获取包含不同技术的其他基架支架的 NuGet 包（例如，现在 LINQ 到 SQL 都有一个概念验证包），并将它们混合并匹配在一起

ASP.NET MVC 3 工具更新包括针对此基架系统的巨大 Visual Studio 支持，例如：

- 添加控制器对话框现在支持创建、读取、更新和删除控制器操作和相应视图的完整自动基架。 默认情况下，此基架数据访问代码使用 EF 代码优先。
- 添加控制器对话框支持通过 NuGet 包（如*MvcScaffold）**进行扩展基架*。 这允许将自定义基架插入对话框中，这样，如果您倾向于的话，您可以为其他数据访问技术（如 NHibernate）创建基架，甚至使用 ODBCDirect 的 JET！

有关 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：

- 史蒂夫·桑德森的系列帖子，包括： 

    1. [简介： 使用 MvcScaffoldss 封装，ASP.NET MVC 3 项目脚手架](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [标准用法：典型用例和选项](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一对多关系](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [脚手架操作和单元测试](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [覆盖 T4 模板](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [这篇文章：创建自定义脚手架](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- 斯科特·汉塞尔曼的帖子从他的PDC 2010会话[建立博客与微软"未命名的网络爱包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 项目模板

"新项目"对话框包括一个复选框，该复选框启用 HTML 5 版本的项目模板。 这些模板利用 Modernizr 1.7 在低级浏览器中为 HTML 5 和 CSS 3 提供兼容性支持。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>剃刀视图引擎

ASP.NET MVC 3 附带了名为 Razor 的新视图引擎，具有以下优点：

- 剃刀语法简洁简洁，需要最少的击键次数。
- Razor 易于学习，部分原因在于它基于现有语言（如 C# 和 Visual Basic）。
- 可视化工作室包括用于 Razor 语法的 IntelliSense 和代码着色。
- Razor 视图可以进行单元测试，而无需运行应用程序或启动 Web 服务器。

一些新的 Razor 功能包括：

- `@model`用于指定传递给视图的类型的语法。
- `@* *@`注释语法。
- 为整个站点指定默认值（如`layoutpage`） 一次的能力。
- 显示`Html.Raw`文本而不进行 HTML 编码的方法。
- 支持在多个视图之间共享代码（*\_视图 start.cshtml*或*\_viewstart.vbhtml*文件）。

Razor 还包括新的 HTML 帮助器，如下所示：

- `Chart`. 渲染图表，提供与 ASP.NET 4 中的图表控件相同的要素。
- `WebGrid`. 渲染数据网格，完成分页和排序功能。
- `Crypto`. 使用哈希算法创建正确加盐和哈希密码。
- `WebImage`. 渲染图像。
- `WebMail`. 发送电子邮件。

有关 Razor 的详细信息，请参阅以下资源：

- [斯科特·古斯里的博客文章介绍剃刀](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [斯科特·古斯里的博客文章介绍关键字@model](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [斯科特·古斯里的博客文章介绍剃刀布局](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [剃刀 API 快速参考](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>支持多视图引擎

ASP.NET MVC 3 中的 **"添加视图"** 对话框允许您选择要使用的视图引擎，而 **"新项目**"对话框允许您为项目指定默认视图引擎。 您可以选择 Web 窗体视图引擎 （ASPX）、Razor 或开源视图引擎（如[Spark、NHaml](https://code.google.com/p/nhaml/)或[Spark](http://sparkviewengine.com/)[NDjango）。](http://ndjango.org/)

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>控制器改进

### <a name="global-action-filters"></a>全局操作筛选器

有时，您希望在操作方法运行之前或操作方法运行之前执行逻辑。 为了支持这一点，ASP.NET MVC 2 提供了操作筛选器。 操作筛选器是自定义属性，提供声明性方法，将操作前和操作后行为添加到特定的控制器操作方法。 但是，在某些情况下，您可能希望指定适用于所有操作方法的操作前或行动后行为。 MVC 3 允许您通过将全局筛选器添加到`GlobalFilters`集合来指定全局筛选器。 有关全局操作筛选器的详细信息，请参阅以下资源：

- [斯科特·古斯里在MVC 3预览的博客](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC 中的筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新的"视图袋"属性

MVC 2 控制器`ViewData`支持一个属性，该属性使您能够使用后期绑定字典 API 将数据传递到视图模板。 在 MVC 3 中，还可以对属性使用更简单`ViewBag`的语法来实现相同的目的。 例如，可以写入 而不是`ViewData["Message"]="text"`写入`ViewBag.Message="text"`。 不需要定义任何强类型类来使用 属性`ViewBag`。 因为它是动态属性，因此只需获取或设置属性，它将在运行时动态解析它们。 在内部`ViewBag`，属性在`ViewData`字典中存储为名称/值对。 （注意：在大多数预发行版本的 MVC 3 中，`ViewBag`属性被命名为属性`ViewModel`。

### <a name="new-actionresult-types"></a>新的"操作结果"类型

以下`ActionResult`类型和相应的帮助器方法在 MVC 3 中是新的或增强的：

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 将 404 HTTP 状态代码返回给客户端。
- [重定向结果](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 返回临时重定向 （HTTP 302 状态代码） 或永久重定向 （HTTP 301 状态代码），具体取决于布尔参数。 结合此更改[，Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在有三种执行永久重定向的方法：、`RedirectPermanent``RedirectToRoutePermanent`和`RedirectToActionPermanent`。 这些方法返回`RedirectResult`属性`Permanent`设置为`true`的 实例。
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). 返回用户指定的 HTTP 状态代码。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 和 Ajax 改进

默认情况下，MVC 3 中的 Ajax 和验证帮助程序使用不显眼的 JavaScript 方法。 不显眼的 JavaScript 避免将内联 JavaScript 注入 HTML。 这使得您的 HTML 更小且不太混乱，并且更易于交换或自定义 JavaScript 库。 默认情况下，MVC `jQueryValidate` 3 中的验证帮助程序也使用该插件。 如果需要 MVC 2 行为，可以使用*Web.config*文件设置禁用不显眼的 JavaScript。 有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：

- [维基百科网站上不显眼的JavaScript的基本介绍](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [布拉德·威尔逊的《不显眼的JavaScript》帖子](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [布拉德·威尔逊的《不显眼的Java脚本验证帖》](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [使用 Razor 和不显眼的 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET网站上的教程）
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>默认情况下启用客户端验证

在早期版本的 MVC 中，需要从视图中显式调用`Html.EnableClientValidation`方法，以便启用客户端验证。 在 MVC 3 中，这不再需要，因为默认情况下启用客户端验证。 （您可以使用*Web.config*文件中的设置禁用此功能。

为了使客户端验证正常工作，您仍然需要引用站点中相应的 jQuery 和 jQuery 验证库。 您可以在自己的服务器上托管这些库，也可以从内容交付网络 （CDN）（如 Microsoft 或 Google 的 CDN）中引用它们。

### <a name="remote-validator"></a>远程验证器

ASP.NET MVC 3 支持新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)类，使您能够利用 jQuery 验证插件的远程验证器支持。 这使客户端验证库能够自动调用您在服务器上定义的自定义方法，以便执行只能执行服务器端的验证逻辑。

`Remote`在下面的示例中，该属性指定客户端验证将调用`UserNameAvailable``UsersController`类上命名的操作以验证该`UserName`字段。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

下面的示例显示了相应的控制器。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

有关如何使用`Remote`该属性的详细信息，请参阅如何：在 MSDN 库中[ASP.NET MVC 中实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。

### <a name="json-binding-support"></a>JSON 绑定支持

ASP.NET MVC 3 包括内置的 JSON 绑定支持，使操作方法能够接收 JSON 编码的数据，并将其模型绑定到操作方法参数。 此功能在涉及客户端模板和数据绑定的方案中非常有用。 （客户端模板使您能够使用在客户端上执行的模板格式化和显示单个数据项或数据项集。MVC 3 使您能够轻松地将客户端模板与发送和接收 JSON 数据的服务器上的操作方法连接。 有关 JSON 绑定支持的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览博客文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript 和 AJAX 改进**部分。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>模型验证改进

### <a name="dataannotations-metadata-attributes"></a>"数据注释"元数据属性

ASP.NET MVC `DataAnnotations` 3 支持元数据`DisplayAttribute`属性，如 。

### <a name="validationattribute-class"></a>"验证属性"类

在`ValidationAttribute`.NET 框架 4 中改进了该类`IsValid`，以支持新的重载，该重载提供有关当前验证上下文的详细信息，例如正在验证的对象。 这支持更丰富的方案，您可以在其中根据模型的另一个属性验证当前值。 例如，新`CompareAttribute`属性允许您比较模型的两个属性的值。 在下面的示例中，`ComparePassword`属性必须匹配`Password`该字段才能有效。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>验证接口

[IValidaobject 接口](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)使您能够执行模型级验证，并且它使您能够提供特定于整个模型状态的验证错误消息，或在模型中的两个属性之间。 MVC 3 现在从`IValidatableObject`模型绑定时从接口检索错误，并使用内置的 HTML 表单帮助器自动标记或突出显示视图中受影响的字段。

[IClientValidaa 可界面](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)使ASP.NET MVC 能够在运行时发现验证器是否支持客户端验证。 此接口的设计使其可以与各种验证框架集成。

有关验证接口的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览博客文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)**模型验证改进**部分。 （但是，请注意，博客中对"IValidateObject"的引用应为"IValidaaobject"。

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>依赖项注入改进

ASP.NET MVC 3 为应用依赖项注入 （DI） 和与依赖项注入或控制反转 （IOC） 容器集成提供更好的支持。 在以下领域添加了对 DI 的支持：

- 控制器（注册和注入控制器工厂，注入控制器）。
- 视图（注册和注入视图引擎，将依赖项注入视图页）。
- 操作筛选器（定位和注入过滤器）。
- 模型活页夹（注册和注入）。
- 模型验证提供程序（注册和注入）。
- 建模元数据提供程序（注册和注入）。
- 价值提供者（注册和注入）。

MVC 3 支持[通用服务定位器](https://github.com/unitycontainer/commonservicelocator)库和支持该库`IServiceLocator`接口的任何 DI 容器。 它还支持一个新的`IDependencyResolver`接口，使集成 DI 框架变得更加容易。

有关 MVC 3 中的 DI 的详细信息，请参阅以下资源：

- [布拉德·威尔逊关于服务地点的一系列博客文章](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>其他新功能

### <a name="nuget-integration"></a>NuGet 集成

ASP.NET MVC 3 自动安装并启用 NuGet 作为其设置的一部分。 NuGet 是一个免费的开源包管理器，可让您在项目中轻松查找、安装和使用 .NET 库和工具。 它适用于所有 Visual Studio 项目类型（包括ASP.NET Web 窗体和ASP.NET MVC）。

NuGet 使维护开源项目的开发人员（例如，像 Moq、NHibernate、Ninject、结构映射、NUnit、温莎、RhinoMocks 和 Elmah）的项目）能够打包其库并将其注册到在线库中。 然后，想要使用这些库之一的 .NET 开发人员可以轻松查找包并将其安装在他们正在处理的项目中。

通过ASP.NET 3 工具更新，项目模板包括预安装的 NuGet 包的 JavaScript 库，因此它们可以通过 NuGet 进行更新。 实体框架代码优先也预装为 NuGet 包。

有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。

### <a name="partial-page-output-caching"></a>部分页面输出缓存

自版本 1 以来ASP.NET MVC 都支持整页响应的输出缓存。 MVC 3 还支持部分页面输出缓存，这允许您轻松缓存响应的区域或片段。 有关缓存的详细信息，请参阅[Scott Guthrie 在 MVC 3 版本候选版和 MVC](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) [3 发行说明](../whitepapers/mvc3-release-notes.md)的 **"子操作输出缓存**"部分部分页面**输出缓存**部分。

### <a name="granular-control-over-request-validation"></a>对请求验证的精细控制

ASP.NET MVC 具有内置请求验证，可自动帮助抵御 XSS 和 HTML 注入攻击。 但是，有时您希望显式禁用请求验证，例如，如果您希望允许用户发布 HTML 内容（例如，在博客条目或 CMS 内容中）。 现在，您可以将[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性添加到模型或视图模型，以便在模型绑定期间禁用基于每个属性的请求验证。 有关请求验证的详细信息，请参阅以下资源：

- [斯科特·古斯里关于MVC 3版本候选的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 **"不显眼的JavaScript和验证**"部分。
- [MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>可扩展的"新项目"对话框

在 mVC 3 ASP.NET，您可以将项目模板、视图引擎和单元测试项目框架添加到 **"新项目**"对话框中。

### <a name="template-scaffolding-improvements"></a>模板基架改进

ASP.NET MVC 3 基架模板比早期版本的 MVC 更好地识别模型上的主键属性并适当地处理它们。 （例如，基架模板现在确保主键不是基架作为可编辑的表单字段。

默认情况下，"创建和编辑"基架现在使用`Html.EditorFor`帮助器而不是`Html.TextBoxFor`帮助程序。 这在 **"添加视图"** 对话框生成视图时，改进了对模型上以数据注释属性形式对元数据的支持。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.Labelfor"和"Html.LabelFormodel"的新重载

已为`LabelFor`和`LabelForModel`帮助器方法添加了新方法重载。 新的重载使您能够指定或覆盖标签文本。

### <a name="sessionless-controller-support"></a>无会话控制器支持

在 mVC 3 ASP.NET 中，可以指示是否希望控制器类使用会话状态，如果是，会话状态应是读/写还是只读。 有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。

### <a name="new-additionalmetadataattribute-class"></a>新的"附加元数据属性"类

可以使用["附加元数据"](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性填充模型属性的`ModelMetadata.AdditionalValues`字典。 例如，如果视图模型具有仅应向管理员显示的属性，则可以对该属性进行加带，如以下示例所示：

[!code-csharp[Main](mvc3/samples/sample4.cs)]

呈现产品视图模型时，此元数据可用于任何显示或编辑器模板。 由您解释元数据信息。

### <a name="accountcontroller-improvements"></a>帐户控制器改进

互联网项目模板中的帐户控制器已大为改善。

### <a name="new-intranet-project-template"></a>新的内联网项目模板

包含新的 Intranet 项目模板，该模板启用 Windows 身份验证并删除帐户控制器。

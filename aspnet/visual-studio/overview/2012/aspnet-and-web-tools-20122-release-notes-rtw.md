---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET和网络工具 2012.2 发行说明 |微软文档
author: rick-anderson
description: ASP.NET和网络工具 2012.2 的发行说明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675903"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 发行说明

> 本文档介绍 ASP.NET 和 Web 工具 2012.2 的发布。 它是可视化工作室 Web 工具和ASP.NET的更新。

- [安装说明](#_Installation)
- [文档](#_Documentation)
- [支持](#_Support)
- [软件要求](#_Software_Requirements)
- [ASP.NET和 Web 工具中的新功能 2012.2](#_New_Features_in)

    - [工具](#_Tooling)
    - [Web 发布](#_Web_Publishing)
    - [ASP.NET MVC 模板](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 友好 URL](#_ASP.NET_Friendly_URLs)
- [已知问题和重大更改](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安装说明

ASP.NET和Web工具2012.2为可视化工作室2012可以使用[Web平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安装。 这是 Visual Studio 2012 或 Visual Studio Express 2012 Web 的更新，这是必要的。 如果您未安装 Visual Studio，则将安装适用于 Web 的 Visual Studio Express 2012。

您还可以手动安装ASP.NET和 Web 工具 2012.2。 您必须安装 Visual Studio 2012 或 Visual Studio Express 2012 以安装 Web。 然后使用以下说明： 

1. 从下载中心下载[ASP.NET和 Web 框架 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安装程序。
2. 当提示时，单击"运行"。 您还可以保存该文件以稍后运行该文件。
3. 验证您将要更新的可视化工作室版本。 您可以通过启动要更新的可视化工作室来执行此操作。 然后单击"帮助"菜单项。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 如果你看到关于微软视觉工作室&quot;2012网页的菜单项&quot;，然后下载[网络开发人员工具2012.2 - Visual Studio Express 2012为Web。](https://go.microsoft.com/fwlink/?LinkID=282228) 否则下载[网络开发人员工具 2012.2 - 视觉工作室 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. 当提示时，单击"运行"。 您还可以保存该文件以稍后运行该文件。

> [!NOTE]
> ASP.NET和 Web 工具 2012.2 版本不包括 SQL Server 数据工具。 SQL Server 和 Windows Azure SQL 数据库提供了一组更丰富的数据库工具，包括脱机项目支持的开发、架构比较和增强的数据库部署功能。 有关详细信息或安装 SQL 服务器数据工具，请访问[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)。

<a id="_Documentation"></a>
## <a name="documentation"></a>文档

有关ASP.NET和 Web 工具 2012.2 的教程和其他信息可从ASP.NET网站https://www.asp.net)（） 获得。

<a id="_Support"></a>
## <a name="support"></a>支持

ASP.NET和网络工具 2012.2 正式发布和支持。 您可以使用正常的支持通道。 您还可以向ASP.NET论坛 （）[https://forums.asp.net/](https://forums.asp.net/)发布问题，ASP.NET社区成员经常能够提供非正式支持。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET和网络工具 2012.2 要求 Visual Studio 2012 或 Visual Studio Express 2012 用于 Web。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET和 Web 工具中的新功能 2012.2

本节介绍在ASP.NET和 Web 工具 2012.2 版本中引入的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>工具

- Page Inspector 

    - 支持 JavaScript 选择映射，允许页面检查器将动态添加到页面的项目映射回相应的 JavaScript 代码。
    - 实时查看 CSS 更新的能力。
    - 有关详细信息，请阅读[页面检查器 中的 CSS 自动同步和 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 编辑器 

    - 支持咖啡脚本、胡须、手柄和 JsRender 的语法突出显示。
    - HTML 编辑器为挖空绑定提供"感知"。
    - 减少编辑和编译器支持，以便使用 LESS 构建动态 CSS。
    - 将 JSON 粘贴为 .NET 类。 使用此特殊粘贴命令将 JSON 粘贴到 C# 或VB.NET代码文件中，Visual Studio 将自动生成从 JSON 推断的 .NET 类。
- 移动仿真器支持增加了扩展性挂钩，以便第三方仿真器可以作为 VSIX 安装。 已安装的仿真器将显示在 F5 下拉列表中，以便开发人员可以在各种移动设备上预览其网站。 阅读更多有关此功能在斯科特汉塞尔曼的博客条目与[视觉工作室新的浏览器堆栈集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 发布

- 网站项目现在具有与 Web 应用程序项目相同的发布体验，包括发布到 Windows Azure 网站。
- 选择性发布&#8211;一个或多个文件，您可以执行以下操作（发布到 Web 部署终结点后）： 

    - 发布选定的文件。
    - 查看本地文件和远程文件之间的区别。
    - 使用远程文件更新本地文件或使用本地文件更新远程文件。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 模板

- 新的 Facebook 应用程序模板可帮助你轻松编写 Facebook Canvas 应用程序。 只需执行几个简单步骤，即可创建一个 Facebook 应用程序，从已登录用户获取数据并与其好友集成。 该模板包含一个新库，可维护构建 Facebook 应用程序时涉及的所有管道（包括身份验证、权限、访问 Facebook 数据等）， 有关使用 Facebook 应用程序模板的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)。
- 使用新的单页应用程序 MVC 模板，开发人员可以在 ASP.NET Web API 之上使用 HTML 5、CSS 3 以及常用的 Knockout 和 jQuery JavaScript 库构建交互式客户端 Web 应用程序。 该模板包括一个"待办事项"列表应用程序，该应用程序演示了构建使用 RESTful 服务器 API 的 JavaScript HTML5 应用程序的常见做法。 您可以在 上阅读更多内容[https://www.asp.net/single-page-application](../../../single-page-application/index.md)。
- 您现在可以创建一个 VSIX，将新模板添加到ASP.NET MVC 新项目对话框。 了解如何在此处：[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- 已更新 &#8211; MVC 项目模板的固定显示模式包，以包括新的"固定显示模式"NuGet 包，该包包含 MVC 4 中 Bug 的解决方法。 有关包中包含的修复程序的详细信息，请参阅 MVC 团队的此博客文章 （[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)）。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 已通过以下几个新功能进行了增强：

- ASP.NET Web API OData
- ASP.NET Web API 跟踪
- ASP.NET Web API 帮助页

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 使您能够灵活地构建具有丰富业务逻辑的 OData 终结点，而不是任何数据源。 使用ASP.NET Web API OData，您可以控制要公开的 OData 语义量。 ASP.NET Web API OData 包含在mVC 4ASP.NET项目模板中，也可从 NuGet[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)（） 获得。

ASP.NET Web API OData 目前支持以下功能：

- 通过应用 [可查询] 属性启用 OData 查询语义。
- 轻松验证 OData 查询并限制支持的查询选项、运算符和函数集。
- 参数直接绑定到 ODataQueryOptions，以获得查询的抽象语法树表示形式，然后可以验证并应用于可查询或 IE500。
- 通过在 [可查询] 属性上指定结果限制，启用服务驱动的分页和下一页链接生成。
- 使用$inlinecount请求匹配资源总数的内联计数。
- 控制无效传播。
- $filter中的任何/所有运算符。
- 按约定推断实体数据模型，或以类似于实体框架代码优先的方式显式自定义模型。
- 通过从实体集控制器派生来公开实体集。
- 用于公开导航属性、操作链接和实现 OData 操作的简单可自定义约定。
- 使用 MapODataRoute 扩展方法简化路由。
- 通过公开多个 EDM 模型来支持版本控制。
- 公开服务文档和$metadata，以便为 Web API 生成客户端（.NET、Windows Phone、Windows 应用商店等）。
- 支持 OData Atom、JSON 和 JSON 详细格式。
- 创建、更新、部分更新（PATCH）和删除实体。
- 查询和操作实体之间的关系。
- 创建连接到您的路线的关系链接。
- 复杂类型。
- 实体类型继承。
- 集合属性。
- 枚举。
- OData 操作。
- 建立与 WCF 数据服务相同的基础，即 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)（）。

有关web API OData ASP.NET的详细信息[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)，请参阅。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 跟踪

ASP.NET Web API 跟踪将从 Web API 的跟踪数据集成到 .NET 跟踪中。 默认情况下，它在 Web API 项目模板中启用。 Web API 的跟踪数据将发送到输出窗口，并通过 IntelliTrace 提供。 ASP.NET Web API 跟踪使您能够通过与[Windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)集成在 Windows Azure 上托管时跟踪有关 Web API 的信息。 您还可以使用ASP.NET Web API 跟踪 NuGet 包 （）[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)在任何应用程序中安装和启用ASP.NET Web API 跟踪。

有关配置和使用ASP.NET Web API 跟踪的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 帮助页

默认情况下，Web API 帮助页ASP.NET包含在 Web API 项目模板中。 ASP.NET Web API 帮助页会自动为 Web API 生成文档，包括 HTTP 终结点、支持的 HTTP 方法、参数以及示例请求和响应消息负载。 文档会自动从代码中的注释中提取。 您还可以使用ASP.NET Web API 帮助页 NuGet 包 （）[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)将ASP.NET Web API 帮助页添加到任何应用程序。

有关设置和自定义ASP.NET Web API 帮助页的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 使将实时 Web 功能添加到ASP.NET应用程序中变得简单，如果使用 WebSocket（如果可用），则在不可用时自动回归到其他技术。

有关使用ASP.NET信号R的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 友好 URL

ASP.NET友好 URL 使 Web 表单开发人员能够非常轻松地生成外观更简洁的 URL（没有 .aspx 扩展）。 它只需要很少或不需要配置，并且可用于现有的ASP.NET v4.0 应用程序。 友好 URL 功能还支持桌面视图和移动视图之间的切换，使开发人员能够更轻松地向其应用程序添加移动支持。

有关安装和使用ASP.NET友好 URL 的详细信息，请参阅[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

本节介绍 ASP.NET 和 Web 工具 2012.2 版本中的已知问题和重大更改。

### <a name="installation-issues"></a>安装问题

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>视觉工作室 2012 的有序安装

安装ASP.NET和 Web 工具 2012.2 后安装 Visual Studio 2012 的额外 SKU 将需要修复操作。 考虑以下序列：

1. 安装可视化工作室 2012 快速网页
2. 安装ASP.NET和 Web 工具 2012.2
3. 安装视觉工作室 2012 专业， 高级或终极

步骤 2 仅会导致为 Web 安装 Express 的更新。 为了确保在步骤 3 中安装的其他 SKU 包含更新，您需要修复 ASP.NET 和 Web 工具 2012.2 才能安装上次安装的 SKU 的更新。 如果步骤 1 和步骤 3 中的 SKU 颠倒，则这也适用于。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>安装微软ASP.NET和网络工具 2012.2 当可视化工作室打开

如果在安装 Microsoft ASP.NET 和 Web 工具 2012.2 期间打开 VS，则 Visual Studio 可能最终处于不良状态。 建议用户在继续安装之前关闭 Visual Studio 的所有实例。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>在安装中取消ASP.NET和 Web 工具 2012.2 设置

取消ASP.NET和 Web 工具 2012.2 安装将会使 Visual Studio 处于不良状态。 要解决此问题，请执行以下步骤： 

- 转到“添加/删除程序”
- 卸载 Microsoft ASP.NET 和 Web 工具 2012.2（如果存在）。
- 重新安装微软ASP.NET和网络工具 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>卸载ASP.NET和 Web 工具 2012.2 后，缺少ASP.NET MVC 4 模板和 Razor v2 网站模板

卸载ASP.NET和 Web 工具 2012.2 还将从 Visual Studio 2012 卸载所有ASP.NET MVC 4 和 Razor v2 网站模板。

解决方法是修复 Visual Studio 2012 安装，以重新安装ASP.NET MVC 4 和 Razor v2 网站模板。

### <a name="tooling-issues"></a>工具问题

#### <a name="nuget-error-reported-during-project-creation"></a>项目创建期间报告的 NuGet 错误

安装ASP.NET和 Web 工具 2012.2 后，在创建 MVC 4 项目时可能会看到以下错误

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET和网络工具 2012.2 船舶 NuGet 2.1，并将升级 Visual Studio 2012 中的扩展。 在某些情况下，VSIX 安装程序将无法正确更新 VSIX。 以下步骤将允许您解决此问题：

1. 以管理员身份开始视觉工作室 2012
2. 转到工具 -&gt;扩展和更新，卸载 NuGet。
3. 关闭 Visual Studio
4. 导航到ASP.NET和 Web 工具 2012.2 安装文件夹：

    1. 对于视觉工作室 2012：**程序文件_微软 ASP.NET_ASP.NET 网络堆栈_视觉工作室 2012**
    2. 对于 Visual Studio 2012 Web 快讯：**程序文件_微软 ASP.NET_ASP.NET Web 堆栈_Visual Studio Express 2012 网页**
5. 双击 NuGet.Tools.vsix 重新安装 NuGet

### <a name="web-api-issues"></a>Web API 问题

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>分析$filter和 DateTime 文本中的问题

OData URI 解析器无法正确解析部分日期时间文本。 例如，$filter_开始 eq 日期时间'2012-12-31T12：00' 无法正确解析。 解决方法是使用完整的文本，$filter_开始 eq 日期时间'2012-12-31T12：00：00'。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 不支持不区分大小写的属性名称。

OData 不支持 OData 查询和 odata 路径中不区分大小写的属性名称。 请参阅工作项：

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果用户在 javascript 客户端和服务器端具有不同的大小写，他们可能会遇到此问题。 此问题是在 odata 协议中设计的问题。 但是，许多用户报告此问题。 要解决此问题，用户必须更正 URL 中的情况。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>默认 OData 路由约定不支持导航属性上的 POST/PUT。

默认 OData 路由约定不支持导航属性上的 POST/PUT。 请参阅工作项[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。 在默认约定中，我们缺少此常用约定。

要解决它，用户需要扩展新的路由约定来支持它。

### <a name="facebook-template-issues"></a>Facebook 模板问题

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 应用程序模板仅适用于 .NET 4.5

您必须在"新项目"对话框的框架下拉列表中选择 .NET 4.5，才能在 mVC 4 ASP.NET中查看 Facebook 应用程序模板。

#### <a name="real-time-update-controller"></a>实时更新控制器

Facebook 应用程序模板允许用户轻松创建 Web API 控制器来处理来自 Facebook 的实时更新。 如果开发计算机位于 NAT 之后，则如果没有进一步的网络配置，控制器可能无法工作。 有关详细信息，请参阅此处：[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查询字符串值与 Facebook OAuth 参数冲突

以下字段与 Facebook OAuth 对话框的回调 URL 冲突。 不要添加具有以下名称的查询字符串值：代码、错误、错误\_描述、错误\_原因。

#### <a name="using-page-inspector-with-facebook-template"></a>使用带有 Facebook 模板的页面检查器

调试 Facebook 应用程序时，不能在 Visual Studio 2012 中使用页面检查器功能。 页面检查器当前不支持 iframe。

### <a name="single-page-application-template-issues"></a>单页应用程序模板问题

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>使用 JQuery 1.9/挖空 2.2.1 更新时，在运行默认 MVC SPA 项目时，新的 todo 项编辑输入焦点事件处理不正确。

使用 JQuery 1.9/挖空 2.2.1 更新，在运行默认 MVC SPA 项目时，新待办事项编辑在进入待办事项列表的新待办事项后不再聚焦到新的待办事项编辑框。

要进行解决方法引用[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)，并针对以下示例代码进行类似的修复：

文件 todo.model.js  
 函数待办事项（数据），添加以下内容：  
 **自我.is选定 = ko.可观察（假）;**

函数 todoList.原型.addTodo，添加以下黑色文本：  
 **自我.是选择（真）;**  
 自我.新托多标题（）;&quot;&quot;

文件索引.cshtml，添加以下黑色文本：  
 &lt;表单数据绑定*&quot;提交：添加Todo&quot;&gt;  
 &lt;输入类=&quot;addTodo&quot; &quot;类型&quot;= 文本数据&quot;绑定= 值：newTodoTitle，占位符："在此处键入添加"，模糊OnEnter：true，**有焦点：是选定**，事件：[模糊：添加Todo]&quot; /&gt;  
 &lt;/形式&gt;

---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web 工具2012.2 发行说明 |Microsoft Docs
author: rick-anderson
description: ASP.NET 和 Web 工具2012.2 的发行说明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345589"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 发行说明

> 本文档介绍 ASP.NET 和 Web 工具2012.2 的版本。 它是 Visual Studio Web 工具和 ASP.NET 的更新。

- [安装说明](#_Installation)
- [文档](#_Documentation)
- [支持](#_Support)
- [软件要求](#_Software_Requirements)
- [ASP.NET 和 Web 工具2012.2 中的新增功能](#_New_Features_in)

    - [工具](#_Tooling)
    - [Web 发布](#_Web_Publishing)
    - [ASP.NET MVC 模板](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 友好 URL](#_ASP.NET_Friendly_URLs)
- [已知问题和重大更改](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安装说明

可使用 [Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安装 Visual Studio 2012 的 ASP.NET 和 Web 工具2012.2。 这是对 Visual Studio 2012 或 Visual Studio Express 2012 for Web 的更新，这是必需的。 如果尚未安装 Visual Studio，将安装适用于 Web 的 Visual Studio Express 2012。

你还可以手动安装 ASP.NET 和 Web 工具2012.2。 必须安装 Visual Studio 2012 或 Visual Studio Express 2012 for Web。 然后，使用以下说明： 

1. 从下载中心下载 [ASP.NET 和 Web framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 安装程序。
2. 出现提示时，请单击 "运行"。 你还可以保存该文件，以便稍后运行。
3. 验证要更新的 Visual Studio 版本。 可以通过启动要更新的 Visual Studio 来实现此目的。 然后单击 "帮助" 菜单项。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 如果你看到 &quot; 有关 web Microsoft Visual Studio 2012 的菜单项，请 &quot; 下载 [web 开发人员工具 2012.2-Visual Studio Express 2012 for web](https://go.microsoft.com/fwlink/?LinkID=282228)。 否则 [，下载 Web 开发人员工具 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。
5. 出现提示时，请单击 "运行"。 你还可以保存该文件，以便稍后运行。

> [!NOTE]
> ASP.NET 和 Web 工具2012.2 版不包括 SQL Server Data Tools。 SQL Server 和 Microsoft Azure SQL 数据库提供了一组丰富的数据库工具，包括脱机项目支持的开发、架构比较和增强的数据库部署功能。 有关详细信息或安装 SQL Server Data Tools 访问 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127) 。

<a id="_Documentation"></a>
## <a name="documentation"></a>文档

ASP.NET 网站 ( 提供了有关 ASP.NET 和 Web 工具2012.2 的教程和其他信息 https://www.asp.net) 。

<a id="_Support"></a>
## <a name="support"></a>支持

ASP.NET 和 Web 工具2012.2 正式发布并受支持。 你可以使用正常的支持渠道。 你还可以将问题发布到 ASP.NET 论坛 ([https://forums.asp.net/](https://forums.asp.net/)) ，其中 ASP.NET 社区的成员经常能够提供非正式支持。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET 和 Web 工具2012.2 需要适用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 和 Web 工具2012.2 中的新增功能

本部分介绍 ASP.NET 和 Web 工具2012.2 发行版中引入的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>工具

- Page Inspector 

    - 支持 JavaScript 选择映射，Page Inspector 允许将动态添加到页面的项映射回相应的 JavaScript 代码。
    - 能够实时查看 CSS 更新。
    - 有关详细信息，请参阅 [Page Inspector 中的 CSS 自动同步和 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 编辑器 

    - 支持对 CoffeeScript、Mustache、Handlebars 和 JsRender 进行语法突出显示。
    - HTML 编辑器为挖空绑定提供 Intellisense。
    - 使用较少的可以更少的编辑和编译器支持构建动态 CSS。
    - 将 JSON 粘贴为 .NET 类。 使用此特殊的 "粘贴" 命令将 JSON 粘贴到 c # 或 VB.NET 代码文件中，Visual Studio 将自动生成从 JSON 推断出的 .NET 类。
- 移动模拟器支持添加扩展性挂钩，以便可以将第三方模拟器安装为 VSIX。 在 F5 下拉列表中将显示已安装的仿真器，以便开发人员可以在各种移动设备上预览其网站。 有关此功能的详细信息，请参阅 Scott Hanselman 的博客文章 [BrowserStack Visual Studio 的新的集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 发布

- 网站项目现在具有与 Web 应用程序项目相同的发布体验，包括发布到 Microsoft Azure 网站。
- 选择性发布 &#8211; 对于一个或多个文件，你可以在发布到 Web 部署终结点) 后 (执行以下操作： 

    - 发布选定的文件。
    - 请参阅本地文件和远程文件之间的差异。
    - 用远程文件更新本地文件，或用本地文件更新远程文件。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 模板

- 新的 Facebook 应用程序模板可帮助你轻松编写 Facebook Canvas 应用程序。 只需执行几个简单步骤，即可创建一个 Facebook 应用程序，从已登录用户获取数据并与其好友集成。 该模板包含一个新库，可维护构建 Facebook 应用程序时涉及的所有管道（包括身份验证、权限、访问 Facebook 数据等）， 有关使用 Facebook 应用程序模板的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921) 。
- 使用新的单页应用程序 MVC 模板，开发人员可以在 ASP.NET Web API 之上使用 HTML 5、CSS 3 以及常用的 Knockout 和 jQuery JavaScript 库构建交互式客户端 Web 应用程序。 该模板包含一个 "todo" 列表应用程序，该应用程序演示了用于生成使用 RESTful server API 的 JavaScript HTML5 应用程序的常见做法。 有关详细信息，请参阅 [https://www.asp.net/single-page-application](../../../single-page-application/index.md) 。
- 你现在可以创建一个将新模板添加到 "ASP.NET MVC 新项目" 对话框中的 VSIX。 了解以下操作： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 包 &#8211; MVC 项目模板已更新为包含新的 "FixedDisplayModes" NuGet 包，其中包含 MVC 4 中 bug 的解决方法。 有关包中包含的修复的详细信息，请参阅此博客文章 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) MVC 团队。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

利用几项新功能增强了 ASP.NET Web API：

- ASP.NET Web API OData
- ASP.NET Web API 跟踪
- ASP.NET Web API 帮助页

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 使你可以灵活地在任何数据源上构建具有丰富业务逻辑的 OData 终结点。 通过 ASP.NET Web API OData 控制要公开的 OData 语义量。 ASP.NET MVC 4 项目模板附带了 ASP.NET Web API OData，还可从 NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)) 获得。

ASP.NET Web API OData 当前支持以下功能：

- 通过应用 [可查询] 属性启用 OData 查询语义。
- 轻松验证 OData 查询，并限制支持的查询选项、运算符和函数集。
- 参数直接绑定到 ODataQueryOptions，以获取查询的抽象语法树表示形式，然后可以对其进行验证并将其应用于 IQueryable 或 IEnumerable。
- 通过在 [可查询] 特性上指定结果限制，启用服务驱动分页和下一页链接生成。
- 使用 $inlinecount 请求匹配资源总数的内联计数。
- 控制 null 传播。
- $Filter 中的任何/所有运算符。
- 按约定推理实体数据模型，或以类似于实体框架代码优先的方式显式自定义模型。
- 通过从 EntitySetController 派生来公开实体集。
- 简单、可自定义的约定，用于公开导航属性、操作链接和实现 OData 操作。
- 使用 MapODataRoute 扩展方法简化路由。
- 支持通过公开多个 EDM 模型进行版本控制。
- 公开服务文档和 $metadata 以便可以为 Web API ( .NET、Windows Phone、Windows 应用商店等 ) 生成客户端。
- 支持 OData Atom、JSON 和 JSON 详细格式。
- 创建、更新、部分更新 (修补程序) 和删除实体。
- 查询和操作实体之间的关系。
- 创建连接到路由的关系链接。
- 复杂类型。
- 实体类型继承。
- 集合属性。
- 枚举.
- OData 操作。
- 建立在与 WCF 数据服务相同的基础上，即 ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)) 。

有关 ASP.NET Web API OData 的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141) 。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 跟踪

ASP.NET Web API 跟踪通过 .NET 跟踪集成 Web Api 中的跟踪数据。 它现在默认在 Web API 项目模板中启用。 Web Api 的跟踪数据将发送到 "输出" 窗口，并通过 IntelliTrace 提供。 ASP.NET Web API 跟踪，你可以通过与 [windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)的集成，在 windows Azure 上托管时跟踪有关 Web API 的信息。 你还可以使用 ASP.NET Web API 跟踪 NuGet 包 () 在任何应用程序中安装和启用 ASP.NET Web API 跟踪 [http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing) 。

有关配置和使用 ASP.NET Web API 跟踪的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874) 。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 帮助页

默认情况下，"ASP.NET Web API 帮助" 页包含在 Web API 项目模板中。 ASP.NET Web API 帮助页自动生成 Web Api 的文档，包括 HTTP 终结点、支持的 HTTP 方法、参数以及示例请求和响应消息负载。 文档自动从代码中的注释提取。 还可以使用 ASP.NET Web API 帮助页 NuGet 包 () 将 ASP.NET Web API 帮助页添加到任何应用程序 [http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage) 。

有关设置和自定义 ASP.NET Web API 帮助页的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140) 。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 可让你轻松地将实时 web 功能添加到你的 ASP.NET 应用程序，使用 Websocket （如果可用），并在不使用时自动回退到其他技术。

有关使用 ASP.NET SignalR 的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271) 。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 友好 URL

ASP.NET Microsoft.aspnet.friendlyurls 使得 web 窗体开发人员能够轻松地生成外观清晰的 Url (不) .aspx 扩展。 它几乎不需要任何配置，并且可以与现有的 ASP.NET v4.0 应用程序一起使用。 借助 Microsoft.aspnet.friendlyurls 功能，开发人员可以更轻松地向应用程序添加移动支持，方法是支持在桌面和移动视图之间切换。

有关安装和使用 ASP.NET 友好 Url 的详细信息，请参阅 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) 。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

本部分介绍 ASP.NET 和 Web 工具2012.2 发行版中的已知问题和重大更改。

### <a name="installation-issues"></a>安装问题

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012 的顺序安装

安装 ASP.NET 和 Web 工具2012.2 后安装 Visual Studio 2012 的附加 SKU 需要修复操作。 考虑以下序列：

1. 安装 Visual Studio 2012 Express for Web
2. 安装 ASP.NET 和 Web 工具2012。2
3. 安装 Visual Studio 2012 Professional、Premium 或旗舰版

步骤2只会导致为 Express for Web 安装更新。 若要确保在步骤3中安装的其他 SKU 包含更新，你将需要修复 ASP.NET 和 Web 工具2012.2 以安装最后安装的 SKU 的更新。 如果步骤1和3中的 Sku 反转，这同样适用。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio 打开时安装 Microsoft ASP.NET 和 Web 工具2012。2

如果在 Microsoft ASP.NET 和 Web 工具2012.2 的安装过程中打开了 VS，则 Visual Studio 可能会在错误的状态下结束。 建议用户在继续安装前关闭 Visual Studio 的所有实例。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>在安装过程中取消 ASP.NET 和 Web 工具2012.2 安装程序

如果在安装过程中取消 ASP.NET 和 Web 工具2012.2 安装程序，则 Visual Studio 将处于错误状态。 若要解决此问题，请执行以下步骤： 

- 转到“添加/删除程序”
- 卸载 Microsoft ASP.NET 和 Web 工具2012.2 （如果存在）。
- 重新安装 Microsoft ASP.NET 和 Web 工具2012。2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>卸载 ASP.NET 和 Web 工具2012.2 后，ASP.NET MVC 4 模板和 Razor v2 网站模板缺失

卸载 ASP.NET 和 Web 工具2012.2 还将从 Visual Studio 2012 中卸载所有 ASP.NET MVC 4 和 Razor v2 网站模板。

解决方法是修复 Visual Studio 2012 安装，重新安装 ASP.NET MVC 4 和 Razor v2 网站模板。

### <a name="tooling-issues"></a>工具问题

#### <a name="nuget-error-reported-during-project-creation"></a>项目创建过程中报告的 NuGet 错误

安装 ASP.NET 和 Web 工具2012.2 后，创建 MVC 4 项目时可能会看到以下错误

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 和 Web 工具2012.2 随附了 NuGet 2.1，并将在 Visual Studio 2012 中升级扩展。 在某些情况下，VSIX 安装程序将无法正确更新 VSIX。 以下步骤可用于解决此问题：

1. 以管理员身份启动 Visual Studio 2012
2. 请参阅 "工具"-" &gt; 扩展和更新" 和 "卸载 NuGet"。
3. 关闭 Visual Studio
4. 导航到 ASP.NET 和 Web 工具2012.2 安装文件夹：

    1. 对于 Visual Studio 2012： **Program FILES\MICROSOFT NET\ASP.NET Web Stack\Visual Studio 2012**
    2. 对于 Visual Studio 2012 Express for Web： **Program FILES\MICROSOFT NET\ASP.NET web Stack\Visual Studio Express 2012 For web**
5. 双击 "NuGet" 以重新安装 NuGet

### <a name="web-api-issues"></a>Web API 问题

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>分析 $filter 和日期时间文本中的问题

OData URI 分析器无法正确分析部分日期时间文本。 例如，$filter = start eq datetime ' 2012-12-31T12： 00 ' 无法正确分析。 解决方法是使用完整文本，$filter = start eq datetime ' 2012-12-31T12：00： 00 '。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 不支持不区分大小写的属性名。

Odata 在 OData 查询和 OData 路径中不支持不区分大小写的属性名。 请参阅工作项：

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果用户在 javascript 客户端和服务器端具有不同的大小写，则可能会遇到此问题。 此问题是在 odata 协议中设计的。 但是，许多用户会报告此问题。 若要解决此情况，用户必须在 URL 中更正其事例。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>默认 OData 路由约定不支持对导航属性进行 POST/PUT。

默认 OData 路由约定不支持对导航属性进行 POST/PUT。 请参阅工作项 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366) 。 我们在默认约定中缺少此常用约定。

若要解决此情况，用户需要扩展新的路由约定以支持它。

### <a name="facebook-template-issues"></a>Facebook 模板问题

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 应用程序模板仅适用于使用 .NET 4。5

必须在 "新建项目" 对话框的 "框架" 下拉列表中选择 ".NET 4.5"，才能在 ASP.NET MVC 4 中查看 Facebook 应用程序模板。

#### <a name="real-time-update-controller"></a>实时更新控制器

Facebook 应用程序模板允许用户轻松创建一个 Web API 控制器来处理 Facebook 的实时更新。 如果开发计算机位于 NAT 后面，则在没有进一步的网络配置的情况下，控制器可能不起作用。 有关详细信息，请参阅此处： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查询字符串值与 Facebook OAuth 参数冲突

以下字段与 Facebook OAuth 对话的回调 URL 冲突。 不要添加您自己的具有以下名称的查询字符串值：代码、错误、错误 \_ 说明、错误 \_ 原因。

#### <a name="using-page-inspector-with-facebook-template"></a>将 Page Inspector 与 Facebook 模板结合使用

调试 Facebook 应用程序时，不能使用 Visual Studio 2012 中的 Page Inspector 功能。 Page Inspector 当前不支持 iframe。

### <a name="single-page-application-template-issues"></a>单页应用程序模板问题

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>通过 JQuery 1.9/挖空2.2.1 更新时，在运行默认 MVC SPA 项目时，不会正确处理新的 todo 项 "编辑输入焦点事件"。

通过 JQuery 1.9/挖空2.2.1 更新时，在运行默认 MVC SPA 项目时，在将新的 todo 项输入到 todo 列表中后，新的 todo 项 "编辑" 将不再焦点返回到 "新建 todo 项" 编辑框。

若要解决 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html) 此问题，请参考下面的示例代码：

文件 todo.model.js  
 函数 todolist (数据) ，添加以下内容：  
 **isSelected = ko (false) ;**

函数 todoList，添加以下涂黑文本：  
 **isSelected (true) ;**  
 newTodoTitle (&quot; &quot;) ;

文件索引 cshtml，添加以下涂黑文本：  
 &lt;表单数据-bind = &quot; submit： addTodo&quot;&gt;  
 &lt;输入类 = &quot; addTodo &quot; 类型 = &quot; 文本 &quot; 数据-Bind = &quot; 值： newTodoTitle，占位符： "在此处添加的类型"，blurOnEnter： true， **hasfocus： isSelected**，事件： {模糊： addTodo}&quot; /&gt;  
 &lt;/form&gt;

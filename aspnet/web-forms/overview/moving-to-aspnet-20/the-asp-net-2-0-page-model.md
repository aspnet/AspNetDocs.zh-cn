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
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 页型号

由[微软](https://github.com/microsoft)

> 在ASP.NET 1.x 中，开发人员可以选择内联代码模型和代码背后的代码模型。 可以使用 Src 属性或@Page指令的 Code 背后属性实现代码后面。 在ASP.NET 2.0 中，开发人员在内联代码和代码后面之间仍有选择，但代码背后的模型有显著的增强功能。

在ASP.NET 1.x 中，开发人员可以选择内联代码模型和代码背后的代码模型。 可以使用 Src 属性或@Page指令的 Code 背后属性实现代码后面。 在ASP.NET 2.0 中，开发人员在内联代码和代码后面之间仍有选择，但代码背后的模型有显著的增强功能。

## <a name="improvements-in-the-code-behind-model"></a>代码后模型的改进

为了充分理解ASP.NET 2.0 中代码背后的更改，最好快速查看模型，因为它存在于ASP.NET 1.x 中。

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x 中的代码后模型

在ASP.NET 1.x 中，代码后面模型由 ASPX 文件（Webform）和包含编程代码的代码后文件组成。 两个文件使用 ASPX@Page文件中的指令连接。 ASPX 页面上的每个控件在代码后面的文件中都有相应的声明作为实例变量。 代码背后的文件还包含事件绑定的代码和 Visual Studio 设计器所需的生成代码。 此模型工作相当良好，但由于 ASPX 页中的每个ASP.NET元素都需要代码背后的文件中的相应代码，因此代码和内容没有真正的分离。 例如，如果设计器向 Visual Studio IDE 外部的 ASPX 文件添加了新的服务器控件，则应用程序将由于代码背后的文件中缺少该控件的声明而中断。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 中的代码后模型

ASP.NET 2.0 大大改进了此模型。 在 ASP.NET 2.0 中，使用 ASP.NET 2.0 中提供的新*部分类*实现代码后面。 ASP.NET 2.0 中的代码后面类定义为部分类，这意味着它只包含类定义的一部分。 类定义的其余部分由 ASP.NET 2.0 在运行时或使用 ASPX 页或预编译网站时动态生成。 代码背后的文件和 ASPX 页之间的链接仍使用 @ Page 指令建立。 但是，ASP.NET 2.0 现在使用 CodeFile 属性，而不是代码背后或 Src 属性。 继承属性还用于指定页面的类名称。

典型的 @ 页面指令可能如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 代码背后的文件中的典型类定义可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# 和 Visual Basic 是当前支持部分类的唯一托管语言。 因此，使用 J# 的开发人员将无法在 ASP.NET 2.0 中使用代码后面模型。

新模型增强了代码背后的模型，因为开发人员现在将具有仅包含他们创建的代码的代码文件。 它还提供了代码和内容的真正分离，因为代码后面的文件中没有实例变量声明。

> [!NOTE]
> 由于 ASPX 页的部分类是事件绑定发生的位置，因此 Visual Basic 开发人员可以通过在代码后面中使用 Handles 关键字绑定事件来实现轻微的性能提升。 C# 没有等效关键字。

## <a name="new--page-directive-attributes"></a>新建 = 页面指令属性

ASP.NET 2.0 向 @ Page 指令添加了许多新属性。 以下属性在 ASP.NET 2.0 中是新的。

## <a name="async"></a>Async

Async 属性允许您配置要异步执行的页面。 本模块稍后将介绍异步页面。

## <a name="asynctimeout"></a>同步超时

指定异步页面的超时。 默认值为 45 秒。

## <a name="codefile"></a>代码文件

CodeFile 属性是 Visual Studio 2002/2003 中 CodeForin 属性的替换。

### <a name="codefilebaseclass"></a>代码文件基础类

在希望多个页面从单个基类派生的情况下，使用 CodeFileBaseClass 属性。 由于在ASP.NET中实现部分类，如果没有此属性，使用共享公共字段引用在 ASPX 页中声明的控件的基类将无法正常工作，因为 ASP.NETs 编译引擎将根据页面中的控件自动创建新成员。 因此，如果要在ASP.NET中为两个或多个页面定义一个公共基类，则需要在 CodeFileBaseClass 属性中定义指定基类，然后从该基类派生每个页面类。 使用此属性时，也需要 CodeFile 属性。

## <a name="compilationmode"></a>编译模式

此属性允许您设置 ASPX 页的编译模式属性。 "编译模式"属性是包含值 **"始终**、**自动**"和 **"从不"** 的枚举。 默认值为 **"始终**"。 如果可能，**自动**设置将阻止ASP.NET动态编译页面。 从动态编译中排除页面可提高性能。 但是，如果排除的页面包含必须编译的代码，则在浏览页面时将引发错误。

## <a name="enableeventvalidation"></a>启用事件验证

此属性指定是否验证回退和回调事件。 启用此功能后，将检查用于回退或回调事件的参数，以确保它们源自最初呈现这些事件的服务器控件。

## <a name="enabletheming"></a>启用"启用"

此属性指定ASP.NET主题是否在页面上使用。 默认值为**false**。 ASP.NET主题在第[10单元](profiles-themes-and-web-parts.md)中介绍。

## <a name="linepragmas"></a>线普拉格玛斯

此属性指定是否应在编译期间添加行杂注。 行杂注是调试器用于标记代码特定部分的选项。

## <a name="maintainscrollpositiononpostback"></a>保持滚动位置后回

此属性指定是否将 JavaScript 注入页面以保持回退之间的滚动位置。 默认情况下，此属性**为 false。**

当此属性为**true**时，ASP.NET&lt;将在&gt;回退后添加如下所示的脚本块：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

请注意，此脚本块的 src 是 WebResource.axd。 此资源不是物理路径。 请求此脚本时，ASP.NET动态生成脚本。

### <a name="masterpagefile"></a>母版页面文件

此属性指定当前页面的主页文件。 路径可以是相对路径或绝对路径。 母版页在[单元 4](master-pages.md)中介绍。

## <a name="stylesheettheme"></a>样式表主题

此属性允许您覆盖由ASP.NET 2.0 主题定义的用户界面外观属性。 主题在第[10 单元](profiles-themes-and-web-parts.md)中介绍。

## <a name="theme"></a>主题

指定页面的主题。 如果未为 StyleSheetTheme 属性指定值，则主题属性将覆盖应用于页面上控件的所有样式。

## <a name="title"></a>标题

设置页面的标题。 此处指定的值将显示在呈现页面&lt;的标题&gt;元素中。

### <a name="viewstateencryptionmode"></a>查看状态加密模式

设置视图状态加密模式枚举的值。 可用值为 **"始终**、**自动**"和 **"从不**"。 默认值为 **"自动**"。当此属性设置为 **"自动"** 的值时，视图状态被加密是控件通过调用**注册需求视点状态加密**方法请求它。

## <a name="setting-public-property-values-via-the--page-directive"></a>通过 @ 页面指令设置公共财产值

ASP.NET 2.0 中 @ Page 指令的另一个新功能是设置基类公共属性的初始值的能力。 例如，假设您的基类中具有名为 **"SomeText"** 的公共属性，并且您希望在加载页面时将其初始化为**Hello。** 只需在 @ Page 指令中设置值即可实现此目的：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@Page 指令的 **"一些文本"** 属性将基类中的"SomeText"属性的初始值设置为*Hello！*。 以下视频是使用 @ Page 指令设置基类中公共属性的初始值的演练。

![](the-asp-net-2-0-page-model/_static/image1.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>页面类的新公共属性

以下公共属性是 ASP.NET 2.0 中的新属性。

## <a name="apprelativetemplatesourcedirectory"></a>应用相关模板源目录

返回与应用程序相关的路径到页面或控件。 例如，对于 位于 的http://app/folder/page.aspx页面，属性返回 */文件夹/。

## <a name="apprelativevirtualpath"></a>应用相对虚拟路径

将相对虚拟目录路径返回到页面或控件。 例如，对于 位于 的http://app/folder/page.aspx页面，属性返回 */文件夹/页.aspx。

## <a name="asynctimeout"></a>同步超时

获取或设置用于异步页面处理的超时。 （此模块稍后将介绍异步页面。

## <a name="clientquerystring"></a>客户端查询字符串

返回请求 URL 的查询字符串部分的只读属性。 此值是 URL 编码的。 您可以使用 HttpServer 实用程序类的 Url 解码方法对其进行解码。

## <a name="clientscript"></a>客户端脚本

此属性返回一个客户端ScriptManager对象，该对象可用于管理客户端脚本的 ASP.NET 发射。 （本模块稍后将介绍客户端脚本管理器类。

## <a name="enableeventvalidation"></a>启用事件验证

此属性控制是否为回退和回调事件启用事件验证。 启用后，将验证用于回退或回调事件的参数，以确保它们源自最初呈现这些事件的服务器控件。

## <a name="enabletheming"></a>启用"启用"

此属性获取或设置布尔，用于指定 ASP.NET 2.0 主题是否应用于页面。

## <a name="form"></a>Form

此属性将 ASPX 页上的 HTML 窗体作为 HtmlForm 对象返回。

## <a name="header"></a>标头

此属性返回对包含页面标题的 HtmlHead 对象的引用。 您可以使用返回的 HtmlHead 对象获取/设置样式表、元标记等。

## <a name="idseparator"></a>IdSe参数

当ASP.NET为页面上的控件构建唯一 ID 时，此只读属性获取用于分隔控件标识符的字符。 它不可直接通过代码使用。

## <a name="isasync"></a>IsAsync

此属性允许异步页面。 本模块稍后将讨论异步页面。

## <a name="iscallback"></a>IsCallback

如果页面是回电的结果，则此只读属性将**返回 true。** 本模块稍后将讨论回电。

## <a name="iscrosspagepostback"></a>是交叉页面后返回

如果页面是跨页回邮的一部分，则此只读属性将**返回 true。** 本模块稍后将介绍跨页回邮。

## <a name="items"></a>Items

返回对 I字典实例的引用，该实例包含存储在页面上下文中的所有对象。 您可以将项添加到此 I字典对象，它们将在上下文的整个生存期内可供您使用。

## <a name="maintainscrollpositiononpostback"></a>保持滚动位置后回

此属性控制ASP.NET是否发出 JavaScript，该 JavaScript 在回退后在浏览器中维护页面滚动位置。 （本模块前面讨论了此属性的详细信息。

## <a name="master"></a>主设备

此只读属性返回对已应用母版页的页面的 MasterPage 实例的引用。

## <a name="masterpagefile"></a>母版页面文件

获取或设置页面的主页文件名。 此属性只能在 PreInit 方法中设置。

## <a name="maxpagestatefieldlength"></a>最大页面状态长度

此属性获取或设置以字节为单位的页面状态的最大长度。 如果属性设置为正数，则页面视图状态将分解为多个隐藏字段，以便不超过指定的字节数。 如果属性为负数，则视图状态不会分解为块。

## <a name="pageadapter"></a>页面适配器

返回对 PageAdapter 对象的引用，该对象修改请求浏览器的页面。

## <a name="previouspage"></a>上一页

在服务器.传输或跨页回发的情况下返回对上一页的引用。

## <a name="skinid"></a>皮肤ID

指定要应用于页面的ASP.NET 2.0 外观。

## <a name="stylesheettheme"></a>样式表主题

此属性获取或设置应用于页面的样式表。

## <a name="templatecontrol"></a>模板控制

返回对页面的包含控件的引用。

## <a name="theme"></a>主题

获取或设置应用于页面的ASP.NET 2.0 主题的名称。 此值必须在 PreInit 方法之前设置。

## <a name="title"></a>标题

此属性获取或设置从页眉获取的页面的标题。

## <a name="viewstateencryptionmode"></a>查看状态加密模式

获取或设置页面的 ViewState 加密模式。 在本模块前面查看对此属性的详细讨论。

## <a name="new-protected-properties-of-the-page-class"></a>页面类的新受保护属性

以下是 ASP.NET 2.0 中 Page 类的新受保护属性。

## <a name="adapter"></a>适配器

返回对在请求该页面的设备上呈现该页的 ControlAdapter 的引用。

## <a name="asyncmode"></a>异步模式

此属性指示页面是否异步处理。 它供运行时使用，而不是直接在代码中使用。

## <a name="clientidseparator"></a>客户端 ID 分离器

此属性返回在为控件创建唯一客户端 ID 时用作分隔符的字符。 它供运行时使用，而不是直接在代码中使用。

## <a name="pagestatepersister"></a>佩奇·邦斯特

此属性返回页面的 PageStatePersister 对象。 此属性主要由ASP.NET控件开发人员使用。

## <a name="uniquefilepathsuffix"></a>唯一的文件路径修复

此属性返回一个唯一的后缀，该后缀追加到缓存浏览器的文件路径上。 默认值为\_\_ufps* 和 6 位数字。

## <a name="new-public-methods-for-the-page-class"></a>页面类的新公共方法

以下公共方法是 ASP.NET 2.0 中的 Page 类的新增方法。

## <a name="addonprerendercompleteasync"></a>附加预渲染完成同步

此方法注册事件处理程序委托以进行异步页面执行。 本模块稍后将讨论异步页面。

## <a name="applystylesheetskin"></a>应用样式表外观

将页面样式表中的属性应用于页面。

## <a name="executeregisteredasynctasks"></a>执行已注册的同步任务

此方法是异步任务。

### <a name="getvalidators"></a>获取验证器

如果未指定任何验证组或默认验证组，则返回验证器的集合。

## <a name="registerasynctask"></a>注册同步任务

此方法注册新的异步任务。 本模块稍后将介绍异步页面。

## <a name="registerrequirescontrolstate"></a>注册需要控制状态

此方法告诉ASP.NET必须保留页面控件状态。

## <a name="registerrequiresviewstateencryption"></a>注册需要查看状态加密

此方法告诉ASP.NET页面视图状态需要加密。

## <a name="resolveclienturl"></a>解析客户端

返回可用于图像等客户端请求的相对 URL。

## <a name="setfocus"></a>SetFocus

此方法将焦点设置为最初加载页面时指定的控件。

## <a name="unregisterrequirescontrolstate"></a>取消注册需要控制状态

此方法将取消注册传递给它的控件，因为不再需要控件状态持久性。

## <a name="changes-to-the-page-lifecycle"></a>对页面生命周期的更改

ASP.NET 2.0 中的页面生命周期没有显著变化，但您应该知道一些新方法。 下面概述了ASP.NET 2.0 页生命周期。

## <a name="preinit-new-in-aspnet-20"></a>PreInit（ASP.NET 2.0 中的新增功能）

PreInit 事件是开发人员可以访问的生命周期中最早的阶段。 通过添加此事件，可以以编程方式更改ASP.NET 2.0 主题、母版页、ASP.NET 2.0 配置文件的访问属性等。如果您处于后回状态，则实现 Viewstate 尚未应用于生命周期的此时控件非常重要。 因此，如果开发人员在此阶段更改控件的属性，则在页面生命周期的稍后版本中可能会覆盖该控件的属性。

## <a name="init"></a>Init

Init 事件未从 ASP.NET 1.x 更改。 这是您希望读取或初始化页面上控件属性的位置。 在此阶段，母版页、主题等已应用于该页。

## <a name="initcomplete-new-in-20"></a>InitComplete（2.0 中新增）

InitComplete 事件在页面初始化阶段结束时调用。 在生命周期的此时，可以访问页面上的控件，但尚未填充其状态。

## <a name="preload-new-in-20"></a>预加载（2.0 中新增）

此事件是在应用所有回邮数据后，并在页面\_加载之前调用的。

## <a name="load"></a>加载

加载事件未从 ASP.NET 1.x 更改。

## <a name="loadcomplete-new-in-20"></a>加载完成（2.0 中新增）

LoadComplete 事件是页面加载阶段的最后一个事件。 在此阶段，所有回退和视图状态数据已应用于页面。

## <a name="prerender"></a>预渲染

如果希望对动态添加到页面的控件正确维护视图状态，则 PreRender 事件是添加它们的最后机会。

## <a name="prerendercomplete-new-in-20"></a>预渲染完成（2.0 中新增）

在预渲染完成阶段，所有控件都已添加到页面，并且页面已准备好呈现。 预渲染完成事件是保存页面视图状态之前引发的最后一个事件。

## <a name="savestatecomplete-new-in-20"></a>保存状态完成（2.0 中的新增功能）

保存所有页面视图状态和控制状态后，将立即调用"保存状态完成"事件。 这是页面实际呈现到浏览器之前的最后一个事件。

## <a name="render"></a>呈现

自 1.x ASP.NET以来，渲染方法未更改。 这是 HtmlTextWriter 初始化并将页面呈现到浏览器的位置。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 中的跨页回邮

在ASP.NET 1.x 中，需要回邮后贴到同一页。 不允许进行跨页回邮。 ASP.NET 2.0 添加了通过 IButtonControl 界面发回其他页面的功能。 实现新的 IButtonControl 界面的任何控件（除了第三方自定义控件之外，还可以利用此新功能，使用 PostBackUrl 属性。 以下代码显示将回发回第二页的 Button 控件。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

当页面被发回时，启动回邮的页面可通过第二页上的"上页"属性访问。 此功能通过新的 WebForm\_DoPostBackOptions 客户端功能实现，该功能ASP.NET 2.0 在控件回退回其他页面时呈现到页面。 此 JavaScript 函数由向客户端发出脚本的新 WebResource.axd 处理程序提供。

下面的视频是跨页回帖的演练。

![](the-asp-net-2-0-page-model/_static/image2.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>有关跨页回邮的更多详细信息

### <a name="viewstate"></a>视图状态

您可能已经问自己，在跨页回退方案中，从第一页中查看状态会发生什么情况。 毕竟，任何不实现 IPostBackDataHandler 的控件都将通过视图状态保持其状态，因此，要访问跨页后回的第二页上该控件的属性，您必须有权访问该页的视图状态。 ASP.NET 2.0 使用第二页中称为\_\_"上页"的新隐藏字段处理此方案。 "\_\_上一页"窗体字段包含第一页的视图状态，以便您可以访问第二页中所有控件的属性。

### <a name="circumventing-findcontrol"></a>绕过查找控制

在跨页回发的视频演练中，我使用 FindControl 方法获取对第一页上的 TextBox 控件的引用。 该方法适用于此目的，但 FindControl 成本高昂，需要编写其他代码。 幸运的是，ASP.NET 2.0 为此提供了 FindControl 的替代方法，这在很多方案中都不起作用。 使用"上一页类型"指令允许您使用 TypeName 或 VirtualPath 属性对上一页进行强类型引用。 TypeName 属性允许您指定上一页的类型，而 VirtualPath 属性允许您使用虚拟路径引用上一页。 设置上一页类型指令后，必须公开要允许使用公共属性访问的控件等。

## <a name="lab-1-cross-page-postback"></a>实验室 1 跨页回邮

在本实验中，您将创建一个应用程序，该应用程序使用 ASP.NET 2.0 的新跨页回邮功能。

1. 打开 Visual Studio 2005 并创建新ASP.NET网站。
2. 添加新的 Web 表单，称为页 2.aspx。
3. 在"设计"视图中打开默认.aspx 并添加按钮控件和 TextBox 控件。 

    1. 为按钮控件指定 **"提交按钮**"的 ID，而文本框控件为**用户名**ID。
    2. 将按钮的 PostBackUrl 属性设置为页 2.aspx。
4. 在源视图中打开页面 2.aspx。
5. 添加 # 上一页类型指令，如下所示：
6. 将以下代码添加到页 2.aspx 的代码后面的页面\_加载： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 单击"生成"菜单上的"生成"菜单生成项目。
8. 将以下代码添加到 Default.aspx 的代码后面： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 将页\_2.aspx 中的页面加载更改为以下内容： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 生成项目。
11. 运行该项目。
12. 在文本框中输入您的姓名，然后单击该按钮。
13. 结果如何？

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 中的异步页面

ASP.NET中的许多争用问题是由外部调用（如 Web 服务或数据库调用）的延迟、文件 IO 延迟等引起的。当针对ASP.NET应用程序发出请求时，ASP.NET使用其工作线程之一来为该请求提供服务。 该请求拥有该线程，直到请求完成并发送响应。 ASP.NET 2.0 寻求通过添加异步执行页面的功能来解决此类问题的延迟问题。 这意味着工作线程可以启动请求，然后将其他执行交给另一个线程，从而快速返回到可用的线程池。 当文件 IO、数据库调用等完成时，将从线程池获取一个新线程以完成请求。

使页面异步执行的第一步是设置页面指令的**Async**属性，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

此属性告诉ASP.NET实现页面的 IHttpAsyncHandler。

下一步是在预渲染之前在页面生命周期的某一点调用 AddOnPreRenderCompleteAsync 方法。 （此方法通常在页面\_加载中调用。AddOnPreRenderCompleteasync方法采用两个参数;a BeginEventHandler 和 endEventHandler。 BeginEventHandler 返回一个 IAsyncResult，然后将该结果作为参数传递给 EndEventHandler。

下面的视频是异步页面请求的演练。

![](the-asp-net-2-0-page-model/_static/image3.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> 在结束事件处理程序完成之前，异步页面不会呈现给浏览器。 毫无疑问，但一些开发人员会认为异步请求类似于异步回调。 重要的是要意识到他们不是。 异步请求的好处是，可以将第一个辅助线程返回到线程池以服务新请求，从而减少由于受 IO 绑定等原因引起的争用。

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 中的脚本回调

Web 开发人员一直在寻找防止与回调关联的闪烁的方法。 在 ASP.NET 1.x 中，智能导航是避免闪烁的最常见方法，但智能导航由于在客户端上实现的复杂性而给一些开发人员带来了问题。 ASP.NET 2.0 使用脚本回调解决此问题。 脚本回调利用 XMLHttp 通过 JavaScript 对 Web 服务器发出请求。 XMLHttp 请求返回 XML 数据，然后可以通过浏览器的 DOM 进行操作。 XMLHttp 代码由新的 WebResource.axd 处理程序对用户隐藏。

为了在 2.0 ASP.NET配置脚本回调，需要执行几个步骤。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>步骤 1 ： 实现 IcallbackEventHandler 接口

为了ASP.NET识别您的页面参与脚本回调，必须实现 ICallbackEventHandler 接口。 您可以在代码后面的文件中执行此操作，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

您还可以使用 # 实现指令执行此操作，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

在使用内联ASP.NET代码时，通常可以使用 @ 实现指令。

## <a name="step-2--call-getcallbackeventreference"></a>第 2 步 ： 调用返回事件引用

如前所述，XMLHttp 调用封装在 WebResource.axd 处理程序中。 呈现页面时，ASP.NET将添加对 WebForm DoCallback\_的调用，WebForm DoCallback 是 WebResource.axd 提供的客户端脚本。 WebForm\_DoCallback 函数将替换\_\_回调的 doPostBack 函数。 请记住，\_\_以编程方式提交页面上的表单。 在回调方案中，您希望防止回退，因此\_\_PostBack 是不够的。

> [!NOTE]
> \_\_doPostBack 仍呈现在客户端脚本回调方案中的页面。 但是，它不用于回调。

WebForm\_DoCallback 客户端函数的参数通过服务器端函数 GetCallbackEventReference 提供，该函数通常在页面\_加载中调用。 对 GetbackEvent 参考的典型调用可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 在这种情况下，cm 是客户端脚本管理器的实例。 本模块稍后将介绍客户端脚本管理器类。

有几个重载版本的 GetbackEvent 参考。 在这种情况下，参数如下所示：

`this`

对调用 GetbackEvent参照的控件的引用。 在这种情况下，它是页面本身。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

将从客户端代码传递到服务器端事件的字符串参数。 在这种情况下，我传递名为 ddlCompany 的下拉的值。

`ShowCompanyName`

客户端函数的名称，该函数将接受服务器端回调事件的返回值（作为字符串）。 仅当服务器端回调成功时，才会调用此功能。 因此，为了鲁棒性，通常建议使用重载版本的 GetCallbackEventReference，该版本需要一个额外的字符串参数，指定客户端函数的名称，在发生错误时执行。

`null`

表示在回调到服务器之前启动的客户端函数的字符串。 在这种情况下，没有这样的脚本，因此参数为 null。

`true`

指定是否异步执行回调的布尔。

客户端上对 WebForm\_DoCallback 的调用将传递这些参数。 因此，在客户端上呈现此页面时，该代码将如下所示：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

请注意，客户端上函数的签名有点不同。 客户端函数传递 5 个字符串和一个布尔。 附加字符串（在上例中为空）包含客户端函数，该函数将处理来自服务器端回调的任何错误。

## <a name="step-3--hook-the-client-side-control-event"></a>步骤 3 ： 钩客户端控制事件

请注意，上面 GetCallbackEventReference 的返回值已分配给字符串变量。 该字符串用于钩接启动回调的控件的客户端事件。 在此示例中，回调由页面上的下拉展开，因此我想挂接*OnChange*事件。

要挂接客户端事件，只需将处理程序添加到客户端标记，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

回想一下*cbRef*是从调用 GetbackEvent 参考的返回值。 它包含上面显示的对 WebForm\_DoCallback 的调用。

## <a name="step-4--register-the-client-side-script"></a>步骤 4 ： 注册客户端脚本

回想一下，对 GetCallbackEventReference 的调用指定在服务器端回调成功时将执行名为**ShowCompanyName**的客户端脚本。 需要使用 ClientScriptManager 实例将该脚本添加到页面。 （本模块稍后将讨论客户端脚本管理器类。你这样做，像这样：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>步骤 5 ： 调用 ICallbackEventHandler 接口的方法

ICallbackEventHandler 包含需要在代码中实现的两种方法。 它们是 **"提高回调事件**"和 **"获取回调事件**"。

**RaiseCallbackEvent**将字符串作为参数，不返回任何内容。 字符串参数从客户端调用传递到 WebForm\_DoCallback。 在这种情况下，该值是名为 ddlCompany 的下拉*的值*属性。 服务器端代码应放在"提高回调事件"方法中。 例如，如果您的回调针对外部资源发出 Web 请求，则应将该代码放在"提高回调事件"中。

**GetCallbackEvent**负责处理回调返回给客户端的问题。 它不需要参数并返回字符串。 它返回的字符串将作为参数传递给客户端函数，在本例中*为 ShowCompanyName*。

完成上述步骤后，即可在 2.0 ASP.NET执行脚本回调。

![](the-asp-net-2-0-page-model/_static/image4.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET脚本回调在支持进行 XMLHttp 调用的任何浏览器中都受支持。 这包括当今使用的所有现代浏览器。 Internet Explorer 使用 XMLHttp ActiveX 对象，而其他现代浏览器（包括即将推出的 IE 7）使用内部 XMLHttp 对象。 要以编程方式确定浏览器是否支持回调，可以使用 **"请求.Browser.支持回拨"** 属性。 如果请求的客户端支持脚本回调，则此属性将返回**true。**

## <a name="working-with-client-script-in-aspnet-20"></a>在 ASP.NET 2.0 中使用客户端脚本

ASP.NET 2.0 中的客户端脚本是使用客户端脚本管理器类管理的。 客户端脚本管理器类使用类型和名称跟踪客户端脚本。 这样可以防止同一脚本多次以编程方式插入到页面上。

> [!NOTE]
> 在页面上成功注册脚本后，任何后续注册同一脚本的尝试都将导致脚本无法第二次注册。 不添加重复的脚本，也不会发生异常。 为了避免不必要的计算，可以使用一些方法来确定脚本是否已注册，以便不要尝试多次注册脚本。

客户端脚本管理器的方法应对所有当前ASP.NET开发人员都熟悉：

## <a name="registerclientscriptblock"></a>注册客户端脚本块

此方法将脚本添加到呈现页面的顶部。 这对于添加将在客户端上显式调用的函数非常有用。

此方法有两个重载版本。 四个参数中有三个在它们中很常见。 它们分别是：

`type (string)`

***类型***参数标识脚本的类型。 通常最好使用页面的类型（这。获取类型的类型。

`key (string)`

***键***参数是脚本的用户定义的密钥。 对于每个脚本来说，这应该是唯一的。 如果尝试添加具有相同键和已添加脚本类型的脚本，则不会添加该脚本。

`script (string)`

***脚本***参数是包含要添加的实际脚本的字符串。 建议使用 StringBuilder 创建脚本，然后在 StringBuilder 上使用 ToString（） 方法分配***脚本***参数。

如果使用加载的注册客户端脚本块，该参数仅包含三个参数，则必须在脚本中包含脚本元素&lt;（&gt;脚本&lt;和&gt;/脚本）。

您可以选择使用采用第四个参数的注册客户端脚本块的重载。 第四个参数是布尔，它指定ASP.NET是否应该为您添加脚本元素。 如果此参数**为 true，** 则脚本不应显式包含脚本元素。

使用 IsClientScriptBlock 注册方法确定脚本是否已注册。 这允许您避免尝试重新注册已注册的脚本。

### <a name="registerclientscriptinclude-new-in-20"></a>注册客户端脚本包括（2.0 中的新增功能）

注册客户端脚本包含标记创建链接到外部脚本文件的脚本块。 它有两个过载。 一个需要一个键和一个URL。 第二个参数添加第三个参数，指定类型。

例如，以下代码生成一个脚本块，该脚本块链接到应用程序脚本文件夹的根目录中的 js 函数.js：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

此代码在呈现的页面中生成以下代码：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 脚本块呈现在页面底部。

使用 IsClientScript 包括注册方法确定脚本是否已注册。 这允许您避免尝试重新注册脚本。

## <a name="registerstartupscript"></a>注册启动脚本

注册启动脚本方法采用与注册客户端脚本块方法相同的参数。 注册到注册启动脚本的脚本在页面加载后在 OnLoad 客户端事件之前执行。 在 1.X 中，注册到的&lt;脚本位于关闭 /窗体&gt;标记之前，而注册到 RegisterClientScriptBlock 的脚本则紧随打开&lt;表单&gt;标记之后放置。 在 ASP.NET 2.0 中，两者都放在&lt;关闭&gt;/窗体标记之前。

> [!NOTE]
> 如果向注册启动脚本注册函数，则在客户端代码中显式调用该函数之前，该函数不会执行。

使用 IsStartupScript 注册方法确定脚本是否已注册，并避免尝试重新注册脚本。

## <a name="other-clientscriptmanager-methods"></a>其他客户端脚本管理器方法

下面是客户端ScriptManager 类的其他一些有用方法。

|  <strong>获取回拨事件引用</strong>   |                                                 请参阅本模块前面的脚本回调。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>获取后回客户端超链接</strong>  |                获取可用于从客户端事件发回的 JavaScript 引用（javascript：&lt;调用&gt;）。                 |
|  <strong>获取后回活动参考</strong>   |                                   获取可用于从客户端发起回帖子的字符串。                                    |
|      <strong>获取Web资源Url</strong>       | 返回嵌入在程序集中的资源的 URL。 必须与<strong>注册客户端脚本资源</strong>结合使用。 |
| <strong>注册客户端脚本资源</strong> |     将 Web 资源注册到该页。 这些资源嵌入到程序集中并由新的 WebResource.axd 处理程序处理。      |
|     <strong>注册隐藏字段</strong>      |                                                 将隐藏的表单字段与页面注册。                                                 |
|  <strong>注册提交声明</strong>   |                                  注册提交 HTML 窗体时执行的客户端代码。                                   |

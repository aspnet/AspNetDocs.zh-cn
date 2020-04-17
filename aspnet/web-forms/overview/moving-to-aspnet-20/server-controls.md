---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控制 |微软文档
author: rick-anderson
description: ASP.NET 2.0 在许多方面增强了服务器控件。 在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 200 的方式的一些体系结构更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543738"
---
# <a name="server-controls"></a>服务器控件

由[微软](https://github.com/microsoft)

> ASP.NET 2.0 在许多方面增强了服务器控件。 在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。

ASP.NET 2.0 在许多方面增强了服务器控件。 在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。

## <a name="view-state"></a>查看状态

ASP.NET 2.0 中视图状态的主要变化是大小显著减小。 考虑一个只有"日历"控件的页面。 下面是ASP.NET 1.1 中的视图状态。

[!code-css[Main](server-controls/samples/sample1.css)]

现在，下面是ASP.NET 2.0 中相同页面上的视图状态。

[!code-css[Main](server-controls/samples/sample2.css)]

这是一个相当重大的变化，考虑到视图状态在线上来回移动，此更改可以显著提高开发人员的性能。 视图状态大小的减小主要是由于我们在内部处理它的方式。 请记住，视图状态是 Base64 编码字符串。 为了更好地了解 ASP.NET 2.0 中视图状态的变化，让我们从上面的示例中查看解码的值。

下面是已解码的 1.1 视图状态：

[!code-css[Main](server-controls/samples/sample3.css)]

这可能看起来有点胡言乱语，但这里有一个模式。 在ASP.NET 1.x 中，我们使用单个字符来标识&lt;&gt;数据类型并使用字符分隔值。 上面的视图状态示例中的"t"表示三重。 三重列表包含一对数组列表（"l"表示数组列表）。其中一个数组列表包含一个 Int32 （"i"），其值为 1，另一个包含另一个 Triplet。 三重包含一对数组列表等。需要记住的重要的事情是，我们使用包含对的三脚架，我们通过字母识别数据类型，并使用 和&lt;&gt;字符作为分隔符。

在ASP.NET 2.0 中，解码的视图状态看起来有点不同。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

您应该注意到解码视图状态的外观发生巨大变化。 此更改具有多个体系结构基础。 ASP.NET 1.x 中的视图状态使用 LosFormatter 对数据进行序列化。 在 2.0 中，我们使用新的 ObjectStateFormatter 类。 此类是专门为帮助视图状态和控制状态的序列化和反序列化而设计的。 （下一节将介绍控制状态。通过改变序列化和反序列化的方法，可以带来许多好处。 其中最戏剧性的是，与使用文本Writer的LosFormatter不同，ObjectStateFormatter使用二进制写入器。 这允许ASP.NET 2.0 存储一系列字节而不是字符串的视图状态。 以整数为例。 在ASP.NET 1.1 中，整数需要 4 个字节的视图状态。 在ASP.NET 2.0 中，相同的整数只需要 1 个字节。 进行了其他增强，以减少存储的视图状态量。 例如，DateTime 值现在使用 TickCount 而不是字符串进行存储。

似乎所有这一切还不够，特别注意的是，在 1.x 中，视图状态的最大使用者之一是 DataGrid 和类似的控件。 控件（如视图状态所在的 DataGrid）的一个主要缺点是，它通常包含大量重复的信息。 在ASP.NET 1.x 中，重复的信息只是一遍又一遍地存储，导致视图状态膨胀。 在 ASP.NET 2.0 中，我们使用新的 IndexedString 类来存储此类数据。 如果字符串重复，我们只需将索引String 和索引的令牌存储在索引String 对象的运行表中。

## <a name="control-state"></a>控制状态

开发人员对视图状态的主要抱怨之一是它添加到 HTTP 负载的大小。 如前所述，视图状态的最大使用者之一是 DataGrid 控件。 为了避免 DataGrid 生成的大量视图状态，许多开发人员只是禁用该控件的视图状态。 不幸的是，这个解决方案并不总是一个好的。 ASP.NET 1.x 中的视图状态不仅包含控件正确功能所需的数据。 它还包含有关控件 UI 的状态的信息。 这意味着，如果要允许在 DataGrid 上进行分页，则必须启用视图状态，即使您不需要视图状态包含的所有 UI 信息也是如此。 这是一个全有或全无的情况。

在ASP.NET 2.0 中，控制状态通过引入控制状态很好地解决了该问题。 控件状态包含控件正确功能绝对必要的数据。 与视图状态不同，无法禁用控件状态。 因此，必须严格控制存储在受控状态的数据。

> [!NOTE]
> 控件状态与\_\_"视图状态隐藏窗体"字段中的视图状态一起保留。

此视频是视图状态和控制状态的演练。

![](server-controls/_static/image1.png)

[打开全屏视频](server-controls/_static/state1.wmv)

为了使服务器控件读取和写入以控制状态，必须执行三个步骤。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>第 1 步：调用寄存器需求控制状态方法

注册需求控制状态方法ASP.NET通知控件需要保持控制状态。 它采用类型控制（即正在注册的控件）的一个参数。

请务必注意，注册不会从请求持续到请求。 因此，如果控件要保留控制状态，则必须在每个请求上调用此方法。 建议在 OnInit 中调用该方法。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>第 2 步：重写保存控制状态

自上次回帖以来，SaveControlState 方法保存控件的控制状态更改。 它返回表示控件状态的对象。

## <a name="step-3-override-loadcontrolstate"></a>步骤 3：覆盖负载控制状态

LoadControlState 方法将保存的状态加载到控件中。 该方法采用一种类型 Object 的参数，该参数保存控件的保存状态。

## <a name="full-xhtml-compliance"></a>完全 XHTML 合规性

任何 Web 开发人员都知道标准在 Web 应用程序中的重要性。 为了维护基于标准的开发环境，ASP.NET 2.0 完全符合 XHTML 标准。 因此，所有标记都根据支持 HTML 4.0 或更高程度的浏览器中的 XHTML 标准进行呈现。

ASP.NET 1.1 中的 DOCTYPE 定义如下：

[!code-html[Main](server-controls/samples/sample6.html)]

在 ASP.NET 2.0 中，默认的 DOCTYPE 定义如下所示：

[!code-html[Main](server-controls/samples/sample7.html)]

如果选择，您可以通过配置文件中的 xhtml 一致性节点更改默认 XHTML 合规性。 例如，Web.config 文件中的以下节点将 XHTML 符合性更改为 XHTML 1.0 严格：

[!code-xml[Main](server-controls/samples/sample8.xml)]

如果选择，还可以配置ASP.NET以使用 ASP.NET 1.x 中使用的旧配置，如下所示：

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>使用适配器进行自适应渲染

在 ASP.NET 1.x 中，配置文件&lt;包含填充&gt;HttpBrowser 功能对象的浏览器Cap 节。 此对象允许开发人员确定正在发出特定请求的设备并适当地呈现代码。 在 ASP.NET 2.0 中，模型已改进，现在使用新的 ControlAdapter 类。 ControlAdapter 类覆盖控件生命周期中的事件，并控制基于用户代理功能的控件的呈现。 特定用户代理的功能由存储在 c：_windows_microsoft.net_framework_v2.0 中的浏览器定义文件（具有 .browser 文件扩展名的文件）定义。\* \* \*[CONFIG]浏览器\*文件夹。

> [!NOTE]
> ControlAdapter 类是一个抽象类。

与 1.x 中的&lt;浏览器Cap&gt;节类似，浏览器定义文件使用正则表达式来分析用户代理字符串以标识请求的浏览器。 它们定义该用户代理的特定功能。 控件适配器通过渲染方法呈现控件。 因此，如果重写 Render 方法，则不应在基类上调用 Render。 这样做可能会导致渲染发生两次，一次用于适配器，一次用于控件本身。

## <a name="developing-a-custom-adapter"></a>开发自定义适配器

您可以通过从 ControlAdapter 继承来开发自己的自定义适配器。 此外，在页面需要适配器的情况下，可以从抽象类 PageAdapter 继承。 控件映射到自定义适配器是通过浏览器定义文件中的&lt;控件适配器&gt;元素完成的。 例如，浏览器定义文件中的以下 XML 将菜单控件映射到 MenuAdapter 类：

[!code-html[Main](server-controls/samples/sample10.html)]

使用此模型，控件开发人员很容易定位特定设备或浏览器。 对于开发人员来说，完全控制每个设备上的页面呈现方式也非常简单。

## <a name="per-device-rendering"></a>每设备渲染

ASP.NET 2.0 中的服务器控件属性可以使用特定于浏览器的前缀按设备指定。 例如，下面的代码将更改标签的文本，具体取决于用于浏览页面的设备。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

当包含此标签的页面从 Internet Explorer 浏览时，标签将显示文本，上面写着"您正在从 Internet 资源管理器浏览"。 当从 Firefox 浏览页面时，标签将显示文本"您正在从 Firefox 浏览"。 从任何其他设备浏览页面时，将显示"您正在从未知设备浏览"。 可以使用此特殊语法指定任何属性。

## <a name="setting-focus"></a>设置焦点

ASP.NET 1.x 开发人员经常询问如何将初始焦点放在特定控件上。 例如，在登录页上，让用户 ID 文本框在页面首次加载时获取焦点非常有用。 在ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。 尽管此类脚本是一项琐碎的任务，但由于 SetFocus 方法，ASP.NET 2.0 中不再需要它。 SetFocus 方法采用一个参数，指示应接收焦点的控件。 此参数可以是控件的客户端 ID 作为字符串，也可以是 Server 控件的名称作为控件对象。 例如，要将初始焦点设置为页面首次加载时称为 txtUserID 的 TextBox 控件，请向页面\_加载添加以下代码：

[!code-csharp[Main](server-controls/samples/sample12.cs)]

- 或

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 使用 Webresource.axd 处理程序（前面讨论）来呈现设置焦点的客户端函数。 客户端函数的名称是 WebForm\_自动焦点，如下所示：

[!code-html[Main](server-controls/samples/sample14.html)]

或者，可以使用控件的 Focus 方法将初始焦点设置为该控件。 Focus 方法派生自 Control 类，可用于所有ASP.NET 2.0 控件。 当发生验证错误时，还可以将焦点设置为特定控件。 稍后将介绍这一点。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 中的新服务器控件

以下是 ASP.NET 2.0 中的新服务器控件。 我们将在后面的模块中更详细地介绍其中一些内容。

## <a name="imagemap-control"></a>图像映射控件

ImageMap 控件允许您向图像添加热点，该图像可以启动帖子或导航到 URL。 有三种类型的热点可用;圆热点、矩形热点和多边形热点。 热点通过 Visual Studio 中的集合编辑器添加，或在代码中以编程方式添加。 没有可用于在图像上绘制热点的用户界面。 必须声明性地指定热点的坐标、大小或半径。 设计器中也没有热点的可视表示形式。 如果热点配置为导航到 URL，则 URL 将通过热点的 NavigateUrl 属性指定。 在后回热点的情况下，PostBackValue 属性允许您传递后回的字符串，该字符串可以在服务器端代码中检索。

![可视化工作室中的热点集合编辑器](server-controls/_static/image1.jpg)

**图 1**： 可视化工作室中的热点集合编辑器

## <a name="bulletedlist-control"></a>项目符号列表控制

"项目符号列表"控件是一个项目符号列表，可以轻松绑定数据。 列表可以通过"项目符号样式"属性排序（编号）或无序排序。 列表中的每个项都由 ListItem 对象表示。

![可视化工作室中的项目符号列表控制](server-controls/_static/image1.gif)

**图 2**： 可视化工作室中的项目列表控制

## <a name="hiddenfield-control"></a>隐藏字段控制

HiddenField 控件向页面添加隐藏表单字段，其值在服务器端代码中可用。 隐藏窗体字段的值通常预计在后背之间保持不变。 但是，恶意用户可能会在回发布之前更改该值。 如果发生这种情况，"隐藏字段"控件将引发"值更改"事件。 如果在 HiddenField 控件中具有敏感信息，并且希望确保信息保持不变，则应在代码中处理 Value"更改"事件。

## <a name="fileupload-control"></a>文件上传控制

ASP.NET 2.0 中的 FileUpload 控件使得可以通过ASP.NET页面将文件上载到 Web 服务器成为可能。 此控件与 ASP.NET 1.x HtmlInputFile 类非常相似，但有一些例外。 在 ASP.NET 1.x 中，建议将"已发布文件"属性检查为 null，以确定您是否具有良好的文件。 ASP.NET 2.0 中的 FileUpload 控件添加了一个新的 HasFile 属性，您可以将其用于同一目的，并且效率更高一些。

已发布文件属性仍可用于访问 HttpPostedFile 对象，但 HttpPostedFile 的某些功能现在可通过 FileUpload 控件在本质上可用。 例如，要将上载的文件保存在 ASP.NET 1.x 中，请调用 HttpPostedFile 对象上的 SaveAs 方法。 使用 ASP.NET 2.0 中的 FileUpload 控件，您将在 FileUpload 控件本身上调用 SaveAs 方法。

2.0 行为（可能是最重要的更改）的另一个重要变化是，在保存整个上载的文件之前，不再需要将整个上载的文件加载到内存中。 在 1.x 中，上载的任何文件在写入磁盘之前都完全保存到内存中。 此体系结构可防止上载大型文件。

在 ASP.NET 2.0 中，httpRuntime 元素的请求长度磁盘阈值属性允许您配置在写入磁盘之前在内存中存储缓冲区中的数量。

**重要提示**：MSDN 文档（和其他地方的文档）指定此值以字节为单位（不是千字节），默认值为 256。 该值实际上以千字节为单位指定，默认值为 80。 通过默认值 80K，我们确保缓冲区不会最终位于大型对象堆上。

## <a name="wizard-control"></a>向导控制

遇到ASP.NET开发人员在尝试使用面板在一系列"页面"中收集信息或从一个页面传输到一个页面时遇到这样的常见情况。 很多时候，这种努力是令人沮丧的，而且非常耗时。 新的向导控件通过在用户熟悉的向导界面中允许线性和非线性步骤来解决问题。 向导控件以一系列步骤显示输入窗体。 每个步骤都是控件的 StepType 属性指定的特定类型。 可用的步骤类型如下：

| **步长类型** | **说明** |
| --- | --- |
| 自动 | 向导根据步骤层次结构中的位置自动确定步骤的类型。 |
| 开始 | 第一步，通常用于提出介绍性陈述。 |
| 步骤 | 正常步骤。 |
| 完成 | 最后一步，通常用于显示一个按钮来完成向导。 |
| 完成 | 显示传达成功或失败的信息。 |

> [!NOTE]
> 向导控件使用ASP.NET控制状态跟踪其状态。 因此，启用视图状态属性可以设置为 false，而不会造成任何损害。

此视频是向导控件的演练。

![](server-controls/_static/image2.png)

[打开全屏视频](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>本地化控制

本地化控件类似于文本控件。 但是，本地化控件具有一个**Mode**属性，用于控制如何向其添加标记。 Mode 属性支持以下值：

| **模式** | **说明** |
| --- | --- |
| 转换 | 标记根据发出请求的浏览器的协议进行转换。 |
| 直通 | 标记将呈现为"正样"。 |
| 编码 | 添加到控件的标记使用 HtmlEncode 进行编码。 |

## <a name="multiview-and-view-controls"></a>多视图和视图控件

MultiView 控件充当视图控件的容器，视图控件充当其他控件的容器（与面板控件类似）。 MultiView 控件中的每个视图都由单个视图控件表示。 MultiView 中的第一个视图控件是视图 0，第二个视图 1 等。您可以通过指定 MultiView 控件的 ActiveViewIndex 来切换视图。

## <a name="substitution-control"></a>替代控制

替换控件与ASP.NET缓存一起使用。 如果要利用缓存，但具有必须在每个请求上更新页面的某些部分（换句话说，免除缓存的页面部分），则替换组件提供了一个很好的解决方案。 控件实际上不会自行呈现任何输出。 相反，它绑定到服务器端代码中的方法。 请求页面时，将调用该方法，并呈现返回的标记来代替替换控件。

通过**MethodName**属性指定替换控件绑定到的方法。 该方法必须满足以下条件：

- 它必须是静态（在 VB 中共享）方法。
- 它接受 HttpContext 类型的一个参数。
- 它返回一个字符串，表示应替换页面上的控件的标记。

替换控件无法修改页面上的任何其他控件，但它确实可以通过其参数访问当前 HttpContext。

## <a name="gridview-control"></a>网格视图控制

GridView 控件是 DataGrid 控件的替换。 此控件将在后面的模块中更详细地介绍。

## <a name="detailsview-control"></a>详细信息查看控件

"详细信息视图"控件允许您从数据源显示单个记录，并对其进行编辑或删除。 在后面的模块中更详细地介绍它。

## <a name="formview-control"></a>窗体视图控件

FormView 控件用于在可配置的界面中显示来自数据源的单个记录。 在后面的模块中更详细地介绍它。

## <a name="accessdatasource-control"></a>访问数据源控制

AccessDataSource 控件用于数据绑定 Access 数据库。 在后面的模块中更详细地介绍它。

## <a name="objectdatasource-control"></a>对象数据源控制

ObjectDataSource 控件用于支持三层体系结构，以便控件可以将数据绑定到中间层业务对象，而不是控件直接绑定到数据源的双层模型。 稍后将在后面的模块中更详细地讨论它。

## <a name="xmldatasource-control"></a>XmlDataSource 控制

XmlDataSource 控件用于绑定到 XML 数据源的数据。 在后面的模块中更详细地介绍它。

## <a name="sitemapdatasource-control"></a>站点映射数据源控制

SiteMapDataSource 控件基于站点地图为站点导航控件提供数据绑定。 稍后将在后面的模块中更详细地讨论它。

## <a name="sitemappath-control"></a>站点地图路径控制

SiteMapPath 控件显示一系列导航链接，通常称为痕迹。 在后面的模块中更详细地介绍它。

## <a name="menu-control"></a>Menu 控件

"菜单"控件使用 DHTML 显示动态菜单。 在后面的模块中更详细地介绍它。

## <a name="treeview-control"></a>TreeView 控件

TreeView 控件用于显示数据的分层树视图。 在后面的模块中更详细地介绍它。

## <a name="login-control"></a>登录控制

登录控件提供了登录到网站的机制。 在后面的模块中更详细地介绍它。

## <a name="loginview-control"></a>LoginView 控件

登录视图控件允许根据用户的登录状态显示不同的模板。 在后面的模块中更详细地介绍它。

## <a name="passwordrecovery-control"></a>密码恢复控制

密码恢复控件用于检索ASP.NET应用程序的用户忘记的密码。 在后面的模块中更详细地介绍它。

## <a name="loginstatus"></a>LoginStatus

登录状态控件显示用户的登录状态。 在后面的模块中更详细地介绍它。

## <a name="loginname"></a>LoginName

登录名称控件在登录到ASP.NET应用程序后显示用户的用户名。 在后面的模块中更详细地介绍它。

## <a name="createuserwizard"></a>创建用户向导

CreateUserWizard 是一个可配置的向导，它使用户能够创建ASP.NET成员资格帐户，供ASP.NET应用程序使用。 在后面的模块中更详细地介绍它。

## <a name="changepassword"></a>ChangePassword

更改密码控件允许用户更改其ASP.NET应用程序的密码。 在后面的模块中更详细地介绍它。

## <a name="various-webparts"></a>各种 Web 部件

ASP.NET 2.0 船舶与各种 Web 部件。 这些将在后面的模块中详细介绍。

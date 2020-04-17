---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 实现映射方案 |微软文档
author: rick-anderson
description: 步骤 11 演示如何将 AJAX 映射支持集成到我们的 NerdDinner 应用程序中，使正在创建、编辑或查看晚餐的用户能够查看 l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542581"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 实现映射方案

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第11步，该教程演示如何使用mVC 1构建小型但完整的Web应用程序ASP.NET。
> 
> 步骤 11 演示如何将 AJAX 映射支持集成到我们的 NerdDinner 应用程序中，使正在创建、编辑或查看晚餐的用户能够以图形方式查看晚餐的位置。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>神经晚餐第11步：集成AJAX地图

现在，我们将通过集成 AJAX 映射支持，使我们的应用程序在视觉上更加精彩。 这将使创建、编辑或查看晚餐的用户能够以图形方式查看晚餐的位置。

### <a name="creating-a-map-partial-view"></a>创建地图部分视图

我们将在应用程序中的几个位置使用映射功能。 为了保持我们的代码 DRY，我们将将通用映射功能封装在单个部分模板中，我们可以在多个控制器操作和视图中重复使用。 我们将此部分视图命名为"map.ascx"，并在 [Views_Dinners] 目录中创建它。

我们可以通过右键单击"视图\Dinners"目录并选择"添加视图&gt;"菜单命令来创建 map.ascx 部分内容。 我们将视图命名为"Map.ascx"，将其作为部分视图选中，并指示我们将通过一个强类型"Dinner"模型类：

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

当我们单击"添加"按钮时，将创建部分模板。 然后，我们将更新 Map.ascx 文件，以包含以下内容：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一&lt;个&gt;脚本引用指向 Microsoft 虚拟地球 6.2 映射库。 第二&lt;个&gt;脚本引用指向我们即将创建的 map.js 文件，该文件将封装我们常见的 Javascript 映射逻辑。 div &lt;id="theMap"&gt;元素是虚拟地球将用来承载地图的 HTML 容器。

然后，我们有一个&lt;嵌入式&gt;脚本块，其中包含特定于此视图的两个 JavaScript 函数。 第一个函数使用 jQuery 来连接在页面准备好运行客户端脚本时执行的函数。 它调用 LoadMap（） 帮助器函数，我们将在 Map.js 脚本文件中定义该函数以加载虚拟地球地图控件。 第二个函数是回调事件处理程序，该处理程序向标识位置的地图添加引脚。

请注意，如何在客户端脚本块中使用服务器端&lt;%+&gt; % 块来嵌入要映射到 JavaScript 的 Dinner 的纬度和经度。 这是一种有用的技术来输出客户端脚本可以使用的动态值（无需单独的 AJAX 调用服务器即可检索值 ， 使其更快）。 &lt;当视图在服务器上&gt;呈现时，%= % 块将执行 ，因此 HTML 的输出将最终使用嵌入的 JavaScript 值（例如：var 纬度 = 47.64312;）。

### <a name="creating-a-mapjs-utility-library"></a>创建 Map.js 实用程序库

现在，让我们创建 Map.js 文件，可用于封装地图的 JavaScript 功能（并实现上面的 LoadMap 和 LoadPin 方法）。 我们可以通过右键单击项目中的 #Scripts 目录来执行此操作，然后选择"添加新&gt;项目"菜单命令，选择 JScript 项，并将其命名为"Map.js"。

下面是我们将添加到 Map.js 文件的 JavaScript 代码，该代码将与虚拟地球交互以显示我们的地图，并为其添加位置图钉以进行晚餐：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>将地图与创建和编辑窗体集成

现在，我们将 Map 支持与现有的创建和编辑方案集成。 好消息是，这是很容易做到的，并且不需要我们更改任何控制器代码。 由于我们的"创建"和"编辑"视图共享一个通用的"DinnerForm"部分视图来实现晚餐表单 UI，因此我们可以在一个位置添加地图，并同时使用我们的"创建"和"编辑"方案。

我们只需要打开 [Views_Dinners_DinnerForm.ascx 部分视图]并更新它，以包括我们的新地图部分。 下面是添加地图后更新的 DinnerForm 的外观（注意：为了简洁起见，下面代码段省略了 HTML 表单元素）：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上面的 DinnerForm 部分将类型为"DinnerFormViewModel"的对象作为其模型类型（因为它既需要 Dinner 对象，也需要 SelectList 来填充国家/地区的下拉列表）。 我们的地图部分只需要一个类型"Dinner"的对象作为其模型类型，因此当我们渲染地图部分时，我们只传递给 DinnerFormViewModel 的 Dinner 子属性：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我们添加到部分使用的 JavaScript 函数使用 jQuery 将"模糊"事件附加到"地址"HTML 文本框。 您可能听说过当用户单击或选项卡进入文本框时触发的"焦点"事件。 相反，当用户退出文本框时，将触发"模糊"事件。 上述事件处理程序在发生此情况时清除纬度和经度文本框值，然后绘制地图上的新地址位置。 然后，我们在 map.js 文件中定义的回调事件处理程序将使用虚拟地球返回的值更新窗体上的经度和纬度文本框，具体取决于我们提供的地址。

现在，当我们再次运行我们的应用程序，然后单击"主机晚餐"选项卡，我们将看到默认地图显示连同我们的标准晚餐表单元素：

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

当我们键入地址，然后选项卡离开时，地图将动态更新以显示位置，并且事件处理程序将用位置值填充纬度/经度文本框：

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果我们保存新晚餐，然后再次打开它进行编辑，我们会发现在页面加载时显示地图位置：

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次更改地址字段时，地图和纬度/经度坐标都将更新。

现在，地图显示"晚餐"位置，我们还可以将"纬度和经度"窗体字段从可见文本框更改为隐藏元素（因为每次输入地址时，地图都会自动更新它们）。 为此，我们将从使用 Html.TextBox（） HTML 帮助程序切换到使用 Html.Hidden（） 帮助器方法：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

现在，我们的表单更加方便用户，避免显示原始纬度/经度（同时仍将其与数据库中的每个晚餐一起存储）：

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>将地图与详细信息视图集成

现在，我们已经将地图与我们的创建和编辑方案集成，让我们也将其与我们的详细信息方案集成。 我们只需要调用&lt;% Html.Render 部分（"地图"）;"&gt;详细信息"视图中的百分比。

下面是完整详细信息视图的源代码（具有地图集成）的外观：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

现在，当用户导航到 /Dinners/细节/[id] URL 时，他们将看到有关晚餐的详细信息、地图上的晚餐位置（随鼠标悬停在地图上的图钉显示晚餐的标题和地址），并为其提供指向 RSVP 的 AJAX 链接：

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在我们的数据库和存储库中实现位置搜索

为了完成我们的AJAX实现，让我们向应用程序的主页添加一个地图，允许用户以图形方式搜索附近的晚餐。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

我们将首先在数据库和数据存储库层中实施支持，以高效地执行基于位置的 Dinner 半径搜索。 我们可以使用 SQL [2008 的新地理空间功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)来实现这一点，或者我们可以使用 Gary Dryden 在本文中讨论的 SQL 函数方法：Rob [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) Conery 会在这里写关于使用 LINQ 到 SQL 的文章：[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

为了实现此技术，我们将在 Visual Studio 中打开"服务器资源管理器"，选择 NerdDinner 数据库，然后右键单击其下的"函数"子节点，然后选择创建新的"Scalar 值函数"：

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

然后，我们将粘贴到以下距离之间函数中：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

然后，我们将在 SQL Server 中创建一个新的表值函数，我们称之为"最近的晚餐"：

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

此"最近的晚餐"表函数使用距离之间的帮助器功能返回我们提供它的自由经 100 英里内的所有晚餐：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

要调用此函数，我们将首先通过双击我们的 #Model 目录中的 NerdDinner.dbml 文件向 SQL 设计器打开 LINQ：

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

然后，我们将最近 Dinner 和距离之间的函数拖动到 LINQ 到 SQL 设计器，这将导致它们作为 LINQ 上的方法添加到 SQL NerdDinnerDataContext 类：

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

然后，我们可以在我们的 DinnerRepository 类中公开"FindByLocation"查询方法，该方法使用"最近 Dinner"功能返回即将在指定位置 100 英里范围内的晚餐：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>实现基于JSON的AJAX搜索操作方法

现在，我们将实现一个控制器操作方法，该方法利用新的 FindByLocation（） 存储库方法返回可用于填充地图的 Dinner 数据列表。 我们将让此操作方法以 JSON（JavaScript 对象表示法）格式返回 Dinner 数据，以便可以轻松地在客户端上使用 JavaScript 对其进行操作。

为了实现这一点，我们将通过右键单击 \控制器目录并选择"添加控制器&gt;"菜单命令创建新的"SearchController"类。 然后，我们将在新的 SearchController 类中实现"搜索ByLocation"操作方法，如下所示：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 的 SearchByLocation 操作方法在内部调用晚餐存储库上的 FindByLocation 方法，以获取有关附近晚餐的列表。 但是，它不是将 Dinner 对象直接返回给客户端，而是返回 JsonDinner 对象。 JsonDinner 类公开了 Dinner 属性的子集（例如：出于安全原因，它不披露有 RSVP d 的晚餐人员的姓名）。 它还包括一个在晚餐上不存在的 RSVPCount 属性，该属性通过计算与特定晚餐关联的 RSVP 对象数进行动态计算。

然后，我们使用 Controller 基类上的 Json（） 帮助器方法使用基于 JSON 的线格式返回晚餐序列。 JSON 是一种标准文本格式，用于表示简单的数据结构。 下面是从操作方法返回时由 JSON 格式为两个 JsonDinner 对象的列表的示例：

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>使用 jQuery 调用基于 JSON 的 AJAX 方法

现在，我们准备更新 NerdDinner 应用程序的主页，以使用搜索控制器的搜索ByLocation操作方法。 为此，我们将打开 /Views/Home/Index.aspx 视图模板并更新该模板，使其具有文本框、搜索按钮、地图和名为 dinnerList 的&lt;&gt; div 元素：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

然后，我们可以向页面添加两个 JavaScript 函数：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

当页面首次加载时，第一个 JavaScript 函数加载地图。 第二个 JavaScript 函数在搜索按钮上连接了 JavaScript 单击事件处理程序。 按下按钮后，它将调用 FindDinnersGivenLocation（） JavaScript 函数，我们将该函数添加到我们的 Map.js 文件中：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

此查找晚餐给定位置（） 函数调用映射。在虚拟地球控制上查找（）以将其居于输入的位置。 当虚拟地球地图服务返回时，地图。Find（） 方法调用回调UpdateMapDinners回调方法，我们将其作为最后参数传递。

回调UpdateMapDinners（）方法是完成实际工作的地方。 它使用 jQuery 的 $.post（） 帮助器方法对我们的 SearchController 的 SearchByLocation（） 操作方法执行 AJAX 调用 - 传递新居中地图的纬度和经度。 它定义了一个内联函数，将在 $.post（） 帮助器方法完成时调用，并且从 SearchByLocation（） 操作方法返回的 JSON 格式的晚餐结果将使用名为"dinners"的变量传递它。 然后，它在每个返回的晚餐上做一个foron，并使用晚餐的纬度和经度和其他属性在地图上添加新的图钉。 它还在地图右侧的 HTML 晚餐列表中添加了一个晚餐条目。 然后，它会为图钉和 HTML 列表启用悬停事件，以便在用户悬停在它们上时显示有关晚餐的详细信息：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

现在，当我们运行应用程序并访问主页时，我们将显示一张地图。 当我们输入城市名称时，地图将显示附近即将举办的晚宴：

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

悬停在晚餐上将显示有关它的详细信息。

单击气泡中的晚餐标题或在 HTML 列表中的右侧将引导我们前往晚宴 - 然后，我们可以选择 RSVP 进行以下操作：

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>下一步

现在，我们已经实现了 NerdDinner 应用程序的所有应用程序功能。 现在，让我们来看看如何实现自动单元测试。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)

---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 实现映射方案 |Microsoft Docs
author: rick-anderson
description: 步骤11显示了如何将 AJAX 映射支持集成到 NerdDinner 应用程序中，从而允许正在创建、编辑或查看就的用户查看 .。。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 03b3a27d4b761d0417160b95cc6f39a345385065
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044319"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 实现映射方案

由 [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的 ["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md) 的第11步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤11显示了如何将 AJAX 映射支持集成到 NerdDinner 应用程序中，使创建、编辑或查看就的用户能够以图形方式查看晚餐的位置。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 或 [Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 教程中的入门。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner 步骤11：集成 AJAX 地图

接下来，我们将使应用程序更引人注目，因为集成了 AJAX 映射支持。 这将允许创建、编辑或查看就的用户以图形方式查看晚餐的位置。

### <a name="creating-a-map-partial-view"></a>创建地图分部视图

我们将在应用程序中的多个位置使用映射功能。 为了使我们的代码保持干燥，我们将在单个部分模板中封装常见地图功能，可跨多个控制器操作和视图重复使用这些功能。 我们会将此分部视图命名为 "map .ascx"，并在 \Views\Dinners 目录中创建它。

可以通过右键单击 \Views\Dinners 目录，然后选择 "添加 &gt; 视图" 菜单命令来创建映射 .ascx 部分。 我们会将视图命名为 ".Map"，将其作为分部视图进行检查，并指示我们将向其传递强类型 "晚餐" 模型类：

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

单击 "添加" 按钮时，将会创建部分模板。 然后，我们将更新映射 .ascx 文件，使其包含以下内容：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一个 &lt; 脚本 &gt; 引用指向 Microsoft Virtual 地球6.2 映射库。 第二个 &lt; 脚本 &gt; 引用指向稍后将创建的 map.js 文件，这将封装常见的 Javascript 映射逻辑。 &lt;Div id = "theMap" &gt; 元素是 Virtual 地球用来托管地图的 HTML 容器。

然后，将包含一个 &lt; 嵌入 &gt; 的脚本块，其中包含特定于此视图的两个 JavaScript 函数。 第一个函数使用 jQuery 来连接一个函数，该函数在页面准备好运行客户端脚本时执行。 它会调用 LoadMap ( # A1 helper 函数，我们将在 Map.js 脚本文件中定义该函数以加载虚拟的地图控件。 第二个函数是回调事件处理程序，它将 pin 添加到标识位置的映射。

请注意，我们如何使用 &lt; 客户端脚本块中的服务器端% =% &gt; 块嵌入要映射到 JavaScript 中的晚餐的纬度和经度。 这是一项有用的技术，用于输出可由客户端脚本 (使用的动态值，而无需单独的 AJAX 回调服务器来检索值，从而使其更快) 。 &lt; &gt; 当在服务器上呈现视图时，% =% 块将会执行–因此，HTML 的输出将以嵌入的 JavaScript 值结束， (例如： var 纬度 = 47.64312; ) 。

### <a name="creating-a-mapjs-utility-library"></a>创建 Map.js 实用工具库

现在，让我们创建一个 Map.js 文件，该文件可用于封装用于映射的 JavaScript 功能 (并实现上述) 上的 LoadMap 和 LoadPin 方法。 为此，我们可以右键单击项目中的 \Scripts 目录，然后选择 "添加- &gt; 新建项" 菜单命令，选择 JScript 项，并将其命名为 "Map.js"。

下面是要添加到 Map.js 文件中的 JavaScript 代码，该文件将与 Virtual 地球交互，以便为就显示地图并为其添加位置 pin：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>将地图与创建和编辑表单集成

现在，我们会将地图支持与现有的创建和编辑方案相集成。 好消息是，这是非常简单的操作，不需要我们更改任何控制器代码。 由于我们的 "创建" 和 "编辑" 视图共享公共的 "DinnerForm" 分部视图来实现晚餐窗体 UI，因此可以在一个位置添加地图，同时让创建和编辑方案使用该地图。

我们需要做的就是打开 \Views\Dinners\DinnerForm.ascx 分部视图，并将其更新为包含新的映射部分。 下面是已更新的 DinnerForm 在添加地图后的外观 (注意：下面的代码片段中省略了 HTML 窗体元素以便于简洁) ：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上面的 DinnerForm 部分采用类型为 "DinnerFormViewModel" 的对象作为其模型类型 (因为它需要晚餐对象，以及用于填充) 国家/地区的 dropdownlist 的 SelectList。 我们的地图部分只需要一个 "晚餐" 类型的对象作为其模型类型，因此，当我们呈现地图部分时，我们只会将 DinnerFormViewModel 的晚餐子属性传递给它：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我们添加到部分的 JavaScript 函数使用 jQuery 将 "模糊" 事件附加到 "地址" HTML 文本框。 你可能听说过当用户在文本框中单击或选项卡时激发的 "焦点" 事件。 相反，就是用户退出文本框时激发的 "模糊" 事件。 上述事件处理程序会在发生这种情况时清除纬度和经度文本框的值，然后在地图上绘制新地址位置。 然后，在 map.js 文件中定义的回调事件处理程序将使用虚拟地球基于我们提供的地址的值来更新窗体上的经度和纬度文本框。

现在，当我们再次运行应用程序，然后单击 "主机晚餐" 选项卡时，将看到与标准晚餐窗体元素一起显示的默认地图：

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

当我们键入地址，然后按 tab 键时，地图会动态更新以显示位置，并且我们的事件处理程序将使用 location 值填充纬度/经度文本框：

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果我们保存新晚餐，然后再次将其打开进行编辑，则会发现当页面加载时，会显示地图位置：

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次更改地址字段时，地图和纬度/经度坐标都将更新。

现在，地图显示晚餐位置，还可以将 "纬度" 和 "经度" 窗体字段从 "可见" 文本框改为隐藏元素，因为在每次) 输入地址时，地图会自动更新 (。 要执行此操作，我们将使用 Html. TextBox ( # A1 HTML helper 来使用 Html. Hidden ( # A3 帮助器方法：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

现在，我们的窗体更易于用户理解，并避免 (显示原始纬度/经度，同时还会将它们存储在数据库中的每个晚餐中) ：

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>将映射与详细信息视图集成

现在，我们已将地图与我们的创建和编辑方案集成，接下来让我们将其与我们的详细方案相集成。 我们需要做的就是在 &lt; &gt; 详细信息视图中调用% RenderPartial ( "map" ) ;%。

下面是 (与地图集成) 的 "完整详细信息" 视图的源代码：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

现在，当用户导航到/Dinners/Details/[id] URL 时，他们将看到晚餐的详细信息，地图上晚餐的位置 (使用图钉完成后，当悬停在上方时，将显示晚餐的标题和其地址) ，并为其提供一个指向 RSVP 的 AJAX 链接：

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在数据库和存储库中实现位置搜索

若要完成 AJAX 实现，请向应用程序主页添加一个映射，使用户能够以图形方式搜索附近的就。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

首先，我们将在数据库和数据存储库层中实现支持，以便有效地执行基于位置的 radius 搜索就。 我们可以使用 SQL 2008 的新的 [地理空间功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 实现此功能，也可以使用以下文章中所述的用于 DRYDEN 的 sql 函数方法： [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 和 "Conery LINQ to SQL 针对发表"。 [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

若要实现此方法，我们将在 Visual Studio 中打开 "服务器资源管理器"，选择 NerdDinner 数据库，然后右键单击其下的 "函数" 子节点，然后选择创建新的 "标量值函数"：

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

然后，将粘贴到以下 DistanceBetween 函数：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

然后，将在 SQL Server 中创建一个新的表值函数，我们将调用 "NearestDinners"：

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

此 "NearestDinners" 表函数使用 DistanceBetween helper 函数来返回所提供的纬度和经度100英里以内的所有就：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

若要调用此函数，我们首先要打开 LINQ to SQL 设计器，方法是双击 \Models 目录中的 NerdDinner 文件：

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

然后，将 NearestDinners 和 DistanceBetween 函数拖到 LINQ to SQL 设计器，这将导致这些函数作为 LINQ to SQL NerdDinnerDataContext 类的方法添加：

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

然后，可以在 DinnerRepository 类上公开 "FindByLocation" 查询方法，该方法使用 NearestDinner 函数返回指定位置100英里以内的即将到来的就：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>实现基于 JSON 的 AJAX 搜索操作方法

现在，我们将实现一种控制器操作方法，该方法利用新的 FindByLocation ( # A1 存储库方法返回可用于填充地图的晚餐数据列表。 此操作方法会以 JSON (JavaScript 对象表示法) 格式返回晚餐数据，以便在客户端上使用 JavaScript 轻松地对其进行操作。

为实现此方法，我们将创建一个新的 "SearchController" 类，方法是右键单击 "\Controllers" 目录，然后选择 "添加 &gt; 控制器" 菜单命令。 然后，在新的 SearchController 类中实现 "SearchByLocation" 操作方法，如下所示：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 的 SearchByLocation 操作方法在内部调用 DinnerRepository 上的 FindByLocation 方法，以获取附近就的列表。 但不是将晚餐对象直接返回给客户端，而是返回 JsonDinner 对象。 JsonDinner 类公开了晚餐属性的子集 (例如：出于安全原因，它不会透露有 RSVP) 的人员的姓名。 它还包含 RSVPCount 属性，该属性不存在于晚宴上–并且通过对与特定晚餐关联的 RSVP 对象的数量进行动态计算。

然后，使用 Json ( # A1 helper 方法在控制器基类上使用基于 JSON 的线路格式返回就序列。 JSON 是一种用于表示简单数据结构的标准文本格式。 下面是一个示例，其中包含以下两个 JsonDinner 对象的 JSON 格式列表：

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.txt)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>使用 jQuery 调用基于 JSON 的 AJAX 方法

现在，我们已准备好更新 NerdDinner 应用程序的主页，以使用 SearchController 的 SearchByLocation 操作方法。 为此，我们将打开 "/Views/Home/Index.aspx" 视图模板并将其更新为包含 "文本框"、"搜索" 按钮、映射和 &lt; 一个 &gt; 名为 "dinnerList" 的 div 元素：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

然后，可以将两个 JavaScript 函数添加到页面：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

第一次加载页面时，第一个 JavaScript 函数会加载该映射。 第二个 JavaScript 函数在 "搜索" 按钮上向 JavaScript 单击事件处理程序。 按下该按钮时，它会调用 FindDinnersGivenLocation ( # A1 JavaScript 函数，我们会将其添加到 Map.js 文件：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

此 FindDinnersGivenLocation ( # A1 函数调用 map。在虚拟地球控件上查找 ( # A3，使其在输入位置上居中。 当虚拟的地球地图服务返回时，映射。Find ( # A1 方法会调用 callbackUpdateMapDinners 回调方法，并将其作为最后一个参数传递。

CallbackUpdateMapDinners ( # A1 方法是实际工作的位置。 它使用 jQuery 的 $. post ( # A1 helper 方法，以对我们的 SearchController 的 SearchByLocation 执行 AJAX 调用。 ( # A3 操作方法–向其传递新居中地图的纬度和经度。 它定义了一个内联函数，当 $ post ( # A1 helper 方法完成时，将调用该函数，并将使用一个名为 "就" 的变量向 ( SearchByLocation 中返回的 JSON 格式的晚餐结果传递该函数。 然后，它对每个返回的晚餐执行 foreach，并使用晚餐的纬度和经度以及其他属性在地图上添加新的 pin。 它还会将晚餐条目添加到地图右侧就的 HTML 列表。 然后，它将图钉和 HTML 列表的悬停事件上滑，以便在用户将其悬停在其上方时显示晚餐的详细信息：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

现在，当我们运行应用程序并访问主页时，我们会看到一个地图。 输入城市名称后，地图会在其附近显示即将到来的就：

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

将鼠标悬停在晚宴上方会显示有关它的详细信息。

单击 "冒泡" 或 "HTML" 列表右侧的晚餐标题即可导航到晚餐，然后可以选择 RSVP：

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>下一步

现在，我们实现了 NerdDinner 应用程序的所有应用程序功能。 现在我们来看看如何启用它的自动单元测试。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)

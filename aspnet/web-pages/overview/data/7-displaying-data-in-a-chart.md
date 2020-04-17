---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: 在图表中显示数据，其中ASP.NET网页 （Razor） |微软文档
author: rick-anderson
description: 本章介绍如何在图表中显示数据。 在前面的章节中，您学习了如何在网格中手动显示数据。 本章解释...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542880"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>在图表中显示具有ASP.NET网页（Razor）的数据

由[微软](https://github.com/microsoft)

> 本文介绍如何使用图表使用`Chart`帮助程序在ASP.NET网页 （Razor） 网站中显示数据。
> 
> **您将学习：**
> 
> - 如何在图表中显示数据。
> - 如何使用内置主题对图表进行样式设置。
> - 如何保存图表以及如何缓存图表以获得更好的性能。
> 
> 以下是本文介绍的ASP.NET编程功能：
> 
> - 帮手`Chart`
> 
> > [!NOTE]
> > 本文中的信息适用于ASP.NET网页 1.0 和网页 2。

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>图表帮助程序

当您要以图形形式显示数据时，可以使用`Chart`帮助程序。 `Chart`帮助程序可以渲染显示各种图表类型中的数据的图像。 它支持许多格式设置和标签选项。 `Chart`帮助程序可以呈现 30 多种图表类型，包括您可能从 Microsoft Excel 或其他工具&#8212;区域图、条形图、柱形图、折线图和饼图等工具中熟悉的所有类型的图表，以及更专业的图表（如股票图表）。

| **面积图**![描述：面积图类型的图片](7-displaying-data-in-a-chart/_static/image1.jpg) | **条形图**![说明：条形图类型的图片](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **柱形图**![说明：柱形图类型的图片](7-displaying-data-in-a-chart/_static/image3.jpg) | **折线图**![描述：折线图类型的图片](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **饼图**![说明：饼图类型的图片](7-displaying-data-in-a-chart/_static/image5.jpg) | **股票图表**![描述：股票图表类型的图片](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>图表元素

图表显示数据和其他元素，如图例、轴、系列等。 下图显示了使用`Chart`帮助器时可以自定义的许多图表元素。 本文介绍如何设置其中某些（不是全部）元素。

![说明：显示图表元素的图片](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>从数据创建图表

在图表中显示的数据可以来自数组、从数据库返回的结果或 XML 文件中的数据。

### <a name="using-an-array"></a>使用数组

如ASP.NET[网页编程简介中所述，使用 Razor 语法](https://go.microsoft.com/fwlink/?LinkId=202890)编程，数组允许您在单个变量中存储类似项的集合。 可以使用数组来包含要包含在图表中的数据。

此过程演示如何使用默认图表类型从数组中的数据创建图表。 它还演示如何在页面中显示图表。

1. 创建名为*ChartArrayBasic.cshtml*的新文件。
2. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    代码首先创建一个新图表并设置其宽度和高度。 使用`AddTitle`方法指定图表标题。 要添加数据，请使用 方法`AddSeries`。 在此示例中`name`，使用`xValue``yValues``AddSeries`方法 的 和 参数。 参数`name`显示在图表图例中。 该`xValue`参数包含沿图表水平轴显示的数据数组。 该`yValues`参数包含用于绘制图表垂直点的数据数组。

    该方法`Write`实际上呈现图表。 在这种情况下，由于您没有指定图表类型，`Chart`帮助程序将呈现其默认图表，即柱形图。
3. 在浏览器中运行页面。 浏览器显示图表。 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>对图表数据使用数据库查询

如果要绘制图表的信息位于数据库中，则可以运行数据库查询，然后使用结果中的数据创建图表。 此过程演示如何读取和显示在[文章"使用ASP.NET网页网站中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)"中创建的数据库中的数据。

1. 如果该文件夹不存在，则向网站的根目录添加*应用\_数据*文件夹。
2. 在 *"应用\_数据*"文件夹中，添加名为*SmallBakery.sdf*的数据库文件，该文件在["使用ASP.NET网页网站中的数据库简介"中](https://go.microsoft.com/fwlink/?LinkId=202893)所述。
3. 创建名为*ChartDataQuery.cshtml*的新文件。
4. 将现有内容替换为以下内容：   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    代码首先打开 SmallBakery 数据库并将其分配给名为 的`db`变量。 此变量表示可用于`Database`读取数据库和写入数据库的对象。 接下来，代码运行 SQL 查询以获取每个产品的名称和价格。 代码创建一个新图表，并通过调用图表`DataBindTable`的方法将数据库查询传递给它。 此方法采用两个参数：`dataSource`参数用于查询中的数据，`xField`该参数允许您设置用于图表 x 轴的数据列。

    作为使用 方法的替代方法`DataBindTable`，可以使用`AddSeries``Chart`帮助器的方法。 该方法`AddSeries`允许您设置 和`xValue``yValues`参数。 例如，而不是使用如下所示`DataBindTable`的方法：

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    可以使用如下所示`AddSeries`的方法：

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    两者都呈现相同的结果。 该方法`AddSeries`更灵活，因为您可以更明确地指定图表类型和数据，但如果不需要额外的灵活性，`DataBindTable`则该方法更易于使用。
5. 在浏览器中运行页面。 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>使用 XML 数据

图表的第三个选项是使用 XML 文件作为图表的数据。 这要求 XML 文件也具有描述 XML 结构的架构文件 *（.xsd*文件）。 此过程演示如何从 XML 文件读取数据。

1. 在*应用\_数据*文件夹中，创建名为*data.xml*的新 XML 文件。
2. 将现有 XML 替换为以下内容，即有关虚构公司员工的一些 XML 数据。 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 在*应用\_数据*文件夹中，创建名为*data.xsd*的新 XML 文件。 （请注意，这次的扩展是 *.xsd*.）
4. 将现有 XML 替换为以下内容： 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 在网站的根目录中，创建一个名为*ChartDataXML.cshtml*的新文件。
6. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    代码首先创建一个`DataSet`对象。 此对象用于管理从 XML 文件读取的数据，并根据架构文件中的信息对其进行组织。 （请注意，代码的顶部包括 语句`using SystemData`。 这是为了能够处理`DataSet`对象所必需的。 有关详细信息，请参阅[&quot;本文后面的使用&quot;语句和完全限定名称](#SB_UsingStatements)。

    接下来，代码基于数据集创建`DataView`一个对象。 数据视图提供图表可以绑定到&#8212;的对象，即读取和绘图。 `AddSeries`图表使用 方法绑定到数据，如您前面在绘制数组数据图表时所看到的那样，但此`xValue`时间和`yValues`参数设置为`DataView`对象除外。

    此示例还演示如何指定特定的图表类型。 在`AddSeries`方法中添加数据时，`chartType`参数也会设置为显示饼图。
7. 在浏览器中运行页面。 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"使用"语句和完全限定的名称
> 
> 使用 Razor 语法ASP.NET网页的 .NET 框架由数千个组件（类）组成。 为了使使用所有这些类可以管理，它们被组织成*命名空间*，有点像库。 例如，`System.Web`命名空间包含支持浏览器/服务器通信的类，`System.Xml`命名空间包含用于创建和读取 XML 文件的类，`System.Data`并且命名空间包含允许您处理数据的类。
> 
> 为了访问 .NET Framework 中的任何给定类，代码不仅需要了解类名称，还需要了解类中的命名空间。 例如，为了使用`Chart`帮助程序，代码需要查找`System.Web.Helpers.Chart`类，该类将命名空间 （）`System.Web.Helpers`与类名称 （ （ ）`Chart`合并在一起。 这称为类的*完全限定*名称&#8212;其在 .NET 框架的庞大范围内的完整、明确位置。 在代码中，如下所示：
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 但是，每次要引用类或帮助程序时，必须使用这些长而完全限定的名称是繁琐的（且容易出错）。 因此，为了更轻松地使用类名，可以*导入*您感兴趣的命名空间，这通常只是 .NET 框架中许多命名空间中的少数。 如果已导入命名空间，则只能使用类名称 （`Chart`） 而不是完全限定的名称 （`System.Web.Helpers.Chart`。 当代码运行并遇到类名称时，它可以只查看已导入的命名空间来查找该类。
> 
> 当您使用带有 Razor 语法的ASP.NET网页创建网页时，您通常每次都使用相同的类集，包括`WebPage`类、各种帮助器等。 为了节省您每次创建网站时导入相关命名空间的工作，ASP.NET进行了配置，以便自动为每个网站导入一组核心命名空间。 这就是为什么到目前为止您不必处理命名空间或导入名称空间的原因;您使用的所有类都位于已导入的命名空间中。
> 
> 但是，有时您需要使用不在自动导入的命名空间中的类。 在这种情况下，可以使用该类的完全限定名称，也可以手动导入包含该类的命名空间。 要导入命名空间，请使用`using`语句（`import`在 Visual Basic 中），如您前面的示例一样。
> 
> 例如，`DataSet`类位于命名空间中`System.Data`。 命名`System.Data`空间不能自动可用于ASP.NET Razor 页面。 因此，要使用完全限定`DataSet`名称使用类，可以使用如下所示的代码：
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 如果必须重复使用类，`DataSet`则可以导入如下所示的命名空间，然后在代码中仅使用类名称：
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 可以为要引用`using`的任何其他 .NET 框架命名空间添加语句。 但是，如上所述，您不需要经常执行此操作，因为要使用的大多数类都位于命名空间中，名称空间由ASP.NET自动导入，用于 *.cshtml*和 *.vbhtml*页面。

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>在网页内显示图表

在到目前为止看到的示例中，您将创建一个图表，然后将图表作为图形直接呈现给浏览器。 但是，在许多情况下，您希望将图表显示为页面的一部分，而不仅仅是在浏览器中。 为此，需要两步过程。 第一步是创建生成图表的页面，正如您已经看到的那样。

第二步是在另一页中显示生成的图像。 要显示图像，请使用 HTML`<img>`元素，就像显示任何图像一样。 但是`<img>`，该元素引用的不是 *.jpg*或 *.png*文件，而是引用包含创建图表`Chart`的帮助器的 *.cshtml*文件。 当显示页运行时，`<img>`元素获取帮助器的`Chart`输出并呈现图表。

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 创建名为*ShowChart.cshtml*的文件。
2. 将现有内容替换为以下内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    代码使用 元素`<img>`来显示您在*ChartArrayBasic.cshtml*文件中创建的图表。
3. 在浏览器中运行网页。 *ShowChart.cshtml*文件基于*ChartArrayBasic.cshtml*文件中的代码显示图表图像。

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>设置图表的样式

`Chart`帮助程序支持大量选项，这些选项允许您自定义图表的外观。 您可以设置颜色、字体、边框等。 自定义图表外观的一种简单方法是使用*主题*。 主题是信息的集合，用于指定如何使用字体、颜色、标签、调色板、边框和效果来呈现图表。 （请注意，图表的样式并不指示图表的类型。

下表列出了内置主题。

| 主题 | 描述 |
| --- | --- |
| `Vanilla` | 在白色背景上显示红色列。 |
| `Blue` | 在蓝色渐变背景上显示蓝色列。 |
| `Green` | 在绿色渐变背景上显示蓝色列。 |
| `Yellow` | 在黄色渐变背景上显示橙色列。 |
| `Vanilla3D` | 在白色背景上显示三维红色列。 |

您可以指定创建新图表时要使用的主题。

1. 创建名为*ChartStyleGreen.cshtml*的新文件。
2. 将页面中的现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    此代码与使用数据库进行数据的早期示例相同，但在创建`theme``Chart`对象时添加参数。 下面显示了更改的代码：

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 在浏览器中运行页面。 您看到的数据与以前相同，但图表看起来更精美： 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>保存图表

当您在本文中看到的帮助`Chart`器时，帮助程序每次调用图表时都会从头开始重新创建图表。 如有必要，图表的代码还会重新查询数据库或重新读取 XML 文件以获取数据。 在某些情况下，执行此操作可能是一个复杂的操作，例如，如果您要查询的数据库很大，或者 XML 文件包含大量数据。 即使图表不涉及大量数据，动态创建图像的过程也会占用服务器资源，如果许多人请求显示图表的页面或页面，也会对网站的性能产生影响。

为了帮助减少创建图表的潜在性能影响，可以在第一次创建图表时创建图表，然后保存它。 当再次需要图表时，而不是重新生成它时，只需获取保存的版本并呈现它。

您可以通过以下方式保存图表：

- 将图表缓存在计算机内存中（在服务器上）。
- 将图表另存为图像文件。
- 将图表另存为 XML 文件。 此选项允许您在保存图表之前对其进行修改。

### <a name="caching-a-chart"></a>缓存图表

创建图表后，可以缓存它。 缓存图表意味着，如果需要再次显示图表，则不必重新创建图表。 在缓存中保存图表时，会为它提供一个必须是唯一的图表的键。

如果服务器内存不足，则保存到缓存的图表可能会被删除。 此外，如果应用程序出于任何原因重新启动，缓存将被清除。 因此，使用缓存图表的标准方法是始终检查缓存中是否可用，如果没有，则先创建或重新创建它。

1. 在网站的根目录，创建一个名为*ShowCachedChart.cshtml*的文件。
2. 将现有内容替换为以下内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    该`<img>`标记包括指向`src` *ChartSaveToCache.cshtml*文件并将密钥作为查询字符串传递到页面的属性。 该键包含"我的图表&quot;键&quot;"的值。 *ChartSaveToCache.cshtml*文件包含创建图表`Chart`的帮助程序。 您将在一瞬间创建此页面。

    在页面的末尾有一个指向*名为ClearCache.cshtml*的页面的链接。 稍后还将创建该页面。 您只需要*ClearCache.cshtml*来测试此示例的缓存 - 它不是在使用缓存的图表时通常包含的链接或页面。
3. 在网站的根目录，创建一个名为*ChartSaveToCache.cshtml*的新文件。
4. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    代码首先检查是否传递了任何内容作为查询字符串中的键值。 如果是这样，代码会尝试通过调用`GetFromCache`方法并传递密钥来从缓存中读取图表。 如果事实证明该键下的缓存中没有任何内容（在首次请求图表时发生），则代码将像往常一样创建图表。 图表完成后，代码通过调用`SaveToCache`将其保存到缓存中。 该方法需要一个键（以便以后可以请求图表），以及图表应保存在缓存中的时间量。 （缓存图表的确切时间取决于您认为图表表示的数据可能会更改的频率。该方法`SaveToCache`还需要一个`slidingExpiration`参数&#8212;如果设置为 true，则每次访问图表时都会重置超时计数器。 在这种情况下，它实际上意味着图表的缓存条目在上次有人访问图表后 2 分钟过期。 （滑动过期的替代方法是绝对过期的，这意味着缓存条目在放入缓存后正好 2 分钟后过期，无论访问频率如何。

    最后，代码使用 方法`WriteFromCache`从缓存中获取和呈现图表。 请注意，此方法位于检查缓存`if`的块之外，因为它将从缓存中获取图表，无论图表是开始还是必须生成并保存在缓存中。

    请注意，在此示例中，`AddTitle`该方法包含时间戳。 （它将当前日期和时间&#8212;&#8212;`DateTime.Now`添加到标题中。
5. 创建名为*ClearCache.cshtml*的新页面，并将其内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    此页使用`WebCache`帮助程序删除在*ChartSaveToCache.cshtml*中缓存的图表。 如前所述，您通常不必有这样的页面。 您在此处创建它只是为了更轻松地测试缓存。
6. 在浏览器中运行*ShowCachedChart.cshtml*网页。 该页面基于*ChartSaveToCache.cshtml*文件中的代码显示图表图像。 记下时间戳在图表标题中的内容。 

    ![说明：图表标题中带有时间戳的基本图表图片](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 关闭浏览器。
8. 再次运行*ShowCachedChart.cshtml。* 请注意，时间戳与以前相同，表示图表未重新生成，而是从缓存中读取。
9. 在*ShowCachedChart.cshtml*中，单击**清除缓存**链接。 这将带您到*ClearCache.cshtml*，它报告缓存已清除。
10. 单击 **"返回显示缓存图表.cshtml"** 链接，或从 WebMatrix 重新运行*ShowCachedChart.cshtml。* 请注意，此时间戳已更改，因为缓存已清除。 因此，代码必须重新生成图表并将其放回缓存中。

### <a name="saving-a-chart-as-an-image-file"></a>将图表保存为图像文件

您还可以将图表另存为服务器上的图像文件（例如，作为 *.jpg*文件）。 然后，您可以像使用任何图像的方式使用图像文件。 优点是文件被存储而不是保存到临时缓存。 您可以在不同时间（例如，每小时）保存新的图表图像，然后保留随时间变化的永久记录。 请注意，必须确保 Web 应用程序具有将文件保存到要放置图像文件的服务器上的文件夹的权限。

1. 在网站的根目录，创建名为*\_ChartFiles 的*文件夹（如果该文件夹不存在）。
2. 在网站的根目录，创建一个名为*ChartSave.cshtml*的新文件。
3. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    代码首先通过调用`File.Exists`方法检查 *.jpg*文件是否存在。 如果文件不存在，代码将从数组创建一个新`Chart`。 这一次，代码调用`Save`方法并传递`path`参数以指定保存图表的位置的文件路径和文件名。 在页面正文中，`<img>`元素使用路径指向要显示的 *.jpg*文件。
4. 运行*ChartSave.cshtml*文件。
5. 返回到 WebMatrix。 请注意，名为*chart01.jpg*的图像文件已保存在*\_图表文件*文件夹中。

### <a name="saving-a-chart-as-an-xml-file"></a>将图表保存为 XML 文件

最后，您可以将图表另存为服务器上的 XML 文件。 使用此方法对缓存图表或将图表保存到文件中的一个优点是，如果需要，可以在显示图表之前修改 XML。 应用程序必须具有要放置映像文件的服务器上的文件夹的读/写权限。

1. 在网站的根目录，创建一个名为*ChartSaveXml.cshtml*的新文件。
2. 将现有内容替换为以下内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    此代码类似于您之前在缓存中存储图表时看到的代码，只不过它使用 XML 文件。 代码首先通过调用`File.Exists`方法检查 XML 文件是否存在。 如果文件确实存在，代码将创建一个新`Chart`对象，并将文件名作为`themePath`参数传递。 这将基于 XML 文件中的任何内容创建图表。 如果 XML 文件不存在，代码将创建一个类似于正常图表的图表，然后调用`SaveXml`以保存它。 图表使用 方法呈现，`Write`如您以前看到的那样。

    与显示缓存的页面一样，此代码在图表标题中包括时间戳。
3. 创建名为*ChartDisplayXMLChart.cshtml*的新页面，并添加以下标记： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 运行*图表显示XMLChart.cshtml*页面。 将显示图表。 记下图表标题中的时间戳。
5. 关闭浏览器。
6. 在 WebMatrix 中，右键单击*\_图表文件*文件夹，单击 **"刷新**"，然后打开该文件夹。 此文件夹中的*XMLChart.xml*文件由`Chart`帮助程序创建。 

    ![说明：显示图表帮助程序创建的 XMLChart.xml 文件的_ChartFiles文件夹。](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 再次运行*图表显示XMLChart.cshtml*页面。 该图表显示的时间戳与首次运行页面时的时间戳相同。 这是因为图表是从您之前保存的 XML 生成的。
8. 在 WebMatrix 中，打开*\_图表文件*文件夹并删除*XMLChart.xml*文件。
9. 再次运行*图表显示XMLChart.cshtml*页面。 这一次，时间戳将更新，因为`Chart`帮助程序必须重新创建 XML 文件。 如果需要，请检查*\_ChartFiles*文件夹，并注意到 XML 文件已返回。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [ASP.NET网页网站中使用数据库的简介](https://go.microsoft.com/fwlink/?LinkId=202893)
- [在ASP.NET网页网站中使用缓存以提高性能](https://go.microsoft.com/fwlink/?LinkId=202903)
- [图表类](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99))（ASP.NET MSDN 上的网页 API 引用）

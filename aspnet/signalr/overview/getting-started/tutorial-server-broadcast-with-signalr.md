---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教程：使用 SignalR 2 进行服务器广播 |微软文档
author: tdykstra
description: 本教程演示如何创建使用ASP.NET SignalR 2 提供服务器广播功能的 Web 应用程序。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675723"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>教程：使用 SignalR 2 进行服务器广播

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

本教程演示如何创建使用ASP.NET SignalR 2 提供服务器广播功能的 Web 应用程序。 服务器广播意味着服务器启动发送到客户端的通信。

您将在本教程中创建的应用程序模拟股票代码，这是服务器广播功能的典型方案。 服务器定期随机更新股票价格并将更新广播给所有连接的客户端。 在浏览器中，"更改"和 **"** 列"中的数字和**%** 符号会动态更改，以响应来自服务器的通知。 如果打开其他浏览器到同一 URL，它们都同时显示相同的数据和对数据的相同更改。

![创建 Web](tutorial-server-broadcast-with-signalr/_static/image1.png)

本教程介绍以下操作：

> [!div class="checklist"]
> * 创建项目
> * 设置服务器代码
> * 检查服务器代码
> * 设置客户端代码
> * 检查客户端代码
> * 测试应用程序
> * 启用日志记录

> [!IMPORTANT]
> 如果不想完成构建应用程序的步骤，可以在新的空ASP.NET Web 应用程序项目中安装 SignalR.sample 包。 如果不执行本教程中的步骤，安装 NuGet 包，则必须按照*readme.txt*文件中的说明进行操作。 要运行包，您需要添加一个 OWIN 启动类，`ConfigureSignalR`该类调用已安装包中的方法。 如果不添加 OWIN 启动类，您将收到错误。 请参阅本文[的"安装库存价格"示例](#install-the-stockticker-sample)部分。

## <a name="prerequisites"></a>先决条件

* 带有 ASP.NET 和 Web 开发**** 工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。

## <a name="create-the-project"></a>创建项目

本节演示如何使用 Visual Studio 2017 创建空ASP.NET Web 应用程序。

1. 在可视化工作室中，创建一个ASP.NET Web 应用程序。

    ![创建 Web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 在新**ASP.NET Web 应用程序 - SignalR.StockTicker**窗口中，保留 **"空**"并选择 **"确定**"。

## <a name="set-up-the-server-code"></a>设置服务器代码

在本节中，您可以设置在服务器上运行的代码。

### <a name="create-the-stock-class"></a>创建"库存"类

首先创建用于存储和传输库存信息*的 Stock*模型类。

1. 在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **类**"。

1. 命名类*Stock*并将其添加到项目中。

1. 将*Stock.cs*文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    创建股票时要设置的两个属性是`Symbol`（例如，微软的 MSFT）和`Price`。 其他属性取决于设置`Price`的方式和时间。 第一次设置`Price`时，值将传播到 。 `DayOpen` `Price`之后，当您设置 时，应用根据 和`Change``PercentChange``Price``DayOpen`之间的差异计算 和 属性值。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>创建股票价格中心和股票提克类

您将使用 SignalR 中心 API 来处理服务器到客户端的交互。 派生`StockTickerHub`自 SignalR`Hub`类的类将处理来自客户端的接收连接和方法调用。 您还需要维护库存数据并运行对象`Timer`。 该`Timer`对象将定期触发独立于客户端连接的价格更新。 不能将这些函数放在`Hub`类中，因为中心是瞬态的。 应用为中心中的每个`Hub`任务创建一个类实例，例如从客户端到服务器的连接和调用。 因此，保存库存数据、更新价格和广播价格更新的机制必须运行在单独的类中。 您将命名该类`StockTicker`。

![从斯托克蒂克广播](tutorial-server-broadcast-with-signalr/_static/image3.png)

您只需要在服务器上运行类的`StockTicker`一个实例，因此您需要设置从每个`StockTickerHub`实例到 singleton`StockTicker`实例的引用。 类`StockTicker`必须广播给客户端，因为它具有股票数据并触发更新，但不是`StockTicker``Hub`类。 类`StockTicker`必须获取对 SignalR 中心连接上下文对象的引用。 然后，它可以使用 SignalR 连接上下文对象广播到客户端。

#### <a name="create-stocktickerhubcs"></a>创建StockTickerHub.cs

1. 在**解决方案资源管理器**中，右键单击项目并选择**Add** > "**添加新项**"。

1. 在**添加新项目 - SignalR.StockTicker**中，选择 **"已安装** > **的可视 C#** > **Web** > **信号R"，** 然后选择**信号R集线器类 （v2）。**

1. 命名类*StockTickerHub*并将其添加到项目中。

    此步骤将创建*StockTickerHub.cs*类文件。 同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到项目中。

1. 将*StockTickerHub.cs*文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 保存文件。

应用使用[Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)类定义客户端可以在服务器上调用的方法。 您正在定义一种方法： `GetAllStocks()`。 当客户端最初连接到服务器时，它将调用此方法来获取所有股票及其当前价格的列表。 该方法可以同步运行并返回`IEnumerable<Stock>`，因为它正在从内存返回数据。

如果方法必须通过执行涉及等待（如数据库查找或 Web 服务调用）来获取数据，则可以指定`Task<IEnumerable<Stock>>`为返回值以启用异步处理。 有关详细信息，请参阅[ASP.NET信号R集线器 API 指南 - 服务器 - 何时异步执行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。

该`HubName`属性指定应用如何在客户端上的 JavaScript 代码中引用 Hub。 如果不使用此属性，客户端上的默认名称是类名称的 camelCase 版本，在这种情况下，该版本为`stockTickerHub`。

稍后在创建`StockTicker`类时将看到，应用在其静态`Instance`属性中创建该类的单例实例。 无论连接或断开连接的`StockTicker`客户端数，该单例实例都位于内存中。 该实例是`GetAllStocks()`该方法用于返回当前库存信息的方法。

#### <a name="create-stocktickercs"></a>创建StockTicker.cs

1. 在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **类**"。

1. 命名类*StockTicker*并将其添加到项目中。

1. 将*StockTicker.cs*文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

由于所有线程都将运行同一个 StockTicker 代码实例，因此 StockTicker 类必须具有线程安全。

### <a name="examine-the-server-code"></a>检查服务器代码

如果检查服务器代码，它将帮助您了解应用的工作原理。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>将单例实例存储在静态字段中

代码初始化使用类的实例`_instance`支持`Instance`属性的静态字段。 由于构造函数是私有的，因此它是应用可以创建的唯一类实例。 应用对`_instance`字段使用[延迟初始化](/dotnet/framework/performance/lazy-initialization)。 这不是出于性能原因。 它确保实例创建是线程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例从`StockTicker.Instance`静态属性获取 StockTicker 单例实例，如您在`StockTickerHub`类中前面看到的。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>将库存数据存储在并发字典中

构造函数使用一些样本库存`_stocks`数据初始化集合，并`GetAllStocks`返回数据。 如前所述，此股票集合由 返回`StockTickerHub.GetAllStocks`，这是客户端可以调用的类中的`Hub`服务器方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

出于线程安全，股票集合定义为[并发字典](https://msdn.microsoft.com/library/dd287191.aspx)类型。 作为替代方法，您可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)对象，并在对字典进行更改时显式锁定字典。

对于此示例应用程序，可以将应用程序数据存储在内存中，并在应用释放`StockTicker`实例时丢失数据。 在实际应用程序中，您将像数据库一样使用后端数据存储。

#### <a name="periodically-updating-stock-prices"></a>定期更新股票价格

构造函数启动一个`Timer`对象，该对象定期调用随机更新股票价格的方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`调用`UpdateStockPrices`， 在状态参数中传递为 null。 在更新价格之前，应用会锁定`_updateStockPricesLock`对象。 代码检查另一个线程是否已更新价格，然后调用`TryUpdateStockPrice`列表中的每个股票。 该方法`TryUpdateStockPrice`决定是否更改股票价格，以及更改多少股票价格。 如果股票价格发生变化，应用将调用`BroadcastStockPrice`向所有连接的客户端广播股票价格变化。

指定`_updatingStockPrices`[易失性](https://msdn.microsoft.com/library/x13ttww7.aspx)的标志，以确保它是线程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

在实际应用程序中，`TryUpdateStockPrice`该方法将调用 Web 服务来查找价格。 在此代码中，应用程序使用随机数生成器随机进行更改。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>获取 SignalR 上下文，以便 StockTicker 类可以广播给客户端

由于价格变化源自对象，`StockTicker`因此需要在所有连接的客户端上调用`updateStockPrice`方法的对象。 在类`Hub`中，您有用于调用客户端方法的 API，`StockTicker`但不派生自类`Hub`，并且没有对任何`Hub`对象的引用。 要广播到已连接的客户端`StockTicker`，类必须获取`StockTickerHub`类的 SignalR 上下文实例，并用它来调用客户端上的方法。

当代码创建单例类实例、传递该引用到构造函数时获取对 SignalR 上下文的`Clients`引用，构造函数将其放入属性中。

您只想获取上下文一次的原因有两个：获取上下文是一项昂贵的任务，一次获取上下文可确保应用保留发送到客户端的消息的预期顺序。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

通过获取`Clients`上下文的属性并将其放入属性，`StockTickerClient`可以编写代码来调用与`Hub`类中看起来相同的客户端方法。 例如，要广播到所有客户端，您可以写入`Clients.All.updateStockPrice(stock)`。

您`updateStockPrice`调用`BroadcastStockPrice`的方法尚不存在。 稍后，当您编写在客户端上运行的代码时，将添加它。 您可以在此处引用，`updateStockPrice`因为`Clients.All`是动态的，这意味着应用将在运行时计算表达式。 执行此方法调用时，SignalR 将向客户端发送方法名称和参数值，如果客户端具有名为`updateStockPrice`的方法，则应用将调用该方法并将参数值传递给客户端。

`Clients.All`表示发送到所有客户端。 SignalR 为您提供了其他选项来指定要发送到的客户端或客户端组。 有关详细信息，请参阅[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>注册信号R路由

服务器需要知道要拦截哪个 URL 并定向到 SignalR。 为此，添加 OWIN 启动类：

1. 在**解决方案资源管理器**中，右键单击项目并选择**Add** > "**添加新项**"。

1. 在 **"添加新项目 - SignalR.StockTicker"中选择****"已安装** > **的可视化 C#** > **Web"，** 然后选择**OWIN 启动类**。

1. 命名类 *"启动"* 并选择 **"确定**"。

1. 将*Startup.cs*文件中的默认代码替换为此代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

您现在已完成服务器代码的设置。 在下一节中，您将设置客户端。

## <a name="set-up-the-client-code"></a>设置客户端代码

在本节中，设置在客户端上运行的代码。

### <a name="create-the-html-page-and-javascript-file"></a>创建 HTML 页面和 JavaScript 文件

HTML 页面将显示数据，JavaScript 文件将组织数据。

#### <a name="create-stocktickerhtml"></a>创建股票Ticker.html

首先，您将添加 HTML 客户端。

1. 在**解决方案资源管理器**中，右键单击项目并选择"**添加** > **HTML 页面**"。

1. 命名文件*库存Ticker*并选择 **"确定**"。

1. 将*StockTicker.html*文件中的默认代码替换为以下代码：

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML 创建一个包含五列的表、一个标题行和一个包含一个跨所有五列的单元格的数据行。 数据行显示"加载..."当应用程序启动时，瞬间。 JavaScript 代码将删除该行，并在其位置添加从服务器检索的股票数据行。

    脚本标记指定：

    * jQuery 脚本文件。

    * SignalR 核心脚本文件。

    * SignalR 代理脚本文件。

    * 稍后将创建的 StockTicker 脚本文件。

    应用程序动态生成 SignalR 代理脚本文件。 它指定"/信号器/集线器"URL，并为 的 Hub 类（本例中）为 定义方法`StockTickerHub.GetAllStocks`的代理方法。 如果您愿意，可以使用[SignalR 实用程序](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件。 不要忘记在方法调用中`MapHubs`禁用动态文件创建。

1. 在**解决方案资源管理器中**，展开**脚本**。

    jQuery 和 SignalR 的脚本库在项目中可见。

    > [!IMPORTANT]
    > 包管理器将安装更高版本的 SignalR 脚本。

1. 更新代码块中的脚本引用，以对应于项目中的脚本文件版本。

1. 在**解决方案资源管理器**中，右键单击*StockTicker.html*，然后选择 **"设置为起始页**"。

#### <a name="create-stocktickerjs"></a>创建库存Ticker.js

现在创建 JavaScript 文件。

1. 在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **JavaScript 文件**"。

1. 命名文件*库存Ticker*并选择 **"确定**"。

1. 将此代码添加到*StockTicker.js*文件：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>检查客户端代码

如果检查客户端代码，它将帮助您了解客户端代码如何与服务器代码交互以使应用正常工作。

#### <a name="starting-the-connection"></a>启动连接

`$.connection`指 SignalR 代理。 代码获取对类代理的引用，`StockTickerHub`并将其放入变量中。 `ticker` 代理名称是由`HubName`属性设置的名称：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR 函数初始化 SignalR`start`连接。 函数`start`异步执行并返回[jQuery 延迟对象](http://api.jquery.com/category/deferred-object/)。 可以调用完成函数来指定应用完成异步操作时要调用的函数。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>获取所有股票

该`init`函数调用服务器上`getAllStocks`的函数，并使用服务器返回的信息来更新库存表。 请注意，默认情况下，您必须在客户端上使用 camelCasing，即使方法名称在服务器上是 pascalcase 的。 CamelCasing 规则仅适用于方法，不适用于对象。 例如，`stock.Symbol`您引用 和`stock.Price`，`stock.symbol`而不是`stock.price`或 。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

在`init`方法中，应用通过`formatStock`调用对象的属性`stock`格式化，然后调用`supplant`将变量中的`rowTemplate`占位符替换为`stock`对象属性值，为从服务器接收的每个股票对象的表行创建 HTML。 然后，生成的 HTML 将追加到库存表中。

> [!NOTE]
> 通过将其`init`作为在`callback`异步`start`函数完成后执行的函数传入来调用。 如果在调用`start`后`init`调用作为单独的 JavaScript 语句调用 ，则函数将失败，因为它将立即运行，而无需等待启动函数完成建立连接。 在这种情况下，`init`该函数将尝试在`getAllStocks`应用建立服务器连接之前调用该函数。

#### <a name="getting-updated-stock-prices"></a>获取更新的股票价格

当服务器更改股票价格时，它将调用`updateStockPrice`连接的客户端。 应用将该函数添加到代理的客户端属性，`stockTicker`使其可用于来自服务器的调用。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

该`updateStockPrice`函数将从服务器接收的 Stock 对象格式化为表行，其方式与函数`init`中相同。 它不是将行追加到表中，而是在表中查找股票的当前行，并将该行替换为新行。

## <a name="test-the-application"></a>测试应用程序

您可以测试应用以确保其正常工作。 您将看到所有浏览器窗口显示股票价格波动的实时库存表。

1. 在工具栏中，打开**脚本调试**，然后选择播放按钮以在调试模式下运行应用。

    ![用户打开调试模式和选择播放的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    将打开一个浏览器窗口，显示**实时库存表**。 库存表最初显示"加载..."行，然后，在很短的时间后，应用程序显示初始股票数据，然后股票价格开始变化。

1. 从浏览器复制 URL，打开另外两个浏览器，并将 URL 粘贴到地址栏中。

    初始库存显示与第一个浏览器相同，更改同时发生。

1. 关闭所有浏览器，打开新浏览器，然后转到相同的 URL。

    StockTicker 单例对象继续在服务器中运行。 **实时库存表**显示，股票继续变化。 您看不到具有零更改数字的初始表。

1. 关闭浏览器。

## <a name="enable-logging"></a>启用日志记录

SignalR 具有内置日志记录功能，您可以在客户端上启用该功能，以帮助进行故障排除。 在本节中，您可以启用日志记录，并查看示例，这些示例显示了日志如何告诉您 SignalR 正在使用以下哪种传输方法：

* [WebSockets，](http://en.wikipedia.org/wiki/WebSocket)由IIS 8和当前浏览器支持。

* [服务器发送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet 资源管理器以外的浏览器支持。

* [永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)，由 Internet 资源管理器支持。

* [Ajax长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)，由所有浏览器支持。

对于任何给定的连接，SignalR 选择服务器和客户端都支持的最佳传输方法。

1. 打开*股票Ticker.js*.

1. 添加此突出显示的代码行，以便在文件末尾初始化连接的代码之前启用日志记录：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. 按**F5**以运行项目。

1. 打开浏览器的开发人员工具窗口，然后选择控制台以查看日志。 您可能需要刷新页面才能看到 SignalR 协商新连接传输方法的日志。

    * 如果您在 Windows 8 （IIS 8） 上运行 Internet 资源管理器 10，则传输方法是**WebSocket。**

    * 如果您在 Windows 7（IIS 7.5）上运行 Internet 资源管理器 10，则传输方法是**iframe**。

    * 如果您在 Windows 8 （IIS 8） 上运行 Firefox 19，则传输方法是**WebSocket。**

        > [!TIP]
        > 在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。

    * 如果您在 Windows 7（IIS 7.5）上运行 Firefox 19，则传输方法是**服务器发送**的事件。

## <a name="install-the-stockticker-sample"></a>安装库存价格示例

[微软.AspNet.SignalR.sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安装StockTicker应用程序。 与从头开始创建的简化版本相比，NuGet 包包含的功能更多。 在本教程的这一部分中，您可以安装 NuGet 包并查看新功能和实现这些功能的代码。

> [!IMPORTANT]
> 如果不执行本教程的早期步骤，安装包，则必须向项目添加 OWIN 启动类。 NuGet 包的此 readme.txt 文件解释了此步骤。

### <a name="install-the-signalrsample-nuget-package"></a>安装信号R.样品 NuGet 封装

1. 在**解决方案资源管理器**中，右键单击项目并选择 **"管理 NuGet 包**"。

1. 在**NuGet 软件包管理器中：SignalR.StockTicker**，选择 **"浏览**"。

1. 从**包源**中，选择**nuget.org。**

1. 在搜索框中输入*SignalR.示例*，然后选择**Microsoft.AspNet.SignalR.示例** > **安装**。

1. 在**解决方案资源管理器中**，展开*SignalR.Sample*文件夹。

    安装 SignalR.Sample 包创建了文件夹及其内容。

1. 在*SignalR.sample*文件夹中，右键单击*StockTicker.html*，然后选择"**设置为起始页**"。

    > [!NOTE]
    > 安装 SignalR.sample NuGet 包可能会更改*脚本*文件夹中的 jQuery 版本。 包在*SignalR.Sample*文件夹中安装的新*StockTicker.html*文件将与包安装的 jQuery 版本同步，但如果要再次运行原始*StockTicker.html*文件，您可能需要首先更新脚本标记中的 jQuery 引用。

### <a name="run-the-application"></a>运行应用程序

 您在第一个应用中看到的表具有有用的功能。 完整的股票代码应用程序显示新的功能：一个水平滚动窗口，显示股票数据和股票的变化颜色，因为他们的上升和下降。

1. 按**F5**以运行应用。

     首次运行应用时，"市场"是"关闭的"，您将看到一个静态表和一个未滚动的刻度窗口。

1. 选择**公开市场**。

    ![实时代码的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **实时库存报价框**开始水平滚动，服务器开始随机广播股票价格变化。

    * 每次股票价格变化时，应用程序都会更新**实时库存表**和**实时股票报价器**。

    * 当股票价格变化为正时，应用程序将显示具有绿色背景的股票。

    * 当更改为负时，应用程序将显示具有红色背景的股票。

1. 选择**关闭市场**。

    * 表更新停止。

    * 刻度线停止滚动。

1. 选择“重置”****。

    * 重置所有库存数据。

    * 应用在价格更改开始之前还原初始状态。

1. 从浏览器复制 URL，打开另外两个浏览器，并将 URL 粘贴到地址栏中。

1. 在每个浏览器中，您都会看到相同的数据同时动态更新。

1. 当您选择任何控件时，所有浏览器都同时以相同的方式响应。

### <a name="live-stock-ticker-display"></a>实时库存报价显示

**实时库存报价显示**是按 CSS 样式格式化为`<div>`单行的元素中的无序列表。 应用以与表相同的方式初始化和更新代码：通过在`<li>`模板字符串中替换占位符并动态地将`<li>`元素添加到`<ul>`元素。 该应用程序包括使用 jQuery`animate`函数来更改 中无序列表的边距左侧滚动。 `<div>`

#### <a name="signalrsample-stocktickerhtml"></a>信号R.样品库存Ticker.html

股票代码 HTML 代码：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>信号R.样品库存Ticker.css

股票代码 CSS 代码：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>信号R.样品信号R.StockTicker.js

使其滚动的 jQuery 代码：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>客户端可以调用的服务器上的其他方法

为了增加应用的灵活性，应用可以调用其他方法。

#### <a name="signalrsample-stocktickerhubcs"></a>信号R.样品StockTickerHub.cs

该`StockTickerHub`类定义了客户端可以调用的其他四种方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

应用调用`OpenMarket`，`CloseMarket`并`Reset`响应页面顶部的按钮。 它们演示了一个客户端触发状态更改的模式，该更改将立即传播到所有客户端。 这些方法中的每种方法都调用类中`StockTicker`导致市场状态更改然后广播新状态的方法。

#### <a name="signalrsample-stocktickercs"></a>信号R.样品StockTicker.cs

在类`StockTicker`中，应用使用返回`MarketState``MarketState`枚举值的属性维护市场状态：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

更改市场状态的每个方法都会在锁块内执行此操作，`StockTicker`因为类必须是线程安全的：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

为了确保此代码是线程安全的，支持指定的`_marketState``MarketState``volatile`属性的字段：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`和`BroadcastMarketReset`方法与您已经看到的广播股票价格方法类似，但它们调用在客户端定义的不同方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>服务器可以调用的客户端上的其他功能

该`updateStockPrice`函数现在同时处理表和刻度显示，它用于`jQuery.Color`闪烁红色和绿色。

*SignalR.StockTicker.js*中的新功能根据市场状态启用和禁用按钮。 它们还会停止或启动**实时库存刻度**水平滚动。 由于许多函数被添加到`ticker.client`，应用程序使用[jQuery 扩展函数](http://api.jquery.com/jQuery.extend/)来添加它们。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立连接后的其他客户端设置

客户端建立连接后，它还有一些额外的工作要做：

* 了解市场是开放的还是关闭的，以调用适当的`marketOpened`或`marketClosed`功能。

* 将服务器方法调用附加到按钮。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

服务器方法直到应用建立连接后才会连接到按钮。 因此，代码在服务器方法可用之前无法调用它们。

## <a name="additional-resources"></a>其他资源

在本教程中，您学习了如何对将消息从服务器广播到所有连接客户端的 SignalR 应用程序进行编程。 现在，您可以定期广播消息，并响应来自任何客户端的通知。 您可以使用多线程单例实例的概念在多人在线游戏方案中维护服务器状态。 例如，请参阅基于[SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。

有关显示对等通信场景的教程，请参阅[使用 SignalR 入门](introduction-to-signalr.md)和使用[SignalR 进行实时更新](tutorial-high-frequency-realtime-with-signalr.md)。

有关 SignalR 的更多，请参阅以下资源：

* [ASP.NET SignalR](../../index.md)
* [信号器项目](http://signalr.net/)
* [信号R GitHub 和示例](https://github.com/SignalR/SignalR)
* [信号R维基](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>后续步骤

本教程介绍以下操作：

> [!div class="checklist"]
> * 已创建项目
> * 设置服务器代码
> * 检查服务器代码
> * 设置客户端代码
> * 检查客户端代码
> * 已测试应用程序
> * 已启用日志记录

进入下一篇文章，了解如何创建使用ASP.NET SignalR 2 的实时 Web 应用程序。
> [!div class="nextstepaction"]
> [使用 SignalR 创建实时 Web 应用](real-time-web-applications-with-signalr.md)

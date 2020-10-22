---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教程： Server 广播与 SignalR 2 |Microsoft Docs
author: tdykstra
description: 本教程介绍如何创建使用 ASP.NET SignalR 2 的 web 应用程序来提供服务器广播功能。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345606"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>教程：服务器广播与 SignalR 2

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

本教程介绍如何创建使用 ASP.NET SignalR 2 的 web 应用程序来提供服务器广播功能。 服务器广播意味着服务器启动发送到客户端的通信。

你将在本教程中创建的应用程序模拟股票行情，这是服务器广播功能的典型方案。 服务器会定期定期更新股票价格，并将更新广播到所有连接的客户端。 在浏览器中， **更改** 和列中的数字和符号会 **%** 动态更改以响应来自服务器的通知。 如果你打开相同 URL 的其他浏览器，则它们都同时显示相同的数据和相同的数据更改。

![创建 web](tutorial-server-broadcast-with-signalr/_static/image1.png)

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
> 如果不想完成生成应用程序的步骤，可以在新的空 ASP.NET Web 应用程序项目中安装 SignalR 包。 如果在不执行本教程中的步骤的情况下安装 NuGet 程序包，则必须按照 *readme.txt* 文件中的说明进行操作。 若要运行包，您需要添加 OWIN startup 类，该类调用 `ConfigureSignalR` 已安装包中的方法。 如果未添加 OWIN startup 类，会收到错误。 请参阅本文的 [安装 StockTicker 示例](#install-the-stockticker-sample) 部分。

## <a name="prerequisites"></a>必备条件

* 带有 ASP.NET 和 Web 开发**** 工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。

## <a name="create-the-project"></a>创建项目

本部分演示如何使用 Visual Studio 2017 创建空的 ASP.NET Web 应用程序。

1. 在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。

    ![创建 web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 在 **新的 ASP.NET Web 应用程序-SignalR. StockTicker** 窗口中，保留 **为空** ，并选择 **"确定"**。

## <a name="set-up-the-server-code"></a>设置服务器代码

在本部分中，将设置运行在服务器上的代码。

### <a name="create-the-stock-class"></a>创建 Stock 类

首先，创建用于存储和传输股票信息的 *stock* 模型类。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **类**"。

1. 命名类 *库存* 并将其添加到项目。

1. 将 *Stock.cs* 文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    创建股票时将设置的两个属性 `Symbol` 为 (例如，MSFT For Microsoft) 和 `Price` 。 其他属性取决于设置的方式和时间 `Price` 。 第一次设置时 `Price` ，该值将传播到 `DayOpen` 。 之后，在设置时 `Price` ，应用程序会 `Change` `PercentChange` 基于和之间的差异计算和属性值 `Price` `DayOpen` 。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>创建 StockTickerHub 和 StockTicker 类

你将使用 SignalR 中心 API 来处理服务器到客户端的交互。 `StockTickerHub`派生自 SignalR 类的类 `Hub` 将处理从客户端接收连接和方法调用。 还需要维护股票数据并运行 `Timer` 对象。 `Timer`对象将定期触发价格更新，独立于客户端连接。 不能将这些函数放在 `Hub` 类中，因为中心是暂时性的。 应用程序 `Hub` 为中心上的每个任务创建一个类实例，如连接和从客户端到服务器的调用。 因此，保留股票数据、更新价格和广播价格更新的机制必须在单独的类中运行。 你将为类命名 `StockTicker` 。

![从 StockTicker 广播](tutorial-server-broadcast-with-signalr/_static/image3.png)

您只希望在 `StockTicker` 服务器上运行类的一个实例，因此您需要设置从每个 `StockTickerHub` 实例到单一实例的引用 `StockTicker` 。 `StockTicker`类必须广播到客户端，因为它具有股票数据并触发更新，但 `StockTicker` 不是 `Hub` 类。 `StockTicker`类必须获取对 SignalR 中心连接上下文对象的引用。 然后，它可以使用 SignalR 连接上下文对象广播到客户端。

#### <a name="create-stocktickerhubcs"></a>创建 StockTickerHub.cs

1. 在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **新项**"。

1. 在 "**添加新项-SignalR. StockTicker**" 中，选择 "**已安装**  >  **Visual c #**  >  **Web**  >  **SignalR** "，然后选择**SignalR Hub 类 (v2) **。

1. 将类命名为 *StockTickerHub* ，并将其添加到项目。

    此步骤将创建 *StockTickerHub.cs* 类文件。 同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到项目。

1. 将 *StockTickerHub.cs* 文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 保存文件。

应用使用 [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 类定义客户端可以在服务器上调用的方法。 您正在定义一个方法： `GetAllStocks()` 。 当客户端最初连接到服务器时，它将调用此方法以获取所有股票的列表及其当前价格。 方法可以同步运行并返回， `IEnumerable<Stock>` 因为它是从内存返回数据。

如果该方法必须通过执行需要等待的内容（如数据库查找或 web 服务调用）来获取数据，则应将指定 `Task<IEnumerable<Stock>>` 为返回值以启用异步处理。 有关详细信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-When to 异步执行的时间](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。

`HubName`特性指定应用程序将如何在客户端上的 JavaScript 代码中引用中心。 如果不使用此属性，则客户端上的默认名称是类名的 camelCase 版本，在本例中为 `stockTickerHub` 。

稍后在创建 `StockTicker` 类时，应用程序会在其静态属性中创建该类的单一实例 `Instance` 。 无论 `StockTicker` 有多少客户端连接或断开连接，的单一实例都在内存中。 该实例就是 `GetAllStocks()` 方法用来返回当前股票信息的内容。

#### <a name="create-stocktickercs"></a>创建 StockTicker.cs

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **类**"。

1. 将类命名为 *StockTicker* ，并将其添加到项目。

1. 将 *StockTicker.cs* 文件中的代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

由于所有线程都将运行 StockTicker 代码的同一个实例，因此 StockTicker 类必须是线程安全的。

### <a name="examine-the-server-code"></a>检查服务器代码

如果检查服务器代码，它将帮助你了解应用的工作原理。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>将单一实例存储在静态字段中

此代码 `_instance` 使用类的实例初始化用于支持属性的静态字段 `Instance` 。 由于构造函数是私有的，因此它是应用可创建的类的唯一实例。 该应用对字段使用 [迟缓初始化](/dotnet/framework/performance/lazy-initialization) `_instance` 。 这不是出于性能方面的原因。 这是为了确保实例创建是线程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例将从静态属性获取 StockTicker 单一实例 `StockTicker.Instance` ，正如你之前在类中看到的一样 `StockTickerHub` 。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>在 ConcurrentDictionary 中存储股票数据

构造函数 `_stocks` 用一些示例股票数据初始化集合，并 `GetAllStocks` 返回股票。 如前文所述，此股票集合由返回 `StockTickerHub.GetAllStocks` ，这是客户端可调用的类中的服务器方法 `Hub` 。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

股票集合定义为线程安全的 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 类型。 作为替代方法，可以使用 [字典](https://msdn.microsoft.com/library/xfhwa508.aspx) 对象，并在对字典进行更改时显式锁定字典。

在此示例应用程序中，可以将应用程序数据存储在内存中，并在应用程序释放实例时丢失数据  `StockTicker` 。 在实际应用程序中，可以使用数据库之类的后端数据存储。

#### <a name="periodically-updating-stock-prices"></a>定期更新股票价格

构造函数将启动一个 `Timer` 对象，该对象定期调用可随机更新股票价格的方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer` 调用 `UpdateStockPrices` ，在状态参数中传入 null。 更新价格之前，应用会对对象进行锁定 `_updateStockPricesLock` 。 该代码将检查是否有另一个线程正在更新价格，然后 `TryUpdateStockPrice` 在列表中的每个股票上调用。 `TryUpdateStockPrice`方法决定是否更改股票价格，以及更改的量。 如果股票价格发生变化，应用程序 `BroadcastStockPrice` 将调用以将股票价格更改广播到所有连接的客户端。

`_updatingStockPrices`指定为[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)的标志，以确保它是线程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

在实际应用程序中，该 `TryUpdateStockPrice` 方法将调用 web 服务来查找价格。 在此代码中，应用程序使用随机数生成器来随机进行更改。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>获取 SignalR 上下文以便 StockTicker 类可以广播到客户端

因为价格变化源自 `StockTicker` 对象，所以它是需要 `updateStockPrice` 在所有连接的客户端上调用方法的对象。 在 `Hub` 类中，你有一个用于调用客户端方法的 API，但它 `StockTicker` 不是从类派生的， `Hub` 并且不具有对任何对象的引用 `Hub` 。 若要广播到连接的客户端， `StockTicker` 该类必须获取类的 SignalR 上下文实例， `StockTickerHub` 并使用该实例对客户端调用方法。

此代码在创建单一实例类实例时获取对 SignalR 上下文的引用，将该引用传递给构造函数，构造函数将该引用传递到 `Clients` 属性中。

只需获取上下文一次只需两个原因：获取上下文是一种成本高昂的任务，并将其启用一次，确保应用保留发送到客户端的预期消息顺序。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

如果获取 `Clients` 上下文的属性并将其放在属性中， `StockTickerClient` 则可以编写代码来调用与类中外观相同的客户端方法 `Hub` 。 例如，要广播到可以写入的所有客户端 `Clients.All.updateStockPrice(stock)` 。

`updateStockPrice`你在中调用的方法 `BroadcastStockPrice` 尚不存在。 稍后在编写在客户端上运行的代码时，将添加此代码。 您可以在 `updateStockPrice` 这里引用 `Clients.All` ，因为是动态的，这意味着应用程序将在运行时计算表达式。 此方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有名为的方法 `updateStockPrice` ，则应用程序将调用该方法并向其传递参数值。

`Clients.All` 表示发送到所有客户端。 SignalR 提供其他选项来指定要发送到的客户端或客户端组。 有关详细信息，请参阅 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>注册 SignalR 路由

服务器需要知道要截获哪个 URL，并将其定向到 SignalR。 为此，请添加 OWIN startup 类：

1. 在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **新项**"。

1. 在 "**添加新项-SignalR. StockTicker** " 中选择 "**已安装**  >  **Visual c #**  >  **Web** "，然后选择 " **OWIN Startup 类**"。

1. 将类命名为 " *启动* "，然后选择 **"确定"**。

1. 将 *Startup.cs* 文件中的默认代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

你现在已经完成了服务器代码的设置。 在下一部分中，你将设置客户端。

## <a name="set-up-the-client-code"></a>设置客户端代码

在本部分中，将设置在客户端上运行的代码。

### <a name="create-the-html-page-and-javascript-file"></a>创建 HTML 页和 JavaScript 文件

HTML 页面将显示数据，JavaScript 文件将对数据进行组织。

#### <a name="create-stocktickerhtml"></a>创建 StockTicker.html

首先，您将添加 HTML 客户端。

1. 在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **HTML 页**"。

1. 将该文件命名为 *StockTicker* ，然后选择 **"确定"**。

1. 将 *StockTicker.html* 文件中的默认代码替换为以下代码：

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML 将创建一个表，其中包含五个列和一个标题行，以及一个包含跨所有5列的单个单元的数据行。 数据行显示 "正在加载 ..."应用启动。 JavaScript 代码将删除该行，并在其位置行中添加从服务器检索到的股票数据。

    脚本标记指定：

    * JQuery 脚本文件。

    * SignalR 核心脚本文件。

    * SignalR 代理脚本文件。

    * 稍后将创建的 StockTicker 脚本文件。

    应用会动态生成 SignalR 代理脚本文件。 它指定 "/signalr/hubs" URL，并为 Hub 类上的方法（在本例中为）定义代理方法 `StockTickerHub.GetAllStocks` 。 如果愿意，可以使用 [SignalR 实用工具](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件。 请不要忘记在方法调用中禁用动态文件创建 `MapHubs` 。

1. 在 **解决方案资源管理器**中，展开 " **脚本**"。

    JQuery 和 SignalR 的脚本库在项目中可见。

    > [!IMPORTANT]
    > 程序包管理器将安装较新版本的 SignalR 脚本。

1. 更新代码块中的脚本引用，使其与项目中的脚本文件版本相对应。

1. 在 **解决方案资源管理器**中，右键单击 *StockTicker.html*，然后选择 " **设为起始页**"。

#### <a name="create-stocktickerjs"></a>创建 StockTicker.js

现在创建 JavaScript 文件。

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **JavaScript 文件**"。

1. 将该文件命名为 *StockTicker* ，然后选择 **"确定"**。

1. 将以下代码添加到 *StockTicker.js* 文件：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>检查客户端代码

如果检查客户端代码，它将帮助您了解客户端代码如何与服务器代码交互以使应用程序正常工作。

#### <a name="starting-the-connection"></a>启动连接

`$.connection` 引用 SignalR 代理。 此代码获取对类的代理的引用 `StockTickerHub` 并将其放在变量中 `ticker` 。 代理名称是由属性设置的名称 `HubName` ：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR 函数初始化 SignalR 连接 `start` 。 `start`函数以异步方式执行，并返回[jQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)。 可以调用 done 函数来指定应用完成异步操作时要调用的函数。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>获取所有股票

`init`函数调用 `getAllStocks` 服务器上的函数，并使用服务器返回的信息更新股票表。 请注意，默认情况下，你必须在客户端上使用 camelCasing，即使方法名称在服务器上采用 pascal 大小写形式。 CamelCasing 规则仅适用于方法，而不适用于对象。 例如，引用 `stock.Symbol` 和 `stock.Price` ，而不是 `stock.symbol` 或 `stock.price` 。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

在 `init` 方法中，应用程序为从服务器接收的每个 stock 对象创建一个表行的 HTML，方法是调用 `formatStock` 以设置 `stock` 对象的属性，然后调用 `supplant` 将变量中的占位符替换为 `rowTemplate` `stock` 对象属性值。 然后，将生成的 HTML 追加到 stock 表中。

> [!NOTE]
> 通过将 `init` 其作为在 `callback` 异步函数完成后执行的函数传入来调用 `start` 。 如果在 `init` 调用后将作为单独的 JavaScript 语句调用 `start` ，则函数将失败，因为它会立即运行，而不会等待启动函数完成连接的建立。 在这种情况下，该 `init` 函数将尝试在 `getAllStocks` 应用程序建立服务器连接之前调用函数。

#### <a name="getting-updated-stock-prices"></a>获取更新后的股票价格

当服务器更改股票价格时，它将 `updateStockPrice` 在连接的客户端上调用。 应用将函数添加到代理的客户端属性 `stockTicker` ，使其可用于从服务器调用。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice`函数将从服务器接收的 stock 对象的格式设置为与在函数中相同的方式 `init` 。 它在表中查找股票的当前行，而不是将该行追加到表中，而是将该行替换为新行。

## <a name="test-the-application"></a>测试应用程序

可以测试应用程序以确保其正常运行。 你将看到所有浏览器窗口都显示股票价格波动的实时股票表。

1. 在工具栏上，打开 " **脚本调试** "，然后选择 "播放" 按钮以调试模式运行应用。

    ![用户打开调试模式并选择 "播放" 的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    将打开一个浏览器窗口，其中显示了 **实时股票表**。 Stock 表最初显示 "正在加载 ..."行，然后在一小段时间后，应用程序会显示初始股票数据，然后股票价格开始改变。

1. 从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。

    初始股票显示器与第一个浏览器相同，同时发生更改。

1. 关闭所有浏览器，打开新的浏览器，并中转到相同的 URL。

    StockTicker singleton 对象继续在服务器中运行。 **Live 表**显示股票已继续更改。 看不到具有零更改图的初始表。

1. 关闭浏览器。

## <a name="enable-logging"></a>启用日志记录

SignalR 具有内置日志记录功能，可以在客户端上启用该功能以帮助进行故障排除。 在本部分中，将启用日志记录，并查看示例，其中显示了日志如何说明 SignalR 正在使用以下哪种传输方法：

* [Websocket](http://en.wikipedia.org/wiki/WebSocket)，受 IIS 8 和当前浏览器支持。

* Internet Explorer 之外的浏览器所支持的[服务器发送事件](http://en.wikipedia.org/wiki/Server-sent_events)。

* Internet Explorer 支持的[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。

* 所有浏览器都支持[Ajax 长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。

对于任何给定的连接，SignalR 将选择服务器和客户端都支持的最佳传输方法。

1. 打开 *StockTicker.js*。

1. 添加以下突出显示的代码行，以便在文件末尾初始化连接的代码之前立即启用日志记录：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. 按 **F5** 运行项目。

1. 打开浏览器的 "开发人员工具" 窗口，并选择控制台查看日志。 您可能必须刷新该页才能查看为新连接协商传输方法的 SignalR 的日志。

    * 如果你在 Windows 8 上运行 Internet Explorer 10 (IIS 8) ，则传输方法为 **websocket**。

    * 如果在 Windows 7 (IIS 7.5) 上运行 Internet Explorer 10，则传输方法为 **iframe**。

    * 如果你在 Windows 8 上运行 Firefox 19 (IIS 8) ，则传输方法为 **websocket**。

        > [!TIP]
        > 在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。

    * 如果在 Windows 7 上运行 Firefox 19 (IIS 7.5) ，则传输方法为 **服务器发送** 事件。

## <a name="install-the-stockticker-sample"></a>安装 StockTicker 示例

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安装 StockTicker 应用程序。 NuGet 包包含的功能比从头创建的简化版本多。 在本教程的此部分中，你将安装 NuGet 包并查看实现这些功能的新功能和代码。

> [!IMPORTANT]
> 如果在不执行本教程前面的步骤的情况下安装包，则必须将 OWIN startup 类添加到项目。 此 NuGet 包的 readme.txt 文件说明了此步骤。

### <a name="install-the-signalrsample-nuget-package"></a>安装 SignalR NuGet 包

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“管理 NuGet 包” 。

1. 在 **NuGet 包管理器中： SignalR. StockTicker**，选择 " **浏览**"。

1. 从 " **包源**" 中，选择 **nuget.org**。

1. 在搜索框中输入*SignalR* ，并选择 " **SignalR**  >  **安装**"。

1. 在 **解决方案资源管理器**中，展开 " *SignalR* " 文件夹。

    安装 SignalR 包时，将创建该文件夹及其内容。

1. 在 *SignalR* 文件夹中，右键单击 *StockTicker.html*，然后选择 " **设为起始页**"。

    > [!NOTE]
    > 安装 SignalR NuGet 包可能会更改你在 *脚本* 文件夹中拥有的 jQuery 版本。 包安装在*SignalR*文件夹中的新*StockTicker.html*文件将与包所安装的 jQuery 版本同步，但是，如果想要再次运行原始*StockTicker.html*文件，则可能必须首先更新 script 标记中的 jQuery 引用。

### <a name="run-the-application"></a>运行应用程序

 在第一个应用中看到的表具有有用的功能。 整个股票行情股票行情应用程序将显示新功能：一个水平滚动窗口，其中显示了股票数据以及在其上升和下降时颜色变化的股票。

1. 按 **F5** 运行应用。

     首次运行应用程序时，"市场" 将为 "已关闭"，并且会看到一个静态表和一个不滚动的滚动条窗口。

1. 选择 " **开放市场**"。

    ![实时滚动的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * " **实时股票行情** " 框开始横向滚动，服务器将开始随机广播股票价格变化。

    * 每次股票价格变化时，应用都会更新 **实时股票表** 和 **实时股票**代码。

    * 当股票价格变化为正时，应用程序会显示绿色背景的纸张。

    * 如果更改为负数，应用程序会显示红色背景。

1. 选择 " **关闭市场**"。

    * 表更新停止。

    * 股票行情停止滚动。

1. 选择“重置”****。

    * 所有股票数据都将重置。

    * 应用在价格更改开始之前还原初始状态。

1. 从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。

1. 可以在每个浏览器中同时动态更新相同的数据。

1. 选择任何控件时，所有浏览器都将以相同的方式进行响应。

### <a name="live-stock-ticker-display"></a>直播股票行情显示

**Live 股票行情**显示在 `<div>` 按 CSS 样式格式化为单行的元素中的未排序列表。 应用程序以与表相同的方式初始化和更新该代号：通过在模板字符串中替换占位符 `<li>` 并将元素动态添加 `<li>` 到元素中 `<ul>` 。 应用包括使用 jQuery 函数进行滚动， `animate` 以改变中的无序列表的左边距 `<div>` 。

#### <a name="signalrsample-stocktickerhtml"></a>SignalR StockTicker.html

股票行情 HTML 代码：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR StockTicker

股票行情，CSS 代码：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR SignalR.StockTicker.js

使其滚动的 jQuery 代码：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>客户端可以调用的服务器上的其他方法

若要为应用添加灵活性，应用可以调用其他方法。

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR StockTickerHub.cs

`StockTickerHub`类定义了客户端可以调用的四种附加方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

应用程序会调用 `OpenMarket` 、 `CloseMarket` 和 `Reset` 以响应页面顶部的按钮。 它们演示了触发状态更改的客户端的模式立即传播到所有客户端。 其中每个方法都调用类中的一个方法 `StockTicker` ，该方法会导致市场状态发生变化，然后广播新状态。

#### <a name="signalrsample-stocktickercs"></a>SignalR StockTicker.cs

在 `StockTicker` 类中，应用使用 `MarketState` 返回枚举值的属性维护市场的状态 `MarketState` ：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

更改市场状态的每个方法都在锁块内进行，因为 `StockTicker` 该类必须是线程安全的：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

若要确保此代码是线程安全的，可 `_marketState` 支持 `MarketState` 指定属性的字段 `volatile` ：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`和 `BroadcastMarketReset` 方法类似于你已看到的 BroadcastStockPrice 方法，只不过它们调用在客户端定义的不同方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>服务器可以调用的客户端上的其他函数

`updateStockPrice`函数现在同时处理表和滚动条的显示，并使用 `jQuery.Color` 闪烁红色和绿色颜色。

中的新函数 *SignalR.StockTicker.js* 根据市场状态启用和禁用按钮。 它们还会停止或启动 **实时股票行情** 滚动条。 由于正在向添加很多函数 `ticker.client` ，应用程序使用 [jQuery extend 函数](http://api.jquery.com/jQuery.extend/) 添加它们。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立连接后的其他客户端设置

客户端建立连接后，还需要执行一些额外的工作：

* 查明市场是否已打开或已关闭，以调用相应的 `marketOpened` 或 `marketClosed` 函数。

* 将服务器方法调用附加到这些按钮。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

在应用程序建立连接之前，服务器方法不会连接到按钮。 这是为了使代码在可用之前无法调用服务器方法。

## <a name="additional-resources"></a>其他资源

在本教程中，你已了解如何对 SignalR 应用程序进行编程，以便将消息从服务器广播到所有连接的客户端。 现在，你可以定期广播消息和响应来自任何客户端的通知。 您可以使用多线程单一实例的概念在多玩家联机游戏方案中维护服务器状态。 有关示例，请参阅 [基于 SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。

有关显示对等通信方案的教程，入门请参阅 [SignalR With](introduction-to-signalr.md) And [实时更新 with SignalR](tutorial-high-frequency-realtime-with-signalr.md)。

有关 SignalR 的详细信息，请参阅以下资源：

* [ASP.NET SignalR](../../index.md)
* [SignalR 项目](http://signalr.net/)
* [SignalR GitHub 和示例](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>后续步骤

本教程介绍以下操作：

> [!div class="checklist"]
> * 已创建项目
> * 设置服务器代码
> * 检查服务器代码
> * 设置客户端代码
> * 检查了客户端代码
> * 已测试应用程序
> * 启用的日志记录

转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 的实时 web 应用程序。
> [!div class="nextstepaction"]
> [通过 SignalR 创建实时 web 应用](real-time-web-applications-with-signalr.md)

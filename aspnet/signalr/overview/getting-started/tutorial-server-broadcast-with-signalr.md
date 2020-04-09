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
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="1de15-103">教程：使用 SignalR 2 进行服务器广播</span><span class="sxs-lookup"><span data-stu-id="1de15-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="1de15-104">本教程演示如何创建使用ASP.NET SignalR 2 提供服务器广播功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1de15-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="1de15-105">服务器广播意味着服务器启动发送到客户端的通信。</span><span class="sxs-lookup"><span data-stu-id="1de15-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="1de15-106">您将在本教程中创建的应用程序模拟股票代码，这是服务器广播功能的典型方案。</span><span class="sxs-lookup"><span data-stu-id="1de15-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="1de15-107">服务器定期随机更新股票价格并将更新广播给所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="1de15-108">在浏览器中，"更改"和 **"** 列"中的数字和**%** 符号会动态更改，以响应来自服务器的通知。</span><span class="sxs-lookup"><span data-stu-id="1de15-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="1de15-109">如果打开其他浏览器到同一 URL，它们都同时显示相同的数据和对数据的相同更改。</span><span class="sxs-lookup"><span data-stu-id="1de15-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![创建 Web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="1de15-111">本教程介绍以下操作：</span><span class="sxs-lookup"><span data-stu-id="1de15-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1de15-112">创建项目</span><span class="sxs-lookup"><span data-stu-id="1de15-112">Create the project</span></span>
> * <span data-ttu-id="1de15-113">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-113">Set up the server code</span></span>
> * <span data-ttu-id="1de15-114">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-114">Examine the server code</span></span>
> * <span data-ttu-id="1de15-115">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-115">Set up the client code</span></span>
> * <span data-ttu-id="1de15-116">检查客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-116">Examine the client code</span></span>
> * <span data-ttu-id="1de15-117">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="1de15-117">Test the application</span></span>
> * <span data-ttu-id="1de15-118">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="1de15-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1de15-119">如果不想完成构建应用程序的步骤，可以在新的空ASP.NET Web 应用程序项目中安装 SignalR.sample 包。</span><span class="sxs-lookup"><span data-stu-id="1de15-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="1de15-120">如果不执行本教程中的步骤，安装 NuGet 包，则必须按照*readme.txt*文件中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="1de15-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="1de15-121">要运行包，您需要添加一个 OWIN 启动类，`ConfigureSignalR`该类调用已安装包中的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="1de15-122">如果不添加 OWIN 启动类，您将收到错误。</span><span class="sxs-lookup"><span data-stu-id="1de15-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="1de15-123">请参阅本文[的"安装库存价格"示例](#install-the-stockticker-sample)部分。</span><span class="sxs-lookup"><span data-stu-id="1de15-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1de15-124">先决条件</span><span class="sxs-lookup"><span data-stu-id="1de15-124">Prerequisites</span></span>

* <span data-ttu-id="1de15-125">带有 ASP.NET 和 Web 开发\*\*\*\* 工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="1de15-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="1de15-126">创建项目</span><span class="sxs-lookup"><span data-stu-id="1de15-126">Create the project</span></span>

<span data-ttu-id="1de15-127">本节演示如何使用 Visual Studio 2017 创建空ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1de15-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="1de15-128">在可视化工作室中，创建一个ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1de15-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 Web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="1de15-130">在新**ASP.NET Web 应用程序 - SignalR.StockTicker**窗口中，保留 **"空**"并选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="1de15-131">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-131">Set up the server code</span></span>

<span data-ttu-id="1de15-132">在本节中，您可以设置在服务器上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="1de15-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="1de15-133">创建"库存"类</span><span class="sxs-lookup"><span data-stu-id="1de15-133">Create the Stock class</span></span>

<span data-ttu-id="1de15-134">首先创建用于存储和传输库存信息*的 Stock*模型类。</span><span class="sxs-lookup"><span data-stu-id="1de15-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="1de15-135">在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **类**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="1de15-136">命名类*Stock*并将其添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="1de15-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="1de15-137">将*Stock.cs*文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="1de15-138">创建股票时要设置的两个属性是`Symbol`（例如，微软的 MSFT）和`Price`。</span><span class="sxs-lookup"><span data-stu-id="1de15-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="1de15-139">其他属性取决于设置`Price`的方式和时间。</span><span class="sxs-lookup"><span data-stu-id="1de15-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="1de15-140">第一次设置`Price`时，值将传播到 。 `DayOpen`</span><span class="sxs-lookup"><span data-stu-id="1de15-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="1de15-141">`Price`之后，当您设置 时，应用根据 和`Change``PercentChange``Price``DayOpen`之间的差异计算 和 属性值。</span><span class="sxs-lookup"><span data-stu-id="1de15-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="1de15-142">创建股票价格中心和股票提克类</span><span class="sxs-lookup"><span data-stu-id="1de15-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="1de15-143">您将使用 SignalR 中心 API 来处理服务器到客户端的交互。</span><span class="sxs-lookup"><span data-stu-id="1de15-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="1de15-144">派生`StockTickerHub`自 SignalR`Hub`类的类将处理来自客户端的接收连接和方法调用。</span><span class="sxs-lookup"><span data-stu-id="1de15-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="1de15-145">您还需要维护库存数据并运行对象`Timer`。</span><span class="sxs-lookup"><span data-stu-id="1de15-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="1de15-146">该`Timer`对象将定期触发独立于客户端连接的价格更新。</span><span class="sxs-lookup"><span data-stu-id="1de15-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="1de15-147">不能将这些函数放在`Hub`类中，因为中心是瞬态的。</span><span class="sxs-lookup"><span data-stu-id="1de15-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="1de15-148">应用为中心中的每个`Hub`任务创建一个类实例，例如从客户端到服务器的连接和调用。</span><span class="sxs-lookup"><span data-stu-id="1de15-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="1de15-149">因此，保存库存数据、更新价格和广播价格更新的机制必须运行在单独的类中。</span><span class="sxs-lookup"><span data-stu-id="1de15-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="1de15-150">您将命名该类`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="1de15-150">You'll name the class `StockTicker`.</span></span>

![从斯托克蒂克广播](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="1de15-152">您只需要在服务器上运行类的`StockTicker`一个实例，因此您需要设置从每个`StockTickerHub`实例到 singleton`StockTicker`实例的引用。</span><span class="sxs-lookup"><span data-stu-id="1de15-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="1de15-153">类`StockTicker`必须广播给客户端，因为它具有股票数据并触发更新，但不是`StockTicker``Hub`类。</span><span class="sxs-lookup"><span data-stu-id="1de15-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="1de15-154">类`StockTicker`必须获取对 SignalR 中心连接上下文对象的引用。</span><span class="sxs-lookup"><span data-stu-id="1de15-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="1de15-155">然后，它可以使用 SignalR 连接上下文对象广播到客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="1de15-156">创建StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="1de15-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="1de15-157">在**解决方案资源管理器**中，右键单击项目并选择**Add** > "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="1de15-158">在**添加新项目 - SignalR.StockTicker**中，选择 **"已安装** > **的可视 C#** > **Web** > **信号R"，** 然后选择**信号R集线器类 （v2）。**</span><span class="sxs-lookup"><span data-stu-id="1de15-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="1de15-159">命名类*StockTickerHub*并将其添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="1de15-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="1de15-160">此步骤将创建*StockTickerHub.cs*类文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="1de15-161">同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="1de15-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="1de15-162">将*StockTickerHub.cs*文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="1de15-163">保存文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-163">Save the file.</span></span>

<span data-ttu-id="1de15-164">应用使用[Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)类定义客户端可以在服务器上调用的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="1de15-165">您正在定义一种方法： `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="1de15-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="1de15-166">当客户端最初连接到服务器时，它将调用此方法来获取所有股票及其当前价格的列表。</span><span class="sxs-lookup"><span data-stu-id="1de15-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="1de15-167">该方法可以同步运行并返回`IEnumerable<Stock>`，因为它正在从内存返回数据。</span><span class="sxs-lookup"><span data-stu-id="1de15-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="1de15-168">如果方法必须通过执行涉及等待（如数据库查找或 Web 服务调用）来获取数据，则可以指定`Task<IEnumerable<Stock>>`为返回值以启用异步处理。</span><span class="sxs-lookup"><span data-stu-id="1de15-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="1de15-169">有关详细信息，请参阅[ASP.NET信号R集线器 API 指南 - 服务器 - 何时异步执行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。</span><span class="sxs-lookup"><span data-stu-id="1de15-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="1de15-170">该`HubName`属性指定应用如何在客户端上的 JavaScript 代码中引用 Hub。</span><span class="sxs-lookup"><span data-stu-id="1de15-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="1de15-171">如果不使用此属性，客户端上的默认名称是类名称的 camelCase 版本，在这种情况下，该版本为`stockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="1de15-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="1de15-172">稍后在创建`StockTicker`类时将看到，应用在其静态`Instance`属性中创建该类的单例实例。</span><span class="sxs-lookup"><span data-stu-id="1de15-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="1de15-173">无论连接或断开连接的`StockTicker`客户端数，该单例实例都位于内存中。</span><span class="sxs-lookup"><span data-stu-id="1de15-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="1de15-174">该实例是`GetAllStocks()`该方法用于返回当前库存信息的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="1de15-175">创建StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="1de15-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="1de15-176">在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **类**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="1de15-177">命名类*StockTicker*并将其添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="1de15-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="1de15-178">将*StockTicker.cs*文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="1de15-179">由于所有线程都将运行同一个 StockTicker 代码实例，因此 StockTicker 类必须具有线程安全。</span><span class="sxs-lookup"><span data-stu-id="1de15-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="1de15-180">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-180">Examine the server code</span></span>

<span data-ttu-id="1de15-181">如果检查服务器代码，它将帮助您了解应用的工作原理。</span><span class="sxs-lookup"><span data-stu-id="1de15-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="1de15-182">将单例实例存储在静态字段中</span><span class="sxs-lookup"><span data-stu-id="1de15-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="1de15-183">代码初始化使用类的实例`_instance`支持`Instance`属性的静态字段。</span><span class="sxs-lookup"><span data-stu-id="1de15-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="1de15-184">由于构造函数是私有的，因此它是应用可以创建的唯一类实例。</span><span class="sxs-lookup"><span data-stu-id="1de15-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="1de15-185">应用对`_instance`字段使用[延迟初始化](/dotnet/framework/performance/lazy-initialization)。</span><span class="sxs-lookup"><span data-stu-id="1de15-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="1de15-186">这不是出于性能原因。</span><span class="sxs-lookup"><span data-stu-id="1de15-186">It's not for performance reasons.</span></span> <span data-ttu-id="1de15-187">它确保实例创建是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="1de15-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="1de15-188">每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例从`StockTicker.Instance`静态属性获取 StockTicker 单例实例，如您在`StockTickerHub`类中前面看到的。</span><span class="sxs-lookup"><span data-stu-id="1de15-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="1de15-189">将库存数据存储在并发字典中</span><span class="sxs-lookup"><span data-stu-id="1de15-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="1de15-190">构造函数使用一些样本库存`_stocks`数据初始化集合，并`GetAllStocks`返回数据。</span><span class="sxs-lookup"><span data-stu-id="1de15-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="1de15-191">如前所述，此股票集合由 返回`StockTickerHub.GetAllStocks`，这是客户端可以调用的类中的`Hub`服务器方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="1de15-192">出于线程安全，股票集合定义为[并发字典](https://msdn.microsoft.com/library/dd287191.aspx)类型。</span><span class="sxs-lookup"><span data-stu-id="1de15-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="1de15-193">作为替代方法，您可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)对象，并在对字典进行更改时显式锁定字典。</span><span class="sxs-lookup"><span data-stu-id="1de15-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="1de15-194">对于此示例应用程序，可以将应用程序数据存储在内存中，并在应用释放`StockTicker`实例时丢失数据。</span><span class="sxs-lookup"><span data-stu-id="1de15-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="1de15-195">在实际应用程序中，您将像数据库一样使用后端数据存储。</span><span class="sxs-lookup"><span data-stu-id="1de15-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="1de15-196">定期更新股票价格</span><span class="sxs-lookup"><span data-stu-id="1de15-196">Periodically updating stock prices</span></span>

<span data-ttu-id="1de15-197">构造函数启动一个`Timer`对象，该对象定期调用随机更新股票价格的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="1de15-198">`Timer`调用`UpdateStockPrices`， 在状态参数中传递为 null。</span><span class="sxs-lookup"><span data-stu-id="1de15-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="1de15-199">在更新价格之前，应用会锁定`_updateStockPricesLock`对象。</span><span class="sxs-lookup"><span data-stu-id="1de15-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="1de15-200">代码检查另一个线程是否已更新价格，然后调用`TryUpdateStockPrice`列表中的每个股票。</span><span class="sxs-lookup"><span data-stu-id="1de15-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="1de15-201">该方法`TryUpdateStockPrice`决定是否更改股票价格，以及更改多少股票价格。</span><span class="sxs-lookup"><span data-stu-id="1de15-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="1de15-202">如果股票价格发生变化，应用将调用`BroadcastStockPrice`向所有连接的客户端广播股票价格变化。</span><span class="sxs-lookup"><span data-stu-id="1de15-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="1de15-203">指定`_updatingStockPrices`[易失性](https://msdn.microsoft.com/library/x13ttww7.aspx)的标志，以确保它是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="1de15-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="1de15-204">在实际应用程序中，`TryUpdateStockPrice`该方法将调用 Web 服务来查找价格。</span><span class="sxs-lookup"><span data-stu-id="1de15-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="1de15-205">在此代码中，应用程序使用随机数生成器随机进行更改。</span><span class="sxs-lookup"><span data-stu-id="1de15-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="1de15-206">获取 SignalR 上下文，以便 StockTicker 类可以广播给客户端</span><span class="sxs-lookup"><span data-stu-id="1de15-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="1de15-207">由于价格变化源自对象，`StockTicker`因此需要在所有连接的客户端上调用`updateStockPrice`方法的对象。</span><span class="sxs-lookup"><span data-stu-id="1de15-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="1de15-208">在类`Hub`中，您有用于调用客户端方法的 API，`StockTicker`但不派生自类`Hub`，并且没有对任何`Hub`对象的引用。</span><span class="sxs-lookup"><span data-stu-id="1de15-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="1de15-209">要广播到已连接的客户端`StockTicker`，类必须获取`StockTickerHub`类的 SignalR 上下文实例，并用它来调用客户端上的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="1de15-210">当代码创建单例类实例、传递该引用到构造函数时获取对 SignalR 上下文的`Clients`引用，构造函数将其放入属性中。</span><span class="sxs-lookup"><span data-stu-id="1de15-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="1de15-211">您只想获取上下文一次的原因有两个：获取上下文是一项昂贵的任务，一次获取上下文可确保应用保留发送到客户端的消息的预期顺序。</span><span class="sxs-lookup"><span data-stu-id="1de15-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="1de15-212">通过获取`Clients`上下文的属性并将其放入属性，`StockTickerClient`可以编写代码来调用与`Hub`类中看起来相同的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="1de15-213">例如，要广播到所有客户端，您可以写入`Clients.All.updateStockPrice(stock)`。</span><span class="sxs-lookup"><span data-stu-id="1de15-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="1de15-214">您`updateStockPrice`调用`BroadcastStockPrice`的方法尚不存在。</span><span class="sxs-lookup"><span data-stu-id="1de15-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="1de15-215">稍后，当您编写在客户端上运行的代码时，将添加它。</span><span class="sxs-lookup"><span data-stu-id="1de15-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="1de15-216">您可以在此处引用，`updateStockPrice`因为`Clients.All`是动态的，这意味着应用将在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="1de15-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="1de15-217">执行此方法调用时，SignalR 将向客户端发送方法名称和参数值，如果客户端具有名为`updateStockPrice`的方法，则应用将调用该方法并将参数值传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="1de15-218">`Clients.All`表示发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="1de15-219">SignalR 为您提供了其他选项来指定要发送到的客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="1de15-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="1de15-220">有关详细信息，请参阅[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1de15-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="1de15-221">注册信号R路由</span><span class="sxs-lookup"><span data-stu-id="1de15-221">Register the SignalR route</span></span>

<span data-ttu-id="1de15-222">服务器需要知道要拦截哪个 URL 并定向到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="1de15-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="1de15-223">为此，添加 OWIN 启动类：</span><span class="sxs-lookup"><span data-stu-id="1de15-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="1de15-224">在**解决方案资源管理器**中，右键单击项目并选择**Add** > "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="1de15-225">在 **"添加新项目 - SignalR.StockTicker"中选择\*\*\*\*"已安装** > **的可视化 C#** > **Web"，** 然后选择**OWIN 启动类**。</span><span class="sxs-lookup"><span data-stu-id="1de15-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="1de15-226">命名类 *"启动"* 并选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="1de15-227">将*Startup.cs*文件中的默认代码替换为此代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="1de15-228">您现在已完成服务器代码的设置。</span><span class="sxs-lookup"><span data-stu-id="1de15-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="1de15-229">在下一节中，您将设置客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="1de15-230">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-230">Set up the client code</span></span>

<span data-ttu-id="1de15-231">在本节中，设置在客户端上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="1de15-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="1de15-232">创建 HTML 页面和 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="1de15-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="1de15-233">HTML 页面将显示数据，JavaScript 文件将组织数据。</span><span class="sxs-lookup"><span data-stu-id="1de15-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="1de15-234">创建股票Ticker.html</span><span class="sxs-lookup"><span data-stu-id="1de15-234">Create StockTicker.html</span></span>

<span data-ttu-id="1de15-235">首先，您将添加 HTML 客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="1de15-236">在**解决方案资源管理器**中，右键单击项目并选择"**添加** > **HTML 页面**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="1de15-237">命名文件*库存Ticker*并选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="1de15-238">将*StockTicker.html*文件中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="1de15-239">HTML 创建一个包含五列的表、一个标题行和一个包含一个跨所有五列的单元格的数据行。</span><span class="sxs-lookup"><span data-stu-id="1de15-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="1de15-240">数据行显示"加载..."当应用程序启动时，瞬间。</span><span class="sxs-lookup"><span data-stu-id="1de15-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="1de15-241">JavaScript 代码将删除该行，并在其位置添加从服务器检索的股票数据行。</span><span class="sxs-lookup"><span data-stu-id="1de15-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="1de15-242">脚本标记指定：</span><span class="sxs-lookup"><span data-stu-id="1de15-242">The script tags specify:</span></span>

    * <span data-ttu-id="1de15-243">jQuery 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-243">The jQuery script file.</span></span>

    * <span data-ttu-id="1de15-244">SignalR 核心脚本文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="1de15-245">SignalR 代理脚本文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="1de15-246">稍后将创建的 StockTicker 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="1de15-247">应用程序动态生成 SignalR 代理脚本文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="1de15-248">它指定"/信号器/集线器"URL，并为 的 Hub 类（本例中）为 定义方法`StockTickerHub.GetAllStocks`的代理方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="1de15-249">如果您愿意，可以使用[SignalR 实用程序](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="1de15-250">不要忘记在方法调用中`MapHubs`禁用动态文件创建。</span><span class="sxs-lookup"><span data-stu-id="1de15-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="1de15-251">在**解决方案资源管理器中**，展开**脚本**。</span><span class="sxs-lookup"><span data-stu-id="1de15-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="1de15-252">jQuery 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="1de15-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1de15-253">包管理器将安装更高版本的 SignalR 脚本。</span><span class="sxs-lookup"><span data-stu-id="1de15-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="1de15-254">更新代码块中的脚本引用，以对应于项目中的脚本文件版本。</span><span class="sxs-lookup"><span data-stu-id="1de15-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="1de15-255">在**解决方案资源管理器**中，右键单击*StockTicker.html*，然后选择 **"设置为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="1de15-256">创建库存Ticker.js</span><span class="sxs-lookup"><span data-stu-id="1de15-256">Create StockTicker.js</span></span>

<span data-ttu-id="1de15-257">现在创建 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="1de15-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="1de15-258">在**解决方案资源管理器**中，右键单击项目并选择 **"添加** > **JavaScript 文件**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="1de15-259">命名文件*库存Ticker*并选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="1de15-260">将此代码添加到*StockTicker.js*文件：</span><span class="sxs-lookup"><span data-stu-id="1de15-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="1de15-261">检查客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-261">Examine the client code</span></span>

<span data-ttu-id="1de15-262">如果检查客户端代码，它将帮助您了解客户端代码如何与服务器代码交互以使应用正常工作。</span><span class="sxs-lookup"><span data-stu-id="1de15-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="1de15-263">启动连接</span><span class="sxs-lookup"><span data-stu-id="1de15-263">Starting the connection</span></span>

<span data-ttu-id="1de15-264">`$.connection`指 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="1de15-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="1de15-265">代码获取对类代理的引用，`StockTickerHub`并将其放入变量中。 `ticker`</span><span class="sxs-lookup"><span data-stu-id="1de15-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="1de15-266">代理名称是由`HubName`属性设置的名称：</span><span class="sxs-lookup"><span data-stu-id="1de15-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="1de15-267">定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR 函数初始化 SignalR`start`连接。</span><span class="sxs-lookup"><span data-stu-id="1de15-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="1de15-268">函数`start`异步执行并返回[jQuery 延迟对象](http://api.jquery.com/category/deferred-object/)。</span><span class="sxs-lookup"><span data-stu-id="1de15-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="1de15-269">可以调用完成函数来指定应用完成异步操作时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="1de15-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="1de15-270">获取所有股票</span><span class="sxs-lookup"><span data-stu-id="1de15-270">Getting all the stocks</span></span>

<span data-ttu-id="1de15-271">该`init`函数调用服务器上`getAllStocks`的函数，并使用服务器返回的信息来更新库存表。</span><span class="sxs-lookup"><span data-stu-id="1de15-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="1de15-272">请注意，默认情况下，您必须在客户端上使用 camelCasing，即使方法名称在服务器上是 pascalcase 的。</span><span class="sxs-lookup"><span data-stu-id="1de15-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="1de15-273">CamelCasing 规则仅适用于方法，不适用于对象。</span><span class="sxs-lookup"><span data-stu-id="1de15-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="1de15-274">例如，`stock.Symbol`您引用 和`stock.Price`，`stock.symbol`而不是`stock.price`或 。</span><span class="sxs-lookup"><span data-stu-id="1de15-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="1de15-275">在`init`方法中，应用通过`formatStock`调用对象的属性`stock`格式化，然后调用`supplant`将变量中的`rowTemplate`占位符替换为`stock`对象属性值，为从服务器接收的每个股票对象的表行创建 HTML。</span><span class="sxs-lookup"><span data-stu-id="1de15-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="1de15-276">然后，生成的 HTML 将追加到库存表中。</span><span class="sxs-lookup"><span data-stu-id="1de15-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="1de15-277">通过将其`init`作为在`callback`异步`start`函数完成后执行的函数传入来调用。</span><span class="sxs-lookup"><span data-stu-id="1de15-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="1de15-278">如果在调用`start`后`init`调用作为单独的 JavaScript 语句调用 ，则函数将失败，因为它将立即运行，而无需等待启动函数完成建立连接。</span><span class="sxs-lookup"><span data-stu-id="1de15-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="1de15-279">在这种情况下，`init`该函数将尝试在`getAllStocks`应用建立服务器连接之前调用该函数。</span><span class="sxs-lookup"><span data-stu-id="1de15-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="1de15-280">获取更新的股票价格</span><span class="sxs-lookup"><span data-stu-id="1de15-280">Getting updated stock prices</span></span>

<span data-ttu-id="1de15-281">当服务器更改股票价格时，它将调用`updateStockPrice`连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="1de15-282">应用将该函数添加到代理的客户端属性，`stockTicker`使其可用于来自服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="1de15-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="1de15-283">该`updateStockPrice`函数将从服务器接收的 Stock 对象格式化为表行，其方式与函数`init`中相同。</span><span class="sxs-lookup"><span data-stu-id="1de15-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="1de15-284">它不是将行追加到表中，而是在表中查找股票的当前行，并将该行替换为新行。</span><span class="sxs-lookup"><span data-stu-id="1de15-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="1de15-285">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="1de15-285">Test the application</span></span>

<span data-ttu-id="1de15-286">您可以测试应用以确保其正常工作。</span><span class="sxs-lookup"><span data-stu-id="1de15-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="1de15-287">您将看到所有浏览器窗口显示股票价格波动的实时库存表。</span><span class="sxs-lookup"><span data-stu-id="1de15-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="1de15-288">在工具栏中，打开**脚本调试**，然后选择播放按钮以在调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="1de15-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![用户打开调试模式和选择播放的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="1de15-290">将打开一个浏览器窗口，显示**实时库存表**。</span><span class="sxs-lookup"><span data-stu-id="1de15-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="1de15-291">库存表最初显示"加载..."行，然后，在很短的时间后，应用程序显示初始股票数据，然后股票价格开始变化。</span><span class="sxs-lookup"><span data-stu-id="1de15-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="1de15-292">从浏览器复制 URL，打开另外两个浏览器，并将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="1de15-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="1de15-293">初始库存显示与第一个浏览器相同，更改同时发生。</span><span class="sxs-lookup"><span data-stu-id="1de15-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="1de15-294">关闭所有浏览器，打开新浏览器，然后转到相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="1de15-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="1de15-295">StockTicker 单例对象继续在服务器中运行。</span><span class="sxs-lookup"><span data-stu-id="1de15-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="1de15-296">**实时库存表**显示，股票继续变化。</span><span class="sxs-lookup"><span data-stu-id="1de15-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="1de15-297">您看不到具有零更改数字的初始表。</span><span class="sxs-lookup"><span data-stu-id="1de15-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="1de15-298">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="1de15-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="1de15-299">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="1de15-299">Enable logging</span></span>

<span data-ttu-id="1de15-300">SignalR 具有内置日志记录功能，您可以在客户端上启用该功能，以帮助进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="1de15-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="1de15-301">在本节中，您可以启用日志记录，并查看示例，这些示例显示了日志如何告诉您 SignalR 正在使用以下哪种传输方法：</span><span class="sxs-lookup"><span data-stu-id="1de15-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="1de15-302">[WebSockets，](http://en.wikipedia.org/wiki/WebSocket)由IIS 8和当前浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="1de15-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="1de15-303">[服务器发送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet 资源管理器以外的浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="1de15-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="1de15-304">[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)，由 Internet 资源管理器支持。</span><span class="sxs-lookup"><span data-stu-id="1de15-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="1de15-305">[Ajax长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)，由所有浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="1de15-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="1de15-306">对于任何给定的连接，SignalR 选择服务器和客户端都支持的最佳传输方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="1de15-307">打开*股票Ticker.js*.</span><span class="sxs-lookup"><span data-stu-id="1de15-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="1de15-308">添加此突出显示的代码行，以便在文件末尾初始化连接的代码之前启用日志记录：</span><span class="sxs-lookup"><span data-stu-id="1de15-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="1de15-309">按**F5**以运行项目。</span><span class="sxs-lookup"><span data-stu-id="1de15-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="1de15-310">打开浏览器的开发人员工具窗口，然后选择控制台以查看日志。</span><span class="sxs-lookup"><span data-stu-id="1de15-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="1de15-311">您可能需要刷新页面才能看到 SignalR 协商新连接传输方法的日志。</span><span class="sxs-lookup"><span data-stu-id="1de15-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="1de15-312">如果您在 Windows 8 （IIS 8） 上运行 Internet 资源管理器 10，则传输方法是**WebSocket。**</span><span class="sxs-lookup"><span data-stu-id="1de15-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="1de15-313">如果您在 Windows 7（IIS 7.5）上运行 Internet 资源管理器 10，则传输方法是**iframe**。</span><span class="sxs-lookup"><span data-stu-id="1de15-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="1de15-314">如果您在 Windows 8 （IIS 8） 上运行 Firefox 19，则传输方法是**WebSocket。**</span><span class="sxs-lookup"><span data-stu-id="1de15-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="1de15-315">在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="1de15-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="1de15-316">如果您在 Windows 7（IIS 7.5）上运行 Firefox 19，则传输方法是**服务器发送**的事件。</span><span class="sxs-lookup"><span data-stu-id="1de15-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="1de15-317">安装库存价格示例</span><span class="sxs-lookup"><span data-stu-id="1de15-317">Install the StockTicker sample</span></span>

<span data-ttu-id="1de15-318">[微软.AspNet.SignalR.sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安装StockTicker应用程序。</span><span class="sxs-lookup"><span data-stu-id="1de15-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="1de15-319">与从头开始创建的简化版本相比，NuGet 包包含的功能更多。</span><span class="sxs-lookup"><span data-stu-id="1de15-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="1de15-320">在本教程的这一部分中，您可以安装 NuGet 包并查看新功能和实现这些功能的代码。</span><span class="sxs-lookup"><span data-stu-id="1de15-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1de15-321">如果不执行本教程的早期步骤，安装包，则必须向项目添加 OWIN 启动类。</span><span class="sxs-lookup"><span data-stu-id="1de15-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="1de15-322">NuGet 包的此 readme.txt 文件解释了此步骤。</span><span class="sxs-lookup"><span data-stu-id="1de15-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="1de15-323">安装信号R.样品 NuGet 封装</span><span class="sxs-lookup"><span data-stu-id="1de15-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="1de15-324">在**解决方案资源管理器**中，右键单击项目并选择 **"管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="1de15-325">在**NuGet 软件包管理器中：SignalR.StockTicker**，选择 **"浏览**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="1de15-326">从**包源**中，选择**nuget.org。**</span><span class="sxs-lookup"><span data-stu-id="1de15-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="1de15-327">在搜索框中输入*SignalR.示例*，然后选择**Microsoft.AspNet.SignalR.示例** > **安装**。</span><span class="sxs-lookup"><span data-stu-id="1de15-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="1de15-328">在**解决方案资源管理器中**，展开*SignalR.Sample*文件夹。</span><span class="sxs-lookup"><span data-stu-id="1de15-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="1de15-329">安装 SignalR.Sample 包创建了文件夹及其内容。</span><span class="sxs-lookup"><span data-stu-id="1de15-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="1de15-330">在*SignalR.sample*文件夹中，右键单击*StockTicker.html*，然后选择"**设置为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="1de15-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1de15-331">安装 SignalR.sample NuGet 包可能会更改*脚本*文件夹中的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="1de15-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="1de15-332">包在*SignalR.Sample*文件夹中安装的新*StockTicker.html*文件将与包安装的 jQuery 版本同步，但如果要再次运行原始*StockTicker.html*文件，您可能需要首先更新脚本标记中的 jQuery 引用。</span><span class="sxs-lookup"><span data-stu-id="1de15-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="1de15-333">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1de15-333">Run the application</span></span>

 <span data-ttu-id="1de15-334">您在第一个应用中看到的表具有有用的功能。</span><span class="sxs-lookup"><span data-stu-id="1de15-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="1de15-335">完整的股票代码应用程序显示新的功能：一个水平滚动窗口，显示股票数据和股票的变化颜色，因为他们的上升和下降。</span><span class="sxs-lookup"><span data-stu-id="1de15-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="1de15-336">按**F5**以运行应用。</span><span class="sxs-lookup"><span data-stu-id="1de15-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="1de15-337">首次运行应用时，"市场"是"关闭的"，您将看到一个静态表和一个未滚动的刻度窗口。</span><span class="sxs-lookup"><span data-stu-id="1de15-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="1de15-338">选择**公开市场**。</span><span class="sxs-lookup"><span data-stu-id="1de15-338">Select **Open Market**.</span></span>

    ![实时代码的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="1de15-340">**实时库存报价框**开始水平滚动，服务器开始随机广播股票价格变化。</span><span class="sxs-lookup"><span data-stu-id="1de15-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="1de15-341">每次股票价格变化时，应用程序都会更新**实时库存表**和**实时股票报价器**。</span><span class="sxs-lookup"><span data-stu-id="1de15-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="1de15-342">当股票价格变化为正时，应用程序将显示具有绿色背景的股票。</span><span class="sxs-lookup"><span data-stu-id="1de15-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="1de15-343">当更改为负时，应用程序将显示具有红色背景的股票。</span><span class="sxs-lookup"><span data-stu-id="1de15-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="1de15-344">选择**关闭市场**。</span><span class="sxs-lookup"><span data-stu-id="1de15-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="1de15-345">表更新停止。</span><span class="sxs-lookup"><span data-stu-id="1de15-345">The table updates stop.</span></span>

    * <span data-ttu-id="1de15-346">刻度线停止滚动。</span><span class="sxs-lookup"><span data-stu-id="1de15-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="1de15-347">选择“重置”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="1de15-347">Select **Reset**.</span></span>

    * <span data-ttu-id="1de15-348">重置所有库存数据。</span><span class="sxs-lookup"><span data-stu-id="1de15-348">All stock data is reset.</span></span>

    * <span data-ttu-id="1de15-349">应用在价格更改开始之前还原初始状态。</span><span class="sxs-lookup"><span data-stu-id="1de15-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="1de15-350">从浏览器复制 URL，打开另外两个浏览器，并将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="1de15-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="1de15-351">在每个浏览器中，您都会看到相同的数据同时动态更新。</span><span class="sxs-lookup"><span data-stu-id="1de15-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="1de15-352">当您选择任何控件时，所有浏览器都同时以相同的方式响应。</span><span class="sxs-lookup"><span data-stu-id="1de15-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="1de15-353">实时库存报价显示</span><span class="sxs-lookup"><span data-stu-id="1de15-353">Live Stock Ticker display</span></span>

<span data-ttu-id="1de15-354">**实时库存报价显示**是按 CSS 样式格式化为`<div>`单行的元素中的无序列表。</span><span class="sxs-lookup"><span data-stu-id="1de15-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="1de15-355">应用以与表相同的方式初始化和更新代码：通过在`<li>`模板字符串中替换占位符并动态地将`<li>`元素添加到`<ul>`元素。</span><span class="sxs-lookup"><span data-stu-id="1de15-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="1de15-356">该应用程序包括使用 jQuery`animate`函数来更改 中无序列表的边距左侧滚动。 `<div>`</span><span class="sxs-lookup"><span data-stu-id="1de15-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="1de15-357">信号R.样品库存Ticker.html</span><span class="sxs-lookup"><span data-stu-id="1de15-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="1de15-358">股票代码 HTML 代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="1de15-359">信号R.样品库存Ticker.css</span><span class="sxs-lookup"><span data-stu-id="1de15-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="1de15-360">股票代码 CSS 代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="1de15-361">信号R.样品信号R.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="1de15-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="1de15-362">使其滚动的 jQuery 代码：</span><span class="sxs-lookup"><span data-stu-id="1de15-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="1de15-363">客户端可以调用的服务器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="1de15-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="1de15-364">为了增加应用的灵活性，应用可以调用其他方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="1de15-365">信号R.样品StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="1de15-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="1de15-366">该`StockTickerHub`类定义了客户端可以调用的其他四种方法：</span><span class="sxs-lookup"><span data-stu-id="1de15-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="1de15-367">应用调用`OpenMarket`，`CloseMarket`并`Reset`响应页面顶部的按钮。</span><span class="sxs-lookup"><span data-stu-id="1de15-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="1de15-368">它们演示了一个客户端触发状态更改的模式，该更改将立即传播到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="1de15-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="1de15-369">这些方法中的每种方法都调用类中`StockTicker`导致市场状态更改然后广播新状态的方法。</span><span class="sxs-lookup"><span data-stu-id="1de15-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="1de15-370">信号R.样品StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="1de15-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="1de15-371">在类`StockTicker`中，应用使用返回`MarketState``MarketState`枚举值的属性维护市场状态：</span><span class="sxs-lookup"><span data-stu-id="1de15-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="1de15-372">更改市场状态的每个方法都会在锁块内执行此操作，`StockTicker`因为类必须是线程安全的：</span><span class="sxs-lookup"><span data-stu-id="1de15-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="1de15-373">为了确保此代码是线程安全的，支持指定的`_marketState``MarketState``volatile`属性的字段：</span><span class="sxs-lookup"><span data-stu-id="1de15-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="1de15-374">`BroadcastMarketStateChange`和`BroadcastMarketReset`方法与您已经看到的广播股票价格方法类似，但它们调用在客户端定义的不同方法：</span><span class="sxs-lookup"><span data-stu-id="1de15-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="1de15-375">服务器可以调用的客户端上的其他功能</span><span class="sxs-lookup"><span data-stu-id="1de15-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="1de15-376">该`updateStockPrice`函数现在同时处理表和刻度显示，它用于`jQuery.Color`闪烁红色和绿色。</span><span class="sxs-lookup"><span data-stu-id="1de15-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="1de15-377">*SignalR.StockTicker.js*中的新功能根据市场状态启用和禁用按钮。</span><span class="sxs-lookup"><span data-stu-id="1de15-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="1de15-378">它们还会停止或启动**实时库存刻度**水平滚动。</span><span class="sxs-lookup"><span data-stu-id="1de15-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="1de15-379">由于许多函数被添加到`ticker.client`，应用程序使用[jQuery 扩展函数](http://api.jquery.com/jQuery.extend/)来添加它们。</span><span class="sxs-lookup"><span data-stu-id="1de15-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="1de15-380">建立连接后的其他客户端设置</span><span class="sxs-lookup"><span data-stu-id="1de15-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="1de15-381">客户端建立连接后，它还有一些额外的工作要做：</span><span class="sxs-lookup"><span data-stu-id="1de15-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="1de15-382">了解市场是开放的还是关闭的，以调用适当的`marketOpened`或`marketClosed`功能。</span><span class="sxs-lookup"><span data-stu-id="1de15-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="1de15-383">将服务器方法调用附加到按钮。</span><span class="sxs-lookup"><span data-stu-id="1de15-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="1de15-384">服务器方法直到应用建立连接后才会连接到按钮。</span><span class="sxs-lookup"><span data-stu-id="1de15-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="1de15-385">因此，代码在服务器方法可用之前无法调用它们。</span><span class="sxs-lookup"><span data-stu-id="1de15-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1de15-386">其他资源</span><span class="sxs-lookup"><span data-stu-id="1de15-386">Additional resources</span></span>

<span data-ttu-id="1de15-387">在本教程中，您学习了如何对将消息从服务器广播到所有连接客户端的 SignalR 应用程序进行编程。</span><span class="sxs-lookup"><span data-stu-id="1de15-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="1de15-388">现在，您可以定期广播消息，并响应来自任何客户端的通知。</span><span class="sxs-lookup"><span data-stu-id="1de15-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="1de15-389">您可以使用多线程单例实例的概念在多人在线游戏方案中维护服务器状态。</span><span class="sxs-lookup"><span data-stu-id="1de15-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="1de15-390">例如，请参阅基于[SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="1de15-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="1de15-391">有关显示对等通信场景的教程，请参阅[使用 SignalR 入门](introduction-to-signalr.md)和使用[SignalR 进行实时更新](tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="1de15-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="1de15-392">有关 SignalR 的更多，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="1de15-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="1de15-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="1de15-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="1de15-394">信号器项目</span><span class="sxs-lookup"><span data-stu-id="1de15-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="1de15-395">信号R GitHub 和示例</span><span class="sxs-lookup"><span data-stu-id="1de15-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="1de15-396">信号R维基</span><span class="sxs-lookup"><span data-stu-id="1de15-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="1de15-397">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1de15-397">Next steps</span></span>

<span data-ttu-id="1de15-398">本教程介绍以下操作：</span><span class="sxs-lookup"><span data-stu-id="1de15-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1de15-399">已创建项目</span><span class="sxs-lookup"><span data-stu-id="1de15-399">Created the project</span></span>
> * <span data-ttu-id="1de15-400">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-400">Set up the server code</span></span>
> * <span data-ttu-id="1de15-401">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="1de15-401">Examined the server code</span></span>
> * <span data-ttu-id="1de15-402">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-402">Set up the client code</span></span>
> * <span data-ttu-id="1de15-403">检查客户端代码</span><span class="sxs-lookup"><span data-stu-id="1de15-403">Examined the client code</span></span>
> * <span data-ttu-id="1de15-404">已测试应用程序</span><span class="sxs-lookup"><span data-stu-id="1de15-404">Tested the application</span></span>
> * <span data-ttu-id="1de15-405">已启用日志记录</span><span class="sxs-lookup"><span data-stu-id="1de15-405">Enabled logging</span></span>

<span data-ttu-id="1de15-406">进入下一篇文章，了解如何创建使用ASP.NET SignalR 2 的实时 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1de15-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1de15-407">使用 SignalR 创建实时 Web 应用</span><span class="sxs-lookup"><span data-stu-id="1de15-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)

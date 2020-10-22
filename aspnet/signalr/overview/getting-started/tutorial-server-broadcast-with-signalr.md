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
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="97864-103">教程：服务器广播与 SignalR 2</span><span class="sxs-lookup"><span data-stu-id="97864-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="97864-104">本教程介绍如何创建使用 ASP.NET SignalR 2 的 web 应用程序来提供服务器广播功能。</span><span class="sxs-lookup"><span data-stu-id="97864-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="97864-105">服务器广播意味着服务器启动发送到客户端的通信。</span><span class="sxs-lookup"><span data-stu-id="97864-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="97864-106">你将在本教程中创建的应用程序模拟股票行情，这是服务器广播功能的典型方案。</span><span class="sxs-lookup"><span data-stu-id="97864-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="97864-107">服务器会定期定期更新股票价格，并将更新广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="97864-108">在浏览器中， **更改** 和列中的数字和符号会 **%** 动态更改以响应来自服务器的通知。</span><span class="sxs-lookup"><span data-stu-id="97864-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="97864-109">如果你打开相同 URL 的其他浏览器，则它们都同时显示相同的数据和相同的数据更改。</span><span class="sxs-lookup"><span data-stu-id="97864-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![创建 web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="97864-111">本教程介绍以下操作：</span><span class="sxs-lookup"><span data-stu-id="97864-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="97864-112">创建项目</span><span class="sxs-lookup"><span data-stu-id="97864-112">Create the project</span></span>
> * <span data-ttu-id="97864-113">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-113">Set up the server code</span></span>
> * <span data-ttu-id="97864-114">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-114">Examine the server code</span></span>
> * <span data-ttu-id="97864-115">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-115">Set up the client code</span></span>
> * <span data-ttu-id="97864-116">检查客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-116">Examine the client code</span></span>
> * <span data-ttu-id="97864-117">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="97864-117">Test the application</span></span>
> * <span data-ttu-id="97864-118">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="97864-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97864-119">如果不想完成生成应用程序的步骤，可以在新的空 ASP.NET Web 应用程序项目中安装 SignalR 包。</span><span class="sxs-lookup"><span data-stu-id="97864-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="97864-120">如果在不执行本教程中的步骤的情况下安装 NuGet 程序包，则必须按照 *readme.txt* 文件中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="97864-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="97864-121">若要运行包，您需要添加 OWIN startup 类，该类调用 `ConfigureSignalR` 已安装包中的方法。</span><span class="sxs-lookup"><span data-stu-id="97864-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="97864-122">如果未添加 OWIN startup 类，会收到错误。</span><span class="sxs-lookup"><span data-stu-id="97864-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="97864-123">请参阅本文的 [安装 StockTicker 示例](#install-the-stockticker-sample) 部分。</span><span class="sxs-lookup"><span data-stu-id="97864-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97864-124">必备条件</span><span class="sxs-lookup"><span data-stu-id="97864-124">Prerequisites</span></span>

* <span data-ttu-id="97864-125">带有 ASP.NET 和 Web 开发\*\*\*\* 工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="97864-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="97864-126">创建项目</span><span class="sxs-lookup"><span data-stu-id="97864-126">Create the project</span></span>

<span data-ttu-id="97864-127">本部分演示如何使用 Visual Studio 2017 创建空的 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="97864-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="97864-128">在 Visual Studio 中，创建一个 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="97864-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![创建 web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="97864-130">在 **新的 ASP.NET Web 应用程序-SignalR. StockTicker** 窗口中，保留 **为空** ，并选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="97864-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="97864-131">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-131">Set up the server code</span></span>

<span data-ttu-id="97864-132">在本部分中，将设置运行在服务器上的代码。</span><span class="sxs-lookup"><span data-stu-id="97864-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="97864-133">创建 Stock 类</span><span class="sxs-lookup"><span data-stu-id="97864-133">Create the Stock class</span></span>

<span data-ttu-id="97864-134">首先，创建用于存储和传输股票信息的 *stock* 模型类。</span><span class="sxs-lookup"><span data-stu-id="97864-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="97864-135">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **类**"。</span><span class="sxs-lookup"><span data-stu-id="97864-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="97864-136">命名类 *库存* 并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="97864-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="97864-137">将 *Stock.cs* 文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="97864-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="97864-138">创建股票时将设置的两个属性 `Symbol` 为 (例如，MSFT For Microsoft) 和 `Price` 。</span><span class="sxs-lookup"><span data-stu-id="97864-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="97864-139">其他属性取决于设置的方式和时间 `Price` 。</span><span class="sxs-lookup"><span data-stu-id="97864-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="97864-140">第一次设置时 `Price` ，该值将传播到 `DayOpen` 。</span><span class="sxs-lookup"><span data-stu-id="97864-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="97864-141">之后，在设置时 `Price` ，应用程序会 `Change` `PercentChange` 基于和之间的差异计算和属性值 `Price` `DayOpen` 。</span><span class="sxs-lookup"><span data-stu-id="97864-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="97864-142">创建 StockTickerHub 和 StockTicker 类</span><span class="sxs-lookup"><span data-stu-id="97864-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="97864-143">你将使用 SignalR 中心 API 来处理服务器到客户端的交互。</span><span class="sxs-lookup"><span data-stu-id="97864-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="97864-144">`StockTickerHub`派生自 SignalR 类的类 `Hub` 将处理从客户端接收连接和方法调用。</span><span class="sxs-lookup"><span data-stu-id="97864-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="97864-145">还需要维护股票数据并运行 `Timer` 对象。</span><span class="sxs-lookup"><span data-stu-id="97864-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="97864-146">`Timer`对象将定期触发价格更新，独立于客户端连接。</span><span class="sxs-lookup"><span data-stu-id="97864-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="97864-147">不能将这些函数放在 `Hub` 类中，因为中心是暂时性的。</span><span class="sxs-lookup"><span data-stu-id="97864-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="97864-148">应用程序 `Hub` 为中心上的每个任务创建一个类实例，如连接和从客户端到服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="97864-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="97864-149">因此，保留股票数据、更新价格和广播价格更新的机制必须在单独的类中运行。</span><span class="sxs-lookup"><span data-stu-id="97864-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="97864-150">你将为类命名 `StockTicker` 。</span><span class="sxs-lookup"><span data-stu-id="97864-150">You'll name the class `StockTicker`.</span></span>

![从 StockTicker 广播](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="97864-152">您只希望在 `StockTicker` 服务器上运行类的一个实例，因此您需要设置从每个 `StockTickerHub` 实例到单一实例的引用 `StockTicker` 。</span><span class="sxs-lookup"><span data-stu-id="97864-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="97864-153">`StockTicker`类必须广播到客户端，因为它具有股票数据并触发更新，但 `StockTicker` 不是 `Hub` 类。</span><span class="sxs-lookup"><span data-stu-id="97864-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="97864-154">`StockTicker`类必须获取对 SignalR 中心连接上下文对象的引用。</span><span class="sxs-lookup"><span data-stu-id="97864-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="97864-155">然后，它可以使用 SignalR 连接上下文对象广播到客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="97864-156">创建 StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="97864-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="97864-157">在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **新项**"。</span><span class="sxs-lookup"><span data-stu-id="97864-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="97864-158">在 "**添加新项-SignalR. StockTicker**" 中，选择 "**已安装**  >  **Visual c #**  >  **Web**  >  **SignalR** "，然后选择\*\*SignalR Hub 类 (v2) \*\*。</span><span class="sxs-lookup"><span data-stu-id="97864-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="97864-159">将类命名为 *StockTickerHub* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="97864-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="97864-160">此步骤将创建 *StockTickerHub.cs* 类文件。</span><span class="sxs-lookup"><span data-stu-id="97864-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="97864-161">同时，它将一组支持 SignalR 的脚本文件和程序集引用添加到项目。</span><span class="sxs-lookup"><span data-stu-id="97864-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="97864-162">将 *StockTickerHub.cs* 文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="97864-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="97864-163">保存文件。</span><span class="sxs-lookup"><span data-stu-id="97864-163">Save the file.</span></span>

<span data-ttu-id="97864-164">应用使用 [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 类定义客户端可以在服务器上调用的方法。</span><span class="sxs-lookup"><span data-stu-id="97864-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="97864-165">您正在定义一个方法： `GetAllStocks()` 。</span><span class="sxs-lookup"><span data-stu-id="97864-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="97864-166">当客户端最初连接到服务器时，它将调用此方法以获取所有股票的列表及其当前价格。</span><span class="sxs-lookup"><span data-stu-id="97864-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="97864-167">方法可以同步运行并返回， `IEnumerable<Stock>` 因为它是从内存返回数据。</span><span class="sxs-lookup"><span data-stu-id="97864-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="97864-168">如果该方法必须通过执行需要等待的内容（如数据库查找或 web 服务调用）来获取数据，则应将指定 `Task<IEnumerable<Stock>>` 为返回值以启用异步处理。</span><span class="sxs-lookup"><span data-stu-id="97864-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="97864-169">有关详细信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-When to 异步执行的时间](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。</span><span class="sxs-lookup"><span data-stu-id="97864-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="97864-170">`HubName`特性指定应用程序将如何在客户端上的 JavaScript 代码中引用中心。</span><span class="sxs-lookup"><span data-stu-id="97864-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="97864-171">如果不使用此属性，则客户端上的默认名称是类名的 camelCase 版本，在本例中为 `stockTickerHub` 。</span><span class="sxs-lookup"><span data-stu-id="97864-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="97864-172">稍后在创建 `StockTicker` 类时，应用程序会在其静态属性中创建该类的单一实例 `Instance` 。</span><span class="sxs-lookup"><span data-stu-id="97864-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="97864-173">无论 `StockTicker` 有多少客户端连接或断开连接，的单一实例都在内存中。</span><span class="sxs-lookup"><span data-stu-id="97864-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="97864-174">该实例就是 `GetAllStocks()` 方法用来返回当前股票信息的内容。</span><span class="sxs-lookup"><span data-stu-id="97864-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="97864-175">创建 StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="97864-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="97864-176">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **类**"。</span><span class="sxs-lookup"><span data-stu-id="97864-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="97864-177">将类命名为 *StockTicker* ，并将其添加到项目。</span><span class="sxs-lookup"><span data-stu-id="97864-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="97864-178">将 *StockTicker.cs* 文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="97864-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="97864-179">由于所有线程都将运行 StockTicker 代码的同一个实例，因此 StockTicker 类必须是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="97864-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="97864-180">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-180">Examine the server code</span></span>

<span data-ttu-id="97864-181">如果检查服务器代码，它将帮助你了解应用的工作原理。</span><span class="sxs-lookup"><span data-stu-id="97864-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="97864-182">将单一实例存储在静态字段中</span><span class="sxs-lookup"><span data-stu-id="97864-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="97864-183">此代码 `_instance` 使用类的实例初始化用于支持属性的静态字段 `Instance` 。</span><span class="sxs-lookup"><span data-stu-id="97864-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="97864-184">由于构造函数是私有的，因此它是应用可创建的类的唯一实例。</span><span class="sxs-lookup"><span data-stu-id="97864-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="97864-185">该应用对字段使用 [迟缓初始化](/dotnet/framework/performance/lazy-initialization) `_instance` 。</span><span class="sxs-lookup"><span data-stu-id="97864-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="97864-186">这不是出于性能方面的原因。</span><span class="sxs-lookup"><span data-stu-id="97864-186">It's not for performance reasons.</span></span> <span data-ttu-id="97864-187">这是为了确保实例创建是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="97864-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="97864-188">每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例将从静态属性获取 StockTicker 单一实例 `StockTicker.Instance` ，正如你之前在类中看到的一样 `StockTickerHub` 。</span><span class="sxs-lookup"><span data-stu-id="97864-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="97864-189">在 ConcurrentDictionary 中存储股票数据</span><span class="sxs-lookup"><span data-stu-id="97864-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="97864-190">构造函数 `_stocks` 用一些示例股票数据初始化集合，并 `GetAllStocks` 返回股票。</span><span class="sxs-lookup"><span data-stu-id="97864-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="97864-191">如前文所述，此股票集合由返回 `StockTickerHub.GetAllStocks` ，这是客户端可调用的类中的服务器方法 `Hub` 。</span><span class="sxs-lookup"><span data-stu-id="97864-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="97864-192">股票集合定义为线程安全的 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 类型。</span><span class="sxs-lookup"><span data-stu-id="97864-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="97864-193">作为替代方法，可以使用 [字典](https://msdn.microsoft.com/library/xfhwa508.aspx) 对象，并在对字典进行更改时显式锁定字典。</span><span class="sxs-lookup"><span data-stu-id="97864-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="97864-194">在此示例应用程序中，可以将应用程序数据存储在内存中，并在应用程序释放实例时丢失数据  `StockTicker` 。</span><span class="sxs-lookup"><span data-stu-id="97864-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="97864-195">在实际应用程序中，可以使用数据库之类的后端数据存储。</span><span class="sxs-lookup"><span data-stu-id="97864-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="97864-196">定期更新股票价格</span><span class="sxs-lookup"><span data-stu-id="97864-196">Periodically updating stock prices</span></span>

<span data-ttu-id="97864-197">构造函数将启动一个 `Timer` 对象，该对象定期调用可随机更新股票价格的方法。</span><span class="sxs-lookup"><span data-stu-id="97864-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="97864-198">`Timer` 调用 `UpdateStockPrices` ，在状态参数中传入 null。</span><span class="sxs-lookup"><span data-stu-id="97864-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="97864-199">更新价格之前，应用会对对象进行锁定 `_updateStockPricesLock` 。</span><span class="sxs-lookup"><span data-stu-id="97864-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="97864-200">该代码将检查是否有另一个线程正在更新价格，然后 `TryUpdateStockPrice` 在列表中的每个股票上调用。</span><span class="sxs-lookup"><span data-stu-id="97864-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="97864-201">`TryUpdateStockPrice`方法决定是否更改股票价格，以及更改的量。</span><span class="sxs-lookup"><span data-stu-id="97864-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="97864-202">如果股票价格发生变化，应用程序 `BroadcastStockPrice` 将调用以将股票价格更改广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="97864-203">`_updatingStockPrices`指定为[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)的标志，以确保它是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="97864-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="97864-204">在实际应用程序中，该 `TryUpdateStockPrice` 方法将调用 web 服务来查找价格。</span><span class="sxs-lookup"><span data-stu-id="97864-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="97864-205">在此代码中，应用程序使用随机数生成器来随机进行更改。</span><span class="sxs-lookup"><span data-stu-id="97864-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="97864-206">获取 SignalR 上下文以便 StockTicker 类可以广播到客户端</span><span class="sxs-lookup"><span data-stu-id="97864-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="97864-207">因为价格变化源自 `StockTicker` 对象，所以它是需要 `updateStockPrice` 在所有连接的客户端上调用方法的对象。</span><span class="sxs-lookup"><span data-stu-id="97864-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="97864-208">在 `Hub` 类中，你有一个用于调用客户端方法的 API，但它 `StockTicker` 不是从类派生的， `Hub` 并且不具有对任何对象的引用 `Hub` 。</span><span class="sxs-lookup"><span data-stu-id="97864-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="97864-209">若要广播到连接的客户端， `StockTicker` 该类必须获取类的 SignalR 上下文实例， `StockTickerHub` 并使用该实例对客户端调用方法。</span><span class="sxs-lookup"><span data-stu-id="97864-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="97864-210">此代码在创建单一实例类实例时获取对 SignalR 上下文的引用，将该引用传递给构造函数，构造函数将该引用传递到 `Clients` 属性中。</span><span class="sxs-lookup"><span data-stu-id="97864-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="97864-211">只需获取上下文一次只需两个原因：获取上下文是一种成本高昂的任务，并将其启用一次，确保应用保留发送到客户端的预期消息顺序。</span><span class="sxs-lookup"><span data-stu-id="97864-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="97864-212">如果获取 `Clients` 上下文的属性并将其放在属性中， `StockTickerClient` 则可以编写代码来调用与类中外观相同的客户端方法 `Hub` 。</span><span class="sxs-lookup"><span data-stu-id="97864-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="97864-213">例如，要广播到可以写入的所有客户端 `Clients.All.updateStockPrice(stock)` 。</span><span class="sxs-lookup"><span data-stu-id="97864-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="97864-214">`updateStockPrice`你在中调用的方法 `BroadcastStockPrice` 尚不存在。</span><span class="sxs-lookup"><span data-stu-id="97864-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="97864-215">稍后在编写在客户端上运行的代码时，将添加此代码。</span><span class="sxs-lookup"><span data-stu-id="97864-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="97864-216">您可以在 `updateStockPrice` 这里引用 `Clients.All` ，因为是动态的，这意味着应用程序将在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="97864-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="97864-217">此方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有名为的方法 `updateStockPrice` ，则应用程序将调用该方法并向其传递参数值。</span><span class="sxs-lookup"><span data-stu-id="97864-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="97864-218">`Clients.All` 表示发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="97864-219">SignalR 提供其他选项来指定要发送到的客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="97864-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="97864-220">有关详细信息，请参阅 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="97864-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="97864-221">注册 SignalR 路由</span><span class="sxs-lookup"><span data-stu-id="97864-221">Register the SignalR route</span></span>

<span data-ttu-id="97864-222">服务器需要知道要截获哪个 URL，并将其定向到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="97864-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="97864-223">为此，请添加 OWIN startup 类：</span><span class="sxs-lookup"><span data-stu-id="97864-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="97864-224">在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **新项**"。</span><span class="sxs-lookup"><span data-stu-id="97864-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="97864-225">在 "**添加新项-SignalR. StockTicker** " 中选择 "**已安装**  >  **Visual c #**  >  **Web** "，然后选择 " **OWIN Startup 类**"。</span><span class="sxs-lookup"><span data-stu-id="97864-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="97864-226">将类命名为 " *启动* "，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="97864-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="97864-227">将 *Startup.cs* 文件中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="97864-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="97864-228">你现在已经完成了服务器代码的设置。</span><span class="sxs-lookup"><span data-stu-id="97864-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="97864-229">在下一部分中，你将设置客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="97864-230">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-230">Set up the client code</span></span>

<span data-ttu-id="97864-231">在本部分中，将设置在客户端上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="97864-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="97864-232">创建 HTML 页和 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="97864-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="97864-233">HTML 页面将显示数据，JavaScript 文件将对数据进行组织。</span><span class="sxs-lookup"><span data-stu-id="97864-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="97864-234">创建 StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="97864-234">Create StockTicker.html</span></span>

<span data-ttu-id="97864-235">首先，您将添加 HTML 客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="97864-236">在**解决方案资源管理器**中，右键单击项目并选择 "**添加**  >  **HTML 页**"。</span><span class="sxs-lookup"><span data-stu-id="97864-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="97864-237">将该文件命名为 *StockTicker* ，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="97864-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="97864-238">将 *StockTicker.html* 文件中的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="97864-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="97864-239">HTML 将创建一个表，其中包含五个列和一个标题行，以及一个包含跨所有5列的单个单元的数据行。</span><span class="sxs-lookup"><span data-stu-id="97864-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="97864-240">数据行显示 "正在加载 ..."应用启动。</span><span class="sxs-lookup"><span data-stu-id="97864-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="97864-241">JavaScript 代码将删除该行，并在其位置行中添加从服务器检索到的股票数据。</span><span class="sxs-lookup"><span data-stu-id="97864-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="97864-242">脚本标记指定：</span><span class="sxs-lookup"><span data-stu-id="97864-242">The script tags specify:</span></span>

    * <span data-ttu-id="97864-243">JQuery 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97864-243">The jQuery script file.</span></span>

    * <span data-ttu-id="97864-244">SignalR 核心脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97864-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="97864-245">SignalR 代理脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97864-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="97864-246">稍后将创建的 StockTicker 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97864-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="97864-247">应用会动态生成 SignalR 代理脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97864-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="97864-248">它指定 "/signalr/hubs" URL，并为 Hub 类上的方法（在本例中为）定义代理方法 `StockTickerHub.GetAllStocks` 。</span><span class="sxs-lookup"><span data-stu-id="97864-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="97864-249">如果愿意，可以使用 [SignalR 实用工具](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="97864-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="97864-250">请不要忘记在方法调用中禁用动态文件创建 `MapHubs` 。</span><span class="sxs-lookup"><span data-stu-id="97864-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="97864-251">在 **解决方案资源管理器**中，展开 " **脚本**"。</span><span class="sxs-lookup"><span data-stu-id="97864-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="97864-252">JQuery 和 SignalR 的脚本库在项目中可见。</span><span class="sxs-lookup"><span data-stu-id="97864-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="97864-253">程序包管理器将安装较新版本的 SignalR 脚本。</span><span class="sxs-lookup"><span data-stu-id="97864-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="97864-254">更新代码块中的脚本引用，使其与项目中的脚本文件版本相对应。</span><span class="sxs-lookup"><span data-stu-id="97864-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="97864-255">在 **解决方案资源管理器**中，右键单击 *StockTicker.html*，然后选择 " **设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="97864-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="97864-256">创建 StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="97864-256">Create StockTicker.js</span></span>

<span data-ttu-id="97864-257">现在创建 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="97864-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="97864-258">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加**  >  **JavaScript 文件**"。</span><span class="sxs-lookup"><span data-stu-id="97864-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="97864-259">将该文件命名为 *StockTicker* ，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="97864-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="97864-260">将以下代码添加到 *StockTicker.js* 文件：</span><span class="sxs-lookup"><span data-stu-id="97864-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="97864-261">检查客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-261">Examine the client code</span></span>

<span data-ttu-id="97864-262">如果检查客户端代码，它将帮助您了解客户端代码如何与服务器代码交互以使应用程序正常工作。</span><span class="sxs-lookup"><span data-stu-id="97864-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="97864-263">启动连接</span><span class="sxs-lookup"><span data-stu-id="97864-263">Starting the connection</span></span>

<span data-ttu-id="97864-264">`$.connection` 引用 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="97864-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="97864-265">此代码获取对类的代理的引用 `StockTickerHub` 并将其放在变量中 `ticker` 。</span><span class="sxs-lookup"><span data-stu-id="97864-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="97864-266">代理名称是由属性设置的名称 `HubName` ：</span><span class="sxs-lookup"><span data-stu-id="97864-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="97864-267">定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR 函数初始化 SignalR 连接 `start` 。</span><span class="sxs-lookup"><span data-stu-id="97864-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="97864-268">`start`函数以异步方式执行，并返回[jQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)。</span><span class="sxs-lookup"><span data-stu-id="97864-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="97864-269">可以调用 done 函数来指定应用完成异步操作时要调用的函数。</span><span class="sxs-lookup"><span data-stu-id="97864-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="97864-270">获取所有股票</span><span class="sxs-lookup"><span data-stu-id="97864-270">Getting all the stocks</span></span>

<span data-ttu-id="97864-271">`init`函数调用 `getAllStocks` 服务器上的函数，并使用服务器返回的信息更新股票表。</span><span class="sxs-lookup"><span data-stu-id="97864-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="97864-272">请注意，默认情况下，你必须在客户端上使用 camelCasing，即使方法名称在服务器上采用 pascal 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="97864-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="97864-273">CamelCasing 规则仅适用于方法，而不适用于对象。</span><span class="sxs-lookup"><span data-stu-id="97864-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="97864-274">例如，引用 `stock.Symbol` 和 `stock.Price` ，而不是 `stock.symbol` 或 `stock.price` 。</span><span class="sxs-lookup"><span data-stu-id="97864-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="97864-275">在 `init` 方法中，应用程序为从服务器接收的每个 stock 对象创建一个表行的 HTML，方法是调用 `formatStock` 以设置 `stock` 对象的属性，然后调用 `supplant` 将变量中的占位符替换为 `rowTemplate` `stock` 对象属性值。</span><span class="sxs-lookup"><span data-stu-id="97864-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="97864-276">然后，将生成的 HTML 追加到 stock 表中。</span><span class="sxs-lookup"><span data-stu-id="97864-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="97864-277">通过将 `init` 其作为在 `callback` 异步函数完成后执行的函数传入来调用 `start` 。</span><span class="sxs-lookup"><span data-stu-id="97864-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="97864-278">如果在 `init` 调用后将作为单独的 JavaScript 语句调用 `start` ，则函数将失败，因为它会立即运行，而不会等待启动函数完成连接的建立。</span><span class="sxs-lookup"><span data-stu-id="97864-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="97864-279">在这种情况下，该 `init` 函数将尝试在 `getAllStocks` 应用程序建立服务器连接之前调用函数。</span><span class="sxs-lookup"><span data-stu-id="97864-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="97864-280">获取更新后的股票价格</span><span class="sxs-lookup"><span data-stu-id="97864-280">Getting updated stock prices</span></span>

<span data-ttu-id="97864-281">当服务器更改股票价格时，它将 `updateStockPrice` 在连接的客户端上调用。</span><span class="sxs-lookup"><span data-stu-id="97864-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="97864-282">应用将函数添加到代理的客户端属性 `stockTicker` ，使其可用于从服务器调用。</span><span class="sxs-lookup"><span data-stu-id="97864-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="97864-283">`updateStockPrice`函数将从服务器接收的 stock 对象的格式设置为与在函数中相同的方式 `init` 。</span><span class="sxs-lookup"><span data-stu-id="97864-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="97864-284">它在表中查找股票的当前行，而不是将该行追加到表中，而是将该行替换为新行。</span><span class="sxs-lookup"><span data-stu-id="97864-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="97864-285">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="97864-285">Test the application</span></span>

<span data-ttu-id="97864-286">可以测试应用程序以确保其正常运行。</span><span class="sxs-lookup"><span data-stu-id="97864-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="97864-287">你将看到所有浏览器窗口都显示股票价格波动的实时股票表。</span><span class="sxs-lookup"><span data-stu-id="97864-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="97864-288">在工具栏上，打开 " **脚本调试** "，然后选择 "播放" 按钮以调试模式运行应用。</span><span class="sxs-lookup"><span data-stu-id="97864-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![用户打开调试模式并选择 "播放" 的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="97864-290">将打开一个浏览器窗口，其中显示了 **实时股票表**。</span><span class="sxs-lookup"><span data-stu-id="97864-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="97864-291">Stock 表最初显示 "正在加载 ..."行，然后在一小段时间后，应用程序会显示初始股票数据，然后股票价格开始改变。</span><span class="sxs-lookup"><span data-stu-id="97864-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="97864-292">从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="97864-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="97864-293">初始股票显示器与第一个浏览器相同，同时发生更改。</span><span class="sxs-lookup"><span data-stu-id="97864-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="97864-294">关闭所有浏览器，打开新的浏览器，并中转到相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="97864-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="97864-295">StockTicker singleton 对象继续在服务器中运行。</span><span class="sxs-lookup"><span data-stu-id="97864-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="97864-296">**Live 表**显示股票已继续更改。</span><span class="sxs-lookup"><span data-stu-id="97864-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="97864-297">看不到具有零更改图的初始表。</span><span class="sxs-lookup"><span data-stu-id="97864-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="97864-298">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="97864-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="97864-299">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="97864-299">Enable logging</span></span>

<span data-ttu-id="97864-300">SignalR 具有内置日志记录功能，可以在客户端上启用该功能以帮助进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="97864-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="97864-301">在本部分中，将启用日志记录，并查看示例，其中显示了日志如何说明 SignalR 正在使用以下哪种传输方法：</span><span class="sxs-lookup"><span data-stu-id="97864-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="97864-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket)，受 IIS 8 和当前浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="97864-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="97864-303">Internet Explorer 之外的浏览器所支持的[服务器发送事件](http://en.wikipedia.org/wiki/Server-sent_events)。</span><span class="sxs-lookup"><span data-stu-id="97864-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="97864-304">Internet Explorer 支持的[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。</span><span class="sxs-lookup"><span data-stu-id="97864-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="97864-305">所有浏览器都支持[Ajax 长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。</span><span class="sxs-lookup"><span data-stu-id="97864-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="97864-306">对于任何给定的连接，SignalR 将选择服务器和客户端都支持的最佳传输方法。</span><span class="sxs-lookup"><span data-stu-id="97864-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="97864-307">打开 *StockTicker.js*。</span><span class="sxs-lookup"><span data-stu-id="97864-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="97864-308">添加以下突出显示的代码行，以便在文件末尾初始化连接的代码之前立即启用日志记录：</span><span class="sxs-lookup"><span data-stu-id="97864-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="97864-309">按 **F5** 运行项目。</span><span class="sxs-lookup"><span data-stu-id="97864-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="97864-310">打开浏览器的 "开发人员工具" 窗口，并选择控制台查看日志。</span><span class="sxs-lookup"><span data-stu-id="97864-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="97864-311">您可能必须刷新该页才能查看为新连接协商传输方法的 SignalR 的日志。</span><span class="sxs-lookup"><span data-stu-id="97864-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="97864-312">如果你在 Windows 8 上运行 Internet Explorer 10 (IIS 8) ，则传输方法为 **websocket**。</span><span class="sxs-lookup"><span data-stu-id="97864-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="97864-313">如果在 Windows 7 (IIS 7.5) 上运行 Internet Explorer 10，则传输方法为 **iframe**。</span><span class="sxs-lookup"><span data-stu-id="97864-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="97864-314">如果你在 Windows 8 上运行 Firefox 19 (IIS 8) ，则传输方法为 **websocket**。</span><span class="sxs-lookup"><span data-stu-id="97864-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="97864-315">在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="97864-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="97864-316">如果在 Windows 7 上运行 Firefox 19 (IIS 7.5) ，则传输方法为 **服务器发送** 事件。</span><span class="sxs-lookup"><span data-stu-id="97864-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="97864-317">安装 StockTicker 示例</span><span class="sxs-lookup"><span data-stu-id="97864-317">Install the StockTicker sample</span></span>

<span data-ttu-id="97864-318">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安装 StockTicker 应用程序。</span><span class="sxs-lookup"><span data-stu-id="97864-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="97864-319">NuGet 包包含的功能比从头创建的简化版本多。</span><span class="sxs-lookup"><span data-stu-id="97864-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="97864-320">在本教程的此部分中，你将安装 NuGet 包并查看实现这些功能的新功能和代码。</span><span class="sxs-lookup"><span data-stu-id="97864-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97864-321">如果在不执行本教程前面的步骤的情况下安装包，则必须将 OWIN startup 类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="97864-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="97864-322">此 NuGet 包的 readme.txt 文件说明了此步骤。</span><span class="sxs-lookup"><span data-stu-id="97864-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="97864-323">安装 SignalR NuGet 包</span><span class="sxs-lookup"><span data-stu-id="97864-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="97864-324">在“解决方案资源管理器”中，右键单击项目，然后选择“管理 NuGet 包” 。</span><span class="sxs-lookup"><span data-stu-id="97864-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="97864-325">在 **NuGet 包管理器中： SignalR. StockTicker**，选择 " **浏览**"。</span><span class="sxs-lookup"><span data-stu-id="97864-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="97864-326">从 " **包源**" 中，选择 **nuget.org**。</span><span class="sxs-lookup"><span data-stu-id="97864-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="97864-327">在搜索框中输入*SignalR* ，并选择 " **SignalR**  >  **安装**"。</span><span class="sxs-lookup"><span data-stu-id="97864-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="97864-328">在 **解决方案资源管理器**中，展开 " *SignalR* " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="97864-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="97864-329">安装 SignalR 包时，将创建该文件夹及其内容。</span><span class="sxs-lookup"><span data-stu-id="97864-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="97864-330">在 *SignalR* 文件夹中，右键单击 *StockTicker.html*，然后选择 " **设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="97864-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97864-331">安装 SignalR NuGet 包可能会更改你在 *脚本* 文件夹中拥有的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="97864-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="97864-332">包安装在*SignalR*文件夹中的新*StockTicker.html*文件将与包所安装的 jQuery 版本同步，但是，如果想要再次运行原始*StockTicker.html*文件，则可能必须首先更新 script 标记中的 jQuery 引用。</span><span class="sxs-lookup"><span data-stu-id="97864-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="97864-333">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="97864-333">Run the application</span></span>

 <span data-ttu-id="97864-334">在第一个应用中看到的表具有有用的功能。</span><span class="sxs-lookup"><span data-stu-id="97864-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="97864-335">整个股票行情股票行情应用程序将显示新功能：一个水平滚动窗口，其中显示了股票数据以及在其上升和下降时颜色变化的股票。</span><span class="sxs-lookup"><span data-stu-id="97864-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="97864-336">按 **F5** 运行应用。</span><span class="sxs-lookup"><span data-stu-id="97864-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="97864-337">首次运行应用程序时，"市场" 将为 "已关闭"，并且会看到一个静态表和一个不滚动的滚动条窗口。</span><span class="sxs-lookup"><span data-stu-id="97864-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="97864-338">选择 " **开放市场**"。</span><span class="sxs-lookup"><span data-stu-id="97864-338">Select **Open Market**.</span></span>

    ![实时滚动的屏幕截图。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="97864-340">" **实时股票行情** " 框开始横向滚动，服务器将开始随机广播股票价格变化。</span><span class="sxs-lookup"><span data-stu-id="97864-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="97864-341">每次股票价格变化时，应用都会更新 **实时股票表** 和 **实时股票**代码。</span><span class="sxs-lookup"><span data-stu-id="97864-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="97864-342">当股票价格变化为正时，应用程序会显示绿色背景的纸张。</span><span class="sxs-lookup"><span data-stu-id="97864-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="97864-343">如果更改为负数，应用程序会显示红色背景。</span><span class="sxs-lookup"><span data-stu-id="97864-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="97864-344">选择 " **关闭市场**"。</span><span class="sxs-lookup"><span data-stu-id="97864-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="97864-345">表更新停止。</span><span class="sxs-lookup"><span data-stu-id="97864-345">The table updates stop.</span></span>

    * <span data-ttu-id="97864-346">股票行情停止滚动。</span><span class="sxs-lookup"><span data-stu-id="97864-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="97864-347">选择“重置”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="97864-347">Select **Reset**.</span></span>

    * <span data-ttu-id="97864-348">所有股票数据都将重置。</span><span class="sxs-lookup"><span data-stu-id="97864-348">All stock data is reset.</span></span>

    * <span data-ttu-id="97864-349">应用在价格更改开始之前还原初始状态。</span><span class="sxs-lookup"><span data-stu-id="97864-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="97864-350">从浏览器复制 URL，打开其他两个浏览器，然后将 Url 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="97864-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="97864-351">可以在每个浏览器中同时动态更新相同的数据。</span><span class="sxs-lookup"><span data-stu-id="97864-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="97864-352">选择任何控件时，所有浏览器都将以相同的方式进行响应。</span><span class="sxs-lookup"><span data-stu-id="97864-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="97864-353">直播股票行情显示</span><span class="sxs-lookup"><span data-stu-id="97864-353">Live Stock Ticker display</span></span>

<span data-ttu-id="97864-354">**Live 股票行情**显示在 `<div>` 按 CSS 样式格式化为单行的元素中的未排序列表。</span><span class="sxs-lookup"><span data-stu-id="97864-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="97864-355">应用程序以与表相同的方式初始化和更新该代号：通过在模板字符串中替换占位符 `<li>` 并将元素动态添加 `<li>` 到元素中 `<ul>` 。</span><span class="sxs-lookup"><span data-stu-id="97864-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="97864-356">应用包括使用 jQuery 函数进行滚动， `animate` 以改变中的无序列表的左边距 `<div>` 。</span><span class="sxs-lookup"><span data-stu-id="97864-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="97864-357">SignalR StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="97864-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="97864-358">股票行情 HTML 代码：</span><span class="sxs-lookup"><span data-stu-id="97864-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="97864-359">SignalR StockTicker</span><span class="sxs-lookup"><span data-stu-id="97864-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="97864-360">股票行情，CSS 代码：</span><span class="sxs-lookup"><span data-stu-id="97864-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="97864-361">SignalR SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="97864-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="97864-362">使其滚动的 jQuery 代码：</span><span class="sxs-lookup"><span data-stu-id="97864-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="97864-363">客户端可以调用的服务器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="97864-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="97864-364">若要为应用添加灵活性，应用可以调用其他方法。</span><span class="sxs-lookup"><span data-stu-id="97864-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="97864-365">SignalR StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="97864-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="97864-366">`StockTickerHub`类定义了客户端可以调用的四种附加方法：</span><span class="sxs-lookup"><span data-stu-id="97864-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="97864-367">应用程序会调用 `OpenMarket` 、 `CloseMarket` 和 `Reset` 以响应页面顶部的按钮。</span><span class="sxs-lookup"><span data-stu-id="97864-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="97864-368">它们演示了触发状态更改的客户端的模式立即传播到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="97864-369">其中每个方法都调用类中的一个方法 `StockTicker` ，该方法会导致市场状态发生变化，然后广播新状态。</span><span class="sxs-lookup"><span data-stu-id="97864-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="97864-370">SignalR StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="97864-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="97864-371">在 `StockTicker` 类中，应用使用 `MarketState` 返回枚举值的属性维护市场的状态 `MarketState` ：</span><span class="sxs-lookup"><span data-stu-id="97864-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="97864-372">更改市场状态的每个方法都在锁块内进行，因为 `StockTicker` 该类必须是线程安全的：</span><span class="sxs-lookup"><span data-stu-id="97864-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="97864-373">若要确保此代码是线程安全的，可 `_marketState` 支持 `MarketState` 指定属性的字段 `volatile` ：</span><span class="sxs-lookup"><span data-stu-id="97864-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="97864-374">`BroadcastMarketStateChange`和 `BroadcastMarketReset` 方法类似于你已看到的 BroadcastStockPrice 方法，只不过它们调用在客户端定义的不同方法：</span><span class="sxs-lookup"><span data-stu-id="97864-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="97864-375">服务器可以调用的客户端上的其他函数</span><span class="sxs-lookup"><span data-stu-id="97864-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="97864-376">`updateStockPrice`函数现在同时处理表和滚动条的显示，并使用 `jQuery.Color` 闪烁红色和绿色颜色。</span><span class="sxs-lookup"><span data-stu-id="97864-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="97864-377">中的新函数 *SignalR.StockTicker.js* 根据市场状态启用和禁用按钮。</span><span class="sxs-lookup"><span data-stu-id="97864-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="97864-378">它们还会停止或启动 **实时股票行情** 滚动条。</span><span class="sxs-lookup"><span data-stu-id="97864-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="97864-379">由于正在向添加很多函数 `ticker.client` ，应用程序使用 [jQuery extend 函数](http://api.jquery.com/jQuery.extend/) 添加它们。</span><span class="sxs-lookup"><span data-stu-id="97864-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="97864-380">建立连接后的其他客户端设置</span><span class="sxs-lookup"><span data-stu-id="97864-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="97864-381">客户端建立连接后，还需要执行一些额外的工作：</span><span class="sxs-lookup"><span data-stu-id="97864-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="97864-382">查明市场是否已打开或已关闭，以调用相应的 `marketOpened` 或 `marketClosed` 函数。</span><span class="sxs-lookup"><span data-stu-id="97864-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="97864-383">将服务器方法调用附加到这些按钮。</span><span class="sxs-lookup"><span data-stu-id="97864-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="97864-384">在应用程序建立连接之前，服务器方法不会连接到按钮。</span><span class="sxs-lookup"><span data-stu-id="97864-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="97864-385">这是为了使代码在可用之前无法调用服务器方法。</span><span class="sxs-lookup"><span data-stu-id="97864-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97864-386">其他资源</span><span class="sxs-lookup"><span data-stu-id="97864-386">Additional resources</span></span>

<span data-ttu-id="97864-387">在本教程中，你已了解如何对 SignalR 应用程序进行编程，以便将消息从服务器广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="97864-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="97864-388">现在，你可以定期广播消息和响应来自任何客户端的通知。</span><span class="sxs-lookup"><span data-stu-id="97864-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="97864-389">您可以使用多线程单一实例的概念在多玩家联机游戏方案中维护服务器状态。</span><span class="sxs-lookup"><span data-stu-id="97864-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="97864-390">有关示例，请参阅 [基于 SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="97864-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="97864-391">有关显示对等通信方案的教程，入门请参阅 [SignalR With](introduction-to-signalr.md) And [实时更新 with SignalR](tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="97864-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="97864-392">有关 SignalR 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="97864-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="97864-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="97864-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="97864-394">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="97864-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="97864-395">SignalR GitHub 和示例</span><span class="sxs-lookup"><span data-stu-id="97864-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="97864-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="97864-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="97864-397">后续步骤</span><span class="sxs-lookup"><span data-stu-id="97864-397">Next steps</span></span>

<span data-ttu-id="97864-398">本教程介绍以下操作：</span><span class="sxs-lookup"><span data-stu-id="97864-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="97864-399">已创建项目</span><span class="sxs-lookup"><span data-stu-id="97864-399">Created the project</span></span>
> * <span data-ttu-id="97864-400">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-400">Set up the server code</span></span>
> * <span data-ttu-id="97864-401">检查服务器代码</span><span class="sxs-lookup"><span data-stu-id="97864-401">Examined the server code</span></span>
> * <span data-ttu-id="97864-402">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-402">Set up the client code</span></span>
> * <span data-ttu-id="97864-403">检查了客户端代码</span><span class="sxs-lookup"><span data-stu-id="97864-403">Examined the client code</span></span>
> * <span data-ttu-id="97864-404">已测试应用程序</span><span class="sxs-lookup"><span data-stu-id="97864-404">Tested the application</span></span>
> * <span data-ttu-id="97864-405">启用的日志记录</span><span class="sxs-lookup"><span data-stu-id="97864-405">Enabled logging</span></span>

<span data-ttu-id="97864-406">转到下一篇文章，了解如何创建使用 ASP.NET SignalR 2 的实时 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="97864-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="97864-407">通过 SignalR 创建实时 web 应用</span><span class="sxs-lookup"><span data-stu-id="97864-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)

---
uid: signalr/overview/older-versions/dependency-injection
title: 在 SignalR 中的依赖关系注入 1.x |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: c8aac09c3d3e06529f7834eb3f60dca2f3073922
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042634"
---
<a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="a46ee-102">SignalR 1.x 中的依赖项注入</span><span class="sxs-lookup"><span data-stu-id="a46ee-102">Dependency Injection in SignalR 1.x</span></span>
====================
<span data-ttu-id="a46ee-103">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a46ee-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="a46ee-104">依赖关系注入是一种方法来删除硬编码对象，使其更易替换对象的依赖项，无论是用于测试 （使用 mock 对象） 或运行时行为的更改之间的依赖项。</span><span class="sxs-lookup"><span data-stu-id="a46ee-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="a46ee-105">本教程演示如何执行 SignalR 集线器上的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="a46ee-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="a46ee-106">它还演示如何使用 SignalR 使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="a46ee-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="a46ee-107">IoC 容器是依赖关系注入一个通用框架。</span><span class="sxs-lookup"><span data-stu-id="a46ee-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="a46ee-108">什么是依赖关系注入？</span><span class="sxs-lookup"><span data-stu-id="a46ee-108">What is Dependency Injection?</span></span>

<span data-ttu-id="a46ee-109">如果你已了解如何使用依赖关系注入，跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="a46ee-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="a46ee-110">*依赖关系注入*(DI) 是一种模式不负责创建其自己的依赖项对象。</span><span class="sxs-lookup"><span data-stu-id="a46ee-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="a46ee-111">下面是一个简单的示例以促使 DI。</span><span class="sxs-lookup"><span data-stu-id="a46ee-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="a46ee-112">假设有一个需要登录消息的对象。</span><span class="sxs-lookup"><span data-stu-id="a46ee-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="a46ee-113">您可以定义日志记录接口：</span><span class="sxs-lookup"><span data-stu-id="a46ee-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="a46ee-114">在您的对象，您可以创建`ILogger`记录消息：</span><span class="sxs-lookup"><span data-stu-id="a46ee-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="a46ee-115">此方法有效，但它不是最佳设计。</span><span class="sxs-lookup"><span data-stu-id="a46ee-115">This works, but it's not the best design.</span></span> <span data-ttu-id="a46ee-116">如果你想要替换`FileLogger`与另一个`ILogger`实现中，您将需要修改`SomeComponent`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="a46ee-117">Supposing 大量其他对象使用`FileLogger`，将需要将所有这些更改。</span><span class="sxs-lookup"><span data-stu-id="a46ee-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="a46ee-118">或如果您决定将`FileLogger`单一实例，您还需要进行整个应用程序的更改。</span><span class="sxs-lookup"><span data-stu-id="a46ee-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="a46ee-119">更好的方法是"注入"`ILogger`到对象-例如，通过使用构造函数参数：</span><span class="sxs-lookup"><span data-stu-id="a46ee-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="a46ee-120">现在，该对象不负责选择的`ILogger`使用。</span><span class="sxs-lookup"><span data-stu-id="a46ee-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="a46ee-121">你可以从交换机`ILogger`而无需更改依赖于它的对象的实现。</span><span class="sxs-lookup"><span data-stu-id="a46ee-121">You can swich `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="a46ee-122">此模式称为[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="a46ee-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="a46ee-123">另一种模式是 setter 注入，其中设置通过 setter 方法或属性的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a46ee-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="a46ee-124">在 SignalR 中的简单的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="a46ee-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="a46ee-125">本教程中的聊天应用程序，请考虑[SignalR 入门](../getting-started/tutorial-getting-started-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="a46ee-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="a46ee-126">下面是从该应用程序的中心类：</span><span class="sxs-lookup"><span data-stu-id="a46ee-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="a46ee-127">假设你想要发送之前存储在服务器上的聊天消息。</span><span class="sxs-lookup"><span data-stu-id="a46ee-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="a46ee-128">你可能会定义一个接口，用于提取此功能，并使用 DI 注入到接口`ChatHub`类。</span><span class="sxs-lookup"><span data-stu-id="a46ee-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="a46ee-129">唯一的问题是 SignalR 应用程序不会直接创建中心;SignalR 为你创建它们。</span><span class="sxs-lookup"><span data-stu-id="a46ee-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="a46ee-130">默认情况下，SignalR 希望 hub 类，具有无参数构造函数。</span><span class="sxs-lookup"><span data-stu-id="a46ee-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="a46ee-131">但是，可以轻松地注册创建集线器实例的函数，并使用此函数执行 DI。</span><span class="sxs-lookup"><span data-stu-id="a46ee-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="a46ee-132">通过调用注册函数**GlobalHost.DependencyResolver.Register**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="a46ee-133">现在，SignalR 将调用此匿名函数，每当需要创建`ChatHub`实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="a46ee-134">IoC 容器</span><span class="sxs-lookup"><span data-stu-id="a46ee-134">IoC Containers</span></span>

<span data-ttu-id="a46ee-135">上面的代码是相当不错的简单的用例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="a46ee-136">但您仍需要编写如下：</span><span class="sxs-lookup"><span data-stu-id="a46ee-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="a46ee-137">在具有许多依赖关系的复杂应用程序，可能需要编写大量的此"绑定"代码。</span><span class="sxs-lookup"><span data-stu-id="a46ee-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="a46ee-138">此代码可能难以维护，尤其是如果嵌套依赖项。</span><span class="sxs-lookup"><span data-stu-id="a46ee-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="a46ee-139">也很难进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="a46ee-139">It is also hard to unit test.</span></span>

<span data-ttu-id="a46ee-140">一种解决方案是使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="a46ee-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="a46ee-141">IoC 容器是一个软件组件，负责管理依赖项。您向容器注册类型，然后使用容器来创建对象。</span><span class="sxs-lookup"><span data-stu-id="a46ee-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="a46ee-142">容器自动找出的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a46ee-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="a46ee-143">多个 IoC 容器还可用于控制对象生存期和作用域等。</span><span class="sxs-lookup"><span data-stu-id="a46ee-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="a46ee-144">"IoC"代表"控制反转"，这是一个框架，其中调用到应用程序代码中的一般模式。</span><span class="sxs-lookup"><span data-stu-id="a46ee-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="a46ee-145">IoC 容器构造您的对象，其中"反转"常用控制流。</span><span class="sxs-lookup"><span data-stu-id="a46ee-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="a46ee-146">在 SignalR 中使用 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="a46ee-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="a46ee-147">聊天应用程序可能是非常简单，从 IoC 容器中受益。</span><span class="sxs-lookup"><span data-stu-id="a46ee-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="a46ee-148">相反，让我们看看[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)示例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="a46ee-149">StockTicker 示例定义两个主要类：</span><span class="sxs-lookup"><span data-stu-id="a46ee-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="a46ee-150">`StockTickerHub`：Hub 类，用于管理客户端连接。</span><span class="sxs-lookup"><span data-stu-id="a46ee-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="a46ee-151">`StockTicker`：单一实例，它包含股票价格并定期更新它们。</span><span class="sxs-lookup"><span data-stu-id="a46ee-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="a46ee-152">`StockTickerHub` 保存对的引用`StockTicker`单一实例，而`StockTicker`持有一个指向引用**IHubConnectionContext**为`StockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="a46ee-153">它使用此接口与通信`StockTickerHub`实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="a46ee-154">(有关详细信息，请参阅[服务器与 ASP.NET SignalR 广播](index.md)。)</span><span class="sxs-lookup"><span data-stu-id="a46ee-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="a46ee-155">我们可以使用 IoC 容器有点理清这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a46ee-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="a46ee-156">首先，让我们来简化`StockTickerHub`和`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="a46ee-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="a46ee-157">在下面的代码中，我已注释掉的部分，我们不需要。</span><span class="sxs-lookup"><span data-stu-id="a46ee-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="a46ee-158">删除无参数构造函数从`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="a46ee-159">相反，我们将始终使用 DI 创建中心。</span><span class="sxs-lookup"><span data-stu-id="a46ee-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="a46ee-160">对于 StockTicker，删除的单一实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="a46ee-161">更高版本，我们将使用 IoC 容器来控制 StockTicker 生存期。</span><span class="sxs-lookup"><span data-stu-id="a46ee-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="a46ee-162">此外，请公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="a46ee-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="a46ee-163">接下来，我们可以重构代码，通过创建一个接口，使`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="a46ee-164">我们将使用此接口来分离`StockTickerHub`从`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="a46ee-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="a46ee-165">Visual Studio 进行这种重构轻松。</span><span class="sxs-lookup"><span data-stu-id="a46ee-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="a46ee-166">打开文件 StockTicker.cs，右键单击`StockTicker`类声明，然后选择**重构**...**提取接口**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="a46ee-167">在中**提取接口**对话框中，单击**全**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="a46ee-168">保留其他默认值。</span><span class="sxs-lookup"><span data-stu-id="a46ee-168">Leave the other defaults.</span></span> <span data-ttu-id="a46ee-169">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="a46ee-170">Visual Studio 将创建名为的新接口`IStockTicker`，并且也会更改`StockTicker`为派生`IStockTicker`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="a46ee-171">打开文件 IStockTicker.cs 并更改到接口**公共**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="a46ee-172">在中`StockTickerHub`类中更改的两个实例`StockTicker`到`IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="a46ee-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="a46ee-173">创建`IStockTicker`接口并不是必需的但我将演示如何 DI 可以帮助减少在应用程序中的组件之间的耦合。</span><span class="sxs-lookup"><span data-stu-id="a46ee-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="a46ee-174">添加 Ninject 库</span><span class="sxs-lookup"><span data-stu-id="a46ee-174">Add the Ninject Library</span></span>

<span data-ttu-id="a46ee-175">有许多适用于.NET 的开源 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="a46ee-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="a46ee-176">对于本教程中，我将使用[Ninject](http://www.ninject.org/)。</span><span class="sxs-lookup"><span data-stu-id="a46ee-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="a46ee-177">(其他常用库包括[Castle Windsor](http://www.castleproject.org/)， [Spring.Net](http://www.springframework.net/)， [Autofac](https://code.google.com/p/autofac/)， [Unity](https://github.com/unitycontainer/unity)，和[StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="a46ee-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="a46ee-178">使用 NuGet 包管理器来安装[Ninject 库](https://nuget.org/packages/Ninject/3.0.1.10)。</span><span class="sxs-lookup"><span data-stu-id="a46ee-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="a46ee-179">在 Visual Studio 中，从**工具**菜单中选择**NuGet 包管理器** > **包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="a46ee-180">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a46ee-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="a46ee-181">将 SignalR 依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="a46ee-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="a46ee-182">若要使用 Ninject SignalR 中的，创建派生的类**DefaultDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="a46ee-183">此类重写**GetService**并**getservices 进行提取**方法**DefaultDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="a46ee-184">SignalR 调用这些方法在运行时，包括中心实例，以及由 SignalR 在内部使用的各种服务中创建各种对象。</span><span class="sxs-lookup"><span data-stu-id="a46ee-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="a46ee-185">**GetService**方法创建一种类型的单个实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="a46ee-186">重写此方法以调用 Ninject 内核**TryGet**方法。</span><span class="sxs-lookup"><span data-stu-id="a46ee-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="a46ee-187">如果该方法将返回 null，回退到默认冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="a46ee-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="a46ee-188">**Getservices 进行提取**方法创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="a46ee-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="a46ee-189">重写此方法要串联的结果与默认冲突解决程序 Ninject 的结果。</span><span class="sxs-lookup"><span data-stu-id="a46ee-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="a46ee-190">配置 Ninject 绑定</span><span class="sxs-lookup"><span data-stu-id="a46ee-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="a46ee-191">现在我们将使用 Ninject 声明类型绑定。</span><span class="sxs-lookup"><span data-stu-id="a46ee-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="a46ee-192">打开文件 RegisterHubs.cs。</span><span class="sxs-lookup"><span data-stu-id="a46ee-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="a46ee-193">在中`RegisterHubs.Start`方法中，创建 Ninject 容器，它调用 Ninject*内核*。</span><span class="sxs-lookup"><span data-stu-id="a46ee-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="a46ee-194">创建我们的自定义依赖关系解析程序的实例：</span><span class="sxs-lookup"><span data-stu-id="a46ee-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="a46ee-195">为创建绑定`IStockTicker`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a46ee-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="a46ee-196">此代码会说两件事情。</span><span class="sxs-lookup"><span data-stu-id="a46ee-196">This code is saying two things.</span></span> <span data-ttu-id="a46ee-197">首先，每当应用程序需要`IStockTicker`，内核应创建的实例`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="a46ee-198">第二个，`StockTicker`类应创建为单一实例对象。</span><span class="sxs-lookup"><span data-stu-id="a46ee-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="a46ee-199">Ninject 将创建一个对象的实例，并返回每个请求的相同实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="a46ee-200">为创建绑定**IHubConnectionContext** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a46ee-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="a46ee-201">一个匿名函数，返回此代码 creatres **IHubConnection**。</span><span class="sxs-lookup"><span data-stu-id="a46ee-201">This code creatres an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="a46ee-202">**WhenInjectedInto**方法会示意 Ninject 时要使用此函数仅创建`IStockTicker`实例。</span><span class="sxs-lookup"><span data-stu-id="a46ee-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="a46ee-203">原因是 SignalR 创建**IHubConnectionContext**实例在内部，并且我们不想要重写 SignalR 如何创建它们。</span><span class="sxs-lookup"><span data-stu-id="a46ee-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="a46ee-204">此函数仅适用于我们`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="a46ee-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="a46ee-205">传递到依赖关系解析程序**MapHubs**方法：</span><span class="sxs-lookup"><span data-stu-id="a46ee-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="a46ee-206">现在，SignalR 将使用冲突解决程序中指定**MapHubs**，而不是默认冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="a46ee-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="a46ee-207">下面是完整代码列表`RegisterHubs.Start`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="a46ee-208">若要在 Visual Studio 中运行 StockTicker 应用程序，按 F5。</span><span class="sxs-lookup"><span data-stu-id="a46ee-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="a46ee-209">在浏览器窗口中，导航到`http://localhost:*port*/SignalR.Sample/StockTicker.html`。</span><span class="sxs-lookup"><span data-stu-id="a46ee-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="a46ee-210">该应用程序功能与以前完全相同。</span><span class="sxs-lookup"><span data-stu-id="a46ee-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="a46ee-211">(有关说明，请参阅[服务器与 ASP.NET SignalR 广播](index.md)。)我们尚未更改的行为;只需进行更轻松地测试、 维护和改进代码。</span><span class="sxs-lookup"><span data-stu-id="a46ee-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>

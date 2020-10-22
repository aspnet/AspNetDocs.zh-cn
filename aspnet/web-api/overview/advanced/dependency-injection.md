---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2 中的依赖项注入-ASP.NET 4。x
author: MikeWasson
description: 本教程演示如何在 ASP.NET 4.x 的 ASP.NET Web API 控制器中注入依赖项。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 3342d93340215d937cf7161ee1c4b32931d516a3
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345264"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="3975e-103">ASP.NET Web API 2 中的依赖项注入</span><span class="sxs-lookup"><span data-stu-id="3975e-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="3975e-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3975e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3975e-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="3975e-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="3975e-106">本教程演示如何在 ASP.NET Web API 控制器中注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="3975e-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3975e-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3975e-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3975e-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="3975e-108">Web API 2</span></span>
> - [<span data-ttu-id="3975e-109">Unity 应用程序块</span><span class="sxs-lookup"><span data-stu-id="3975e-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="3975e-110">实体框架 6 (版本5也起作用) </span><span class="sxs-lookup"><span data-stu-id="3975e-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="3975e-111">什么是依赖项注入？</span><span class="sxs-lookup"><span data-stu-id="3975e-111">What is Dependency Injection?</span></span>

<span data-ttu-id="3975e-112">依赖项是指另一个对象所需的任何对象。</span><span class="sxs-lookup"><span data-stu-id="3975e-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="3975e-113">例如，通常定义处理数据访问的 [存储库](http://martinfowler.com/eaaCatalog/repository.html) 。</span><span class="sxs-lookup"><span data-stu-id="3975e-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="3975e-114">我们来看一个示例。</span><span class="sxs-lookup"><span data-stu-id="3975e-114">Let's illustrate with an example.</span></span> <span data-ttu-id="3975e-115">首先，我们将定义域模型：</span><span class="sxs-lookup"><span data-stu-id="3975e-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="3975e-116">下面是一个简单存储库类，它使用实体框架在数据库中存储项。</span><span class="sxs-lookup"><span data-stu-id="3975e-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="3975e-117">现在，让我们定义一个支持实体 GET 请求的 Web API 控制器 `Product` 。</span><span class="sxs-lookup"><span data-stu-id="3975e-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="3975e-118"> (为简单起见，我要退出 POST 和其他方法。 ) 以下是第一次尝试：</span><span class="sxs-lookup"><span data-stu-id="3975e-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="3975e-119">请注意，控制器类依赖于 `ProductRepository` ，我们正在让控制器创建 `ProductRepository` 实例。</span><span class="sxs-lookup"><span data-stu-id="3975e-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="3975e-120">但出于多种原因，对依赖项进行硬编码是一种不好的做法。</span><span class="sxs-lookup"><span data-stu-id="3975e-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="3975e-121">如果要 `ProductRepository` 使用不同的实现替换，还需要修改控制器类。</span><span class="sxs-lookup"><span data-stu-id="3975e-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="3975e-122">如果 `ProductRepository` 有依赖关系，则必须在控制器中对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="3975e-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="3975e-123">对于包含多个控制器的大型项目，你的配置代码将分散到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="3975e-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="3975e-124">这种情况很难进行单元测试，因为控制器是硬编码的，以便查询数据库。</span><span class="sxs-lookup"><span data-stu-id="3975e-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="3975e-125">对于单元测试，应使用模拟或存根存储库，这是当前设计所不可能的。</span><span class="sxs-lookup"><span data-stu-id="3975e-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="3975e-126">可以通过将存储库 *注入* 控制器来解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="3975e-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="3975e-127">首先，将 `ProductRepository` 该类重构为一个接口：</span><span class="sxs-lookup"><span data-stu-id="3975e-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="3975e-128">然后提供 `IProductRepository` 作为构造函数参数：</span><span class="sxs-lookup"><span data-stu-id="3975e-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="3975e-129">此示例使用 [构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="3975e-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="3975e-130">你还可以使用 *setter 注入*，你可以在其中通过 setter 方法或属性设置依赖关系。</span><span class="sxs-lookup"><span data-stu-id="3975e-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="3975e-131">但现在会出现问题，因为应用程序不会直接创建控制器。</span><span class="sxs-lookup"><span data-stu-id="3975e-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="3975e-132">Web API 在路由请求时创建控制器，Web API 不知道有关的任何内容 `IProductRepository` 。</span><span class="sxs-lookup"><span data-stu-id="3975e-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="3975e-133">这就是 Web API 依赖关系解析程序所处的位置。</span><span class="sxs-lookup"><span data-stu-id="3975e-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="3975e-134">Web API 依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="3975e-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="3975e-135">Web API 定义用于解析依赖项的 **IDependencyResolver** 接口。</span><span class="sxs-lookup"><span data-stu-id="3975e-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="3975e-136">下面是接口的定义：</span><span class="sxs-lookup"><span data-stu-id="3975e-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="3975e-137">**IDependencyScope**接口有两种方法：</span><span class="sxs-lookup"><span data-stu-id="3975e-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="3975e-138">**GetService** 创建一个类型的实例。</span><span class="sxs-lookup"><span data-stu-id="3975e-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="3975e-139">**GetServices** 创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="3975e-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="3975e-140">**IDependencyResolver**方法继承**IDependencyScope**并添加**BeginScope**方法。</span><span class="sxs-lookup"><span data-stu-id="3975e-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="3975e-141">我将在本教程的后面部分讨论范围。</span><span class="sxs-lookup"><span data-stu-id="3975e-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="3975e-142">当 Web API 创建控制器实例时，它将首先调用 **IDependencyResolver GetService**，并传入控制器类型。</span><span class="sxs-lookup"><span data-stu-id="3975e-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="3975e-143">可以使用此扩展性挂钩创建控制器，解析任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="3975e-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="3975e-144">如果 **GetService** 返回 Null，Web API 将在控制器类上查找无参数的构造函数。</span><span class="sxs-lookup"><span data-stu-id="3975e-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="3975e-145">与 Unity 容器的依赖项解析</span><span class="sxs-lookup"><span data-stu-id="3975e-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="3975e-146">尽管你可以从头开始编写完整的 **IDependencyResolver** 实现，但该接口实际上设计为在 Web API 与现有 IoC 容器之间充当桥梁。</span><span class="sxs-lookup"><span data-stu-id="3975e-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="3975e-147">IoC 容器是负责管理依赖项的软件组件。</span><span class="sxs-lookup"><span data-stu-id="3975e-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="3975e-148">使用容器注册类型，然后使用容器来创建对象。</span><span class="sxs-lookup"><span data-stu-id="3975e-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="3975e-149">容器自动找出依赖关系。</span><span class="sxs-lookup"><span data-stu-id="3975e-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="3975e-150">许多 IoC 容器还允许您控制对象生存期和范围等任务。</span><span class="sxs-lookup"><span data-stu-id="3975e-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="3975e-151">"IoC" 代表 "控制反转"，这是一个框架对应用程序代码进行调用的常规模式。</span><span class="sxs-lookup"><span data-stu-id="3975e-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="3975e-152">IoC 容器为你构造对象，这会 "反转" 正常的控制流。</span><span class="sxs-lookup"><span data-stu-id="3975e-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="3975e-153">对于本教程，我们将使用 Microsoft 模式实践中的 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) &amp; 。</span><span class="sxs-lookup"><span data-stu-id="3975e-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="3975e-154"> (其他常用库包括 [城堡 Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和 [StructureMap](http://structuremap.github.io/documentation/)。 ) 你可以使用 NuGet 包管理器安装 Unity。</span><span class="sxs-lookup"><span data-stu-id="3975e-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="3975e-155">在 Visual Studio 的 " **工具** " 菜单中，选择 " **NuGet 包管理器**"，然后选择 " **程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="3975e-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="3975e-156">在 "程序包管理器控制台" 窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3975e-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="3975e-157">下面是包装 Unity 容器的 **IDependencyResolver** 实现。</span><span class="sxs-lookup"><span data-stu-id="3975e-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="3975e-158">配置依赖关系解析程序</span><span class="sxs-lookup"><span data-stu-id="3975e-158">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="3975e-159">在全局**HttpConfiguration**对象的**DependencyResolver**属性上设置依赖关系解析程序。</span><span class="sxs-lookup"><span data-stu-id="3975e-159">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="3975e-160">下面的代码 `IProductRepository` 向 Unity 注册接口，然后创建一个 `UnityResolver` 。</span><span class="sxs-lookup"><span data-stu-id="3975e-160">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="3975e-161">依赖关系范围和控制器生存期</span><span class="sxs-lookup"><span data-stu-id="3975e-161">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="3975e-162">控制器是根据请求创建的。</span><span class="sxs-lookup"><span data-stu-id="3975e-162">Controllers are created per request.</span></span> <span data-ttu-id="3975e-163">为了管理对象生存期， **IDependencyResolver** 使用了 *作用域*的概念。</span><span class="sxs-lookup"><span data-stu-id="3975e-163">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="3975e-164">附加到 **HttpConfiguration** 对象的依赖关系解析程序具有全局范围。</span><span class="sxs-lookup"><span data-stu-id="3975e-164">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="3975e-165">当 Web API 创建控制器时，它会调用 **BeginScope**。</span><span class="sxs-lookup"><span data-stu-id="3975e-165">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="3975e-166">此方法返回表示子作用域的 **IDependencyScope** 。</span><span class="sxs-lookup"><span data-stu-id="3975e-166">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="3975e-167">然后，Web API 在子作用域上调用 **GetService** ，以创建控制器。</span><span class="sxs-lookup"><span data-stu-id="3975e-167">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="3975e-168">请求完成后，Web API 会调用子范围中的 **Dispose** 。</span><span class="sxs-lookup"><span data-stu-id="3975e-168">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="3975e-169">使用 **dispose** 方法释放控制器的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="3975e-169">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="3975e-170">如何实现 **BeginScope** 取决于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="3975e-170">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="3975e-171">对于 Unity，范围对应于子容器：</span><span class="sxs-lookup"><span data-stu-id="3975e-171">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="3975e-172">大多数 IoC 容器具有相似的等效项。</span><span class="sxs-lookup"><span data-stu-id="3975e-172">Most IoC containers have similar equivalents.</span></span>

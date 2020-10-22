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
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的依赖项注入

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 本教程演示如何在 ASP.NET Web API 控制器中注入依赖项。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API 2
> - [Unity 应用程序块](https://www.nuget.org/packages/Unity/)
> - 实体框架 6 (版本5也起作用) 

## <a name="what-is-dependency-injection"></a>什么是依赖项注入？

依赖项是指另一个对象所需的任何对象。 例如，通常定义处理数据访问的 [存储库](http://martinfowler.com/eaaCatalog/repository.html) 。 我们来看一个示例。 首先，我们将定义域模型：

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

下面是一个简单存储库类，它使用实体框架在数据库中存储项。

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

现在，让我们定义一个支持实体 GET 请求的 Web API 控制器 `Product` 。  (为简单起见，我要退出 POST 和其他方法。 ) 以下是第一次尝试：

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

请注意，控制器类依赖于 `ProductRepository` ，我们正在让控制器创建 `ProductRepository` 实例。 但出于多种原因，对依赖项进行硬编码是一种不好的做法。

- 如果要 `ProductRepository` 使用不同的实现替换，还需要修改控制器类。
- 如果 `ProductRepository` 有依赖关系，则必须在控制器中对其进行配置。 对于包含多个控制器的大型项目，你的配置代码将分散到你的项目中。
- 这种情况很难进行单元测试，因为控制器是硬编码的，以便查询数据库。 对于单元测试，应使用模拟或存根存储库，这是当前设计所不可能的。

可以通过将存储库 *注入* 控制器来解决这些问题。 首先，将 `ProductRepository` 该类重构为一个接口：

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

然后提供 `IProductRepository` 作为构造函数参数：

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

此示例使用 [构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。 你还可以使用 *setter 注入*，你可以在其中通过 setter 方法或属性设置依赖关系。

但现在会出现问题，因为应用程序不会直接创建控制器。 Web API 在路由请求时创建控制器，Web API 不知道有关的任何内容 `IProductRepository` 。 这就是 Web API 依赖关系解析程序所处的位置。

## <a name="the-web-api-dependency-resolver"></a>Web API 依赖关系解析程序

Web API 定义用于解析依赖项的 **IDependencyResolver** 接口。 下面是接口的定义：

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope**接口有两种方法：

- **GetService** 创建一个类型的实例。
- **GetServices** 创建指定类型的对象的集合。

**IDependencyResolver**方法继承**IDependencyScope**并添加**BeginScope**方法。 我将在本教程的后面部分讨论范围。

当 Web API 创建控制器实例时，它将首先调用 **IDependencyResolver GetService**，并传入控制器类型。 可以使用此扩展性挂钩创建控制器，解析任何依赖项。 如果 **GetService** 返回 Null，Web API 将在控制器类上查找无参数的构造函数。

## <a name="dependency-resolution-with-the-unity-container"></a>与 Unity 容器的依赖项解析

尽管你可以从头开始编写完整的 **IDependencyResolver** 实现，但该接口实际上设计为在 Web API 与现有 IoC 容器之间充当桥梁。

IoC 容器是负责管理依赖项的软件组件。 使用容器注册类型，然后使用容器来创建对象。 容器自动找出依赖关系。 许多 IoC 容器还允许您控制对象生存期和范围等任务。

> [!NOTE]
> "IoC" 代表 "控制反转"，这是一个框架对应用程序代码进行调用的常规模式。 IoC 容器为你构造对象，这会 "反转" 正常的控制流。

对于本教程，我们将使用 Microsoft 模式实践中的 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) &amp; 。  (其他常用库包括 [城堡 Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和 [StructureMap](http://structuremap.github.io/documentation/)。 ) 你可以使用 NuGet 包管理器安装 Unity。 在 Visual Studio 的 " **工具** " 菜单中，选择 " **NuGet 包管理器**"，然后选择 " **程序包管理器控制台**"。 在 "程序包管理器控制台" 窗口中，键入以下命令：

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

下面是包装 Unity 容器的 **IDependencyResolver** 实现。

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

## <a name="configuring-the-dependency-resolver"></a>配置依赖关系解析程序

在全局**HttpConfiguration**对象的**DependencyResolver**属性上设置依赖关系解析程序。

下面的代码 `IProductRepository` 向 Unity 注册接口，然后创建一个 `UnityResolver` 。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>依赖关系范围和控制器生存期

控制器是根据请求创建的。 为了管理对象生存期， **IDependencyResolver** 使用了 *作用域*的概念。

附加到 **HttpConfiguration** 对象的依赖关系解析程序具有全局范围。 当 Web API 创建控制器时，它会调用 **BeginScope**。 此方法返回表示子作用域的 **IDependencyScope** 。

然后，Web API 在子作用域上调用 **GetService** ，以创建控制器。 请求完成后，Web API 会调用子范围中的 **Dispose** 。 使用 **dispose** 方法释放控制器的依赖关系。

如何实现 **BeginScope** 取决于 IoC 容器。 对于 Unity，范围对应于子容器：

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

大多数 IoC 容器具有相似的等效项。

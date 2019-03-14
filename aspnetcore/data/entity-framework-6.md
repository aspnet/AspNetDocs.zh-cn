---
title: ASP.NET Core 和 Entity Framework 6 入门
author: rick-anderson
description: 本文演示如何在 ASP.NET Core 应用程序中使用 Entity Framework 6。
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/24/2018
uid: data/entity-framework-6
ms.openlocfilehash: b7679afbe4c364386fe8f16d22d7e9797a3e0c27
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059154"
---
# <a name="get-started-with-aspnet-core-and-entity-framework-6"></a><span data-ttu-id="49118-103">ASP.NET Core 和 Entity Framework 6 入门</span><span class="sxs-lookup"><span data-stu-id="49118-103">Get Started with ASP.NET Core and Entity Framework 6</span></span>

<span data-ttu-id="49118-104">作者：[Paweł Grudzień](https://github.com/pgrudzien12)、[Damien Pontifex](https://github.com/DamienPontifex) 和 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="49118-104">By [Paweł Grudzień](https://github.com/pgrudzien12), [Damien Pontifex](https://github.com/DamienPontifex), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="49118-105">本文演示如何在 ASP.NET Core 应用程序中使用 Entity Framework 6。</span><span class="sxs-lookup"><span data-stu-id="49118-105">This article shows how to use Entity Framework 6 in an ASP.NET Core application.</span></span>

## <a name="overview"></a><span data-ttu-id="49118-106">概述</span><span class="sxs-lookup"><span data-stu-id="49118-106">Overview</span></span>

<span data-ttu-id="49118-107">若要使用 Entity Framework 6，则项目必须面向 .NET Framework 进行编译，因为 Entity Framework 6 不支持 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="49118-107">To use Entity Framework 6, your project has to compile against .NET Framework, as Entity Framework 6 doesn't support .NET Core.</span></span> <span data-ttu-id="49118-108">如果需要跨平台功能，需升级到 [Entity Framework Core](/ef/)。</span><span class="sxs-lookup"><span data-stu-id="49118-108">If you need cross-platform features you will need to upgrade to [Entity Framework Core](/ef/).</span></span>

<span data-ttu-id="49118-109">在 ASP.NET Core 应用程序中使用 Entity Framework 6 的推荐方法是：将 EF6 上下文和模型类放入面向完整框架的类库项目中。</span><span class="sxs-lookup"><span data-stu-id="49118-109">The recommended way to use Entity Framework 6 in an ASP.NET Core application is to put the EF6 context and model classes in a class library project that targets the full framework.</span></span> <span data-ttu-id="49118-110">添加对 ASP.NET Core 项目中的类库的引用。</span><span class="sxs-lookup"><span data-stu-id="49118-110">Add a reference to the class library from the ASP.NET Core project.</span></span> <span data-ttu-id="49118-111">请参阅示例[针对 EF6 和 ASP.NET Core 项目的 Visual Studio 解决方案](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/)。</span><span class="sxs-lookup"><span data-stu-id="49118-111">See the sample [Visual Studio solution with EF6 and ASP.NET Core projects](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/).</span></span>

<span data-ttu-id="49118-112">不能将 EF6 上下文放入 ASP.NET Core 项目，因为 .NET Core 项目不支持 EF6 命令（如 Enable-Migrations）所需的的各项功能。</span><span class="sxs-lookup"><span data-stu-id="49118-112">You can't put an EF6 context in an ASP.NET Core project because .NET Core projects don't support all of the functionality that EF6 commands such as *Enable-Migrations* require.</span></span>

<span data-ttu-id="49118-113">无论 EF6 上下文属于哪种项目类型，只有 EF6 命令行工具才能使用 EF6 上下文。</span><span class="sxs-lookup"><span data-stu-id="49118-113">Regardless of project type in which you locate your EF6 context, only EF6 command-line tools work with an EF6 context.</span></span> <span data-ttu-id="49118-114">例如，`Scaffold-DbContext` 仅在 Entity Framework Core 中可用。</span><span class="sxs-lookup"><span data-stu-id="49118-114">For example, `Scaffold-DbContext` is only available in Entity Framework Core.</span></span> <span data-ttu-id="49118-115">如果需要对数据库执行反向工程以使其成为 EF6 模型，请参阅[从 Code First 到现有数据库](https://msdn.microsoft.com/jj200620)。</span><span class="sxs-lookup"><span data-stu-id="49118-115">If you need to do reverse engineering of a database into an EF6 model, see [Code First to an Existing Database](https://msdn.microsoft.com/jj200620).</span></span>

## <a name="reference-full-framework-and-ef6-in-the-aspnet-core-project"></a><span data-ttu-id="49118-116">在 ASP.NET Core 项目中引用完整框架和 EF6</span><span class="sxs-lookup"><span data-stu-id="49118-116">Reference full framework and EF6 in the ASP.NET Core project</span></span>

<span data-ttu-id="49118-117">ASP.NET Core 项目需要引用 .NET Framework 和 EF6。</span><span class="sxs-lookup"><span data-stu-id="49118-117">Your ASP.NET Core project needs to reference .NET framework and EF6.</span></span> <span data-ttu-id="49118-118">例如，ASP.NET Core 项目的 .csproj 文件将与以下示例类似（仅显示该文件的相关部分）。</span><span class="sxs-lookup"><span data-stu-id="49118-118">For example, the *.csproj* file of your ASP.NET Core project will look similar to the following example (only relevant parts of the file are shown).</span></span>

[!code-xml[](entity-framework-6/sample/MVCCore/MVCCore.csproj?range=3-9&highlight=2)]

<span data-ttu-id="49118-119">创建新项目时，请使用 ASP.NET Core Web 应用程序（.NET Framework）模板。</span><span class="sxs-lookup"><span data-stu-id="49118-119">When creating a new project, use the **ASP.NET Core Web Application (.NET Framework)** template.</span></span>

## <a name="handle-connection-strings"></a><span data-ttu-id="49118-120">处理连接字符串</span><span class="sxs-lookup"><span data-stu-id="49118-120">Handle connection strings</span></span>

<span data-ttu-id="49118-121">需通过默认构造函数在 EF6 类库项目中使用 EF6 命令行工具，以便它们能够实例化上下文。</span><span class="sxs-lookup"><span data-stu-id="49118-121">The EF6 command-line tools that you'll use in the EF6 class library project require a default constructor so they can instantiate the context.</span></span> <span data-ttu-id="49118-122">但是，如果想指定要在 ASP.NET Core 项目中使用的连接字符串，则上下文构造函数必须具有可允许你在连接字符串中进行传递的参数。</span><span class="sxs-lookup"><span data-stu-id="49118-122">But you'll probably want to specify the connection string to use in the ASP.NET Core project, in which case your context constructor must have a parameter that lets you pass in the connection string.</span></span> <span data-ttu-id="49118-123">示例如下。</span><span class="sxs-lookup"><span data-stu-id="49118-123">Here's an example.</span></span>

[!code-csharp[](entity-framework-6/sample/EF6/SchoolContext.cs?name=snippet_Constructor)]

<span data-ttu-id="49118-124">由于 EF6 上下文不具有无参数构造函数，因此 EF6 项目必须提供 [IDbContextFactory](https://msdn.microsoft.com/library/hh506876) 的实现。</span><span class="sxs-lookup"><span data-stu-id="49118-124">Since your EF6 context doesn't have a parameterless constructor, your EF6 project has to provide an implementation of [IDbContextFactory](https://msdn.microsoft.com/library/hh506876).</span></span> <span data-ttu-id="49118-125">EF6 命令行工具将查找和使用该实现，以便它们能够实例化上下文。</span><span class="sxs-lookup"><span data-stu-id="49118-125">The EF6 command-line tools will find and use that implementation so they can instantiate the context.</span></span> <span data-ttu-id="49118-126">示例如下。</span><span class="sxs-lookup"><span data-stu-id="49118-126">Here's an example.</span></span>

[!code-csharp[](entity-framework-6/sample/EF6/SchoolContextFactory.cs?name=snippet_IDbContextFactory)]

<span data-ttu-id="49118-127">在此示例代码中，`IDbContextFactory` 实现将在硬编码的连接字符串中传递。</span><span class="sxs-lookup"><span data-stu-id="49118-127">In this sample code, the `IDbContextFactory` implementation passes in a hard-coded connection string.</span></span> <span data-ttu-id="49118-128">这是命令行工具要使用的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="49118-128">This is the connection string that the command-line tools will use.</span></span> <span data-ttu-id="49118-129">你需要实施策略以确保类库与调用应用程序使用相同的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="49118-129">You'll want to implement a strategy to ensure that the class library uses the same connection string that the calling application uses.</span></span> <span data-ttu-id="49118-130">例如，可从这两个项目的环境变量中获取值。</span><span class="sxs-lookup"><span data-stu-id="49118-130">For example, you could get the value from an environment variable in both projects.</span></span>

## <a name="set-up-dependency-injection-in-the-aspnet-core-project"></a><span data-ttu-id="49118-131">在 ASP.NET Core 项目中设置依赖项注入</span><span class="sxs-lookup"><span data-stu-id="49118-131">Set up dependency injection in the ASP.NET Core project</span></span>

<span data-ttu-id="49118-132">在 Core 项目的 Startup.cs 文件中，为 `ConfigureServices` 中的依赖项注入 (DI) 设置 EF6 上下文。</span><span class="sxs-lookup"><span data-stu-id="49118-132">In the Core project's *Startup.cs* file, set up the EF6 context for dependency injection (DI) in `ConfigureServices`.</span></span> <span data-ttu-id="49118-133">应将 EF 上下文对象的范围设置为按请求生存期。</span><span class="sxs-lookup"><span data-stu-id="49118-133">EF context objects should be scoped for a per-request lifetime.</span></span>

[!code-csharp[](entity-framework-6/sample/MVCCore/Startup.cs?name=snippet_ConfigureServices&highlight=5)]

<span data-ttu-id="49118-134">然后即可使用 DI 在控制器中获取上下文的实例。</span><span class="sxs-lookup"><span data-stu-id="49118-134">You can then get an instance of the context in your controllers by using DI.</span></span> <span data-ttu-id="49118-135">此代码与针对 EF Core 上下文编写的代码相似：</span><span class="sxs-lookup"><span data-stu-id="49118-135">The code is similar to what you'd write for an EF Core context:</span></span>

[!code-csharp[](entity-framework-6/sample/MVCCore/Controllers/StudentsController.cs?name=snippet_ContextInController)]

## <a name="sample-application"></a><span data-ttu-id="49118-136">示例应用程序</span><span class="sxs-lookup"><span data-stu-id="49118-136">Sample application</span></span>

<span data-ttu-id="49118-137">若要获取有效的示例应用程序，请参阅本文随附的[示例 Visual Studio 解决方案](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/)。</span><span class="sxs-lookup"><span data-stu-id="49118-137">For a working sample application, see the [sample Visual Studio solution](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/entity-framework-6/sample/) that accompanies this article.</span></span>

<span data-ttu-id="49118-138">可在 Visual Studio 中按照以下步骤从头创建此示例：</span><span class="sxs-lookup"><span data-stu-id="49118-138">This sample can be created from scratch by the following steps in Visual Studio:</span></span>

* <span data-ttu-id="49118-139">创建解决方案。</span><span class="sxs-lookup"><span data-stu-id="49118-139">Create a solution.</span></span>

* <span data-ttu-id="49118-140">添加 > 新建项目 > Web > ASP.NET Core Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="49118-140">**Add** > **New Project** > **Web** > **ASP.NET Core Web Application**</span></span>
  * <span data-ttu-id="49118-141">在“项目模板选择”对话框的下拉列表中，选择 API 和 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="49118-141">In project template selection dialog, select API and .NET Framework in dropdown</span></span>

* <span data-ttu-id="49118-142">添加 > 新建项目 > Windows 桌面 > 类库(.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="49118-142">**Add** > **New Project** > **Windows Desktop** > **Class Library (.NET Framework)**</span></span>

* <span data-ttu-id="49118-143">在两个项目的“包管理器控制台”(PMC) 中运行 `Install-Package Entityframework` 命令。</span><span class="sxs-lookup"><span data-stu-id="49118-143">In **Package Manager Console** (PMC) for both projects, run the command `Install-Package Entityframework`.</span></span>

* <span data-ttu-id="49118-144">在类库项目中，创建数据模型类和上下文类，并创建 `IDbContextFactory` 的实现。</span><span class="sxs-lookup"><span data-stu-id="49118-144">In the class library project, create data model classes and a context class, and an implementation of `IDbContextFactory`.</span></span>

* <span data-ttu-id="49118-145">在类库项目的 PMC 中，运行 `Enable-Migrations` 和 `Add-Migration Initial` 命令。</span><span class="sxs-lookup"><span data-stu-id="49118-145">In PMC for the class library project, run the commands `Enable-Migrations` and `Add-Migration Initial`.</span></span> <span data-ttu-id="49118-146">如果已将 ASP.NET Core 项目设置为启动项目，请向这些命令添加 `-StartupProjectName EF6`。</span><span class="sxs-lookup"><span data-stu-id="49118-146">If you have set the ASP.NET Core project as the startup project, add `-StartupProjectName EF6` to these commands.</span></span>

* <span data-ttu-id="49118-147">在 Core 项目中，添加对类库项目的项目引用。</span><span class="sxs-lookup"><span data-stu-id="49118-147">In the Core project, add a project reference to the class library project.</span></span>

* <span data-ttu-id="49118-148">在 Core 项目的 Startup.cs 中，为 DI 注册上下文。</span><span class="sxs-lookup"><span data-stu-id="49118-148">In the Core project, in *Startup.cs*, register the context for DI.</span></span>

* <span data-ttu-id="49118-149">在 Core 项目的 appsettings.json 中，添加连接字符串。</span><span class="sxs-lookup"><span data-stu-id="49118-149">In the Core project, in *appsettings.json*, add the connection string.</span></span>

* <span data-ttu-id="49118-150">在 Core 项目中，添加控制器和视图以验证可读取和写入数据。</span><span class="sxs-lookup"><span data-stu-id="49118-150">In the Core project, add a controller and view(s) to verify that you can read and write data.</span></span> <span data-ttu-id="49118-151">（请注意，ASP.NET Core MVC 基架不会使用从类库引用的 EF6 上下文。）</span><span class="sxs-lookup"><span data-stu-id="49118-151">(Note that ASP.NET Core MVC scaffolding won't work with the EF6 context referenced from the class library.)</span></span>

## <a name="summary"></a><span data-ttu-id="49118-152">总结</span><span class="sxs-lookup"><span data-stu-id="49118-152">Summary</span></span>

<span data-ttu-id="49118-153">本文提供了在 ASP.NET Core 应用程序中使用 Entity Framework 6 的基本指南。</span><span class="sxs-lookup"><span data-stu-id="49118-153">This article has provided basic guidance for using Entity Framework 6 in an ASP.NET Core application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49118-154">其他资源</span><span class="sxs-lookup"><span data-stu-id="49118-154">Additional resources</span></span>

* [<span data-ttu-id="49118-155">Entity Framework - 基于代码的配置</span><span class="sxs-lookup"><span data-stu-id="49118-155">Entity Framework - Code-Based Configuration</span></span>](https://msdn.microsoft.com/data/jj680699.aspx)

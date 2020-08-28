---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045112"
---
# <a name="adding-a-model"></a><span data-ttu-id="dbf56-102">添加模型</span><span class="sxs-lookup"><span data-stu-id="dbf56-102">Adding a Model</span></span>

<span data-ttu-id="dbf56-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dbf56-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="dbf56-104">在本部分中，你将添加一些用于在数据库中管理电影的类。</span><span class="sxs-lookup"><span data-stu-id="dbf56-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="dbf56-105">这些类将是 &quot; &quot; ASP.NET MVC 应用的模型部分。</span><span class="sxs-lookup"><span data-stu-id="dbf56-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="dbf56-106">您将使用一种称为 [实体框架](https://docs.microsoft.com/ef/) 的 .NET Framework 数据访问技术来定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="dbf56-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="dbf56-107">实体框架 (通常称为 EF) 支持名为 *Code First*的开发模式。</span><span class="sxs-lookup"><span data-stu-id="dbf56-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="dbf56-108">Code First 允许通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="dbf56-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="dbf56-109"> (这些类也称为 POCO 类，从 &quot; 纯旧 CLR 对象开始。 &quot;) 然后可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。</span><span class="sxs-lookup"><span data-stu-id="dbf56-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="dbf56-110">如果需要首先创建数据库，仍可以遵循本教程来了解 MVC 和 EF 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="dbf56-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="dbf56-111">然后，你可以遵循 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 教程，其中介绍了数据库优先方法。</span><span class="sxs-lookup"><span data-stu-id="dbf56-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="dbf56-112">添加模型类</span><span class="sxs-lookup"><span data-stu-id="dbf56-112">Adding Model Classes</span></span>

<span data-ttu-id="dbf56-113">在 **解决方案资源管理器**中，右键单击 " *模型* " 文件夹，选择 " **添加**"，然后选择 " **类**"。</span><span class="sxs-lookup"><span data-stu-id="dbf56-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="dbf56-114">输入 " *类* 名" &quot; 电影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="dbf56-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="dbf56-115">将以下五个属性添加到 `Movie` 类：</span><span class="sxs-lookup"><span data-stu-id="dbf56-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="dbf56-116">我们将使用 `Movie` 类来表示数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="dbf56-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="dbf56-117">对象的每个实例 `Movie` 都对应于数据库表中的一行，类的每个属性 `Movie` 都将映射到表中的一个列。</span><span class="sxs-lookup"><span data-stu-id="dbf56-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="dbf56-118">注意：若要使用 System.web 和相关类，需要安装 [实体框架 NuGet 包](https://www.nuget.org/packages/EntityFramework/)。）</span><span class="sxs-lookup"><span data-stu-id="dbf56-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="dbf56-119">请单击链接获取进一步的说明。</span><span class="sxs-lookup"><span data-stu-id="dbf56-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="dbf56-120">在同一文件中，添加以下 `MovieDBContext` 类：</span><span class="sxs-lookup"><span data-stu-id="dbf56-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="dbf56-121">`MovieDBContext`类表示实体框架的电影数据库上下文，用于处理数据库中的提取、存储和更新 `Movie` 类实例。</span><span class="sxs-lookup"><span data-stu-id="dbf56-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="dbf56-122">`MovieDBContext`派生自 `DbContext` 实体框架提供的基类。</span><span class="sxs-lookup"><span data-stu-id="dbf56-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="dbf56-123">为了能够引用 `DbContext` 和 `DbSet` ，你需要在 `using` 文件顶部添加以下语句：</span><span class="sxs-lookup"><span data-stu-id="dbf56-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="dbf56-124">您可以通过手动添加 using 语句来实现此目的，也可以将鼠标悬停在红色波浪线上，单击 `Show potential fixes` 并单击 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="dbf56-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="dbf56-125">注意：已删除多个未使用的 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="dbf56-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="dbf56-126">Visual Studio 会将未使用的依赖项显示为灰色。</span><span class="sxs-lookup"><span data-stu-id="dbf56-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="dbf56-127">您可以通过将鼠标悬停在灰色依赖项上来删除未使用的依赖项，单击 `Show potential fixes` 并单击 " **删除未使用的 using**</span><span class="sxs-lookup"><span data-stu-id="dbf56-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="dbf56-128">我们最后在 MVC) 中添加了 (M 的模型。</span><span class="sxs-lookup"><span data-stu-id="dbf56-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="dbf56-129">在下一部分中，你将使用数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="dbf56-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dbf56-130">[上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="dbf56-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>

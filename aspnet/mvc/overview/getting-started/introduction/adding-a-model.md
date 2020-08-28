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
# <a name="adding-a-model"></a>添加模型

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本部分中，你将添加一些用于在数据库中管理电影的类。 这些类将是 &quot; &quot; ASP.NET MVC 应用的模型部分。

您将使用一种称为 [实体框架](https://docs.microsoft.com/ef/) 的 .NET Framework 数据访问技术来定义和使用这些模型类。 实体框架 (通常称为 EF) 支持名为 *Code First*的开发模式。 Code First 允许通过编写简单的类来创建模型对象。  (这些类也称为 POCO 类，从 &quot; 纯旧 CLR 对象开始。 &quot;) 然后可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。 如果需要首先创建数据库，仍可以遵循本教程来了解 MVC 和 EF 应用程序开发。 然后，你可以遵循 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 教程，其中介绍了数据库优先方法。

## <a name="adding-model-classes"></a>添加模型类

在 **解决方案资源管理器**中，右键单击 " *模型* " 文件夹，选择 " **添加**"，然后选择 " **类**"。

![](adding-a-model/_static/image1.png)

输入 " *类* 名" &quot; 电影 &quot; 。

将以下五个属性添加到 `Movie` 类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用 `Movie` 类来表示数据库中的影片。 对象的每个实例 `Movie` 都对应于数据库表中的一行，类的每个属性 `Movie` 都将映射到表中的一个列。

注意：若要使用 System.web 和相关类，需要安装 [实体框架 NuGet 包](https://www.nuget.org/packages/EntityFramework/)。） 请单击链接获取进一步的说明。

在同一文件中，添加以下 `MovieDBContext` 类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`类表示实体框架的电影数据库上下文，用于处理数据库中的提取、存储和更新 `Movie` 类实例。 `MovieDBContext`派生自 `DbContext` 实体框架提供的基类。

为了能够引用 `DbContext` 和 `DbSet` ，你需要在 `using` 文件顶部添加以下语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

您可以通过手动添加 using 语句来实现此目的，也可以将鼠标悬停在红色波浪线上，单击 `Show potential fixes` 并单击 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注意：已删除多个未使用的 `using` 语句。 Visual Studio 会将未使用的依赖项显示为灰色。 您可以通过将鼠标悬停在灰色依赖项上来删除未使用的依赖项，单击 `Show potential fixes` 并单击 " **删除未使用的 using**

![](adding-a-model/_static/image3.png)

我们最后在 MVC) 中添加了 (M 的模型。 在下一部分中，你将使用数据库连接字符串。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)

---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038864"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="6b731-101">将模型添加到 ASP.NET Core MVC 应用</span><span class="sxs-lookup"><span data-stu-id="6b731-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="6b731-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6b731-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="6b731-103">在本部分中，将添加用于管理数据库中电影的一些类。</span><span class="sxs-lookup"><span data-stu-id="6b731-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6b731-104">这些类将是 MVC 应用的“Model”部分。</span><span class="sxs-lookup"><span data-stu-id="6b731-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="6b731-105">可以结合 [Entity Framework Core](/ef/core) (EF Core) 使用这些类来处理数据库。</span><span class="sxs-lookup"><span data-stu-id="6b731-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="6b731-106">EF Core 是对象关系映射 (ORM) 框架，可以简化需要编写的数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="6b731-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="6b731-107">[EF Core 支持许多数据库引擎](/ef/core/providers/)。</span><span class="sxs-lookup"><span data-stu-id="6b731-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="6b731-108">要创建的模型类称为 POCO 类（源自“普通旧 CLR 对象”），因为它们与 EF Core 没有任何依赖关系。</span><span class="sxs-lookup"><span data-stu-id="6b731-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="6b731-109">它们只定义将存储在数据库中的数据的属性。</span><span class="sxs-lookup"><span data-stu-id="6b731-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="6b731-110">在本教程中，首先将编写模型类，然后 EF Core 将创建数据库。</span><span class="sxs-lookup"><span data-stu-id="6b731-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="6b731-111">有一种备选方法（此处未介绍）是从已存在的数据库生成模型类。</span><span class="sxs-lookup"><span data-stu-id="6b731-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="6b731-112">有关此方法的信息，请参阅 [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db)（ASP.NET Core - 现有数据库）。</span><span class="sxs-lookup"><span data-stu-id="6b731-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="6b731-113">添加数据模型类</span><span class="sxs-lookup"><span data-stu-id="6b731-113">Add a data model class</span></span>

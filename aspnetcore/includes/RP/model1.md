---
ms.openlocfilehash: 934db70fe49ba9a5330b25596dc694e0ac50c04e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037894"
---
<span data-ttu-id="afbf7-101">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="afbf7-101">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="afbf7-102">在本部分中将添加用于管理数据库中的电影的类。</span><span class="sxs-lookup"><span data-stu-id="afbf7-102">In this section, you add classes for managing movies in a database.</span></span> <span data-ttu-id="afbf7-103">可以结合使用这些类和 [Entity Framework Core](/ef/core) (EF Core) 来处理数据库。</span><span class="sxs-lookup"><span data-stu-id="afbf7-103">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="afbf7-104">EF Core 是对象关系映射 (ORM) 框架，可以简化必须要编写的数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="afbf7-104">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span>

<span data-ttu-id="afbf7-105">要创建的模型类称为 POCO 类（源自“简单传统 CLR 对象”），因为它们与 EF Core 没有任何依赖关系。</span><span class="sxs-lookup"><span data-stu-id="afbf7-105">The model classes you create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="afbf7-106">它们定义数据库中存储的数据属性。</span><span class="sxs-lookup"><span data-stu-id="afbf7-106">They define the properties of the data that are stored in the database.</span></span>

<span data-ttu-id="afbf7-107">在本教程中，首先要编写模型类，然后 EF Core 将创建数据库。</span><span class="sxs-lookup"><span data-stu-id="afbf7-107">In this tutorial, you write the model classes first, and EF Core creates the database.</span></span> <span data-ttu-id="afbf7-108">有一种备选方法（此处未介绍）：[从现有数据库生成模型类](/ef/core/get-started/aspnetcore/existing-db)。</span><span class="sxs-lookup"><span data-stu-id="afbf7-108">An alternate approach not covered here is to [generate model classes from an existing database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

<span data-ttu-id="afbf7-109">[查看或下载](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie)示例。</span><span class="sxs-lookup"><span data-stu-id="afbf7-109">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) sample.</span></span>

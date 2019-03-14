---
ms.openlocfilehash: 984edac5f093d59bd5e1d826df8f32fda89f9e46
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024574"
---
# <a name="work-with-sqlite-in-an-aspnet-core-mvc-app"></a><span data-ttu-id="ddb86-101">在 ASP.NET Core MVC 应用中使用 SQLite</span><span class="sxs-lookup"><span data-stu-id="ddb86-101">Work with SQLite in an ASP.NET Core MVC app</span></span>

<span data-ttu-id="ddb86-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ddb86-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ddb86-103">`MvcMovieContext` 对象处理连接到数据库并将 `Movie` 对象映射到数据库记录的任务。</span><span class="sxs-lookup"><span data-stu-id="ddb86-103">The `MvcMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="ddb86-104">在 Startup.cs 文件的 `ConfigureServices` 方法中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="ddb86-104">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a><span data-ttu-id="ddb86-105">SQLite</span><span class="sxs-lookup"><span data-stu-id="ddb86-105">SQLite</span></span>

<span data-ttu-id="ddb86-106">[SQLite](https://www.sqlite.org/) 网站上表示：</span><span class="sxs-lookup"><span data-stu-id="ddb86-106">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="ddb86-107">SQLite 是一个自包含、高可靠性、嵌入式、功能完整、公共域的 SQL 数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="ddb86-107">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="ddb86-108">SQLite 是世界上使用最多的数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="ddb86-108">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="ddb86-109">可以下载许多第三方工具来管理并查看 SQLite 数据库。</span><span class="sxs-lookup"><span data-stu-id="ddb86-109">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="ddb86-110">下面的图片来自 [DB Browser for SQLite](http://sqlitebrowser.org/)。</span><span class="sxs-lookup"><span data-stu-id="ddb86-110">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="ddb86-111">如果你有最喜欢的 SQLite 工具，请发表评论以分享你喜欢的方面。</span><span class="sxs-lookup"><span data-stu-id="ddb86-111">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![显示电影数据库的 DB Browser for SQLite](~/tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="ddb86-113">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="ddb86-113">Seed the database</span></span>

<span data-ttu-id="ddb86-114">在 Models 文件夹中创建一个名为 `SeedData` 的新类。</span><span class="sxs-lookup"><span data-stu-id="ddb86-114">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="ddb86-115">将生成的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="ddb86-115">Replace the generated code with the following:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="ddb86-116">如果 DB 中没有任何电影，则会返回种子初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="ddb86-116">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="ddb86-117">添加种子初始值设定项</span><span class="sxs-lookup"><span data-stu-id="ddb86-117">Add the seed initializer</span></span>

<span data-ttu-id="ddb86-118">将种子初始值设定项添加 Program.cs 文件中的 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="ddb86-118">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]

::: moniker-end

### <a name="test-the-app"></a><span data-ttu-id="ddb86-119">测试应用</span><span class="sxs-lookup"><span data-stu-id="ddb86-119">Test the app</span></span>

<span data-ttu-id="ddb86-120">删除 DB 中的所有记录（使种子方法运行）。</span><span class="sxs-lookup"><span data-stu-id="ddb86-120">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="ddb86-121">停止并启动应用以设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="ddb86-121">Stop and start the app to seed the database.</span></span>
   
<span data-ttu-id="ddb86-122">应用将显示设定为种子的数据。</span><span class="sxs-lookup"><span data-stu-id="ddb86-122">The app shows the seeded data.</span></span>

![MVC 电影应用程序打开的显示电影数据的浏览器](~/tutorials/first-mvc-app/working-with-sql/_static/m55.png)

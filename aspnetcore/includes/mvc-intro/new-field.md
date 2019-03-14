---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036754"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a>将新字段添加到 ASP.NET Core MVC 应用

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本教程将向 `Movies` 表添加一个新字段。 当更改架构（添加一个新的字段）时，我们将丢弃数据库并创建一个新的数据库。 此工作流适用于在没有要保留的任何生产数据的早期开发阶段。

在部署了应用并且具有要保留的数据后，在需要更改架构时则不能丢弃数据库。 Entity Framework [Code First 迁移](/ef/core/get-started/aspnetcore/new-db)使你能够更新架构并迁移数据库，而不会导致数据丢失。 迁移是使用 SQL Server 时的一个常用的功能，但 SQLlite 不支持许多迁移架构操作，因此只可能进行非常简单的迁移。 有关详细信息，请参阅 [SQLite 限制](/ef/core/providers/sqlite/limitations)。

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

打开 Models/Movie.cs 文件，并添加 `Rating` 属性：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

因为已经添加新字段到 `Movie` 类，所以还需要更新绑定允许名单，将此新属性纳入其中。 在 MoviesController.cs 中，更新 `Create` 和 `Edit` 操作方法的 `[Bind]` 属性，以包括 `Rating` 属性：

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

还需要更新视图模板以在浏览器视图中显示、创建和编辑新的 `Rating` 属性。

编辑 /Views/Movies/Index.cshtml 文件并添加 `Rating` 字段：

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

使用 `Rating` 字段更新 /Views/Movies/Create.cshtml。

在将 DB 更新为包括新字段之前，应用不会正常工作。 如果现在运行，会出现以下 `SqliteException`：

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

看到此错误是因为更新的 Movie 模型类与现有数据库的 Movie 表架构不同。 （数据库表中没有 `Rating` 列。）

可通过几种方法解决此错误：

1. 丢弃数据库，让 Entity Framework 基于新的模型类架构自动重新创建数据库。 如果使用此方法，则会丢失数据库中的现有数据，因此不能对生产数据库使用此方法！ 使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用的有效方式。

2. 手动修改现有数据库的架构，使它与模型类匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。

3. 使用 Code First 迁移更新数据库架构。

在本教程中，我们将在架构更改时丢弃并重新创建数据库。 从终端运行以下命令丢弃 db：

`dotnet ef database drop`

更新 `SeedData` 类，使它提供新列的值。 示例更改如下所示，但可能需要对每个 `new Movie` 做出此更改。

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

将 `Rating` 字段添加到 `Edit`、`Details` 和 `Delete` 视图。

运行应用，并验证是否可以创建/编辑/显示具有 `Rating` 字段的电影。 模板。

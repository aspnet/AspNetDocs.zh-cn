---
title: 将新字段添加到 ASP.NET Core MVC 应用
author: rick-anderson
description: 了解如何使用 Entity Framework Code First 迁移将新字段添加到模型，并将此更改迁移到数据库。
ms.author: riande
ms.custom: mvc
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/new-field
ms.openlocfilehash: 7993b36bf9115225e082d2929bb253aba5b18310
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039314"
---
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a>将新字段添加到 ASP.NET Core MVC 应用

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

在此部分中，[Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First 迁移用于：

* 将新字段添加到模型。
* 将新字段迁移到数据库。

使用 EF Code First 自动创建数据库时，Code First 将：

* 将表添加到数据库，以跟踪数据库的架构。
* 验证数据库与生成它的模型类是否同步。 如果它们不同步，EF 则会引发异常。 这使查找不一致的数据库/代码问题变得更加轻松。

## <a name="add-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

将 `Rating` 属性添加到 Models/Movie.cs：

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

生成应用 (Ctrl+Shift+B)。

因为已经添加新字段到 `Movie` 类，所以需要更新绑定允许名单，将此新属性纳入其中。 在 MoviesController.cs 中，更新 `Create` 和 `Edit` 操作方法的 `[Bind]` 属性，以包括 `Rating` 属性：

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

更新视图模板以在浏览器视图中显示、创建和编辑新的 `Rating` 属性。

编辑 /Views/Movies/Index.cshtml 文件并添加 `Rating` 字段：

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexGenreRating.cshtml?highlight=16,38&range=24-64)]

使用 `Rating` 字段更新 /Views/Movies/Create.cshtml。

<!-- VS -------------------------->
# <a name="visual-studio--visual-studio-for-mactabvisual-studiovisual-studio-mac"></a>[Visual Studio / Visual Studio for Mac](#tab/visual-studio+visual-studio-mac)

可以复制/粘贴之前的“窗体组”，并让 intelliSense 帮助更新字段。 IntelliSense 适用于[标记帮助程序](xref:mvc/views/tag-helpers/intro)。

![开发人员已在视图的第二个标签元素中键入字母 R 用作 asp-for 的特性值。 出现了 Intellisense 上下文菜单，其中显示了可用字段，包括在列表中自动突出显示的“Rating”。 开发人员单击此字段或在键盘上按 Enter 键时，此值将设置为“Rating”。](new-field/_static/cr.png)

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)
<!-- This tab intentionally left blank. -->
---  
<!-- End of VS tabs -->

更新 `SeedData` 类，使它提供新列的值。 示例更改如下所示，但可能需要对每个 `new Movie` 做出此更改。

[!code-csharp[](start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

在 DB 更新为包括新字段之前，应用将不会正常工作。 如果它现在运行，将引发以下 `SqlException`：

`SqlException: Invalid column name 'Rating'.`

发生此错误是因为更新的 Movie 模型类与现有数据库的 Movie 表架构不同。 （数据库表中没有 `Rating` 列。）

可通过几种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 在测试数据库上进行开发时，此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。 但其缺点是会丢失数据库中的现有数据 - 因此请勿对生产数据库使用此方法！ 使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用程序的有效方式。 对于早期开发和使用 SQLite 的情况，这是一个不错的方法。

2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。

3. 使用 Code First 迁移更新数据库架构。

对于本教程，请使用 Code First 迁移。

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

从“工具”菜单中，选择“NuGet 包管理器”>“包管理器控制台”。

  ![PMC 菜单](adding-model/_static/pmc.png)

在 PMC 中，输入以下命令：

```powershell
Add-Migration Rating
Update-Database
```

`Add-Migration` 命令会通知迁移框架使用当前 `Movie` DB 架构检查当前 `Movie` 模型，并创建必要的代码，将 DB 迁移到新模型。

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[Visual Studio Code / Visual Studio for Mac](#tab/visual-studio-code+visual-studio-mac)

[!INCLUDE[](~/includes/RP-mvc-shared/sqlite-warn.md)]

运行下面的命令：

```cli
dotnet ef migrations add Rating
dotnet ef database update
```

---  
<!-- End of VS tabs -->

名称“Rating”是任意的，用于对迁移文件进行命名。 为迁移文件使用有意义的名称是有帮助的。

如果删除 DB 中的所有记录，初始化方法会设定 DB 种子，并将包括 `Rating` 字段。

运行应用，并验证是否可以创建/编辑/显示具有 `Rating` 字段的电影。 应向 `Edit`、`Details` 和 `Delete` 视图模板添加 `Rating` 字段。

> [!div class="step-by-step"]
> [上一页](search.md)
> [下一页](validation.md)  

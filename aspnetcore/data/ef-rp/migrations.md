---
title: ASP.NET Core 中的 Razor 页面和 EF Core - 迁移 - 第 4 个教程（共 8 个）
author: rick-anderson
description: 本教程使用 EF Core 迁移功能管理 ASP.NET Core MVC 应用中的数据模型更改。
ms.author: riande
ms.date: 6/31/2017
uid: data/ef-rp/migrations
ms.openlocfilehash: 2051f55bfa7a9582486df78ec91315f0b03cb1e8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030114"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---migrations---4-of-8"></a>ASP.NET Core 中的 Razor 页面和 EF Core - 迁移 - 第 4 个教程（共 8 个）

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

作者：[Tom Dykstra](https://github.com/tdykstra)、[Jon P Smith](https://twitter.com/thereformedprog) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [about the series](~/includes/RP-EF/intro.md)]

本教程使用 EF Core 迁移功能管理数据模型更改。

如果遇到无法解决的问题，请下载[已完成应用](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)。

开发新应用时，数据模型会频繁更改。 每当模型发生更改时，都无法与数据库进行同步。 本教程首先配置 Entity Framework 以创建数据库（如果不存在）。 每当数据模型发生更改时：

* DB 都会被删除。
* EF 都会创建一个新数据库来匹配该模型。
* 应用使用测试数据为 DB 设定种子。

这种使 DB 与数据模型保持同步的方法适用于多种情况，但将应用部署到生产环境的情况除外。 当应用在生产环境中运行时，应用通常会存储需要保留的数据。 每当发生更改（例如添加新列）时，应用都无法在具有测试 DB 的环境下启动。 EF Core 迁移功能可通过使 EF Core 更新 DB 架构而不是创建新 DB 来解决此问题。

数据模型发生更改时，迁移将更新架构并保留现有数据，而无需删除或重新创建 DB。

## <a name="drop-the-database"></a>删除数据库

使用 SQL Server 对象资源管理器 (SSOX) 或 `database drop` 命令：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

在“包管理器控制台”(PMC) 中运行以下命令：

```PMC
Drop-Database
```

从 PMC 运行 `Get-Help about_EntityFrameworkCore`，获取帮助信息。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

打开命令窗口并导航到项目文件夹。 项目文件夹包含 Startup.cs 文件。

在命令窗口中输入以下内容：

 ```console
 dotnet ef database drop
 ```

------

## <a name="create-an-initial-migration-and-update-the-db"></a>创建初始迁移并更新 DB

生成项目并创建第一个迁移。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

```PMC
Add-Migration InitialCreate
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

------

### <a name="examine-the-up-and-down-methods"></a>了解 Up 和 Down 方法

EF Core `migrations add` 命令已生成用于创建 DB 的代码。 此迁移代码位于 Migrations\<timestamp>_InitialCreate.cs 文件中。 `InitialCreate` 类的 `Up` 的方法创建与数据模型实体集相对应的 DB 表。 `Down` 方法删除这些表，如下例所示：

[!code-csharp[](intro/samples/cu21/Migrations/20180626224812_InitialCreate.cs?range=7-24,77-88)]

迁移调用 `Up` 方法为迁移实现数据模型更改。 输入用于回退更新的命令时，迁移调用 `Down` 方法。

前面的代码适用于初始迁移。 该代码是运行 `migrations add InitialCreate` 命令时创建的。 迁移名称参数（本示例中为“InitialCreate”）用于指定文件名。 迁移名称可以是任何有效的文件名。 最好选择能概括迁移中所执行操作的字词或短语。 例如，添加了系表的迁移可称为“AddDepartmentTable”。

如果创建了初始迁移并且存在 DB：

* 会生成 DB 创建代码。
* DB 创建代码不需要运行，因为 DB 已与数据模型相匹配。 即使 DB 创建代码运行也不会做出任何更改，因为 DB 已与数据模型相匹配。

如果将应用部署到新环境，则必须运行 DB 创建代码才能创建 DB。

先前删除了 DB，因此已不存在，所以迁移会创建新的 DB。

### <a name="the-data-model-snapshot"></a>数据模型快照

迁移在 Migrations/SchoolContextModelSnapshot.cs 中创建当前数据库架构的快照。 添加迁移时，EF 会通过将数据模型与快照文件进行对比来确定已更改的内容。

若要删除迁移，请使用以下命令：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Remove-Migration

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```console
dotnet ef migrations remove
```

有关详细信息，请参阅 [dotnet ef migrations remove](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove)。

------

删除迁移命令会删除迁移并确保正确重置快照。

### <a name="remove-ensurecreated-and-test-the-app"></a>删除 EnsureCreated 并测试应用

早期开发使用了 `EnsureCreated`。 本教程将使用迁移。 `EnsureCreated` 具有以下限制：

* 绕过迁移并创建 DB 和架构。
* 不会创建迁移表。
* 不能与迁移一起使用。
* 专门用于在频繁删除并重新创建 DB 的情况下进行测试或快速制作原型。

删除 `DbInitializer` 中的以下行：

```csharp
context.Database.EnsureCreated();
```

运行应用并验证 DB 设定为种子。

### <a name="inspect-the-database"></a>检查数据库

使用 SQL Server 对象资源管理器检查 DB。 请注意，增加了 `__EFMigrationsHistory` 表。 `__EFMigrationsHistory` 表跟踪已应用到 DB 的迁移。 查看 `__EFMigrationsHistory` 表中的数据，其中显示对应初始迁移的一行数据。 上面的 CLI 输出示例中最后部分的日志显示了创建此行的 INSERT 语句。

运行应用并验证一切正常运行。

## <a name="applying-migrations-in-production"></a>在生产环境中应用迁移

不建议生产应用在应用程序启动时调用 [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)。 不应从服务器场中的应用调用 `Migrate`。 例如，已将应用在云中部署为横向扩展（运行应用的多个示例）的情况。

应在部署过程中以受控的方式执行数据库迁移。 生产数据库迁移方法包括：

* 使用迁移创建 SQL 脚本，并在部署过程中使用 SQL 脚本。
* 在受控的环境中运行 `dotnet ef database update`。

EF Core 使用 `__MigrationsHistory` 表查看是否需要运行任何迁移。 如果 DB 已是最新，则无需运行迁移。

## <a name="troubleshooting"></a>疑难解答

下载[已完成应用](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。

应用会生成以下异常：

```text
SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

解决方案：运行 `dotnet ef database update`

### <a name="additional-resources"></a>其他资源

* [.NET Core CLI](/ef/core/miscellaneous/cli/dotnet).
* [包管理器控制台 (Visual Studio)](/ef/core/miscellaneous/cli/powershell)

::: moniker-end

> [!div class="step-by-step"]
> [上一页](xref:data/ef-rp/sort-filter-page)
> [下一页](xref:data/ef-rp/complex-data-model)

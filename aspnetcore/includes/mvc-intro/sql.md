---
ms.openlocfilehash: 984edac5f093d59bd5e1d826df8f32fda89f9e46
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024574"
---
# <a name="work-with-sqlite-in-an-aspnet-core-mvc-app"></a>在 ASP.NET Core MVC 应用中使用 SQLite

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

`MvcMovieContext` 对象处理连接到数据库并将 `Movie` 对象映射到数据库记录的任务。 在 Startup.cs 文件的 `ConfigureServices` 方法中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：

[!code-csharp[](~/tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a>SQLite

[SQLite](https://www.sqlite.org/) 网站上表示：

> SQLite 是一个自包含、高可靠性、嵌入式、功能完整、公共域的 SQL 数据库引擎。 SQLite 是世界上使用最多的数据库引擎。

可以下载许多第三方工具来管理并查看 SQLite 数据库。 下面的图片来自 [DB Browser for SQLite](http://sqlitebrowser.org/)。 如果你有最喜欢的 SQLite 工具，请发表评论以分享你喜欢的方面。

![显示电影数据库的 DB Browser for SQLite](~/tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a>设定数据库种子

在 Models 文件夹中创建一个名为 `SeedData` 的新类。 将生成的代码替换为以下代码：

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

如果 DB 中没有任何电影，则会返回种子初始值设定项。

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a>添加种子初始值设定项

将种子初始值设定项添加 Program.cs 文件中的 `Main` 方法：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]

::: moniker-end

### <a name="test-the-app"></a>测试应用

删除 DB 中的所有记录（使种子方法运行）。 停止并启动应用以设定数据库种子。
   
应用将显示设定为种子的数据。

![MVC 电影应用程序打开的显示电影数据的浏览器](~/tutorials/first-mvc-app/working-with-sql/_static/m55.png)

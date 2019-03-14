---
title: 使用数据库和 ASP.NET Core
author: rick-anderson
description: 说明如何使用数据库和 ASP.NET Core。
ms.author: riande
ms.date: 12/07/2017
uid: tutorials/razor-pages/sql
ms.openlocfilehash: 3e05f5dbc73c35f1f938346b2eaab8c0fa7d8ab9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061494"
---
# <a name="work-with-a-database-and-aspnet-core"></a><span data-ttu-id="88866-103">使用数据库和 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="88866-103">Work with a database and ASP.NET Core</span></span>

<span data-ttu-id="88866-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="88866-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="88866-105">`RazorPagesMovieContext` 对象处理连接到数据库并将 `Movie` 对象映射到数据库记录的任务。</span><span class="sxs-lookup"><span data-stu-id="88866-105">The `RazorPagesMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="88866-106">在 Startup.cs 的 `ConfigureServices` 方法中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="88866-106">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in *Startup.cs*:</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="88866-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88866-107">Visual Studio</span></span>](#tab/visual-studio)

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Startup.cs?name=snippet_ConfigureServices&highlight=15-18)]

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="88866-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88866-108">Visual Studio Code</span></span>](#tab/visual-studio-code)

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Startup.cs?name=snippet_UseSqlite&highlight=11-12)]

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="88866-109">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="88866-109">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Startup.cs?name=snippet_UseSqlite&highlight=11-12)]

---  
<!-- End of VS tabs -->

<span data-ttu-id="88866-110">有关 `ConfigureServices` 中使用的方法的详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="88866-110">For more information on the methods used in `ConfigureServices`, see:</span></span>

* <span data-ttu-id="88866-111">面向 `CookiePolicyOptions` 的 [ASP.NET Core 中的欧盟一般数据保护条例 (GDPR) 支持](xref:security/gdpr)。</span><span class="sxs-lookup"><span data-stu-id="88866-111">[EU General Data Protection Regulation (GDPR) support in ASP.NET Core](xref:security/gdpr) for `CookiePolicyOptions`.</span></span>
* [<span data-ttu-id="88866-112">SetCompatibilityVersion</span><span class="sxs-lookup"><span data-stu-id="88866-112">SetCompatibilityVersion</span></span>](xref:mvc/compatibility-version)

<span data-ttu-id="88866-113">ASP.NET Core [配置](xref:fundamentals/configuration/index)系统会读取 `ConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="88866-113">The ASP.NET Core [Configuration](xref:fundamentals/configuration/index) system reads the `ConnectionString`.</span></span> <span data-ttu-id="88866-114">为了进行本地开发，它会从 appsettings.json 文件获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="88866-114">For local development, it gets the connection string from the *appsettings.json* file.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="88866-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88866-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="88866-116">生成代码的数据库名称值 (`Database={Database name}`) 将并不不同。</span><span class="sxs-lookup"><span data-stu-id="88866-116">The name value for the database (`Database={Database name}`) will be different for your generated code.</span></span> <span data-ttu-id="88866-117">名称值是任意的。</span><span class="sxs-lookup"><span data-stu-id="88866-117">The name value is arbitrary.</span></span>

[!code-json[](razor-pages-start/sample/RazorPagesMovie22/appsettings.json)]

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="88866-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88866-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

[!code-json[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings_SQLite.json?highlight=8-10)]

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="88866-119">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="88866-119">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

[!code-json[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings_SQLite.json?highlight=8-10)]

---  
<!-- End of VS tabs -->

<span data-ttu-id="88866-120">将应用部署到测试或生产服务器时，可以使用环境变量将连接字符串设置为实际的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="88866-120">When the app is deployed to a test or production server, an environment variable can be used to set the connection string to a real database server.</span></span> <span data-ttu-id="88866-121">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="88866-121">See [Configuration](xref:fundamentals/configuration/index) for more information.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="88866-122">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88866-122">Visual Studio</span></span>](#tab/visual-studio)

## <a name="sql-server-express-localdb"></a><span data-ttu-id="88866-123">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="88866-123">SQL Server Express LocalDB</span></span>

<span data-ttu-id="88866-124">LocalDB 是轻型版的 SQL Server Express 数据库引擎，以程序开发为目标。</span><span class="sxs-lookup"><span data-stu-id="88866-124">LocalDB is a lightweight version of the SQL Server Express database engine that's targeted for program development.</span></span> <span data-ttu-id="88866-125">LocalDB 作为按需启动并在用户模式下运行的轻量级数据库没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="88866-125">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="88866-126">默认情况下，LocalDB 数据库在 `C:/Users/<user/>` 目录下创建 `*.mdf` 文件。</span><span class="sxs-lookup"><span data-stu-id="88866-126">By default, LocalDB database creates `*.mdf` files in the `C:/Users/<user/>` directory.</span></span>

<a name="ssox"></a>
* <span data-ttu-id="88866-127">从“视图”菜单中，打开“SQL Server 对象资源管理器”(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="88866-127">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![“视图”菜单](sql/_static/ssox.png)

* <span data-ttu-id="88866-129">右键单击 `Movie` 表，然后选择“视图设计器”：</span><span class="sxs-lookup"><span data-stu-id="88866-129">Right click on the `Movie` table and select **View Designer**:</span></span>

  ![Movie 表上打开的上下文菜单](sql/_static/design.png)

  ![设计器中打开的 Movie 表](sql/_static/dv.png)

<span data-ttu-id="88866-132">请注意 `ID` 旁边的密钥图标。</span><span class="sxs-lookup"><span data-stu-id="88866-132">Note the key icon next to `ID`.</span></span> <span data-ttu-id="88866-133">默认情况下，EF 为该主键创建一个名为 `ID` 的属性。</span><span class="sxs-lookup"><span data-stu-id="88866-133">By default, EF creates a property named `ID` for the primary key.</span></span>

* <span data-ttu-id="88866-134">右键单击 `Movie` 表，然后选择“查看数据”：</span><span class="sxs-lookup"><span data-stu-id="88866-134">Right click on the `Movie` table and select **View Data**:</span></span>

  <span data-ttu-id="88866-135">![显示表数据的打开的 Movie 表](sql/_static/vd22.png)
<!-- Code --------------------------></span><span class="sxs-lookup"><span data-stu-id="88866-135">![Movie table open showing table data](sql/_static/vd22.png)
<!-- Code --------------------------></span></span>
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="88866-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88866-136">Visual Studio Code</span></span>](#tab/visual-studio-code)

[!INCLUDE[](~/includes/rp/sqlite.md)]

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="88866-137">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="88866-137">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

[!INCLUDE[](~/includes/rp/sqlite.md)]

---  
<!-- End of VS tabs -->

## <a name="seed-the-database"></a><span data-ttu-id="88866-138">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="88866-138">Seed the database</span></span>

<span data-ttu-id="88866-139">使用以下代码在 Models 文件夹中创建一个名为 `SeedData` 的新类：</span><span class="sxs-lookup"><span data-stu-id="88866-139">Create a new class named `SeedData` in the *Models* folder with the following code:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="88866-140">如果 DB 中有任何电影，则会返回种子初始值设定项，并且不会添加任何电影。</span><span class="sxs-lookup"><span data-stu-id="88866-140">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```
<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="88866-141">添加种子初始值设定项</span><span class="sxs-lookup"><span data-stu-id="88866-141">Add the seed initializer</span></span>

<span data-ttu-id="88866-142">在 Program.cs 中，修改 `Main` 方法以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="88866-142">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="88866-143">从依赖关系注入容器获取数据库上下文实例。</span><span class="sxs-lookup"><span data-stu-id="88866-143">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="88866-144">调用 seed 方法，并将上下文传递给它。</span><span class="sxs-lookup"><span data-stu-id="88866-144">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="88866-145">Seed 方法完成时释放上下文。</span><span class="sxs-lookup"><span data-stu-id="88866-145">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="88866-146">下面的代码显示更新后的 Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="88866-146">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Program.cs)]

<span data-ttu-id="88866-147">生产应用不会调用 `Database.Migrate`。</span><span class="sxs-lookup"><span data-stu-id="88866-147">A production app would not call `Database.Migrate`.</span></span> <span data-ttu-id="88866-148">它会添加到上面的代码中，以防止在未运行 `Update-Database` 时出现以下异常：</span><span class="sxs-lookup"><span data-stu-id="88866-148">It's added to the preceding code to prevent the following exception when `Update-Database` has not been run:</span></span>

<span data-ttu-id="88866-149">SqlException：无法打开登录请求的数据库“RazorPagesMovieContext-21”。</span><span class="sxs-lookup"><span data-stu-id="88866-149">SqlException: Cannot open database "RazorPagesMovieContext-21" requested by the login.</span></span> <span data-ttu-id="88866-150">登录失败。</span><span class="sxs-lookup"><span data-stu-id="88866-150">The login failed.</span></span>
<span data-ttu-id="88866-151">用户“用户名”登录失败。</span><span class="sxs-lookup"><span data-stu-id="88866-151">Login failed for user 'user name'.</span></span>

### <a name="test-the-app"></a><span data-ttu-id="88866-152">测试应用</span><span class="sxs-lookup"><span data-stu-id="88866-152">Test the app</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="88866-153">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88866-153">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="88866-154">删除 DB 中的所有记录。</span><span class="sxs-lookup"><span data-stu-id="88866-154">Delete all the records in the DB.</span></span> <span data-ttu-id="88866-155">可以使用浏览器中的删除链接，也可以从 [SSOX](xref:tutorials/razor-pages/new-field#ssox) 执行此操作</span><span class="sxs-lookup"><span data-stu-id="88866-155">You can do this with the delete links in the browser or from [SSOX](xref:tutorials/razor-pages/new-field#ssox)</span></span>
* <span data-ttu-id="88866-156">强制应用初始化（调用 `Startup` 类中的方法），使种子方法能够正常运行。</span><span class="sxs-lookup"><span data-stu-id="88866-156">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="88866-157">若要强制进行初始化，必须先停止 IIS Express，然后再重新启动它。</span><span class="sxs-lookup"><span data-stu-id="88866-157">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="88866-158">可以使用以下任一方法来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="88866-158">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="88866-159">右键单击通知区域中的 IIS Express 系统任务栏图标，然后点击“退出”或“停止站点”：</span><span class="sxs-lookup"><span data-stu-id="88866-159">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**:</span></span>

    ![IIS Express 系统任务栏图标](../first-mvc-app/working-with-sql/_static/iisExIcon.png)

    ![上下文菜单](sql/_static/stopIIS.png)

    * <span data-ttu-id="88866-162">如果是在非调试模式下运行 VS 的，请按 F5 以在调试模式下运行。</span><span class="sxs-lookup"><span data-stu-id="88866-162">If you were running VS in non-debug mode, press F5 to run in debug mode.</span></span>
    * <span data-ttu-id="88866-163">如果是在调试模式下运行 VS 的，请停止调试程序并按 F5。</span><span class="sxs-lookup"><span data-stu-id="88866-163">If you were running VS in debug mode, stop the debugger and press F5.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="88866-164">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88866-164">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="88866-165">删除 DB 中的所有记录（使种子方法运行）。</span><span class="sxs-lookup"><span data-stu-id="88866-165">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="88866-166">停止并启动应用以设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="88866-166">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="88866-167">应用将显示设定为种子的数据。</span><span class="sxs-lookup"><span data-stu-id="88866-167">The app shows the seeded data.</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="88866-168">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="88866-168">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="88866-169">删除 DB 中的所有记录（使种子方法运行）。</span><span class="sxs-lookup"><span data-stu-id="88866-169">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="88866-170">停止并启动应用以设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="88866-170">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="88866-171">应用将显示设定为种子的数据。</span><span class="sxs-lookup"><span data-stu-id="88866-171">The app shows the seeded data.</span></span>

---  
<!-- End of VS tabs -->


   
<span data-ttu-id="88866-172">应用将显示设定为种子的数据：</span><span class="sxs-lookup"><span data-stu-id="88866-172">The app shows the seeded data:</span></span>

![在 Chrome 中打开的显示电影数据的电影应用程序](sql/_static/m55.png)

<span data-ttu-id="88866-174">在下一教程中将对数据的展示进行整理。</span><span class="sxs-lookup"><span data-stu-id="88866-174">The next tutorial will clean up the presentation of the data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="88866-175">[上一篇：已搭建基架的 Razor Pages](xref:tutorials/razor-pages/page)
> [下一篇：更新页面](xref:tutorials/razor-pages/da1)</span><span class="sxs-lookup"><span data-stu-id="88866-175">[Previous: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)
[Next: Updating the pages](xref:tutorials/razor-pages/da1)</span></span>

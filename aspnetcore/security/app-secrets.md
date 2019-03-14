---
title: 安全存储中 ASP.NET Core 中开发的应用程序机密
author: rick-anderson
description: 了解如何存储和检索在 ASP.NET Core 应用程序开发期间为应用程序机密的敏感信息。
ms.author: scaddie
ms.custom: mvc
ms.date: 01/31/2019
uid: security/app-secrets
ms.openlocfilehash: eaa2e9d1ba98d391a29a9ff55872d062df016b87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030144"
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="04575-103">安全存储中 ASP.NET Core 中开发的应用程序机密</span><span class="sxs-lookup"><span data-stu-id="04575-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="04575-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Daniel Roth](https://github.com/danroth27)，和[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="04575-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="04575-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="04575-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="04575-106">本文档介绍用于存储和检索敏感数据的 ASP.NET Core 应用程序开发过程的技术。</span><span class="sxs-lookup"><span data-stu-id="04575-106">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="04575-107">永远不要将密码或其他敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="04575-107">Never store passwords or other sensitive data in source code.</span></span> <span data-ttu-id="04575-108">不应使用生产机密进行开发或测试。</span><span class="sxs-lookup"><span data-stu-id="04575-108">Production secrets shouldn't be used for development or test.</span></span> <span data-ttu-id="04575-109">可使用 [Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)存储和保护 Azure 测试和生产机密。</span><span class="sxs-lookup"><span data-stu-id="04575-109">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="04575-110">环境变量</span><span class="sxs-lookup"><span data-stu-id="04575-110">Environment variables</span></span>

<span data-ttu-id="04575-111">使用环境变量以避免在代码中或在本地配置文件中的应用机密的存储。</span><span class="sxs-lookup"><span data-stu-id="04575-111">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="04575-112">环境变量重写所有以前指定的配置源的配置的值。</span><span class="sxs-lookup"><span data-stu-id="04575-112">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="04575-113">通过调用配置的环境变量值的读取[AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="04575-113">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=8)]

::: moniker-end

<span data-ttu-id="04575-114">请考虑在其中一个 ASP.NET Core web 应用**单个用户帐户**已启用安全性。</span><span class="sxs-lookup"><span data-stu-id="04575-114">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="04575-115">默认数据库连接字符串包含在项目的*appsettings.json*文件具有键`DefaultConnection`。</span><span class="sxs-lookup"><span data-stu-id="04575-115">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="04575-116">默认连接字符串是 localdb，这在用户模式下运行，不需要密码。</span><span class="sxs-lookup"><span data-stu-id="04575-116">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="04575-117">应用程序在部署期间，`DefaultConnection`使用环境变量的值可以重写密钥值。</span><span class="sxs-lookup"><span data-stu-id="04575-117">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="04575-118">环境变量可以存储敏感凭据与完整的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="04575-118">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="04575-119">环境变量通常存储在普通的未加密的文本。</span><span class="sxs-lookup"><span data-stu-id="04575-119">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="04575-120">如果计算机或进程受到攻击，可以由不受信任方访问环境变量。</span><span class="sxs-lookup"><span data-stu-id="04575-120">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="04575-121">可能需要更多措施，防止用户机密泄露。</span><span class="sxs-lookup"><span data-stu-id="04575-121">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="04575-122">机密管理器</span><span class="sxs-lookup"><span data-stu-id="04575-122">Secret Manager</span></span>

<span data-ttu-id="04575-123">密码管理器工具在 ASP.NET Core 项目的开发过程中存储敏感数据。</span><span class="sxs-lookup"><span data-stu-id="04575-123">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="04575-124">在此上下文中，一种敏感数据是应用程序密码。</span><span class="sxs-lookup"><span data-stu-id="04575-124">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="04575-125">应用程序机密存储在项目树不同的位置。</span><span class="sxs-lookup"><span data-stu-id="04575-125">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="04575-126">与特定项目关联或在多个项目之间共享的应用程序机密。</span><span class="sxs-lookup"><span data-stu-id="04575-126">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="04575-127">应用机密不会签入源代码管理。</span><span class="sxs-lookup"><span data-stu-id="04575-127">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="04575-128">机密管理器工具不会加密存储的机密，不应被视为受信任存储区。</span><span class="sxs-lookup"><span data-stu-id="04575-128">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="04575-129">它是仅限开发目的。</span><span class="sxs-lookup"><span data-stu-id="04575-129">It's for development purposes only.</span></span> <span data-ttu-id="04575-130">在用户配置文件目录中的 JSON 配置文件中存储的键和值。</span><span class="sxs-lookup"><span data-stu-id="04575-130">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="04575-131">机密管理器工具的工作原理</span><span class="sxs-lookup"><span data-stu-id="04575-131">How the Secret Manager tool works</span></span>

<span data-ttu-id="04575-132">机密管理器工具抽象化实现详细信息，例如位置和方式存储的值。</span><span class="sxs-lookup"><span data-stu-id="04575-132">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="04575-133">如果不知道这些实现的详细信息，可以使用该工具。</span><span class="sxs-lookup"><span data-stu-id="04575-133">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="04575-134">值存储在本地计算机上 JSON 配置文件中的系统保护的用户配置文件文件夹中：</span><span class="sxs-lookup"><span data-stu-id="04575-134">The values are stored in a JSON configuration file in a system-protected user profile folder on the local machine:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="04575-135">Windows</span><span class="sxs-lookup"><span data-stu-id="04575-135">Windows</span></span>](#tab/windows)

<span data-ttu-id="04575-136">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="04575-136">File system path:</span></span>

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[<span data-ttu-id="04575-137">macOS</span><span class="sxs-lookup"><span data-stu-id="04575-137">macOS</span></span>](#tab/macos)

<span data-ttu-id="04575-138">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="04575-138">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[<span data-ttu-id="04575-139">Linux</span><span class="sxs-lookup"><span data-stu-id="04575-139">Linux</span></span>](#tab/linux)

<span data-ttu-id="04575-140">文件系统路径：</span><span class="sxs-lookup"><span data-stu-id="04575-140">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

<span data-ttu-id="04575-141">在前面文件路径中，替换`<user_secrets_id>`与`UserSecretsId`中指定值 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="04575-141">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="04575-142">不编写代码，取决于使用机密管理器工具中保存的数据的格式的位置。</span><span class="sxs-lookup"><span data-stu-id="04575-142">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="04575-143">这些实现细节可能会更改。</span><span class="sxs-lookup"><span data-stu-id="04575-143">These implementation details may change.</span></span> <span data-ttu-id="04575-144">例如，机密的值不会加密，但可能在将来。</span><span class="sxs-lookup"><span data-stu-id="04575-144">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"

## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="04575-145">安装机密管理器工具</span><span class="sxs-lookup"><span data-stu-id="04575-145">Install the Secret Manager tool</span></span>

<span data-ttu-id="04575-146">机密管理器工具是可与.NET Core CLI，在.NET Core SDK 2.1.300 捆绑或更高版本。</span><span class="sxs-lookup"><span data-stu-id="04575-146">The Secret Manager tool is bundled with the .NET Core CLI in .NET Core SDK 2.1.300 or later.</span></span> <span data-ttu-id="04575-147">有关.NET Core SDK 2.1.300 之前的版本中，工具安装是必需的。</span><span class="sxs-lookup"><span data-stu-id="04575-147">For .NET Core SDK versions before 2.1.300, tool installation is necessary.</span></span>

> [!TIP]
> <span data-ttu-id="04575-148">运行`dotnet --version`从命令行界面中，若要查看已安装的.NET Core SDK 版本号。</span><span class="sxs-lookup"><span data-stu-id="04575-148">Run `dotnet --version` from a command shell to see the installed .NET Core SDK version number.</span></span>

<span data-ttu-id="04575-149">如果正在使用的.NET Core SDK 包括的工具，将显示警告：</span><span class="sxs-lookup"><span data-stu-id="04575-149">A warning is displayed if the .NET Core SDK being used includes the tool:</span></span>

```console
The tool 'Microsoft.Extensions.SecretManager.Tools' is now included in the .NET Core SDK. Information on resolving this warning is available at (https://aka.ms/dotnetclitools-in-box).
```

<span data-ttu-id="04575-150">安装[Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) ASP.NET Core 项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="04575-150">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project.</span></span> <span data-ttu-id="04575-151">例如：</span><span class="sxs-lookup"><span data-stu-id="04575-151">For example:</span></span>

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=15-16)]

<span data-ttu-id="04575-152">在验证工具的安装命令行界面中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="04575-152">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="04575-153">机密管理器工具会显示示例用法、 选项和命令帮助：</span><span class="sxs-lookup"><span data-stu-id="04575-153">The Secret Manager tool displays sample usage, options, and command help:</span></span>

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> <span data-ttu-id="04575-154">您必须位于与相同的目录 *.csproj*文件中定义的工具在运行 *.csproj*文件的`DotNetCliToolReference`元素。</span><span class="sxs-lookup"><span data-stu-id="04575-154">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>

::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="04575-155">设置的机密</span><span class="sxs-lookup"><span data-stu-id="04575-155">Set a secret</span></span>

<span data-ttu-id="04575-156">机密管理器工具对存储在用户配置文件中的特定于项目的配置设置进行操作。</span><span class="sxs-lookup"><span data-stu-id="04575-156">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="04575-157">若要使用用户机密，定义`UserSecretsId`中的元素`PropertyGroup`的 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="04575-157">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="04575-158">值`UserSecretsId`是任意的但仅适用于该项目。</span><span class="sxs-lookup"><span data-stu-id="04575-158">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="04575-159">开发人员通常会生成的 GUID `UserSecretsId`。</span><span class="sxs-lookup"><span data-stu-id="04575-159">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

> [!TIP]
> <span data-ttu-id="04575-160">在 Visual Studio 中，右键单击解决方案资源管理器中的项目并选择**管理用户机密**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="04575-160">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="04575-161">添加了此笔势`UserSecretsId`元素中，为填充 guid *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="04575-161">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="04575-162">Visual Studio 将打开*secrets.json*在文本编辑器中的文件。</span><span class="sxs-lookup"><span data-stu-id="04575-162">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="04575-163">内容替换为*secrets.json*与要存储的键 / 值对。</span><span class="sxs-lookup"><span data-stu-id="04575-163">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="04575-164">例如：</span><span class="sxs-lookup"><span data-stu-id="04575-164">For example:</span></span>
> ```json
> {
>   "Movies": {
>     "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true",
>     "ServiceApiKey": "12345"
>   }
> }
> ```
> <span data-ttu-id="04575-165">JSON 结构平展后通过修改`dotnet user-secrets remove`或`dotnet user-secrets set`。</span><span class="sxs-lookup"><span data-stu-id="04575-165">The JSON structure is flattened after modifications via `dotnet user-secrets remove` or `dotnet user-secrets set`.</span></span> <span data-ttu-id="04575-166">例如，运行`dotnet user-secrets remove "Movies:ConnectionString"`折叠`Movies`对象文字。</span><span class="sxs-lookup"><span data-stu-id="04575-166">For example, running `dotnet user-secrets remove "Movies:ConnectionString"` collapses the `Movies` object literal.</span></span> <span data-ttu-id="04575-167">修改后的文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="04575-167">The modified file resembles the following:</span></span>
> ```json
> {
>   "Movies:ServiceApiKey": "12345"
> }
> ```

<span data-ttu-id="04575-168">定义由一个键和其值组成的应用程序密码。</span><span class="sxs-lookup"><span data-stu-id="04575-168">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="04575-169">密钥是与项目相关联`UserSecretsId`值。</span><span class="sxs-lookup"><span data-stu-id="04575-169">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="04575-170">例如，从在其中的目录运行以下命令 *.csproj*文件是否存在：</span><span class="sxs-lookup"><span data-stu-id="04575-170">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="04575-171">在前面的示例中，冒号表示`Movies`是一个对象文字与`ServiceApiKey`属性。</span><span class="sxs-lookup"><span data-stu-id="04575-171">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="04575-172">机密管理器工具可以过使用从其他目录。</span><span class="sxs-lookup"><span data-stu-id="04575-172">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="04575-173">使用`--project`选项可提供文件系统路径，在 *.csproj*文件存在。</span><span class="sxs-lookup"><span data-stu-id="04575-173">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="04575-174">例如：</span><span class="sxs-lookup"><span data-stu-id="04575-174">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="04575-175">设置多个机密</span><span class="sxs-lookup"><span data-stu-id="04575-175">Set multiple secrets</span></span>

<span data-ttu-id="04575-176">可以通过管道传递到 JSON 设置机密一批`set`命令。</span><span class="sxs-lookup"><span data-stu-id="04575-176">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="04575-177">在以下示例中， *input.json*文件的内容通过管道传递给`set`命令。</span><span class="sxs-lookup"><span data-stu-id="04575-177">In the following example, the *input.json* file's contents are piped to the `set` command.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="04575-178">Windows</span><span class="sxs-lookup"><span data-stu-id="04575-178">Windows</span></span>](#tab/windows)

<span data-ttu-id="04575-179">打开命令外壳中，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="04575-179">Open a command shell, and execute the following command:</span></span>

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[<span data-ttu-id="04575-180">macOS</span><span class="sxs-lookup"><span data-stu-id="04575-180">macOS</span></span>](#tab/macos)

<span data-ttu-id="04575-181">打开命令外壳中，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="04575-181">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[<span data-ttu-id="04575-182">Linux</span><span class="sxs-lookup"><span data-stu-id="04575-182">Linux</span></span>](#tab/linux)

<span data-ttu-id="04575-183">打开命令外壳中，并执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="04575-183">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a><span data-ttu-id="04575-184">访问机密</span><span class="sxs-lookup"><span data-stu-id="04575-184">Access a secret</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="04575-185">[ASP.NET Core 配置 API](xref:fundamentals/configuration/index)提供对机密 Manager 机密的访问。</span><span class="sxs-lookup"><span data-stu-id="04575-185">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="04575-186">如果项目面向.NET Framework，安装[Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="04575-186">If your project targets the .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="04575-187">在 ASP.NET Core 2.0 或更高版本，用户机密配置源时，自动添加在开发模式下项目调用<xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>来初始化与预配置的默认主机的新实例。</span><span class="sxs-lookup"><span data-stu-id="04575-187">In ASP.NET Core 2.0 or later, the user secrets configuration source is automatically added in development mode when the project calls <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> to initialize a new instance of the host with preconfigured defaults.</span></span> <span data-ttu-id="04575-188">`CreateDefaultBuilder` 调用<xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*>时<xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName>是<xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span><span class="sxs-lookup"><span data-stu-id="04575-188">`CreateDefaultBuilder` calls <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> when the <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName> is <xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]

<span data-ttu-id="04575-189">当`CreateDefaultBuilder`不是调用，通过调用显式添加的用户机密配置源<xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*>中`Startup`构造函数。</span><span class="sxs-lookup"><span data-stu-id="04575-189">When `CreateDefaultBuilder` isn't called, add the user secrets configuration source explicitly by calling <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> in the `Startup` constructor.</span></span> <span data-ttu-id="04575-190">调用`AddUserSecrets`仅运行的应用在开发环境中，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="04575-190">Call `AddUserSecrets` only when the app runs in the Development environment, as shown in the following example:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="04575-191">[ASP.NET Core 配置 API](xref:fundamentals/configuration/index)提供对机密 Manager 机密的访问。</span><span class="sxs-lookup"><span data-stu-id="04575-191">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="04575-192">安装[Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="04575-192">Install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="04575-193">添加用户机密配置源通过调用[AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets)中`Startup`构造函数：</span><span class="sxs-lookup"><span data-stu-id="04575-193">Add the user secrets configuration source with a call to [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

<span data-ttu-id="04575-194">可以通过检索用户机密`Configuration`API:</span><span class="sxs-lookup"><span data-stu-id="04575-194">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=26)]

::: moniker-end

## <a name="map-secrets-to-a-poco"></a><span data-ttu-id="04575-195">映射到 POCO 的机密</span><span class="sxs-lookup"><span data-stu-id="04575-195">Map secrets to a POCO</span></span>

<span data-ttu-id="04575-196">将整个对象文字映射到 POCO （具有属性的简单.NET 类） 可用于聚合相关的属性。</span><span class="sxs-lookup"><span data-stu-id="04575-196">Mapping an entire object literal to a POCO (a simple .NET class with properties) is useful for aggregating related properties.</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="04575-197">若要映射到 POCO，前面的机密，使用`Configuration`API 的[对象 graph 绑定](xref:fundamentals/configuration/index#bind-to-an-object-graph)功能。</span><span class="sxs-lookup"><span data-stu-id="04575-197">To map the preceding secrets to a POCO, use the `Configuration` API's [object graph binding](xref:fundamentals/configuration/index#bind-to-an-object-graph) feature.</span></span> <span data-ttu-id="04575-198">以下代码将绑定到自定义`MovieSettings`POCO 和访问`ServiceApiKey`属性值：</span><span class="sxs-lookup"><span data-stu-id="04575-198">The following code binds to a custom `MovieSettings` POCO and accesses the `ServiceApiKey` property value:</span></span>

::: moniker range=">= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

::: moniker range="= aspnetcore-1.0"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

<span data-ttu-id="04575-199">`Movies:ConnectionString`并`Movies:ServiceApiKey`机密映射到相应的属性中`MovieSettings`:</span><span class="sxs-lookup"><span data-stu-id="04575-199">The `Movies:ConnectionString` and `Movies:ServiceApiKey` secrets are mapped to the respective properties in `MovieSettings`:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Models/MovieSettings.cs?name=snippet_MovieSettingsClass)]

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="04575-200">包含机密的字符串替换</span><span class="sxs-lookup"><span data-stu-id="04575-200">String replacement with secrets</span></span>

<span data-ttu-id="04575-201">以纯文本形式存储密码是不安全。</span><span class="sxs-lookup"><span data-stu-id="04575-201">Storing passwords in plain text is insecure.</span></span> <span data-ttu-id="04575-202">例如，数据库连接字符串存储在*appsettings.json*可能包括指定用户的密码：</span><span class="sxs-lookup"><span data-stu-id="04575-202">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="04575-203">更安全的方法是将密码存储为机密。</span><span class="sxs-lookup"><span data-stu-id="04575-203">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="04575-204">例如：</span><span class="sxs-lookup"><span data-stu-id="04575-204">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="04575-205">删除`Password`中的连接字符串中的键 / 值对*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="04575-205">Remove the `Password` key-value pair from the connection string in *appsettings.json*.</span></span> <span data-ttu-id="04575-206">例如：</span><span class="sxs-lookup"><span data-stu-id="04575-206">For example:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="04575-207">在上设置的机密的值[SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder)对象的[密码](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password)属性来完成的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="04575-207">The secret's value can be set on a [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) object's [Password](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) property to complete the connection string:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-17)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=26-29)]

::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="04575-208">列出机密</span><span class="sxs-lookup"><span data-stu-id="04575-208">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="04575-209">从在其中的目录运行以下命令 *.csproj*文件是否存在：</span><span class="sxs-lookup"><span data-stu-id="04575-209">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="04575-210">将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="04575-210">The following output appears:</span></span>

```console
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
Movies:ServiceApiKey = 12345
```

<span data-ttu-id="04575-211">在前面的示例中，在项名称中的冒号表示对象层次结构内的*secrets.json*。</span><span class="sxs-lookup"><span data-stu-id="04575-211">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="04575-212">删除单个机密</span><span class="sxs-lookup"><span data-stu-id="04575-212">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="04575-213">从在其中的目录运行以下命令 *.csproj*文件是否存在：</span><span class="sxs-lookup"><span data-stu-id="04575-213">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="04575-214">应用程序的*secrets.json*已修改文件，以删除与关联的键 / 值对`MoviesConnectionString`密钥：</span><span class="sxs-lookup"><span data-stu-id="04575-214">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="04575-215">运行`dotnet user-secrets list`会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="04575-215">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="04575-216">删除所有机密</span><span class="sxs-lookup"><span data-stu-id="04575-216">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="04575-217">从在其中的目录运行以下命令 *.csproj*文件是否存在：</span><span class="sxs-lookup"><span data-stu-id="04575-217">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="04575-218">从已删除应用程序的所有用户机密*secrets.json*文件：</span><span class="sxs-lookup"><span data-stu-id="04575-218">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="04575-219">运行`dotnet user-secrets list`会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="04575-219">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="04575-220">其他资源</span><span class="sxs-lookup"><span data-stu-id="04575-220">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>

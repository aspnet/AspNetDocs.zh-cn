---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: 081a631c9c3e74c01e15f4b0b272d650c162bd20
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031284"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>在 Windows 服务中托管 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)

不使用 IIS 时，可以在 Windows 上将 ASP.NET Core 应用作为 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)进行托管。 作为 Windows 服务进行托管时，应用将在重新启动后自动启动。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="deployment-type"></a>部署类型

可以创建依赖框架的 Windows 服务部署或独立的 Windows 服务部署。 有关部署方案的信息和建议，请参阅 [.NET Core 应用程序部署](/dotnet/core/deploying/)。

### <a name="framework-dependent-deployment"></a>依赖框架的部署

依赖框架的部署 (FDD) 依赖目标系统上存在共享系统级版本的 .NET Core。 当 FDD 方案用于 ASP.NET Core Windows 服务应用时，SDK 会生成一个称为“依赖框架的可执行文件”的可执行文件 (*\*.exe*)。

### <a name="self-contained-deployment"></a>独立部署

独立部署 (SCD) 不依赖目标系统上存在的共享组件。 运行时和应用的依赖项将与应用一起部署到托管系统。

## <a name="convert-a-project-into-a-windows-service"></a>将项目转换为 Windows 服务

对现有 ASP.NET Core 项目进行以下更改，以将应用作为服务运行：

### <a name="project-file-updates"></a>项目文件更新

根据所选的[部署类型](#deployment-type)，更新项目文件：

#### <a name="framework-dependent-deployment-fdd"></a>依赖框架的部署 (FDD)

将 Windows [运行时标识符 (RID)](/dotnet/core/rid-catalog) 添加到包含目标框架的 `<PropertyGroup>` 中。 在以下示例中，将 RID 设置为 `win7-x64`。 将 `<SelfContained>` 属性集添加到 `false`。 这些属性指示 SDK 为 Windows 生成可执行 (.exe) 文件。

web.config文件（通常在发布 ASP.NET Core 应用时生成）对于 Windows 服务应用来说是不必要的。 若要禁止创建 web.config 文件，请将 `<IsTransformWebConfigDisabled>` 属性集添加到 `true`。

::: moniker range=">= aspnetcore-2.2"

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

将 `<UseAppHost>` 属性集添加到 `true`。 此属性为服务提供 FDD 的激活路径（一个可执行文件，格式为 .exe）。

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.1</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <UseAppHost>true</UseAppHost>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

#### <a name="self-contained-deployment-scd"></a>独立部署 (SCD)

确认是否存在 Windows [运行时标识符 (RID)](/dotnet/core/rid-catalog)，或将 RID 添加到包含目标框架的 `<PropertyGroup>` 中。 通过将 `<IsTransformWebConfigDisabled>` 属性集添加到 `true` 来禁止创建 web.config文件。

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

要发布多个 RID：

* 通过以分号分隔的列表提供 RID。
* 使用属性名称 `<RuntimeIdentifiers>`（复数）。

  有关详细信息，请参阅 [.NET Core RID 目录](/dotnet/core/rid-catalog)。

为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices) 添加包引用。

若要启用 Windows 事件日志记录，请添加 [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) 的包引用。

有关详细信息，请参阅[处理启动和停止事件](#handle-starting-and-stopping-events)部分。

### <a name="programmain-updates"></a>Program.Main 更新

在 `Program.Main` 中，进行下列更改：

* 在服务之外运行时，若要进行测试和调试，请添加代码以确定应用是否作为服务或控制台应用运行。 检查是否已连接调试器或是否存在 `--console` 命令行参数。

  如果其中一个条件为 true（应用不作为服务运行），请在 Web 主机上调用 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*>。

  如果条件为 false（应用作为服务运行）：

  * 调用 <xref:System.IO.Directory.SetCurrentDirectory*> 并使用应用的发布位置路径。 不要调用 <xref:System.IO.Directory.GetCurrentDirectory*> 来获取路径，因为在调用 <xref:System.IO.Directory.GetCurrentDirectory*> 时，Windows 服务应用将返回 C:\\WINDOWS\\system32 文件夹。 有关详细信息，请参阅[当前目录和内容根](#current-directory-and-content-root)部分。
  * 调用 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> 以将应用作为服务运行。

  由于[命令行配置提供程序](xref:fundamentals/configuration/index#command-line-configuration-provider)需要命令行参数的名称/值对，因此将先从参数中删除 `--console` 开关，然后 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 会接收这些参数。

* 若要写入 Windows 事件日志，请将事件日志提供程序添加到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>。 使用 appsettings.Production.json文件中的 `Logging:LogLevel:Default` 键设置日志记录级别。 出于演示和测试目的，示例应用的生产设置文件会将日志记录级别设置为 `Information`。 在生产中，通常会将值设置为 `Error`。 有关详细信息，请参阅 <xref:fundamentals/logging/index#windows-eventlog-provider>。

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

### <a name="publish-the-app"></a>发布应用

使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish)、[Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles) 或 Visual Studio Code 发布应用。 使用 Visual Studio 时，先选择“FolderProfile”并配置“目标位置”，再选择“发布”按钮。

若要使用命令行接口 (CLI) 工具发布示例应用，请在项目文件夹的命令提示符处运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令，并将发布配置传递到 [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) 选项。 使用带有路径的 [-o|--output](/dotnet/core/tools/dotnet-publish#options) 选项发布到应用之外的文件夹。

#### <a name="publish-a-framework-dependent-deployment-fdd"></a>发布依赖框架的部署 (FDD)

在以下示例中，将应用发布到 *c:\\svc* 文件夹：

```console
dotnet publish --configuration Release --output c:\svc
```

#### <a name="publish-a-self-contained-deployment-scd"></a>发布独立部署 (SCD)

必须在项目文件的 `<RuntimeIdenfifier>`（或 `<RuntimeIdentifiers>`）属性中指定 RID。 将运行时提供到 `dotnet publish` 命令的 [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) 选项。

在以下示例中，为 `win7-x64` 运行时发布应用并发布到 c:\\svc 文件夹：

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

### <a name="create-a-user-account"></a>创建用户帐户

在管理命令 shell 中使用 `net user` 命令为服务创建用户帐户：

```console
net user {USER ACCOUNT} {PASSWORD} /add
```

默认密码有效期为 6 个星期。

对于示例应用，使用用户名 `ServiceUser` 和密码创建用户帐户。 在下面的命令中，将 `{PASSWORD}` 替换为[强密码](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)。

```console
net user ServiceUser {PASSWORD} /add
```

如果需要将用户添加到组中，请运行 `net localgroup` 命令（其中 `{GROUP}` 是组名称）：

```console
net localgroup {GROUP} {USER ACCOUNT} /add
```

有关详细信息，请参阅[服务用户帐户](/windows/desktop/services/service-user-accounts)。

使用 Active Directory 时管理用户的另一种方法是使用托管服务帐户。 有关详细信息，请参阅[组托管服务帐户概述](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)。

### <a name="set-permissions"></a>设置权限

#### <a name="access-to-the-app-folder"></a>应用文件夹的访问权限

在管理命令 shell 中使用 [icacls](/windows-server/administration/windows-commands/icacls) 命令，授予对应用文件夹的写入/读取/执行权限：

```console
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* `{PATH}` &ndash; 应用文件夹路径。
* `{USER ACCOUNT}` &ndash; 用户帐户 (SID)。
* `(OI)` &ndash; 对象继承标志将权限传播给从属文件。
* `(CI)` &ndash; 容器继承标志将权限传播给从属文件夹。
* `{PERMISSION FLAGS}` &ndash; 设置应用的访问权限。
  * 写入 (`W`)
  * 读取 (`R`)
  * 执行 (`X`)
  * 完全 (`F`)
  * 修改 (`M`)
* `/t` &ndash; 以递归方式应用于现有从属文件夹和文件。

对于发布到 c:\\sv 文件夹的示例应用，以及拥有写入/读取/执行权限的 `ServiceUser` 帐户，请运行以下命令：

```console
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

有关详细信息，请参阅 [icacls](/windows-server/administration/windows-commands/icacls)。

#### <a name="log-on-as-a-service"></a>作为服务登录

要向用户帐户授予[作为服务登录](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service)权限，请执行以下操作：

1. 在“本地安全策略”控制台或“本地组策略编辑器”控制台中找到“用户权限分配”策略。 有关说明，请参阅：[配置安全策略设置](/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)。
1. 找到“`Log on as a service`”策略。 双击策略以将其打开。
1. 选择“添加用户或组”。
1. 选择“高级”，然后选择“立即查找”。
1. 选择之前在[创建用户帐户](#create-a-user-account)部分中创建的用户帐户。 选择“确定”以接受所选内容。
1. 确定对象名称正确无误后，选择“确定”。
1. 选择“应用”。 选择“确定”关闭策略窗口。

## <a name="manage-the-service"></a>管理服务

### <a name="create-the-service"></a>创建服务

使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具从管理命令 shell 创建服务。 `binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。 每个参数和值的等于号和引号字符之间必须有空格。

```console
sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
```

* `{SERVICE NAME}` &ndash; 要在[服务控制管理器](/windows/desktop/services/service-control-manager)中分配给服务的名称。
* `{PATH}` &ndash; 可执行服务的路径。
* `{DOMAIN}` &ndash; 已加入域的计算机的域。 如果计算机未加入域，则使用本地计算机名称。
* `{USER ACCOUNT}` &ndash; 运行服务所使用的用户帐户。
* `{PASSWORD}` &ndash; 用户帐户密码。

> [!WARNING]
> 请勿省略 `obj` 参数。 `obj` 的默认值为 [LocalSystem 帐户](/windows/desktop/services/localsystem-account)。 使用 `LocalSystem` 帐户运行服务会带来重大安全风险。 请始终使用拥有有限权限的用户帐户运行服务。

在下面的示例应用示例中：

* 服务名为 MyService。
* 已发布的服务驻留在 c:\\svc 文件夹中。 应用可执行文件名为 SampleApp.exe。 用双引号 (") 将 `binPath` 值引起来。
* 服务是使用 `ServiceUser` 帐户运行。 将 `{DOMAIN}` 替换为用户帐户的域或本地计算机名称。 用双引号 (") 将 `obj` 值引起来。 示例:如果托管系统是名为 `MairaPC` 的本地计算机，请将 `obj` 设置为 `"MairaPC\ServiceUser"`。
* 将 `{PASSWORD}` 替换为用户帐户密码。 用双引号 (") 将 `password` 值引起来。

```console
sc create MyService binPath= "c:\svc\sampleapp.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
```

> [!IMPORTANT]
> 请确保参数的等于号和参数值之间有空格。

### <a name="start-the-service"></a>启动服务

使用 `sc start {SERVICE NAME}` 命令启动服务。

要启动示例应用服务，请使用以下命令：

```console
sc start MyService
```

此命令需要几秒钟才能启动服务。

### <a name="determine-the-service-status"></a>确定服务状态

要检查服务的状态，请使用 `sc query {SERVICE NAME}` 命令。 状态报告为以下值之一：

* `START_PENDING`
* `RUNNING`
* `STOP_PENDING`
* `STOPPED`

使用以下命令检查示例应用服务的状态：

```console
sc query MyService
```

### <a name="browse-a-web-app-service"></a>浏览 Web 应用服务

当服务处于 `RUNNING` 状态并且服务是 Web 应用时，在应用所在路径中浏览应用（默认路径为 `http://localhost:5000`；在使用 [HTTPS 重定向中间件](xref:security/enforcing-ssl)时，它将重定向到 `https://localhost:5001`）。

对于示例应用服务，请在 `http://localhost:5000` 浏览应用。

### <a name="stop-the-service"></a>停止服务

使用 `sc stop {SERVICE NAME}` 命令停止服务。

以下命令可停止示例应用服务：

```console
sc stop MyService
```

### <a name="delete-the-service"></a>删除服务

停止服务并经过短暂延迟后，使用 `sc delete {SERVICE NAME}` 命令卸载服务。

检查示例应用服务的状态：

```console
sc query MyService
```

当示例应用服务处于 `STOPPED` 状态时，使用以下命令卸载示例应用服务：

```console
sc delete MyService
```

## <a name="handle-starting-and-stopping-events"></a>处理启动和停止事件

若要处理 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>、<xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*> 和 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> 事件，请执行以下其他更改：

1. 使用 `OnStarting`、`OnStarted` 和 `OnStopping` 方法创建从 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService> 派生的类：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. 创建可将 `CustomWebHostService` 传递给 <xref:System.ServiceProcess.ServiceBase.Run*> 的 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 的扩展方法：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. 在 `Program.Main` 中，调用 `RunAsCustomService` 扩展方法，而不是 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>：

   ```csharp
   host.RunAsCustomService();
   ```

   若要在 `Program.Main` 中查看 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> 的位置，请参阅[将项目转换为 Windows 服务](#convert-a-project-into-a-windows-service)部分中所示的代码示例。

## <a name="proxy-server-and-load-balancer-scenarios"></a>代理服务器和负载均衡器方案

与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。 有关详细信息，请参阅 <xref:host-and-deploy/proxy-load-balancer>。

## <a name="configure-https"></a>配置 HTTPS

若要为服务配置安全终结点，请执行以下操作：

1. 使用平台的证书获取和部署机制，为托管系统创建 X.509 证书。

1. 将 [Kestrel 服务器 HTTPS 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)指定为使用此证书。

不支持使用 ASP.NET Core HTTPS 开发证书保护服务终结点。

## <a name="current-directory-and-content-root"></a>当前目录和内容根

通过为 Windows 服务调用 <xref:System.IO.Directory.GetCurrentDirectory*> 返回的当前工作目录是 C:\\WINDOWS\\system32 文件夹。 system32 文件夹不是存储服务文件（如设置文件）的合适位置。 使用以下方法之一来维护和访问服务的资产和设置文件。

### <a name="set-the-content-root-path-to-the-apps-folder"></a>设置应用文件夹的内容根路径

<xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*> 是创建服务时提供给 `binPath` 参数的同一路径。 请调用包含应用内容根的路径的 <xref:System.IO.Directory.SetCurrentDirectory*>，而不是调用 `GetCurrentDirectory` 来创建设置文件的路径。

在 `Program.Main` 中，确定服务可执行文件的文件夹路径，并使用该路径来建立应用的内容根：

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a>将服务的文件存储在磁盘中的合适位置

使用 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> 时，使用 <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> 指定到包含文件的文件夹的绝对路径。

## <a name="additional-resources"></a>其他资源

* [Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>

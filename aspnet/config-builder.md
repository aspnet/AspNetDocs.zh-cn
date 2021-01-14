---
uid: config-builder
title: ASP.NET 的配置生成器
author: rick-anderson
description: 了解如何从外部源中 web.config 值以外的源获取配置数据。
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 04bc6bcc2d9d0be561f8b1f2d909d8c46d90ad81
ms.sourcegitcommit: 1dd64aab844e52ed27819c4ae62167081a067134
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98206109"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET 的配置生成器

作者： [Stephen Molloy](https://github.com/StephenMolloy) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

配置生成器为 ASP.NET 应用提供了新式和敏捷机制，可从外部源获取配置值。

配置生成器：

* 在 .NET Framework 4.7.1 和更高版本中可用。
* 提供用于读取配置值的灵活机制。
* 满足一些应用在容器和以云为中心的环境中的基本需求。
* 可用于通过从以前不可用的源进行绘制来改善配置数据的保护 (例如，.NET 配置系统中) Azure Key Vault 和环境变量。

## <a name="keyvalue-configuration-builders"></a>键/值配置生成器

配置生成器可以处理的常见方案是为遵循键/值模式的配置节提供基本键/值替换机制。 状态的 .NET Framework 概念并不限于特定的配置节或模式。 不过， (github 中的许多配置 `Microsoft.Configuration.ConfigurationBuilders` 生成器[](https://github.com/aspnet/MicrosoftConfigurationBuilders)， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) 在键/值模式内工作。

## <a name="keyvalue-configuration-builders-settings"></a>键/值配置生成器设置

以下设置适用于中的所有键/值配置生成器 `Microsoft.Configuration.ConfigurationBuilders` 。

### <a name="mode"></a>模式

配置生成器使用键/值信息的外部源来填充配置系统的选定键/值元素。 具体而言， `<appSettings/>` 和 `<connectionStrings/>` 部分从配置生成器获得特殊处理。 生成器在三种模式下工作：

* `Strict` -默认模式。 在此模式下，配置生成器仅适用于众所周知的键/值中心的配置节。 `Strict` 模式枚举部分中的每个密钥。 如果在外部源中找到匹配的密钥：

   * 配置生成器会将生成的配置节中的值替换为来自外部源的值。
* `Greedy` -此模式与模式密切相关 `Strict` 。 而不是限于原始配置中已经存在的键：

  * 配置生成器会将外部源中的所有键/值对添加到生成的配置节。

* `Expand` -在原始 XML 上进行操作，然后将其解析为配置节对象。 可以将它视为一个字符串中的标记扩展。 与模式匹配的原始 XML 字符串的任何部分 `${token}` 都是标记扩展的候选项。 如果在外部源中找不到相应的值，则不会更改该令牌。 此模式中的生成器并不局限于 `<appSettings/>` 和 `<connectionStrings/>` 部分。

*web.config* 中的以下标记启用了 [](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) `Strict` 模式下的 EnvironmentConfigBuilder：

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

下面的代码读取 `<appSettings/>` 和 `<connectionStrings/>` 前面 *web.config* 文件中显示的：

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

前面的代码将属性值设置为：

* 如果未在环境变量中设置关键字，则为 *web.config* 文件中的值。
* 环境变量的值（如果已设置）。

例如， `ServiceID` 将包含：

* 如果未设置环境变量，则为 "ServiceID web.config 的值" `ServiceID` 。
* 环境变量的值 `ServiceID` （如果已设置）。

下图显示了 `<appSettings/>` 环境编辑器中前面 *web.config* 文件集中的键/值：

![环境编辑器](config-builder/static/env.png)

注意：可能需要退出并重新启动 Visual Studio 才能查看环境变量中的更改。

### <a name="prefix-handling"></a>前缀处理

密钥前缀可简化设置密钥的原因，原因如下：

* .NET Framework 配置是复杂的，并且是嵌套的。
* 外部键/值源通常是基本的并且本质上是平面的。 例如，环境变量不嵌套。

使用以下任一方法， `<appSettings/>` `<connectionStrings/>` 通过环境变量将和注入到配置中：

* `EnvironmentConfigBuilder`在默认 `Strict` 模式下，在配置文件中具有相应的键名称。 前面的代码和标记采用这种方法。 使用此方法时，和中的密钥 **不** 能相同 `<appSettings/>` `<connectionStrings/>` 。
* 将两个 `EnvironmentConfigBuilder` in `Greedy` 模式与不同的前缀和结合使用 `stripPrefix` 。 利用此方法，应用程序可以读取 `<appSettings/>` 且 `<connectionStrings/>` 无需更新配置文件。 下一部分  [stripPrefix](#stripprefix)介绍了如何执行此操作。
* 将两个 `EnvironmentConfigBuilder` in `Greedy` 模式与不同的前缀一起使用。 使用此方法时，不能具有重复的键名，因为键名称必须以前缀来区分。  例如：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

使用上述标记，可以使用相同的平面键/值源来填充两个不同部分的配置。

下图显示了 `<appSettings/>` `<connectionStrings/>` 环境编辑器中前面 *web.config* 文件集中的和键/值：

![环境编辑器](config-builder/static/prefix.png)

下面的代码读取 `<appSettings/>` `<connectionStrings/>` 前面 *web.config* 文件中包含的和键/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

前面的代码将属性值设置为：

* 如果未在环境变量中设置关键字，则为 *web.config* 文件中的值。
* 环境变量的值（如果已设置）。

例如，使用上一个 *web.config* 文件，前面的环境编辑器图像中的键/值和前面的代码将设置以下值：

|  密钥              | “值” |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | 从 env 变量 AppSetting_ServiceID|
|    AppSetting_default            | 从 env AppSetting_default 值 |
|       ConnStr_default         | 从 env ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`：布尔值，默认为 `false` 。 

上述 XML 标记将应用程序设置与连接字符串分离，但要求 *web.config* 文件中的所有键都使用指定的前缀。 例如， `AppSetting` 必须将前缀添加到 `ServiceID` 密钥 ( "AppSetting_ServiceID" ) 。 对于 `stripPrefix` ，不在 *web.config* 文件中使用前缀。 此前缀在配置生成器源中是必需的 (例如，在环境中。 ) 我们预计大多数开发人员将使用 `stripPrefix` 。

应用程序通常会去除前缀。 以下 *web.config* 将前缀：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

在上述 *web.config* 文件中， `default` 该键同时位于 `<appSettings/>` 和中 `<connectionStrings/>` 。

下图显示了 `<appSettings/>` `<connectionStrings/>` 环境编辑器中前面 *web.config* 文件集中的和键/值：

![环境编辑器](config-builder/static/prefix.png)

下面的代码读取 `<appSettings/>` `<connectionStrings/>` 前面 *web.config* 文件中包含的和键/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

前面的代码将属性值设置为：

* 如果未在环境变量中设置关键字，则为 *web.config* 文件中的值。
* 环境变量的值（如果已设置）。

例如，使用上一个 *web.config* 文件，前面的环境编辑器图像中的键/值和前面的代码将设置以下值：

|  密钥              | “值” |
| ----------------- | ------------ |
|     ServiceID           | 从 env 变量 AppSetting_ServiceID|
|    default            | 从 env AppSetting_default 值 |
|    default         | 从 env ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`： String，默认值为 `@"\$\{(\w+)\}"`

`Expand`生成器的行为会搜索原始 XML 中类似于的标记 `${token}` 。 搜索是通过默认正则表达式来完成的 `@"\$\{(\w+)\}"` 。 匹配的字符集 `\w` 比 XML 和多个配置源允许的严格。 `tokenPattern`当 `@"\$\{(\w+)\}"` 令牌名称中超过所需的字符时，请使用。

`tokenPattern`类似

* 允许开发人员更改用于标记匹配的正则表达式。
* 未进行任何验证，以确保它是格式正确且不具有危险性的正则表达式。
* 它必须包含一个捕获组。 整个正则表达式必须匹配整个标记。 第一个捕获必须是要在配置源中查找的标记名称。

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft.Configuration.ConfigurationBuilders 中的配置生成器

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：

* 是最简单的配置生成器。
* 从环境中读取值。
* 没有任何附加的配置选项。
* `name`属性值为任意值。

**注意：** 在 Windows 容器环境中，在运行时设置的变量仅注入到入口点进程环境中。 作为服务运行或非入口进程运行的应用不会选取这些变量，除非以其他方式通过容器中的机制注入它们。 对于基于 [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)的容器， [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)的当前版本仅在 *DefaultAppPool* 中处理此项。 其他基于 Windows 的容器变体可能需要为非入口进程开发自己的注入机制。

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 切勿在源代码中存储密码、敏感连接字符串或其他敏感数据。 生产机密不应用于开发或测试。

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

此配置生成器提供类似于 [ASP.NET Core 机密管理器](/aspnet/core/security/app-secrets)的功能。

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用于 .NET Framework 项目，但必须指定密码文件。 或者，可以在 `UserSecretsId` 项目文件中定义属性，并在正确的位置创建原始机密文件以进行读取。 若要使外部依赖项不在项目中，则机密文件的格式为 XML。 XML 格式是实现详细信息，不应依赖于该格式。 如果需要与 .NET Core 项目共享 *secrets.js* 文件，请考虑使用 [SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。 `SimpleJsonConfigBuilder`还应将 .Net Core 的格式视为要更改的实现详细信息。

的配置属性 `UserSecretsConfigBuilder` ：

* `userSecretsId` -这是用于标识 XML 机密文件的首选方法。 它的工作方式类似于 .NET Core，后者使用 `UserSecretsId` 项目属性存储此标识符。 该字符串必须是唯一的，不需要是 GUID。 使用此属性时，会 `UserSecretsConfigBuilder` 在已知的本地位置中查找 `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` 属于此标识符的机密文件 () 。
* `userSecretsFile` -一个可选属性，指定包含机密的文件。 `~`可在开头使用字符引用应用程序根目录。 此属性或 `userSecretsId` 属性是必需的。 如果同时指定两者，则 `userSecretsFile` 优先。
* `optional`：布尔值、默认值 `true` -在找不到机密文件时防止出现异常。 
* `name`属性值为任意值。

机密文件采用以下格式：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)读取存储在[Azure Key Vault](/azure/key-vault/key-vault-whatis)中的值。

`vaultName` 需要 (保管库的名称或保管库的 URI) 。 其他属性允许控制要连接到哪个保管库，但仅当应用程序未在使用的环境中运行时才需要 `Microsoft.Azure.Services.AppAuthentication` 。 如果可能，将使用 Azure 服务身份验证库自动从执行环境中获取连接信息。 可以通过提供连接字符串来替代自动选取连接信息。

* `vaultName` -如果未提供，则为必需 `uri` 。 指定 Azure 订阅中要从中读取键/值对的保管库的名称。
* `uri` -连接到其他具有指定值的 Key Vault 提供程序 `uri` 。 如果未指定，Azure (`vaultName`) 是保管库提供程序。
* `version` -Azure Key Vault 为机密提供版本控制功能。 如果 `version` 指定了，则生成器仅检索与此版本匹配的机密。
* `preloadSecretNames` -默认情况下，此生成器在初始化时 querys 密钥保管库中的 **所有** 密钥名称。 若要防止读取所有键值，请将此属性设置为 `false` 。 将此设置为 `false` 每次读取一个密钥。 如果保管库允许 "获取" 访问权限，但不允许 "列表" 访问，则一次读取一个机密会很有用。 **注意：** 使用 `Greedy` 模式时， `preloadSecretNames` 必须 `true` (默认值。 ) 

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 是一个基本的配置生成器，它使用目录的文件作为值的源。 文件的名称为键，内容为值。 在协调的容器环境中运行时，此配置生成器会很有用。 Docker Swarm 和 Kubernetes 之类的系统按 `secrets` 每个文件的方式为其协调的 windows 容器提供。

属性详细信息：

* `directoryPath` - 必需。 指定要在其中查找值的路径。 默认情况下，用于 Windows 的 Docker 密钥存储在 *C:\ProgramData\Docker\secrets* 目录中。
* `ignorePrefix` -排除以此前缀开头的文件。 默认值为“忽略”。
* `keyDelimiter` -默认值为 `null` 。 如果已指定，则配置生成器将遍历目录的多个级别，并生成具有此分隔符的密钥名称。 如果此值为 `null` ，则配置生成器仅查看目录的顶层。
* `optional` -默认值为 `false` 。 如果源目录不存在，则指定配置生成器是否应导致错误。

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 切勿在源代码中存储密码、敏感连接字符串或其他敏感数据。 生产机密不应用于开发或测试。

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core 项目经常使用 JSON 文件进行配置。 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)生成器允许在 .NET Framework 中使用 .NET Core JSON 文件。 此配置生成器提供了从平面键/值源到 .NET Framework 配置的特定键/值区域的基本映射。 此配置生成器不 **提供分层** 配置。 JSON 支持文件类似于字典，而不是复杂的层次结构对象。 可以使用多级别的分层文件。 此提供程序 `flatten` 通过使用作为分隔符追加每个级别上的属性名称来深度 `:` 。

属性详细信息：

* `jsonFile` - 必需。 指定要从中进行读取的 JSON 文件。 `~`可在开头使用字符引用应用根。
* `optional` -布尔值，默认值为 `true` 。 如果找不到 JSON 文件，则防止引发异常。
* `jsonMode` - `[Flat|Sectional]`. `Flat` 为默认值。 如果 `jsonMode` 为 `Flat` ，则 JSON 文件是单个平面键/值源。 `EnvironmentConfigBuilder`和 `AzureKeyVaultConfigBuilder` 也是一个平面键/值源。 如果 `SimpleJsonConfigBuilder` 是在 `Sectional` 模式下配置的：

  * JSON 文件在概念上只分成了多个字典。
  * 每个字典仅适用于与附加到它们的顶级属性名称匹配的配置节。 例如：

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>配置生成器顺序

请参阅[aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub 存储库中[的状态执行顺序](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution)。

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>实现自定义键/值配置生成器

如果配置生成器不能满足您的需要，则可以编写一个自定义的。 `KeyValueConfigBuilder`基类处理替换模式和大多数前缀问题。 实现项目只需要：

* 从基类继承，并通过和实现键/值对的基本源 `GetValue` `GetAllValues` ：
* 将 [Microsoft.Configuration.ConfigurationBuilders](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 添加到项目。

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`基类跨键/值配置生成器提供了许多工作和一致的行为。

## <a name="additional-resources"></a>其他资源

* [配置生成器 GitHub 存储库](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [使用 .NET Azure Key Vault 的服务到服务身份验证](/azure/key-vault/service-to-service-authentication#connection-string-support)

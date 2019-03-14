---
title: 解决 ASP.NET Core 项目
author: Rick-Anderson
description: 理解 ASP.NET Core 项目的警告和错误，并对其进行故障排除。
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: test/troubleshoot
ms.openlocfilehash: c8b34f51fd329eb9a7c34f7be93bd7f2aa054283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026774"
---
# <a name="troubleshoot-aspnet-core-projects"></a>解决 ASP.NET Core 项目

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

以下链接提供的故障排除指南：

* <xref:host-and-deploy/azure-apps/troubleshoot>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-iis-errors-reference>
* [NDC 会议 （伦敦，2018年）：诊断 ASP.NET Core 应用程序中的问题](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [ASP.NET 博客：ASP.NET Core 性能问题故障排除](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a>.NET Core SDK 警告

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a>安装的 32 位和 64 位版本的.NET Core SDK

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> 安装了.NET Core SDK 32 和 64 位版本。 仅从安装在 64 位版本的模板 c:\\Program Files\\dotnet\\sdk\\将显示。

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/both32and64bit.png)

时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET Core SDK](https://www.microsoft.com/net/download/all)安装。 可能安装这两个版本的常见原因包括：

* 你最初下载.NET Core SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。
* 由另一个应用程序安装了 32 位.NET Core SDK。
* 下载并安装了错误的版本。

卸载 32 位.NET Core SDK，以防止出现此警告。 从卸载**Control Panel** > **程序和功能** > **卸载或更改程序**。 如果您了解为何会出现的警告和其影响，则可以忽略该警告。

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a>.NET Core SDK 的安装在多个位置

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> .NET Core SDK 安装在多个位置中。 仅安装在上 SDK 的模板 c:\\Program Files\\dotnet\\sdk\\将显示。

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/multiplelocations.png)

外部的一个目录中有至少一个安装的.NET Core SDK 时，将显示此消息*c:\\Program Files\\dotnet\\sdk\\*。 这通常发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET Core SDK 时。

卸载 32 位.NET Core SDK，以防止出现此警告。 从卸载**Control Panel** > **程序和功能** > **卸载或更改程序**。 如果您了解为何会出现的警告和其影响，则可以忽略该警告。

### <a name="no-net-core-sdks-were-detected"></a>检测到没有.NET Core Sdk

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> 检测到没有.NET Core Sdk，请确保将它们包括在环境变量 PATH。

![显示的警告消息的 OneASP.NET 对话框屏幕截图](troubleshoot/_static/NoNetCore.png)

何时会出现此警告的环境变量`PATH`没有指向计算机上任何.NET Core Sdk (例如，`C:\Program Files\dotnet\`和`C:\Program Files (x86)\dotnet\`)。 若要解决此问题：

* 安装或验证.NET Core SDK 的安装。 获取从最新的安装程序[.NET 下载](https://dotnet.microsoft.com/download)。 
* 验证`PATH`环境变量指向 SDK 安装的位置。 安装程序通常设置`PATH`。

## <a name="obtain-data-from-an-app"></a>从应用中获取数据

如果应用程序能够对请求作出响应，你可以从应用使用中间件获取以下数据：

* 请求&ndash;方法、 方案、 主机、 pathbase、 路径、 查询字符串，标头
* 连接&ndash;远程 IP 地址、 远程端口、 本地 IP 地址、 本地端口、 客户端证书
* 标识&ndash;名称、 显示名称
* 配置设置
* 环境变量

将以下项放[中间件](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder)代码的开头`Startup.Configure`方法的请求处理管道。 中间件运行以确保仅在开发环境中执行的代码之前，将检查该环境。

若要获取该环境，请使用以下方法之一：

* 注入`IHostingEnvironment`到`Startup.Configure`方法，并检查本地变量的环境。 下面的示例代码演示了这种方法。

* 将在环境中的属性分配`Startup`类。 检查在环境中使用属性 (例如， `if (Environment.IsDevelopment())`)。

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, 
    IConfiguration config)
{
    if (env.IsDevelopment())
    {
        app.Run(async (context) =>
        {
            var sb = new StringBuilder();
            var nl = System.Environment.NewLine;
            var rule = string.Concat(nl, new string('-', 40), nl);
            var authSchemeProvider = app.ApplicationServices
                .GetRequiredService<IAuthenticationSchemeProvider>();

            sb.Append($"Request{rule}");
            sb.Append($"{DateTimeOffset.Now}{nl}");
            sb.Append($"{context.Request.Method} {context.Request.Path}{nl}");
            sb.Append($"Scheme: {context.Request.Scheme}{nl}");
            sb.Append($"Host: {context.Request.Headers["Host"]}{nl}");
            sb.Append($"PathBase: {context.Request.PathBase.Value}{nl}");
            sb.Append($"Path: {context.Request.Path.Value}{nl}");
            sb.Append($"Query: {context.Request.QueryString.Value}{nl}{nl}");

            sb.Append($"Connection{rule}");
            sb.Append($"RemoteIp: {context.Connection.RemoteIpAddress}{nl}");
            sb.Append($"RemotePort: {context.Connection.RemotePort}{nl}");
            sb.Append($"LocalIp: {context.Connection.LocalIpAddress}{nl}");
            sb.Append($"LocalPort: {context.Connection.LocalPort}{nl}");
            sb.Append($"ClientCert: {context.Connection.ClientCertificate}{nl}{nl}");

            sb.Append($"Identity{rule}");
            sb.Append($"User: {context.User.Identity.Name}{nl}");
            var scheme = await authSchemeProvider
                .GetSchemeAsync(IISDefaults.AuthenticationScheme);
            sb.Append($"DisplayName: {scheme?.DisplayName}{nl}{nl}");

            sb.Append($"Headers{rule}");
            foreach (var header in context.Request.Headers)
            {
                sb.Append($"{header.Key}: {header.Value}{nl}");
            }
            sb.Append(nl);

            sb.Append($"Websockets{rule}");
            if (context.Features.Get<IHttpUpgradeFeature>() != null)
            {
                sb.Append($"Status: Enabled{nl}{nl}");
            }
            else
            {
                sb.Append($"Status: Disabled{nl}{nl}");
            }

            sb.Append($"Configuration{rule}");
            foreach (var pair in config.AsEnumerable())
            {
                sb.Append($"{pair.Path}: {pair.Value}{nl}");
            }
            sb.Append(nl);

            sb.Append($"Environment Variables{rule}");
            var vars = System.Environment.GetEnvironmentVariables();
            foreach (var key in vars.Keys.Cast<string>().OrderBy(key => key, 
                StringComparer.OrdinalIgnoreCase))
            {
                var value = vars[key];
                sb.Append($"{key}: {value}{nl}");
            }

            context.Response.ContentType = "text/plain";
            await context.Response.WriteAsync(sb.ToString());
        });
    }
}
```

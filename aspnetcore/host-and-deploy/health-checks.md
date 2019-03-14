---
title: ASP.NET Core 中的运行状况检查
author: guardrex
description: 了解如何为 ASP.NET Core 基础结构（如应用和数据库）设置运行状况检查。
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/health-checks
ms.openlocfilehash: e186a3cb484035199a8f355540c3e985db87ad98
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039294"
---
# <a name="health-checks-in-aspnet-core"></a>ASP.NET Core 中的运行状况检查

通过 [Luke Latham](https://github.com/guardrex) 和 [Glenn Condron](https://github.com/glennc)

ASP.NET Core 提供运行状况检查中间件和库，以用于报告应用基础结构组件的运行状况。

运行状况检查由应用程序作为 HTTP 终结点公开。 可以为各种实时监视方案配置运行状况检查终结点：

* 运行状况探测可以由容器业务流程协调程和负载均衡器用于检查应用的状态。 例如，容器业务流程协调程序可以通过停止滚动部署或重新启动容器来响应失败的运行状况检查。 负载均衡器可以通过将流量从失败的实例路由到正常实例，来应对不正常的应用。
* 可以监视内存、磁盘和其他物理服务器资源的使用情况来了解是否处于正常状态。
* 运行状况检查可以测试应用的依赖项（如数据库和外部服务终结点）以确认是否可用和正常工作。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples)（[如何下载](xref:index#how-to-download-a-sample)）

示例应用包含本主题中所述的方案示例。 若要运行给定方案的示例应用，请在命令行界面中从项目文件夹中使用 [dotnet run](/dotnet/core/tools/dotnet-run) 命令。 请参阅示例应用的 README.md 文件和本主题中的方案说明，以了解有关如何使用示例应用的详细信息。

## <a name="prerequisites"></a>系统必备

运行状况检查通常与外部监视服务或容器业务流程协调程序一起用于检查应用的状态。 向应用添加运行状况检查之前，需确定要使用的监视系统。 监视系统决定了要创建的运行状况检查类型以及配置其终结点的方式。

引用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)或将包引用添加到 [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) 包。

示例应用提供了启动代码来演示几个方案的运行状况检查。 [数据库探测](#database-probe)方案使用 [BeatPulse](https://github.com/Xabaril/BeatPulse) 检查数据库连接的运行状况。 [DbContext 探测](#entity-framework-core-dbcontext-probe)方案使用 EF Core `DbContext` 检查数据库。 若要探索数据库方案，示例应用将：

* 创建一个数据库，并在 appsettings.json 文件中提供其连接字符串。
* 其项目文件中具有以下包引用：
  * [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/)
  * [Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore/)

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。

另一个运行状况检查方案演示如何将运行状况检查筛选到某个管理端口。 示例应用要求创建包含管理 URL 和管理端口的 Properties/launchSettings.json 文件。 有关详细信息，请参阅[按端口筛选](#filter-by-port)部分。

## <a name="basic-health-probe"></a>基本运行状况探测

对于许多应用，报告应用在处理请求方面的可用性（运行情况）的基本运行状况探测配置足以发现应用的状态。

基本配置会注册运行状况检查服务，并调用运行状况检查中间件以使用运行状况响应在 URL 终结点处进行响应。 默认情况下，不会注册任何特定运行状况检查来测试任何特定依赖项或子系统。 如果能够在运行状况终结点 URL 处进行响应，则应用被视为正常。 默认响应编写器会以纯文本响应形式将状态 (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>) 写回到客户端，以便指示 [HealthStatus.Healthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus)、[HealthStatus.Degraded](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) 或 [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) 状态。

在 `Startup.ConfigureServices` 中使用 <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> 注册运行状况检查服务。 在 `Startup.Configure` 的请求处理管道中使用 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> 注册运行状况检查中间件。

在示例应用中，在 `/health` 处创建运行状况检查终结点 (BasicStartup.cs)：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/BasicStartup.cs?name=snippet1&highlight=5,10)]

若要使用示例应用运行基本配置方案，请在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario basic
```

### <a name="docker-example"></a>Docker 示例

[Docker](xref:host-and-deploy/docker/index) 提供内置 `HEALTHCHECK` 指令，该指令可以用于检查使用基本运行状况检查配置的应用的状态：

```
HEALTHCHECK CMD curl --fail http://localhost:5000/health || exit
```

## <a name="create-health-checks"></a>创建运行状况检查

运行状况检查通过实现 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck> 接口进行创建。 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck.CheckHealthAsync*> 方法会返回 `Task<` <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> `>`，它以 `Healthy`、`Degraded` 或 `Unhealthy` 的形式指示运行状况。 结果会使用可配置状态代码（配置在[运行状况检查选项](#health-check-options)部分中进行介绍）编写为纯文本响应。 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> 还可以返回可选的键值对。

### <a name="example-health-check"></a>示例运行状况检查

下面的 `ExampleHealthCheck` 类演示运行状况检查的布局：

```csharp
public class ExampleHealthCheck : IHealthCheck
{
    public ExampleHealthCheck()
    {
        // Use dependency injection (DI) to supply any required services to the
        // health check.
    }

    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context, 
        CancellationToken cancellationToken = default(CancellationToken))
    {
        // Execute health check logic here. This example sets a dummy
        // variable to true.
        var healthCheckResultHealthy = true;

        if (healthCheckResultHealthy)
        {
            return Task.FromResult(
                HealthCheckResult.Healthy("The check indicates a healthy result."));
        }

        return Task.FromResult(
            HealthCheckResult.Unhealthy("The check indicates an unhealthy result."));
    }
}
```

### <a name="register-health-check-services"></a>注册运行状况检查服务

`ExampleHealthCheck` 类型使用 <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> 添加到运行状况检查服务：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck<ExampleHealthCheck>("example_health_check");
}
```

以下示例中显示的 <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> 重载会设置要在运行状况检查报告失败时报告的失败状态 (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>)。 如果失败状态设置为 `null`（默认值），则会报告 [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus)。 此重载对于库创建者是一种十分有用的方案，在这种情况下，如果运行状况检查实现遵循该设置，则在发生运行状况检查失败时，应用会强制实施库所指示的失败状态。

标记用于筛选运行状况检查（在[筛选运行状况检查](#filter-health-checks)部分中进行了进一步介绍）。

```csharp
services.AddHealthChecks()
    .AddCheck<ExampleHealthCheck>(
        "example_health_check", 
        failureStatus: HealthStatus.Degraded, 
        tags: new[] { "example" });
```

<xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> 还可以执行 lambda 函数。 在以下示例中，运行状况检查名称指定为 `Example`，并且检查始终返回正常状态：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Example", () => 
            HealthCheckResult.Healthy("Example is OK!"), tags: new[] { "example" })
}
```

### <a name="use-health-checks-middleware"></a>使用运行状况检查中间件

在 `Startup.Configure` 内，在处理管道中使用终结点 URL 或相对路径调用 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*>：

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health");
}
```

如果运行状况检查应侦听特定端口，则使用 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> 的重载设置端口（在[按端口筛选](#filter-by-port)部分中进行了进一步介绍）：

```csharp
app.UseHealthChecks("/health", port: 8000);
```

运行状况检查中间件是应用请求处理管道中的*终端中间件*。 遇到的与请求 URL 完全匹配的第一个运行状况检查终结点会进行执行，并且使中间件管道的其余部分短路。 当短路发生时，不会执行匹配运行状况检查后面的任何中间件。

## <a name="health-check-options"></a>运行状况检查选项

<xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions> 使你可以自定义运行状况检查行为：

* [筛选运行状况检查](#filter-health-checks)
* [自定义 HTTP 状态代码](#customize-the-http-status-code)
* [取消缓存标头](#suppress-cache-headers)
* [自定义输出](#customize-output)

### <a name="filter-health-checks"></a>筛选运行状况检查

默认情况下，运行状况检查中间件会运行所有已注册的运行状况检查。 若要运行运行状况检查的子集，请提供向 <xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.Predicate> 选项返回布尔值的函数。 在以下示例中，`Bar` 运行状况检查在函数条件语句 中由于其标记 (`bar_tag`) 而被筛选掉，在条件语句中，仅当运行状况检查的 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckRegistration.Tags> 属性与 `foo_tag` 或 `baz_tag` 匹配时才返回 `true`：

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Foo", () => 
            HealthCheckResult.Healthy("Foo is OK!"), tags: new[] { "foo_tag" })
        .AddCheck("Bar", () => 
            HealthCheckResult.Unhealthy("Bar is unhealthy!"), tags: new[] { "bar_tag" })
        .AddCheck("Baz", () => 
            HealthCheckResult.Healthy("Baz is OK!"), tags: new[] { "baz_tag" });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // Filter out the 'Bar' health check. Only Foo and Baz execute.
        Predicate = (check) => check.Tags.Contains("foo_tag") || 
            check.Tags.Contains("baz_tag")
    });
}
```

### <a name="customize-the-http-status-code"></a>自定义 HTTP 状态代码

使用 <xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.ResultStatusCodes> 可自定义运行状况状态到 HTTP 状态代码的映射。 以下 <xref:Microsoft.AspNetCore.Http.StatusCodes> 分配是中间件所使用的默认值。 更改状态代码值以满足要求。

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The following StatusCodes are the default assignments for
        // the HealthStatus properties.
        ResultStatusCodes =
        {
            [HealthStatus.Healthy] = StatusCodes.Status200OK,
            [HealthStatus.Degraded] = StatusCodes.Status200OK,
            [HealthStatus.Unhealthy] = StatusCodes.Status503ServiceUnavailable
        }
    });
}
```

### <a name="suppress-cache-headers"></a>取消缓存标头

<xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.AllowCachingResponses> 控制运行状况检查中间件是否将 HTTP 标头添加到探测响应以防止响应缓存。 如果值为 `false`（默认值），则中间件会设置或替代 `Cache-Control`、`Expires` 和 `Pragma` 标头以防止响应缓存。 如果值为 `true`，则中间件不会修改响应的缓存标头。

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The default value is false.
        AllowCachingResponses = false
    });
}
```

### <a name="customize-output"></a>自定义输出

<xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.ResponseWriter> 选项可获取或设置用于编写响应的委托。 默认委托会使用 [HealthReport.Status](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthReport.Status) 字符串值编写最小的纯文本响应。

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // WriteResponse is a delegate used to write the response.
        ResponseWriter = WriteResponse
    });
}

private static Task WriteResponse(HttpContext httpContext, 
    HealthReport result)
{
    httpContext.Response.ContentType = "application/json";

    var json = new JObject(
        new JProperty("status", result.Status.ToString()),
        new JProperty("results", new JObject(result.Entries.Select(pair =>
            new JProperty(pair.Key, new JObject(
                new JProperty("status", pair.Value.Status.ToString()),
                new JProperty("description", pair.Value.Description),
                new JProperty("data", new JObject(pair.Value.Data.Select(
                    p => new JProperty(p.Key, p.Value))))))))));
    return httpContext.Response.WriteAsync(
        json.ToString(Formatting.Indented));
}
```

## <a name="database-probe"></a>数据库探测

运行状况检查可以指定数据库查询作为布尔测试来运行，以指示数据库是否在正常响应。

示例应用使用 [BeatPulse](https://github.com/Xabaril/BeatPulse)（适用于 ASP.NET Core 应用的运行状况检查库）对 SQL Server 数据库执行运行状况检查。 BeatPulse 会对数据库执行 `SELECT 1` 查询以确认数据库连接是否处于正常状态。

> [!WARNING]
> 使用查询检查数据库连接时，请选择快速返回的查询。 查询方法会面临使数据库过载和降低其性能的风险。 在大多数情况下，无需运行测试查询。 只需建立成功的数据库连接便足矣。 如果发现需要运行查询，请选择简单的 SELECT 查询，如 `SELECT 1`。

若要使用 BeatPulse 库，请包含对 [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/) 的包引用。

在应用的 appsettings.json 文件中提供有效数据库连接字符串。 应用使用名为 `HealthCheckSample` 的 SQL Server 数据库：

[!code-json[](health-checks/samples/2.x/HealthChecksSample/appsettings.json?highlight=3)]

在 `Startup.ConfigureServices` 中使用 <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> 注册运行状况检查服务。 示例应用使用数据库连接字符串 (DbHealthStartup.cs) 调用 BeatPulse 的 `AddSqlServer` 方法：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_ConfigureServices)]

在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_Configure)]

若要使用示例应用运行数据库探测方案，请在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario db
```

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。

## <a name="entity-framework-core-dbcontext-probe"></a>Entity Framework Core DbContext 探测

`DbContext` 检查确认应用可以与为 EF Core `DbContext` 配置的数据库通信。 满足以下条件的应用支持 `DbContext` 检查：

* 使用 [Entity Framework (EF) Core](/ef/core/)。
* 包括对 [Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore/) 的包引用。

`AddDbContextCheck<TContext>` 为 `DbContext` 注册运行状况检查。 `DbContext` 作为方法的 `TContext` 提供。 重载可用于配置失败状态、标记和自定义测试查询。

默认情况下：

* `DbContextHealthCheck` 调用 EF Core 的 `CanConnectAsync` 方法。 可以自定义在使用 `AddDbContextCheck` 方法重载检查运行状况时运行的操作。
* 运行状况检查的名称是 `TContext` 类型的名称。

在示例应用中，`AppDbContext` 会提供给 `AddDbContextCheck`，并在 `Startup.ConfigureServices` 中注册为服务。

*DbContextHealthStartup.cs*：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_ConfigureServices)]

在示例应用中，`UseHealthChecks` 在 `Startup.Configure` 中添加运行状况检查中间件。

*DbContextHealthStartup.cs*：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_Configure)]

若要使用示例应用运行 `DbContext` 探测方案，请确认连接字符串指定的数据库在 SQL Server 实例中不存在。 如果该数据库存在，请删除它。

在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario dbcontext
```

在应用运行之后，在浏览器中对 `/health` 终结点发出请求，从而检查运行状况。 数据库和 `AppDbContext` 不存在，因此应用提供以下响应：

```
Unhealthy
```

触发示例应用以创建数据库。 向 `/createdatabase` 发出请求。 应用会进行以下响应：

```
Creating the database...
Done!
Navigate to /health to see the health status.
```

向 `/health` 终结点发出请求。 数据库和上下文存在，因此应用会进行以下响应：

```
Healthy
```

触发示例应用以删除数据库。 向 `/deletedatabase` 发出请求。 应用会进行以下响应：

```
Deleting the database...
Done!
Navigate to /health to see the health status.
```

向 `/health` 终结点发出请求。 应用提供不正常的响应：

```
Unhealthy
```

## <a name="separate-readiness-and-liveness-probes"></a>单独的就绪情况和运行情况探测

在某些托管方案中，会使用一对区分两种应用状态的运行状况检查：

* 应用正常运行，但尚未准备好接收请求。 此状态是应用的就绪情况。
* 应用正常运行并响应请求。 此状态是应用的运行情况。

就绪情况检查通常执行更广泛和耗时的检查集，以确定应用的所有子系统和资源是否都可用。 运行情况检查只是执行一个快速检查，以确定应用是否可用于处理请求。 应用通过其就绪情况检查之后，无需使用成本高昂的就绪情况检查集来进一步增加应用负荷 &mdash; 后续检查只需检查运行情况。

示例应用包含运行状况检查，以报告[托管服务](xref:fundamentals/host/hosted-services)中长时间运行的启动任务的完成。 `StartupHostedServiceHealthCheck` 公开了属性 `StartupTaskCompleted`，托管服务在其长时间运行的任务完成时可以将该属性设置为 `true` (StartupHostedServiceHealthCheck.cs)：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/StartupHostedServiceHealthCheck.cs?name=snippet1&highlight=5)]

长时间运行的后台任务由[托管服务](xref:fundamentals/host/hosted-services) (Services/StartupHostedService) 启动。 在该任务结束时，`StartupHostedServiceHealthCheck.StartupTaskCompleted` 设置为 `true`：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/Services/StartupHostedService.cs?name=snippet1&highlight=18-20)]

运行状况检查在 `Startup.ConfigureServices` 中使用 <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> 与托管服务一起注册。 因为托管服务必须对运行状况检查设置该属性，所以运行状况检查也会在服务容器 (LivenessProbeStartup.cs) 中进行注册：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices)]

在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件。 在示例应用中，在 `/health/ready` 处为就绪情况检查，并且在 `/health/live` 处为运行情况检查创建运行状况检查终结点。 就绪情况检查会将运行状况检查筛选到具有 `ready` 标记的运行状况检查。 运行情况检查通过在 [HealthCheckOptions.Predicate](xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.Predicate) 中返回 `false` 来筛选出 `StartupHostedServiceHealthCheck`（有关详细信息，请参阅[筛选运行状况检查](#filter-health-checks)）：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_Configure)]

若要使用示例应用运行就绪情况/运行情况配置方案，请在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario liveness
```

在浏览器中，访问 `/health/ready` 几次，直到过了 15 秒。 运行状况检查会在前 15 秒内报告“运行不正常”。 15 秒之后，终结点会报告“运行正常”，这反映托管服务完成了长时间运行的任务。

此示例还创建了一个运行第一个就绪检查的运行状况检查发布服务器（<xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实现），延迟时间为两秒。 有关详细信息，请参阅[运行状况检查发布服务器](#health-check-publisher)部分。

### <a name="kubernetes-example"></a>Kubernetes 示例

在诸如 [Kubernetes](https://kubernetes.io/) 这类环境中，使用单独的就绪情况和运行情况检查会十分有用。 在 Kubernetes 中，应用可能需要在接受请求之前执行耗时的启动工作，如基础数据库可用性测试。 使用单独检查使业务流程协调程序可以区分应用是否正常运行但尚未准备就绪，或是应用程序是否未能启动。 有关 Kubernetes 中的就绪情况和运行情况探测的详细信息，请参阅 Kubernetes 文档中的[配置运行情况和就绪情况探测](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)。

以下示例演示如何使用 Kubernetes 就绪情况探测配置：

```
spec:
  template:
  spec:
    readinessProbe:
      # an http probe
      httpGet:
        path: /health/ready
        port: 80
      # length of time to wait for a pod to initialize
      # after pod startup, before applying health checking
      initialDelaySeconds: 30
      timeoutSeconds: 1
    ports:
      - containerPort: 80
```

## <a name="metric-based-probe-with-a-custom-response-writer"></a>具有自定义响应编写器的基于指标的探测

示例应用演示具有自定义响应编写器的内存运行状况检查。

如果应用使用的内存多于给定内存阈值（在示例应用中为 1 GB），则 `MemoryHealthCheck` 报告降级状态。 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> 包括应用的垃圾回收器 (GC) 信息 (MemoryHealthCheck.cs)：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/MemoryHealthCheck.cs?name=snippet1)]

在 `Startup.ConfigureServices` 中使用 <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> 注册运行状况检查服务。 `MemoryHealthCheck` 注册为服务，而不是通过将运行状况检查传递到 <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> 来启用它。 所有 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck> 注册服务都可供运行状况检查服务和中间件使用。 建议将运行状况检查服务注册为单一实例服务。

CustomWriterStartup.cs：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_ConfigureServices&highlight=4)]

在 `Startup.Configure` 内，在应用处理管道中调用运行状况检查中间件。 一个 `WriteResponse` 委托提供给 `ResponseWriter` 属性，以在执行运行状况检查时输出自定义 JSON 响应：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_Configure&highlight=6)]

`WriteResponse` 方法将 `CompositeHealthCheckResult` 格式化为 JSON 对象，并生成运行状况检查响应的 JSON 输出：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_WriteResponse)]

若要使用示例应用运行具有自定义响应编写器输出的基于指标的探测，请在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario writer
```

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 包括基于指标的运行状况检查方案（包括磁盘存储和最大值运行情况检查）。
>
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。

## <a name="filter-by-port"></a>按端口筛选

使用端口调用 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> 会将运行状况检查请求限制到指定端口。 这通常用于在容器环境中公开用于监视服务的端口。

示例应用使用[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)配置端口。 端口在 launchSettings.json 文件设置，并通过环境变量传递到配置提供程序。 还必须配置服务器以在管理端口上侦听请求。

若要使用示例应用演示管理端口配置，请在 Properties 文件夹中创建 launchSettings.json 文件。

以下 launchSettings.json 文件未包含在示例应用的项目文件中，必须手动创建。

Properties/launchSettings.json：

```json
{
  "profiles": {
    "SampleApp": {
      "commandName": "Project",
      "commandLineArgs": "",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_URLS": "http://localhost:5000/;http://localhost:5001/",
        "ASPNETCORE_MANAGEMENTPORT": "5001"
      },
      "applicationUrl": "http://localhost:5000/"
    }
  }
}
```

在 `Startup.ConfigureServices` 中使用 <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> 注册运行状况检查服务。 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> 调用指定管理端口 (ManagementPortStartup.cs)：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ManagementPortStartup.cs?name=snippet1&highlight=12,18)]

> [!NOTE]
> 可以通过在代码中显式设置 URL 和管理端口，来避免在示例应用中创建 launchSettings.json 文件。 在创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 的 Program.cs 中，添加 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseUrls*> 调用并提供应用的正常响应终结点和管理端口终结点。 在调用 <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> 的 ManagementPortStartup.cs 中，显式指定管理端口。
>
> Program.cs:
>
> ```csharp
> return new WebHostBuilder()
>     .UseConfiguration(config)
>     .UseUrls("http://localhost:5000/;http://localhost:5001/")
>     .ConfigureLogging(builder =>
>     {
>         builder.SetMinimumLevel(LogLevel.Trace);
>         builder.AddConfiguration(config);
>         builder.AddConsole();
>     })
>     .UseKestrel()
>     .UseStartup(startupType)
>     .Build();
> ```
>
> ManagementPortStartup.cs：
>
> ```csharp
> app.UseHealthChecks("/health", port: 5001);
> ```

若要使用示例应用运行管理端口配置方案，请在命令行界面中从项目文件夹执行以下命令：

```console
dotnet run --scenario port
```

## <a name="distribute-a-health-check-library"></a>分发运行状况检查库

将运行状况检查作为库进行分发：

1. 编写将 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck> 接口作为独立类来实现的运行状况检查。 该类可以依赖于[依赖关系注入 (DI)](xref:fundamentals/dependency-injection)类型激活和[命名选项](xref:fundamentals/configuration/options)来访问配置数据。

   ```csharp
   using System;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   namespace SampleApp
   {
       public class ExampleHealthCheck : IHealthCheck
       {
           private readonly string _data1;
           private readonly int? _data2;

           public ExampleHealthCheck(string data1, int? data2)
           {
               _data1 = data1 ?? throw new ArgumentNullException(nameof(data1));
               _data2 = data2 ?? throw new ArgumentNullException(nameof(data2));
           }

           public async Task<HealthCheckResult> CheckHealthAsync(
               HealthCheckContext context, CancellationToken cancellationToken)
           {
               try
               {
                   // Health check logic
                   //
                   // data1 and data2 are used in the method to
                   // run the probe's health check logic.

                   // Assume that it's possible for this health check
                   // to throw an AccessViolationException.

                   return HealthCheckResult.Healthy();
               }
               catch (AccessViolationException ex)
               {
                   return new HealthCheckResult(
                       context.Registration.FailureStatus,
                       description: "An access violation occurred during the check.",
                       exception: ex,
                       data: null);
               }
           }
       }
   }
   ```

1. 使用参数编写一个扩展方法，所使用的应用会在其 `Startup.Configure` 方法中调用它。 在以下示例中，假设以下运行状况检查方法签名：

   ```csharp
   ExampleHealthCheck(string, string, int )
   ```

   前面的签名指示 `ExampleHealthCheck` 需要其他数据来处理运行状况检查探测逻辑。 当运行状况检查向扩展方法注册时，数据会提供给用于创建运行状况检查实例的委托。 在以下示例中，调用方会指定可选的：

   * 运行状况检查名称 (`name`)。 如果为 `null`，则使用 `example_health_check`。
   * 运行状况检查的字符串数据点 (`data1`)。
   * 运行状况检查的整数数据点 (`data2`)。 如果为 `null`，则使用 `1`。
   * 失败状态 (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>)。 默认值为 `null`。 如果为 `null`，则报告失败状态 [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus)。
   * 标记 (`IEnumerable<string>`)。

   ```csharp
   using System.Collections.Generic;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   public static class ExampleHealthCheckBuilderExtensions
   {
       const string NAME = "example_health_check";

       public static IHealthChecksBuilder AddExampleHealthCheck(
           this IHealthChecksBuilder builder, 
           string name = default, 
           string data1, 
           int data2 = 1, 
           HealthStatus? failureStatus = default, 
           IEnumerable<string> tags = default)
       {
           return builder.Add(new HealthCheckRegistration(
               name ?? NAME,
               sp => new ExampleHealthCheck(data1, data2),
               failureStatus,
               tags));
       }
   }
   ```

## <a name="health-check-publisher"></a>运行状况检查发布服务器

当 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 添加到服务容器时，运行状况检查系统，会定期执行运行状况检查并使用结果调用 `PublishAsync`。 在期望每个进程定期调用监视系统以便确定运行状况的基于推送的运行状况监视系统方案中，这十分有用。

<xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 接口具有单个方法：

```csharp
Task PublishAsync(HealthReport report, CancellationToken cancellationToken);
```

使用 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions> 可设置：

* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Delay> &ndash; 在应用程序启动后且在应用程序执行 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实例之前所应用的初始延迟。 延迟在启动时应用一次，不适用于后续迭代。 默认值为 5 秒。
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Period> &ndash; <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 执行的时间。 默认值为 30 秒。
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Predicate> &ndash; 如果 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Predicate> 为 `null`（默认值），则运行状况检查发布服务器服务运行所有已注册的运行状况检查。 若要运行运行状况检查的子集，请提供用于筛选检查集的函数。 每个时间段都会评估谓词。
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Timeout> &ndash; 执行所有 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实例的运行状况检查的超时时间。 在不超时的情况下，使用 <xref:System.Threading.Timeout.InfiniteTimeSpan> 执行。 默认值为 30 秒。

::: moniker range="= aspnetcore-2.2"

> [!WARNING]
> 在 ASP.NET Core 2.2 版本中，<xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实现不支持设置 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Period>，它设置 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Delay> 的值。 此问题将在 ASP.NET Core 3.0 中得以修复。 有关详细信息，请参阅 [HealthCheckPublisherOptions.Period 设置 .Delay 值](https://github.com/aspnet/Extensions/issues/1041)。

::: moniker-end

在示例应用中，`ReadinessPublisher` 是 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实现。 运行状况检查状态在 `Entries` 中记录并针对每次检查记录：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ReadinessPublisher.cs?name=snippet_ReadinessPublisher&highlight=20,22-23)]

在示例应用的 `LivenessProbeStartup` 示例中，`StartupHostedService` 就绪状态检查有两秒的启动延迟，并且每 30 秒运行一次检查。 为激活 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实现，示例将 `ReadinessPublisher` 注册为[依存关系注入 (DI)](xref:fundamentals/dependency-injection) 容器中的单一实例服务：

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices&highlight=12-17,28)]

::: moniker range="= aspnetcore-2.2"

> [!NOTE]
> 以下解决方法允许在已将一个或多个其他托管服务添加到应用时，向服务容器添加 <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> 实例。 ASP.NET Core 3.0 发布后，不再需要此解决方法。 有关详细信息，请参见： https://github.com/aspnet/Extensions/issues/639。
>
> ```csharp
> private const string HealthCheckServiceAssembly = 
>     "Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherHostedService";
>
> services.TryAddEnumerable(
>     ServiceDescriptor.Singleton(typeof(IHostedService), 
>         typeof(HealthCheckPublisherOptions).Assembly
>             .GetType(HealthCheckServiceAssembly)));
> ```

::: moniker-end

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 包括多个系统的发布服务器（包括 [Application Insights](/azure/application-insights/app-insights-overview)）。
>
> [BeatPulse](https://github.com/Xabaril/BeatPulse) 不由 Microsoft 进行支持或维护。

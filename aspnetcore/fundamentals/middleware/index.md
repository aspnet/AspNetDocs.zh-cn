---
title: ASP.NET Core 中间件
author: rick-anderson
description: 了解 ASP.NET Core 中间件和请求管道。
ms.author: riande
ms.custom: mvc
ms.date: 02/17/2019
uid: fundamentals/middleware/index
---
# <a name="aspnet-core-middleware"></a>ASP.NET Core 中间件

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)和[Steve Smith](https://ardalis.com/)

中间件是一种装配到应用管道以处理请求和响应的软件。 每个组件：

* 选择是否将请求传递到管道中的下一个组件。
* 可在管道中的下一个组件前后执行工作。

请求委托用于构建请求管道， 并处理每个 HTTP 请求。

使用 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 和 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 扩展方法来配置请求委托。 一个单独的请求委托可以指定为一个内联的匿名方法（称为内联中间件），也可以在可重用类中定义它。 这些可重用的类和并行匿名方法即为中间件，也叫中间件组件。 请求管道中的每个中间件组件负责调用管道中的下一个组件，或使管道短路。 当中间件短路时，它被称为“终端中间件”，因为它阻止中间件进一步处理请求。

<xref:migration/http-modules> 介绍了 ASP.NET Core 和 ASP.NET 4.x 中请求管道之间的差异，并提供了更多的中间件示例。

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a>使用 IApplicationBuilder 创建中间件管道

ASP.NET Core 请求管道包含一系列请求委托，依次调用。 下图演示了这一概念。 沿黑色箭头执行。

![请求处理模式显示请求到达、通过三个中间件进行处理以及响应离开应用。 每个中间件运行其逻辑，并在 next() 语句处将请求传递到下一个中间件。 在第三个中间件处理请求之后，请求按相反顺序返回通过前两个中间件，以进行离开应用前并在其 next() 语句后的其他处理，作为对客户端的响应。](index/_static/request-delegate-pipeline.png)

每个委托可以在下一个委托之前和之后执行操作。 应尽早在管道中调用异常处理委托，这样它们就能捕获在管道的后期阶段发生的异常。

最简单的 ASP.NET Core 应用程序可以设置一个处理所有请求的单一请求委托。 这个例子不包括实际的请求管道。 相反，只调用一个匿名函数来响应每个HTTP请求。

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

第一个 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> 委托终止了管道。

用 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 将多个请求委托链接在一起。 `next` 参数表示管道中的下一个委托。 可通过不调用 next 参数使管道短路。 通常可在下一个委托前后执行操作，如以下示例所示：

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

当委托不将请求传递给下一个委托时，它被称为“让请求管道短路”。 短路往往是必要的，因为它避免了不必要的工作。 例如，[静态文件中间件](xref:fundamentals/static-files)可以处理对静态文件的请求，并让管道的其余部分短路，从而起到终端中间件的作用。 如果中间件添加到管道中，且位于终止进一步处理的中间件前，它们仍处理 `next.Invoke` 语句后面的代码。 不过，请参阅下面有关尝试对已发送的响应执行写入操作的警告。

> [!WARNING]
> 在向客户端发送响应后，请勿调用 `next.Invoke`。 响应启动后，针对 <xref:Microsoft.AspNetCore.Http.HttpResponse> 的更改将引发异常。 例如，设置标头和状态代码更改将引发异常。 在调用`next`之后写入响应正文：
>
> * 可能会导致违反协议。 例如，写入的长度超过规定的 `Content-Length`。
> * 可能会损坏正文格式。 例如，向 CSS 文件中写入一个 HTML 页脚。
>
> <xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> 是一个有用的提示，指示是否已发送标头或已写入正文。

## <a name="order"></a>顺序

向 `Startup.Configure` 方法添加中间件组件的顺序定义了针对请求调用这些组件的顺序，以及响应的相反顺序。 此排序对于安全性、性能和功能至关重要。

以下 `Startup.Configure` 方法将为常见应用方案添加中间件组件：

::: moniker range=">= aspnetcore-2.0"

1. 异常/错误处理
1. HTTP 严格传输安全协议
1. HTTPS 重定向
1. 静态文件服务器
1. Cookie 策略实施
1. 身份验证
1. 会话
1. MVC

```csharp
public void Configure(IApplicationBuilder app)
{
    if (env.IsDevelopment())
    {
        // When the app runs in the Development environment:
        //   Use the Developer Exception Page to report app runtime errors.
        //   Use the Database Error Page to report database runtime errors.
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
    }
    else
    {
        // When the app doesn't run in the Development environment:
        //   Enable the Exception Handler Middleware to catch exceptions
        //     thrown in the following middlewares.
        //   Use the HTTP Strict Transport Security Protocol (HSTS)
        //     Middleware.
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // Use HTTPS Redirection Middleware to redirect HTTP requests to HTTPS.
    app.UseHttpsRedirection();

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Use Cookie Policy Middleware to conform to EU General Data 
    // Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // If the app uses session state, call Session Middleware after Cookie 
    // Policy Middleware and before MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. 异常/错误处理
1. 静态文件
1. 身份验证
1. 会话
1. MVC

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable the Exception Handler Middleware to catch exceptions
    //   thrown in the following middlewares.
    app.UseExceptionHandler("/Home/Error");

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Authenticate before you access secure resources.
    app.UseIdentity();

    // If the app uses session state, call UseSession before 
    // MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

在前面的示例代码中，每个中间件扩展方法都通过 <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> 命名空间在 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 上公开。

<xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> 是添加到管道的第一个中间件组件。 因此，异常处理程序中间件可捕获稍后调用中发生的任何异常。

尽早在管道中调用静态文件中间件，以便它可以处理请求并使其短路，而无需通过剩余组件。 静态文件中间件不提供授权检查。 它所服务的任何文件（包括*wwwroot*下的文件）都是可以公开访问的。 若要了解如何保护静态文件，请参阅 <xref:fundamentals/static-files>。

::: moniker range=">= aspnetcore-2.0"

如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的身份验证中间件 (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>)。 身份验证不使未经身份验证的请求短路。 虽然身份验证中间件对请求进行身份验证，但仅在 MVC 选择特定 Razor 页或 MVC 控制器和操作后，才发生授权（和拒绝）。

::: moniker-end

::: moniker range="< aspnetcore-2.0"

如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的标识中间件 (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>)。 标识不使未经身份验证的请求短路。 虽然标识对请求进行身份验证，但仅在 MVC 选择特定控制器和操作后，才发生授权（和拒绝）。

::: moniker-end

以下示例演示中间件排序，其中静态文件的请求在响应压缩中间件前由静态文件中间件进行处理。 使用此中间件顺序不压缩静态文件。 可以压缩来自 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 的 MVC 响应。

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static File Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a>Use、Run 和 Map

使用 `Use`、`Run` 和 `Map` 配置 HTTP 管道。 `Use` 方法可使管道短路（即不调用 `next` 请求委托）。 `Run` 是一种约定，并且某些中间件组件可公开在管道末尾运行的 `Run[Middleware]` 方法。

<xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>扩展用作分支管道约定。 `Map*` 基于给定请求路径的匹配项来创建请求管道分支。 如果请求路径以给定的路径开头，则执行分支。

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。

| 请求             | 响应                     |
| ------------------- | ---------------------------- |
| localhost:1234      | Hello from non-Map delegate. |
| localhost:1234/map1 | Map Test 1                   |
| localhost:1234/map2 | Map Test 2                   |
| localhost:1234/map3 | Hello from non-Map delegate. |

使用`Map`时，将从`HttpRequest.Path`中删除匹配的路径片段，并将其附加到每个请求的`HttpRequest.PathBase`。

[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) 基于给定谓词的结果创建请求管道分支。 任何类型为`Func<HttpContext, bool>`的谓词都可用于将请求映射到管道的新分支。 在以下示例中，谓词用于检测查询字符串变量`branch`是否存在：

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。

| 请求                       | 响应                     |
| ----------------------------- | ---------------------------- |
| localhost:1234                | Hello from non-Map delegate. |
| localhost:1234/?branch=master | Branch used = master         |

`Map` 支持嵌套，例如：

```csharp
app.Map("/level1", level1App => {
    level1App.Map("/level2a", level2AApp => {
        // "/level1/level2a" processing
    });
    level1App.Map("/level2b", level2BApp => {
        // "/level1/level2b" processing
    });
});
   ```

此外，`Map` 还可同时匹配多个段：

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a>内置中间件

ASP.NET Core 附带以下中间件组件。 “顺序”列提供备注，以说明中间件在请求处理管道中的放置，以及中间件可能会终止请求处理的条件。 如果中间件让请求处理管道短路，并阻止下游中间件进一步处理请求，它被称为“终端中间件”。 若要详细了解短路，请参阅[使用 IApplicationBuilder 创建中间件管道](#create-a-middleware-pipeline-with-iapplicationbuilder)部分。

| 中间件 | 描述 | 顺序 |
| ---------- | ----------- | ----- |
| [身份验证](xref:security/authentication/identity) | 提供身份验证支持。 | 在需要 `HttpContext.User` 之前。 OAuth 回叫的终端。 |
| [Cookie 策略](xref:security/gdpr) | 跟踪用户是否同意存储个人信息，并强制实施 cookie 字段（如 `secure` 和 `SameSite`）的最低标准。 | 在发出 cookie 的中间件之前。 示例：身份验证、会话、MVC (TempData)。 |
| [CORS](xref:security/cors) | 配置跨域资源共享。 | 在使用 CORS 的组件之前。 |
| [诊断](xref:fundamentals/error-handling) | 配置诊断。 | 在生成错误的组件之前。 |
| [转接头](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | 将代理标头转发到当前请求。 | 在使用已更新字段的组件之前。 示例：方案、主机、客户端 IP、方法。 |
| [运行状况检查](xref:host-and-deploy/health-checks) | 检查 ASP.NET Core 应用及其依赖项的运行状况，如检查数据库可用性。 | 如果请求与运行状况检查终结点匹配，则为终端。 |
| [HTTP 方法重写](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | 允许传入 POST 请求重写方法。 | 在使用已更新方法的组件之前。 |
| [HTTPS 重定向](xref:security/enforcing-ssl#require-https) | 将所有 HTTP 请求重定向到 HTTPS（ASP.NET Core 2.1 或更高版本）。 | 在使用 URL 的组件之前。 |
| [HTTP 严格传输安全性 (HSTS)](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | 添加特殊响应标头的安全增强中间件（ASP.NET Core 2.1 或更高版本）。 | 在发送响应之前，修改请求的组件之后。 示例：转接头、URL 重写。 |
| [MVC](xref:mvc/overview) | 用 MVC/Razor Pages 处理请求（ASP.NET Core 2.0 或更高版本）。 | 如果请求与路由匹配，则为终端。 |
| [OWIN](xref:fundamentals/owin) | 与基于 OWIN 的应用、服务器和中间件进行互操作。 | 如果 OWIN 中间件处理完请求，则为终端。 |
| [响应缓存](xref:performance/caching/middleware) | 提供对缓存响应的支持。 | 在需要缓存的组件之前。 |
| [响应压缩](xref:performance/response-compression) | 提供对压缩响应的支持。 | 在需要压缩的组件之前。 |
| [请求本地化](xref:fundamentals/localization) | 提供本地化支持。 | 在对本地化敏感的组件之前。 |
| [路由](xref:fundamentals/routing) | 定义和约束请求路由。 | 用于匹配路由的终端。 |
| [会话](xref:fundamentals/app-state) | 提供对管理用户会话的支持。 | 在需要会话的组件之前。 |
| [静态文件](xref:fundamentals/static-files) | 为服务静态文件和目录浏览提供支持。 | 如果请求与文件匹配，则为终端。 |
| [URL 重写](xref:fundamentals/url-rewriting) | 为Url重写和请求重定向提供支持。 | 在使用 URL 的组件之前。 |
| [WebSockets](xref:fundamentals/websockets) | 启用 WebSockets 协议。 | 在接受 WebSocket 请求所需的组件之前。 |

## <a name="additional-resources"></a>其他资源

* <xref:fundamentals/middleware/write>
* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>

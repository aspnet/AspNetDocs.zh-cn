---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: '从 .NET 客户端调用 Web API （c #）-ASP.NET 4。x'
author: MikeWasson
description: 本教程演示如何从 .NET 4.x 应用程序调用 web API。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172934"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>从 .NET 客户端调用 Web API （c #）

作者： [Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)

[下载完成的项目](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。 [下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。 

本教程演示如何使用[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)从 .net 应用程序调用 web API。

在本教程中，编写了一个使用以下 web API 的客户端应用：

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 根据 ID 获取产品 | GET | /api/products/*id* |
| 创建新产品 | POST | /api/products |
| 更新产品 | PUT | /api/products/*id* |
| 删除产品 | DELETE | /api/products/*id* |

若要了解如何使用 ASP.NET Web API 实现此 API，请参阅[创建支持 CRUD 操作的 WEB API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。

为简单起见，本教程中的客户端应用程序是一个 Windows 控制台应用程序。 Windows Phone 和 Windows 应用商店应用程序也支持**HttpClient** 。 有关详细信息，请参阅[使用可移植库为多个平台编写 WEB API 客户端代码](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)

**注意：** 如果将基 Url 和相对 Uri 作为硬编码值传递，请注意使用 API 的规则 `HttpClient` 。 `HttpClient.BaseAddress`应将属性设置为包含尾随正斜杠（）的地址 `/` 。 例如，将硬编码的资源 Uri 传递给方法时 `HttpClient.GetAsync` ，不要包含前导正斜杠。 `Product`按 ID 获取：

1. 字符集`client.BaseAddress = new Uri("https://localhost:5001/");`
1. 请求 `Product` 。 例如 `client.GetAsync<Product>("api/products/4");`。

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>创建控制台应用程序

在 Visual Studio 中，创建一个名为**HttpClientSample**的新 Windows 控制台应用程序，并粘贴以下代码：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

上面的代码是完整的客户端应用程序。

`RunAsync`运行并一直阻止到完成为止。 大多数**HttpClient**方法都是异步的，因为它们执行网络 i/o。 所有异步任务都在内完成 `RunAsync` 。 通常，应用程序不会阻止主线程，但此应用程序不允许任何交互。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>安装 Web API 客户端库

使用 NuGet 包管理器安装 Web API 客户端库包。

在“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。************ 在 "程序包管理器控制台" （PMC）中，键入以下命令：

`Install-Package Microsoft.AspNet.WebApi.Client`

前面的命令将以下 NuGet 包添加到项目中：

* WebApi。
* Newtonsoft.Json

Netwonsoft （也称为 Json.NET）是适用于 .NET 的常用高性能 JSON 框架。

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>添加模型类

检查 `Product` 类：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

此类与 web API 使用的数据模型相匹配。 应用可以使用**HttpClient** `Product` 从 HTTP 响应中读取实例。 应用无需编写任何反序列化代码。

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>创建和初始化 HttpClient

检查静态**HttpClient**属性：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient**仅可在应用程序的整个生命周期中实例化一次并重复使用。 以下情况可能会导致**SocketException**错误：

* 为每个请求创建一个新的**HttpClient**实例。
* 负载较重的服务器。

为每个请求创建新的**HttpClient**实例可能会耗尽可用的套接字。

下面的代码对**HttpClient**实例进行了初始化：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

前面的代码：

* 设置 HTTP 请求的基 URI。 将端口号更改为服务器应用中使用的端口。 除非使用服务器应用的端口，否则应用不起作用。
* 将 Accept 标头设置为 "application/json"。 设置此标头将告知服务器以 JSON 格式发送数据。

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>发送 GET 请求以检索资源

下面的代码发送一个产品的 GET 请求：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**GetAsync**方法发送 HTTP GET 请求。 当方法完成时，它将返回一个包含 HTTP 响应的**HttpResponseMessage** 。 如果响应中的状态代码是成功代码，则响应正文包含产品的 JSON 表示形式。 调用**ReadAsAsync**将 JSON 负载反序列化为 `Product` 实例。 **ReadAsAsync**方法是异步的，因为响应正文可能会很大。

当 HTTP 响应包含错误代码时， **HttpClient**不会引发异常。 相反，如果状态是错误代码，则 **.issuccessstatuscode**属性为**false** 。 如果希望将 HTTP 错误代码视为例外，请在响应对象上调用[HttpResponseMessage。](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) `EnsureSuccessStatusCode`如果状态代码不在 200 299 范围内，则会引发异常 &ndash; 。 请注意， **HttpClient**可能会出于其他原因 &mdash; （例如，如果请求超时）而引发异常。

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>要反序列化的媒体类型格式化程序

如果在没有参数的情况下调用**ReadAsAsync** ，则它将使用一组默认的*媒体格式化*程序来读取响应正文。 默认格式化程序支持 JSON、XML 和窗体 url 编码数据。

您可以向**ReadAsAsync**方法提供格式化程序列表，而不是使用默认的格式化程序。  如果有自定义的媒体类型格式化程序，则使用格式化程序列表非常有用：

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

有关详细信息，请参阅[ASP.NET Web API 2 中的媒体格式化](../formats-and-model-binding/media-formatters.md)程序

## <a name="sending-a-post-request-to-create-a-resource"></a>发送 POST 请求以创建资源

下面的代码发送 POST 请求，其中包含 `Product` 采用 JSON 格式的实例：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**PostAsJsonAsync**方法：

* 将对象序列化为 JSON。
* 发送 POST 请求中的 JSON 有效负载。

如果请求成功：

* 它应返回201（已创建）响应。
* 响应应在 Location 标头中包含已创建的资源的 URL。

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>发送 PUT 请求以更新资源

以下代码发送 PUT 请求以更新产品：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**PutAsJsonAsync**方法的工作方式类似于**PostAsJsonAsync**，只不过它会发送 PUT 请求而不是 POST。

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>发送删除请求以删除资源

以下代码发送删除请求以删除产品：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

与 GET 一样，删除请求没有请求正文。 不需要指定 JSON 或 XML 格式。

## <a name="test-the-sample"></a>测试示例

测试客户端应用：

1. [下载](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)并运行服务器应用。 [下载说明](/aspnet/core/#how-to-download-a-sample)。 验证服务器应用是否正常工作。 例如， `http://localhost:64195/api/products` 应返回产品列表。
2. 设置 HTTP 请求的基 URI。 将端口号更改为服务器应用中使用的端口。
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. 运行客户端应用。 将生成以下输出：

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```

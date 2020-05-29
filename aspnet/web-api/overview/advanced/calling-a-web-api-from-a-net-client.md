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
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="c3a03-103">从 .NET 客户端调用 Web API （c #）</span><span class="sxs-lookup"><span data-stu-id="c3a03-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="c3a03-104">作者： [Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c3a03-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c3a03-105">[下载完成的项目](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。</span><span class="sxs-lookup"><span data-stu-id="c3a03-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="c3a03-106">[下载说明](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="c3a03-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="c3a03-107">本教程演示如何使用[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)从 .net 应用程序调用 web API。</span><span class="sxs-lookup"><span data-stu-id="c3a03-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="c3a03-108">在本教程中，编写了一个使用以下 web API 的客户端应用：</span><span class="sxs-lookup"><span data-stu-id="c3a03-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="c3a03-109">操作</span><span class="sxs-lookup"><span data-stu-id="c3a03-109">Action</span></span> | <span data-ttu-id="c3a03-110">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="c3a03-110">HTTP method</span></span> | <span data-ttu-id="c3a03-111">相对 URI</span><span class="sxs-lookup"><span data-stu-id="c3a03-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3a03-112">根据 ID 获取产品</span><span class="sxs-lookup"><span data-stu-id="c3a03-112">Get a product by ID</span></span> | <span data-ttu-id="c3a03-113">GET</span><span class="sxs-lookup"><span data-stu-id="c3a03-113">GET</span></span> | <span data-ttu-id="c3a03-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c3a03-114">/api/products/*id*</span></span> |
| <span data-ttu-id="c3a03-115">创建新产品</span><span class="sxs-lookup"><span data-stu-id="c3a03-115">Create a new product</span></span> | <span data-ttu-id="c3a03-116">POST</span><span class="sxs-lookup"><span data-stu-id="c3a03-116">POST</span></span> | <span data-ttu-id="c3a03-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="c3a03-117">/api/products</span></span> |
| <span data-ttu-id="c3a03-118">更新产品</span><span class="sxs-lookup"><span data-stu-id="c3a03-118">Update a product</span></span> | <span data-ttu-id="c3a03-119">PUT</span><span class="sxs-lookup"><span data-stu-id="c3a03-119">PUT</span></span> | <span data-ttu-id="c3a03-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c3a03-120">/api/products/*id*</span></span> |
| <span data-ttu-id="c3a03-121">删除产品</span><span class="sxs-lookup"><span data-stu-id="c3a03-121">Delete a product</span></span> | <span data-ttu-id="c3a03-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="c3a03-122">DELETE</span></span> | <span data-ttu-id="c3a03-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c3a03-123">/api/products/*id*</span></span> |

<span data-ttu-id="c3a03-124">若要了解如何使用 ASP.NET Web API 实现此 API，请参阅[创建支持 CRUD 操作的 WEB API](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="c3a03-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="c3a03-125">为简单起见，本教程中的客户端应用程序是一个 Windows 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3a03-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="c3a03-126">Windows Phone 和 Windows 应用商店应用程序也支持**HttpClient** 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="c3a03-127">有关详细信息，请参阅[使用可移植库为多个平台编写 WEB API 客户端代码](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="c3a03-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<span data-ttu-id="c3a03-128">**注意：** 如果将基 Url 和相对 Uri 作为硬编码值传递，请注意使用 API 的规则 `HttpClient` 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-128">**NOTE:** If you pass base URLs and relative URIs as hard-coded values, be mindful of the rules for utilizing the `HttpClient` API.</span></span> <span data-ttu-id="c3a03-129">`HttpClient.BaseAddress`应将属性设置为包含尾随正斜杠（）的地址 `/` 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-129">The `HttpClient.BaseAddress` property should be set to an address with a trailing forward slash (`/`).</span></span> <span data-ttu-id="c3a03-130">例如，将硬编码的资源 Uri 传递给方法时 `HttpClient.GetAsync` ，不要包含前导正斜杠。</span><span class="sxs-lookup"><span data-stu-id="c3a03-130">For example, when passing hard-coded resource URIs to the `HttpClient.GetAsync` method, don't include a leading forward slash.</span></span> <span data-ttu-id="c3a03-131">`Product`按 ID 获取：</span><span class="sxs-lookup"><span data-stu-id="c3a03-131">To get a `Product` by ID:</span></span>

1. <span data-ttu-id="c3a03-132">字符集`client.BaseAddress = new Uri("https://localhost:5001/");`</span><span class="sxs-lookup"><span data-stu-id="c3a03-132">Set `client.BaseAddress = new Uri("https://localhost:5001/");`</span></span>
1. <span data-ttu-id="c3a03-133">请求 `Product` 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-133">Request a `Product`.</span></span> <span data-ttu-id="c3a03-134">例如 `client.GetAsync<Product>("api/products/4");`。</span><span class="sxs-lookup"><span data-stu-id="c3a03-134">For example, `client.GetAsync<Product>("api/products/4");`.</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="c3a03-135">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="c3a03-135">Create the Console Application</span></span>

<span data-ttu-id="c3a03-136">在 Visual Studio 中，创建一个名为**HttpClientSample**的新 Windows 控制台应用程序，并粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="c3a03-136">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="c3a03-137">上面的代码是完整的客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3a03-137">The preceding code is the complete client app.</span></span>

<span data-ttu-id="c3a03-138">`RunAsync`运行并一直阻止到完成为止。</span><span class="sxs-lookup"><span data-stu-id="c3a03-138">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="c3a03-139">大多数**HttpClient**方法都是异步的，因为它们执行网络 i/o。</span><span class="sxs-lookup"><span data-stu-id="c3a03-139">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="c3a03-140">所有异步任务都在内完成 `RunAsync` 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-140">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="c3a03-141">通常，应用程序不会阻止主线程，但此应用程序不允许任何交互。</span><span class="sxs-lookup"><span data-stu-id="c3a03-141">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="c3a03-142">安装 Web API 客户端库</span><span class="sxs-lookup"><span data-stu-id="c3a03-142">Install the Web API Client Libraries</span></span>

<span data-ttu-id="c3a03-143">使用 NuGet 包管理器安装 Web API 客户端库包。</span><span class="sxs-lookup"><span data-stu-id="c3a03-143">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="c3a03-144">在“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。\*\*\*\*\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="c3a03-144">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="c3a03-145">在 "程序包管理器控制台" （PMC）中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="c3a03-145">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="c3a03-146">前面的命令将以下 NuGet 包添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="c3a03-146">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="c3a03-147">WebApi。</span><span class="sxs-lookup"><span data-stu-id="c3a03-147">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="c3a03-148">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="c3a03-148">Newtonsoft.Json</span></span>

<span data-ttu-id="c3a03-149">Netwonsoft （也称为 Json.NET）是适用于 .NET 的常用高性能 JSON 框架。</span><span class="sxs-lookup"><span data-stu-id="c3a03-149">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="c3a03-150">添加模型类</span><span class="sxs-lookup"><span data-stu-id="c3a03-150">Add a Model Class</span></span>

<span data-ttu-id="c3a03-151">检查 `Product` 类：</span><span class="sxs-lookup"><span data-stu-id="c3a03-151">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="c3a03-152">此类与 web API 使用的数据模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="c3a03-152">This class matches the data model used by the web API.</span></span> <span data-ttu-id="c3a03-153">应用可以使用**HttpClient** `Product` 从 HTTP 响应中读取实例。</span><span class="sxs-lookup"><span data-stu-id="c3a03-153">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="c3a03-154">应用无需编写任何反序列化代码。</span><span class="sxs-lookup"><span data-stu-id="c3a03-154">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="c3a03-155">创建和初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="c3a03-155">Create and Initialize HttpClient</span></span>

<span data-ttu-id="c3a03-156">检查静态**HttpClient**属性：</span><span class="sxs-lookup"><span data-stu-id="c3a03-156">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="c3a03-157">**HttpClient**仅可在应用程序的整个生命周期中实例化一次并重复使用。</span><span class="sxs-lookup"><span data-stu-id="c3a03-157">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="c3a03-158">以下情况可能会导致**SocketException**错误：</span><span class="sxs-lookup"><span data-stu-id="c3a03-158">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="c3a03-159">为每个请求创建一个新的**HttpClient**实例。</span><span class="sxs-lookup"><span data-stu-id="c3a03-159">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="c3a03-160">负载较重的服务器。</span><span class="sxs-lookup"><span data-stu-id="c3a03-160">Server under heavy load.</span></span>

<span data-ttu-id="c3a03-161">为每个请求创建新的**HttpClient**实例可能会耗尽可用的套接字。</span><span class="sxs-lookup"><span data-stu-id="c3a03-161">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="c3a03-162">下面的代码对**HttpClient**实例进行了初始化：</span><span class="sxs-lookup"><span data-stu-id="c3a03-162">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="c3a03-163">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="c3a03-163">The preceding code:</span></span>

* <span data-ttu-id="c3a03-164">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="c3a03-164">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="c3a03-165">将端口号更改为服务器应用中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="c3a03-165">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="c3a03-166">除非使用服务器应用的端口，否则应用不起作用。</span><span class="sxs-lookup"><span data-stu-id="c3a03-166">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="c3a03-167">将 Accept 标头设置为 "application/json"。</span><span class="sxs-lookup"><span data-stu-id="c3a03-167">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="c3a03-168">设置此标头将告知服务器以 JSON 格式发送数据。</span><span class="sxs-lookup"><span data-stu-id="c3a03-168">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="c3a03-169">发送 GET 请求以检索资源</span><span class="sxs-lookup"><span data-stu-id="c3a03-169">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="c3a03-170">下面的代码发送一个产品的 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="c3a03-170">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="c3a03-171">**GetAsync**方法发送 HTTP GET 请求。</span><span class="sxs-lookup"><span data-stu-id="c3a03-171">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="c3a03-172">当方法完成时，它将返回一个包含 HTTP 响应的**HttpResponseMessage** 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-172">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="c3a03-173">如果响应中的状态代码是成功代码，则响应正文包含产品的 JSON 表示形式。</span><span class="sxs-lookup"><span data-stu-id="c3a03-173">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="c3a03-174">调用**ReadAsAsync**将 JSON 负载反序列化为 `Product` 实例。</span><span class="sxs-lookup"><span data-stu-id="c3a03-174">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="c3a03-175">**ReadAsAsync**方法是异步的，因为响应正文可能会很大。</span><span class="sxs-lookup"><span data-stu-id="c3a03-175">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="c3a03-176">当 HTTP 响应包含错误代码时， **HttpClient**不会引发异常。</span><span class="sxs-lookup"><span data-stu-id="c3a03-176">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="c3a03-177">相反，如果状态是错误代码，则 **.issuccessstatuscode**属性为**false** 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-177">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="c3a03-178">如果希望将 HTTP 错误代码视为例外，请在响应对象上调用[HttpResponseMessage。](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="c3a03-178">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="c3a03-179">`EnsureSuccessStatusCode`如果状态代码不在 200 299 范围内，则会引发异常 &ndash; 。</span><span class="sxs-lookup"><span data-stu-id="c3a03-179">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="c3a03-180">请注意， **HttpClient**可能会出于其他原因 &mdash; （例如，如果请求超时）而引发异常。</span><span class="sxs-lookup"><span data-stu-id="c3a03-180">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="c3a03-181">要反序列化的媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="c3a03-181">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="c3a03-182">如果在没有参数的情况下调用**ReadAsAsync** ，则它将使用一组默认的*媒体格式化*程序来读取响应正文。</span><span class="sxs-lookup"><span data-stu-id="c3a03-182">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="c3a03-183">默认格式化程序支持 JSON、XML 和窗体 url 编码数据。</span><span class="sxs-lookup"><span data-stu-id="c3a03-183">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="c3a03-184">您可以向**ReadAsAsync**方法提供格式化程序列表，而不是使用默认的格式化程序。</span><span class="sxs-lookup"><span data-stu-id="c3a03-184">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="c3a03-185">如果有自定义的媒体类型格式化程序，则使用格式化程序列表非常有用：</span><span class="sxs-lookup"><span data-stu-id="c3a03-185">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="c3a03-186">有关详细信息，请参阅[ASP.NET Web API 2 中的媒体格式化](../formats-and-model-binding/media-formatters.md)程序</span><span class="sxs-lookup"><span data-stu-id="c3a03-186">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="c3a03-187">发送 POST 请求以创建资源</span><span class="sxs-lookup"><span data-stu-id="c3a03-187">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="c3a03-188">下面的代码发送 POST 请求，其中包含 `Product` 采用 JSON 格式的实例：</span><span class="sxs-lookup"><span data-stu-id="c3a03-188">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="c3a03-189">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="c3a03-189">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="c3a03-190">将对象序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="c3a03-190">Serializes an object to JSON.</span></span>
* <span data-ttu-id="c3a03-191">发送 POST 请求中的 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="c3a03-191">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="c3a03-192">如果请求成功：</span><span class="sxs-lookup"><span data-stu-id="c3a03-192">If the request succeeds:</span></span>

* <span data-ttu-id="c3a03-193">它应返回201（已创建）响应。</span><span class="sxs-lookup"><span data-stu-id="c3a03-193">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="c3a03-194">响应应在 Location 标头中包含已创建的资源的 URL。</span><span class="sxs-lookup"><span data-stu-id="c3a03-194">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="c3a03-195">发送 PUT 请求以更新资源</span><span class="sxs-lookup"><span data-stu-id="c3a03-195">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="c3a03-196">以下代码发送 PUT 请求以更新产品：</span><span class="sxs-lookup"><span data-stu-id="c3a03-196">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="c3a03-197">**PutAsJsonAsync**方法的工作方式类似于**PostAsJsonAsync**，只不过它会发送 PUT 请求而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="c3a03-197">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="c3a03-198">发送删除请求以删除资源</span><span class="sxs-lookup"><span data-stu-id="c3a03-198">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="c3a03-199">以下代码发送删除请求以删除产品：</span><span class="sxs-lookup"><span data-stu-id="c3a03-199">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="c3a03-200">与 GET 一样，删除请求没有请求正文。</span><span class="sxs-lookup"><span data-stu-id="c3a03-200">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="c3a03-201">不需要指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="c3a03-201">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="c3a03-202">测试示例</span><span class="sxs-lookup"><span data-stu-id="c3a03-202">Test the sample</span></span>

<span data-ttu-id="c3a03-203">测试客户端应用：</span><span class="sxs-lookup"><span data-stu-id="c3a03-203">To test the client app:</span></span>

1. <span data-ttu-id="c3a03-204">[下载](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)并运行服务器应用。</span><span class="sxs-lookup"><span data-stu-id="c3a03-204">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="c3a03-205">[下载说明](/aspnet/core/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="c3a03-205">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="c3a03-206">验证服务器应用是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="c3a03-206">Verify the server app is working.</span></span> <span data-ttu-id="c3a03-207">例如， `http://localhost:64195/api/products` 应返回产品列表。</span><span class="sxs-lookup"><span data-stu-id="c3a03-207">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="c3a03-208">设置 HTTP 请求的基 URI。</span><span class="sxs-lookup"><span data-stu-id="c3a03-208">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="c3a03-209">将端口号更改为服务器应用中使用的端口。</span><span class="sxs-lookup"><span data-stu-id="c3a03-209">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="c3a03-210">运行客户端应用。</span><span class="sxs-lookup"><span data-stu-id="c3a03-210">Run the client app.</span></span> <span data-ttu-id="c3a03-211">将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="c3a03-211">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```

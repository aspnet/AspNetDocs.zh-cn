---
ms.openlocfilehash: 4a4ad30846d1993b3e561c96c00fbf9a0c7f3929
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040804"
---
# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="ff824-101">ASP.NET Core URL 重写示例 (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="ff824-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="ff824-102">本示例演示 ASP.NET Core 2.x URL 重写中间件的用法。</span><span class="sxs-lookup"><span data-stu-id="ff824-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="ff824-103">该应用演示 URL 重定向和 URL 重写选项。</span><span class="sxs-lookup"><span data-stu-id="ff824-103">The app demonstrates URL redirect and URL rewriting options.</span></span>

<span data-ttu-id="ff824-104">运行示例时，如果向请求 URL 应用了其中一个规则，则非文件响应将返回重写或重定向的 URL。</span><span class="sxs-lookup"><span data-stu-id="ff824-104">When running the sample, non-file responses return the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span> <span data-ttu-id="ff824-105">对于 XML 和文本文件示例，静态文件中间件将在中间件重写请求 URL 之后提供该文件。</span><span class="sxs-lookup"><span data-stu-id="ff824-105">For the XML and text file examples, Static File Middleware serves the file after the request URL is rewritten by the middleware.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="ff824-106">此示例中的示例</span><span class="sxs-lookup"><span data-stu-id="ff824-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="ff824-107">成功状态代码：302 （已找到）</span><span class="sxs-lookup"><span data-stu-id="ff824-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="ff824-108">示例（重定向）：/redirect-rule/{capture_group} 到 /redirected/{capture_group}</span><span class="sxs-lookup"><span data-stu-id="ff824-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="ff824-109">成功状态代码：200 （正常）</span><span class="sxs-lookup"><span data-stu-id="ff824-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ff824-110">示例（重写）：/rewrite-rule/{capture_group_1}/{capture_group_2} 到 /rewritten?var1={capture_group_1}&var2={capture_group_2}</span><span class="sxs-lookup"><span data-stu-id="ff824-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="ff824-111">成功状态代码：302 （已找到）</span><span class="sxs-lookup"><span data-stu-id="ff824-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="ff824-112">示例（重定向）：/apache-mod-rules-redirect/{capture_group} 到 /redirected?id={capture_group}</span><span class="sxs-lookup"><span data-stu-id="ff824-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="ff824-113">成功状态代码：200 （正常）</span><span class="sxs-lookup"><span data-stu-id="ff824-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ff824-114">示例（重写）：/iis-rules-rewrite/{capture_group} 到 /rewritten?id={capture_group}</span><span class="sxs-lookup"><span data-stu-id="ff824-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXmlFileRequests)`
  - <span data-ttu-id="ff824-115">成功状态代码：301 （永久移动）</span><span class="sxs-lookup"><span data-stu-id="ff824-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="ff824-116">示例（重定向）：/file.xml 到 /xmlfiles/file.xml</span><span class="sxs-lookup"><span data-stu-id="ff824-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(RewriteTextFileRequests)`
  - <span data-ttu-id="ff824-117">成功状态代码：200 （正常）</span><span class="sxs-lookup"><span data-stu-id="ff824-117">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ff824-118">示例（重写）：/some_file.txt 到 /file.txt</span><span class="sxs-lookup"><span data-stu-id="ff824-118">Example (rewrite): **/some_file.txt** to **/file.txt**</span></span>
* `Add(new RedirectImageRequests(".png", "/png-images")))`<br>`Add(new RedirectImageRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="ff824-119">成功状态代码：301 （永久移动）</span><span class="sxs-lookup"><span data-stu-id="ff824-119">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="ff824-120">示例（重定向）：/image.png 到 /png-images/image.png</span><span class="sxs-lookup"><span data-stu-id="ff824-120">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="ff824-121">示例（重定向）：/image.jpg 到 /jpg-images/image.jpg</span><span class="sxs-lookup"><span data-stu-id="ff824-121">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="use-a-physicalfileprovider"></a><span data-ttu-id="ff824-122">使用 PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="ff824-122">Use a PhysicalFileProvider</span></span>

<span data-ttu-id="ff824-123">也可通过创建 `PhysicalFileProvider` 以传递给 `AddApacheModRewrite()` 和 `AddIISUrlRewrite()` 方法来获取 `IFileProvider`：</span><span class="sxs-lookup"><span data-stu-id="ff824-123">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>

```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```

## <a name="secure-redirection-extensions"></a><span data-ttu-id="ff824-124">安全的重定向扩展</span><span class="sxs-lookup"><span data-stu-id="ff824-124">Secure redirection extensions</span></span>

<span data-ttu-id="ff824-125">此示例包含应用的 `WebHostBuilder` 配置以使用 URL（`https://localhost:5001`、`https://localhost`）和测试证书 (testCert.pfx) 来帮助探索安全重定向方法。</span><span class="sxs-lookup"><span data-stu-id="ff824-125">This sample includes `WebHostBuilder` configuration for the app to use URLs (`https://localhost:5001`, `https://localhost`) and a test certificate (*testCert.pfx*) to assist in exploring the secure redirect methods.</span></span> <span data-ttu-id="ff824-126">如果服务器已分配或正在使用端口 443，则 `https://localhost` 示例不起作用 &mdash; 在 Program.cs 文件的 `CreateWebHostBuilder` 方法中删除端口 443 的 `ListenOptions` 或在服务器上取消绑定端口 443，以便 Kestrel 可以使用该端口。</span><span class="sxs-lookup"><span data-stu-id="ff824-126">If the server already has port 443 assigned or in use, the `https://localhost` example doesn't work&mdash;remove the `ListenOptions` for port 443 in the `CreateWebHostBuilder` method of the *Program.cs* file or unbind port 443 on the server so that Kestrel can use the port.</span></span>

| <span data-ttu-id="ff824-127">方法</span><span class="sxs-lookup"><span data-stu-id="ff824-127">Method</span></span>                           | <span data-ttu-id="ff824-128">状态代码</span><span class="sxs-lookup"><span data-stu-id="ff824-128">Status Code</span></span> |    <span data-ttu-id="ff824-129">端口</span><span class="sxs-lookup"><span data-stu-id="ff824-129">Port</span></span>    |
| -------------------------------- | :---------: | :--------: |
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="ff824-130">301</span><span class="sxs-lookup"><span data-stu-id="ff824-130">301</span></span>     | <span data-ttu-id="ff824-131">null (465)</span><span class="sxs-lookup"><span data-stu-id="ff824-131">null (465)</span></span> |
| `.AddRedirectToHttps()`          |     <span data-ttu-id="ff824-132">302</span><span class="sxs-lookup"><span data-stu-id="ff824-132">302</span></span>     | <span data-ttu-id="ff824-133">null (465)</span><span class="sxs-lookup"><span data-stu-id="ff824-133">null (465)</span></span> |
| `.AddRedirectToHttps(301)`       |     <span data-ttu-id="ff824-134">301</span><span class="sxs-lookup"><span data-stu-id="ff824-134">301</span></span>     | <span data-ttu-id="ff824-135">null (465)</span><span class="sxs-lookup"><span data-stu-id="ff824-135">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="ff824-136">301</span><span class="sxs-lookup"><span data-stu-id="ff824-136">301</span></span>     |    <span data-ttu-id="ff824-137">5001</span><span class="sxs-lookup"><span data-stu-id="ff824-137">5001</span></span>    |

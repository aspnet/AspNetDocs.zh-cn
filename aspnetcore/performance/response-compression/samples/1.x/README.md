---
ms.openlocfilehash: 4add1c40387073f35711b2c8db27e48657a18192
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061624"
---
# <a name="response-compression-sample-application-aspnet-core-1x"></a><span data-ttu-id="e89d8-101">响应压缩示例应用程序 (ASP.NET Core 1.x)</span><span class="sxs-lookup"><span data-stu-id="e89d8-101">Response compression sample application (ASP.NET Core 1.x)</span></span>

<span data-ttu-id="e89d8-102">此示例演示如何使用 ASP.NET Core 1.x 响应的压缩中间件来压缩 HTTP 响应中的。</span><span class="sxs-lookup"><span data-stu-id="e89d8-102">This sample illustrates the use of ASP.NET Core 1.x Response Compression Middleware to compress HTTP responses for.</span></span> <span data-ttu-id="e89d8-103">此示例演示 Gzip 和自定义压缩的文本和图像响应的提供程序，并演示如何添加压缩的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="e89d8-103">The sample demonstrates Gzip and custom compression providers for text and image responses and shows how to add a MIME type for compression.</span></span> <span data-ttu-id="e89d8-104">有关 ASP.NET Core 2.x 示例，请参阅[响应压缩示例应用程序 (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/2.x)。</span><span class="sxs-lookup"><span data-stu-id="e89d8-104">For the ASP.NET Core 2.x sample, see [Response compression sample application (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/2.x).</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="e89d8-105">此示例中的示例</span><span class="sxs-lookup"><span data-stu-id="e89d8-105">Examples in this sample</span></span>

* `GzipCompressionProvider`
  * `text/plain`
    * <span data-ttu-id="e89d8-106">**/** -将压缩为 927 字节的 2,044 字节乱数假文文本文件响应</span><span class="sxs-lookup"><span data-stu-id="e89d8-106">**/** - Lorem Ipsum text file response at 2,044 bytes that will compress to 927 bytes</span></span>
    * <span data-ttu-id="e89d8-107">**/testfile1kb.txt** -1,033 将压缩为 47 个字节的字节的文本文件响应</span><span class="sxs-lookup"><span data-stu-id="e89d8-107">**/testfile1kb.txt** - Text file response at 1,033 bytes that will compress to 47 bytes</span></span>
    * <span data-ttu-id="e89d8-108">**/ 渗透**-每次间隔 1 秒作为单个字符发出的响应</span><span class="sxs-lookup"><span data-stu-id="e89d8-108">**/trickle** - Response issued as single characters at 1 second intervals</span></span>
  * `image/svg+xml`
    * <span data-ttu-id="e89d8-109">**/banner.svg** -9,707 将压缩为 4,459 字节的字节的可缩放向量图形 (SVG) 图像响应</span><span class="sxs-lookup"><span data-stu-id="e89d8-109">**/banner.svg** - A Scalable Vector Graphics (SVG) image response at 9,707 bytes that will compress to 4,459 bytes</span></span>
* `CustomCompressionProvider`<br><span data-ttu-id="e89d8-110">演示如何实现与中间件使用的自定义压缩提供程序</span><span class="sxs-lookup"><span data-stu-id="e89d8-110">Shows how to implement a custom compression provider for use with the middleware</span></span>

<span data-ttu-id="e89d8-111">当请求包括`Accept-Encoding`标头，该示例添加`Vary: Accept-Encoding`到响应的标头。</span><span class="sxs-lookup"><span data-stu-id="e89d8-111">When the request includes the `Accept-Encoding` header, the sample adds a `Vary: Accept-Encoding` header to the response.</span></span> <span data-ttu-id="e89d8-112">`Vary`标头会指示缓存维护的响应的替代值为基础的多个副本`Accept-Encoding`，因此需压缩 (gzip) 和未压缩的版本存储在缓存中的系统可以接受压缩或未压缩的响应。</span><span class="sxs-lookup"><span data-stu-id="e89d8-112">The `Vary` header instructs caches to maintain multiple copies of the response based on alternative values of `Accept-Encoding`, so both a compressed (gzip) and uncompressed version are stored in caches for systems that can either accept the compressed or the uncompressed response.</span></span>

## <a name="using-the-sample"></a><span data-ttu-id="e89d8-113">使用示例</span><span class="sxs-lookup"><span data-stu-id="e89d8-113">Using the sample</span></span>

1. <span data-ttu-id="e89d8-114">使请求使用[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)到应用程序而不`Accept-Encoding`标头并记下响应有效负载，响应大小和响应标头。</span><span class="sxs-lookup"><span data-stu-id="e89d8-114">Make a request using [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to the application without an `Accept-Encoding` header and note the response payload, response size, and response headers.</span></span>
1. <span data-ttu-id="e89d8-115">添加`Accept-Encoding: gzip`标头并记下压缩的响应大小和响应标头。</span><span class="sxs-lookup"><span data-stu-id="e89d8-115">Add an `Accept-Encoding: gzip` header and note the compressed response size and response headers.</span></span> <span data-ttu-id="e89d8-116">请参阅删除，响应大小和`Content-Encoding: gzip`响应标头包含示例应用。</span><span class="sxs-lookup"><span data-stu-id="e89d8-116">You see the response size drop, and the `Content-Encoding: gzip` response header is included by the sample app.</span></span> <span data-ttu-id="e89d8-117">要查看在响应正文的乱数假文或**testfile1kb.txt**响应，你将看到文本是压缩且不可读。</span><span class="sxs-lookup"><span data-stu-id="e89d8-117">When you look at the response body for the Lorem Ipsum or **testfile1kb.txt** response, you see that the text is compressed and unreadable.</span></span>
1. <span data-ttu-id="e89d8-118">添加`Accept-Encoding: mycustomcompression`标头并记下响应标头。</span><span class="sxs-lookup"><span data-stu-id="e89d8-118">Add an `Accept-Encoding: mycustomcompression` header and note the response headers.</span></span> <span data-ttu-id="e89d8-119">`CustomCompressionProvider`是一个空实现，实际上不会压缩响应，但您可以创建自定义压缩流包装器`CreateStream()`方法。</span><span class="sxs-lookup"><span data-stu-id="e89d8-119">The `CustomCompressionProvider` is an empty implementation that doesn't actually compress the response, but you can create a custom compression stream wrapper for the `CreateStream()` method.</span></span>

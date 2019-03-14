---
ms.openlocfilehash: 976cc58dfcd9bba0b88ddd5d0d886cbb99b418ae
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026314"
---
# <a name="response-compression-sample-application-aspnet-core-2x"></a><span data-ttu-id="b8be1-101">响应压缩示例应用程序 (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="b8be1-101">Response compression sample application (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="b8be1-102">此示例演示如何使用 ASP.NET Core 2.x 响应压缩中间件来压缩 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="b8be1-102">This sample illustrates the use of ASP.NET Core 2.x Response Compression Middleware to compress HTTP responses.</span></span> <span data-ttu-id="b8be1-103">此示例演示 Gzip、 Brotli 和自定义压缩的文本和图像响应的提供程序，并演示如何添加压缩的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="b8be1-103">The sample demonstrates Gzip, Brotli, and custom compression providers for text and image responses and shows how to add a MIME type for compression.</span></span> <span data-ttu-id="b8be1-104">有关 ASP.NET Core 1.x 示例，请参阅[响应压缩示例应用程序 (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/1.x)。</span><span class="sxs-lookup"><span data-stu-id="b8be1-104">For the ASP.NET Core 1.x sample, see [Response compression sample application (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/1.x).</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="b8be1-105">此示例中的示例</span><span class="sxs-lookup"><span data-stu-id="b8be1-105">Examples in this sample</span></span>

* `BrotliCompressionProvider`
  * `text/plain`
    * <span data-ttu-id="b8be1-106">**/** -乱数假文文本文件响应为 2,044 个字节，压缩为 ~ 979 字节。</span><span class="sxs-lookup"><span data-stu-id="b8be1-106">**/** - Lorem Ipsum text file response at 2,044 bytes that compresses to ~979 bytes.</span></span>
    * <span data-ttu-id="b8be1-107">**/testfile1kb.txt** -将压缩到 ~ 36 个字节的文本文件响应 1,033 字节。</span><span class="sxs-lookup"><span data-stu-id="b8be1-107">**/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~36 bytes.</span></span>
    * <span data-ttu-id="b8be1-108">**/ 渗透**-每次间隔 1 秒作为单个字符发出的响应。</span><span class="sxs-lookup"><span data-stu-id="b8be1-108">**/trickle** - Response issued as single characters at 1 second intervals.</span></span>
* `GzipCompressionProvider`
  * `text/plain`
    * <span data-ttu-id="b8be1-109">**/** -乱数假文文本文件响应为 2,044 个字节，压缩为 ~ 927 字节。</span><span class="sxs-lookup"><span data-stu-id="b8be1-109">**/** - Lorem Ipsum text file response at 2,044 bytes that compresses to ~927 bytes.</span></span>
    * <span data-ttu-id="b8be1-110">**/testfile1kb.txt** -将压缩到 ~ 47 个字节的文本文件响应 1,033 字节。</span><span class="sxs-lookup"><span data-stu-id="b8be1-110">**/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~47 bytes.</span></span>
    * <span data-ttu-id="b8be1-111">**/ 渗透**-每次间隔 1 秒作为单个字符发出的响应。</span><span class="sxs-lookup"><span data-stu-id="b8be1-111">**/trickle** - Response issued as single characters at 1 second intervals.</span></span>
  * `image/svg+xml`
    * <span data-ttu-id="b8be1-112">**/banner.svg** -将压缩为 ~ 4,459 字节的可缩放向量图形 (SVG) 图像响应 9,707 字节。</span><span class="sxs-lookup"><span data-stu-id="b8be1-112">**/banner.svg** - A Scalable Vector Graphics (SVG) image response at 9,707 bytes that compresses to ~4,459 bytes.</span></span>
* `CustomCompressionProvider`<br><span data-ttu-id="b8be1-113">演示如何实现与中间件使用的自定义压缩提供程序。</span><span class="sxs-lookup"><span data-stu-id="b8be1-113">Shows how to implement a custom compression provider for use with the middleware.</span></span>

<span data-ttu-id="b8be1-114">当请求包括`Accept-Encoding`标头和响应压缩操作成功，则中间件会自动添加`Vary: Accept-Encoding`到响应的标头。</span><span class="sxs-lookup"><span data-stu-id="b8be1-114">When the request includes the `Accept-Encoding` header and response compression is successful, the middleware automatically adds a `Vary: Accept-Encoding` header to the response.</span></span> <span data-ttu-id="b8be1-115">`Vary`标头会指示缓存维护的响应的替代值为基础的多个副本`Accept-Encoding`，因此这两种压缩 （Gzip 或 Brotli） 和未压缩的版本存储在缓存中的系统可以接受压缩或未压缩的响应。</span><span class="sxs-lookup"><span data-stu-id="b8be1-115">The `Vary` header instructs caches to maintain multiple copies of the response based on alternative values of `Accept-Encoding`, so both a compressed (Gzip or Brotli) and uncompressed version are stored in caches for systems that can either accept the compressed or the uncompressed response.</span></span>

## <a name="use-the-sample"></a><span data-ttu-id="b8be1-116">使用示例</span><span class="sxs-lookup"><span data-stu-id="b8be1-116">Use the sample</span></span>

1. <span data-ttu-id="b8be1-117">使请求使用[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)到应用程序而不`Accept-Encoding`标头并记下响应有效负载，响应大小和响应标头。</span><span class="sxs-lookup"><span data-stu-id="b8be1-117">Make a request using [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to the application without an `Accept-Encoding` header and note the response payload, response size, and response headers.</span></span>
1. <span data-ttu-id="b8be1-118">添加`Accept-Encoding: br`或`Accept-Encoding: gzip`标头并记下压缩的响应大小和响应标头。</span><span class="sxs-lookup"><span data-stu-id="b8be1-118">Add an `Accept-Encoding: br` or `Accept-Encoding: gzip` header and note the compressed response size and response headers.</span></span> <span data-ttu-id="b8be1-119">响应大小降至，和`Content-Encoding`响应标头包含由中间件，该值指示该使用任一 Gzip 压缩或 Brotli 发生。</span><span class="sxs-lookup"><span data-stu-id="b8be1-119">The response size drops, and the `Content-Encoding` response header is included by the middleware indicating that compression with either Gzip or Brotli occurred.</span></span> <span data-ttu-id="b8be1-120">要查看在响应正文的乱数假文或**testfile1kb.txt**响应，你将看到文本是压缩且不可读。</span><span class="sxs-lookup"><span data-stu-id="b8be1-120">When you look at the response body for the Lorem Ipsum or **testfile1kb.txt** response, you see that the text is compressed and unreadable.</span></span>
1. <span data-ttu-id="b8be1-121">添加`Accept-Encoding: mycustomcompression`标头并记下响应标头。</span><span class="sxs-lookup"><span data-stu-id="b8be1-121">Add an `Accept-Encoding: mycustomcompression` header and note the response headers.</span></span> <span data-ttu-id="b8be1-122">`CustomCompressionProvider`是一个空实现，实际上不会压缩响应，但您可以创建自定义压缩流包装器`CreateStream()`方法。</span><span class="sxs-lookup"><span data-stu-id="b8be1-122">The `CustomCompressionProvider` is an empty implementation that doesn't actually compress the response, but you can create a custom compression stream wrapper for the `CreateStream()` method.</span></span>

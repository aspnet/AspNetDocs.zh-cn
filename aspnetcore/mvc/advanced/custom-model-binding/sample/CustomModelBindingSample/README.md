---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059634"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="96c0f-101">自定义模型绑定演示</span><span class="sxs-lookup"><span data-stu-id="96c0f-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="96c0f-102">通过运行应用并将 base64 编码的字符串发布至 `ImageController` 终结点 (`/api/image/`) 测试 `ByteArrayModelBinder`。</span><span class="sxs-lookup"><span data-stu-id="96c0f-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="96c0f-103">请在请求正文中将文件和文件名属性指定为表单数据（使用 [Postman](https://www.getpostman.com/) 或类似的工具）。</span><span class="sxs-lookup"><span data-stu-id="96c0f-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="96c0f-104">可以使用[本示例字符串](Base64String.txt)。</span><span class="sxs-lookup"><span data-stu-id="96c0f-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="96c0f-105">结果将以指定的文件名保存在 wwwroot/images/upload 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="96c0f-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="96c0f-106">若要测试自定义绑定示例，请尝试以下终结点：</span><span class="sxs-lookup"><span data-stu-id="96c0f-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="96c0f-107">/api/authors/1</span><span class="sxs-lookup"><span data-stu-id="96c0f-107">/api/authors/1</span></span>
* <span data-ttu-id="96c0f-108">/api/authors/2（未找到）</span><span class="sxs-lookup"><span data-stu-id="96c0f-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="96c0f-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="96c0f-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="96c0f-110">/api/boundauthors/2（未找到）</span><span class="sxs-lookup"><span data-stu-id="96c0f-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="96c0f-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="96c0f-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="96c0f-112">/api/boundauthors/get/2（无内容）&ndash; 此操作不检查 null，并返回“404 未找到”。</span><span class="sxs-lookup"><span data-stu-id="96c0f-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>

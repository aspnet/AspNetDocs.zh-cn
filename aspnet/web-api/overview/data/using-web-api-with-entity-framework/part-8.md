---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 显示项详细信息 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449000"
---
# <a name="display-item-details"></a><span data-ttu-id="3dd50-102">显示项详细信息</span><span class="sxs-lookup"><span data-stu-id="3dd50-102">Display Item Details</span></span>

<span data-ttu-id="3dd50-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3dd50-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="3dd50-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="3dd50-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="3dd50-105">在本部分中，你将添加查看每个书籍的详细信息的能力。</span><span class="sxs-lookup"><span data-stu-id="3dd50-105">In this section, you will add the ability to view details for each book.</span></span> <span data-ttu-id="3dd50-106">在 node.js 中，将以下代码添加到视图模型：</span><span class="sxs-lookup"><span data-stu-id="3dd50-106">In app.js, add to the following code to the view model:</span></span>

[!code-javascript[Main](part-8/samples/sample1.js)]

<span data-ttu-id="3dd50-107">在 Views/Home/索引中，将数据绑定元素添加到详细信息链接：</span><span class="sxs-lookup"><span data-stu-id="3dd50-107">In Views/Home/Index.cshtml, add a data-bind element to the Details link:</span></span>

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

<span data-ttu-id="3dd50-108">这会将 &lt;&gt; 元素的 click 处理程序绑定到视图模型上的 `getBookDetail` 函数。</span><span class="sxs-lookup"><span data-stu-id="3dd50-108">This binds the click handler for the &lt;a&gt; element to the `getBookDetail` function on the view model.</span></span>

<span data-ttu-id="3dd50-109">在同一文件中，替换以下标记：</span><span class="sxs-lookup"><span data-stu-id="3dd50-109">In the same file, replace the following mark-up:</span></span>

[!code-html[Main](part-8/samples/sample3.html)]

<span data-ttu-id="3dd50-110">替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="3dd50-110">with this:</span></span>

[!code-html[Main](part-8/samples/sample4.html)]

<span data-ttu-id="3dd50-111">此标记创建一个表，该表绑定到视图模型中的 `detail` 的属性。</span><span class="sxs-lookup"><span data-stu-id="3dd50-111">This markup creates a table that is data-bound to the properties of the `detail` observable in the view model.</span></span>

<span data-ttu-id="3dd50-112">"&lt;!--ko&gt;&quot; 语法允许在 DOM 元素之外包含挖空绑定。</span><span class="sxs-lookup"><span data-stu-id="3dd50-112">The "&lt;!-- ko --&gt;&quot; syntax lets you include a Knockout binding outside of a DOM element.</span></span> <span data-ttu-id="3dd50-113">在这种情况下，仅当 `details` 为非 null 时，`if` 绑定才会显示此部分标记。</span><span class="sxs-lookup"><span data-stu-id="3dd50-113">In this case, the `if` binding causes this section of markup to be displayed only when `details` is non-null.</span></span>

[!code-html[Main](part-8/samples/sample5.html)]

<span data-ttu-id="3dd50-114">现在，如果运行应用并单击 &quot;详细信息&quot; 链接之一，该应用将显示书籍详细信息。</span><span class="sxs-lookup"><span data-stu-id="3dd50-114">Now if you run the app and click one of the &quot;Detail&quot; links, the app will display the book details.</span></span>

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> <span data-ttu-id="3dd50-115">[上一页](part-7.md)
> [下一页](part-9.md)</span><span class="sxs-lookup"><span data-stu-id="3dd50-115">[Previous](part-7.md)
[Next](part-9.md)</span></span>

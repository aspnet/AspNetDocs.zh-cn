---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: OData v4 中的打开类型，带有ASP.NET Web API |微软文档
author: rick-anderson
description: 在 OData v4 中，除了类型定义中声明的任何属性外，开放类型是包含动态属性的结构化类型。 打开...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543725"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="2c80e-104">oData v4 中的打开类型，具有ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2c80e-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="2c80e-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2c80e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2c80e-106">在 OData v4 中，除了类型定义中声明的任何属性外，*开放类型*是包含动态属性的结构化类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="2c80e-107">打开类型可让您为数据模型增加灵活性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="2c80e-108">本教程演示如何在 Web API OData ASP.NET中使用开放类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="2c80e-109">本教程假定您已经知道如何在ASP.NET Web API 中创建 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="2c80e-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="2c80e-110">如果没有，请首先读取["创建 OData v4 终结点](create-an-odata-v4-endpoint.md)"。</span><span class="sxs-lookup"><span data-stu-id="2c80e-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2c80e-111">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="2c80e-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="2c80e-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="2c80e-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="2c80e-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="2c80e-113">OData v4</span></span>

<span data-ttu-id="2c80e-114">首先，一些 OData 术语：</span><span class="sxs-lookup"><span data-stu-id="2c80e-114">First, some OData terminology:</span></span>

- <span data-ttu-id="2c80e-115">实体类型：具有键的结构化类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="2c80e-116">复杂类型：没有键的结构化类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="2c80e-117">打开类型：具有动态属性的类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="2c80e-118">实体类型和复杂类型都可以打开。</span><span class="sxs-lookup"><span data-stu-id="2c80e-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="2c80e-119">动态属性的值可以是基元类型、复杂类型或枚举类型;因此，动态属性的值可以是基元类型、复杂类型或枚举类型。或任何这些类型的集合。</span><span class="sxs-lookup"><span data-stu-id="2c80e-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="2c80e-120">有关打开类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="2c80e-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="2c80e-121">安装 Web OData 库</span><span class="sxs-lookup"><span data-stu-id="2c80e-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="2c80e-122">使用 NuGet 包管理器安装最新的 Web API OData 库。</span><span class="sxs-lookup"><span data-stu-id="2c80e-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="2c80e-123">从“程序包管理器控制台”窗口：</span><span class="sxs-lookup"><span data-stu-id="2c80e-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="2c80e-124">定义 CLR 类型</span><span class="sxs-lookup"><span data-stu-id="2c80e-124">Define the CLR Types</span></span>

<span data-ttu-id="2c80e-125">首先将 EDM 模型定义为 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="2c80e-126">创建实体数据模型 （EDM） 时，</span><span class="sxs-lookup"><span data-stu-id="2c80e-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="2c80e-127">`Category`是枚举类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="2c80e-128">`Address`是一种复杂的类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-128">`Address` is a complex type.</span></span> <span data-ttu-id="2c80e-129">（它没有密钥，因此它不是实体类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="2c80e-130">`Customer`是实体类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-130">`Customer` is an entity type.</span></span> <span data-ttu-id="2c80e-131">（它有一个键。</span><span class="sxs-lookup"><span data-stu-id="2c80e-131">(It has a key.)</span></span>
- <span data-ttu-id="2c80e-132">`Press`是一种开放的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="2c80e-133">`Book`是打开的实体类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="2c80e-134">要创建打开类型，CLR 类型必须具有类型 属性`IDictionary<string, object>`，该属性包含动态属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="2c80e-135">构建 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="2c80e-135">Build the EDM Model</span></span>

<span data-ttu-id="2c80e-136">如果使用**ODataConventionModelBuilder**创建 EDM，`Press`并且`Book`根据`IDictionary<string, object>`属性的存在自动添加为打开类型。</span><span class="sxs-lookup"><span data-stu-id="2c80e-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="2c80e-137">您还可以使用**ODataModelBuilder**显式构建 EDM。</span><span class="sxs-lookup"><span data-stu-id="2c80e-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="2c80e-138">添加 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="2c80e-138">Add an OData Controller</span></span>

<span data-ttu-id="2c80e-139">接下来，添加 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="2c80e-139">Next, add an OData controller.</span></span> <span data-ttu-id="2c80e-140">在本教程中，我们将使用一个简化的控制器，该控制器仅支持 GET 和 POST 请求，并使用内存中列表来存储实体。</span><span class="sxs-lookup"><span data-stu-id="2c80e-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="2c80e-141">请注意，第一`Book`个实例没有动态属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="2c80e-142">第二`Book`个实例具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="2c80e-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="2c80e-143">"已发布"：原始类型</span><span class="sxs-lookup"><span data-stu-id="2c80e-143">"Published": Primitive type</span></span>
- <span data-ttu-id="2c80e-144">"作者"：基元类型的集合</span><span class="sxs-lookup"><span data-stu-id="2c80e-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="2c80e-145">"其他类别"：枚举类型的集合。</span><span class="sxs-lookup"><span data-stu-id="2c80e-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="2c80e-146">此外，该`Press``Book`实例的属性具有以下动态属性：</span><span class="sxs-lookup"><span data-stu-id="2c80e-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="2c80e-147">"博客"：原始类型</span><span class="sxs-lookup"><span data-stu-id="2c80e-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="2c80e-148">"地址"：复杂类型</span><span class="sxs-lookup"><span data-stu-id="2c80e-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="2c80e-149">查询元数据</span><span class="sxs-lookup"><span data-stu-id="2c80e-149">Query the Metadata</span></span>

<span data-ttu-id="2c80e-150">要获取 OData 元数据文档，请向`~/$metadata`发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="2c80e-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="2c80e-151">响应正文应如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c80e-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="2c80e-152">从元数据文档中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="2c80e-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="2c80e-153">对于`Book`和`Press`类型，`OpenType`属性的值为 true。</span><span class="sxs-lookup"><span data-stu-id="2c80e-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="2c80e-154">`Customer`和`Address`类型没有此属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="2c80e-155">实体`Book`类型具有三个声明属性：ISBN、标题和新闻。</span><span class="sxs-lookup"><span data-stu-id="2c80e-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="2c80e-156">OData 元数据不包括 CLR`Book.Properties`类中的属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="2c80e-157">同样，`Press`复杂类型只有两个声明的属性：名称和类别。</span><span class="sxs-lookup"><span data-stu-id="2c80e-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="2c80e-158">元数据不包括来自 CLR`Press.DynamicProperties`类的属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="2c80e-159">查询实体</span><span class="sxs-lookup"><span data-stu-id="2c80e-159">Query an Entity</span></span>

<span data-ttu-id="2c80e-160">要将 ISBN 的书等于"978-0-7356-7942-9"，请向`~/Books('978-0-7356-7942-9')`发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="2c80e-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="2c80e-161">响应正文应类似于以下内容。</span><span class="sxs-lookup"><span data-stu-id="2c80e-161">The response body should look similar to the following.</span></span> <span data-ttu-id="2c80e-162">（缩进使其更具可读性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="2c80e-163">请注意，动态属性与声明的属性一致。</span><span class="sxs-lookup"><span data-stu-id="2c80e-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="2c80e-164">从实体开始发布</span><span class="sxs-lookup"><span data-stu-id="2c80e-164">POST an Entity</span></span>

<span data-ttu-id="2c80e-165">要添加图书实体，请向`~/Books`发送 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="2c80e-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="2c80e-166">客户端可以在请求负载中设置动态属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="2c80e-167">下面是一个示例请求。</span><span class="sxs-lookup"><span data-stu-id="2c80e-167">Here is an example request.</span></span> <span data-ttu-id="2c80e-168">请注意"价格"和"已发布"属性。</span><span class="sxs-lookup"><span data-stu-id="2c80e-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="2c80e-169">如果在控制器方法中设置了断点，则可以看到 Web API 将这些属性添加到字典中`Properties`。</span><span class="sxs-lookup"><span data-stu-id="2c80e-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="2c80e-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="2c80e-170">Additional Resources</span></span>

[<span data-ttu-id="2c80e-171">O数据打开类型示例</span><span class="sxs-lookup"><span data-stu-id="2c80e-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)

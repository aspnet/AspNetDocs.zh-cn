---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 支持带有 Web API 2 的 OData v3 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。 使用 OData，客户端可以导航到 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600315"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="14d27-104">支持带有 Web API 2 的 OData v3 中的实体关系</span><span class="sxs-lookup"><span data-stu-id="14d27-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="14d27-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="14d27-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="14d27-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="14d27-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="14d27-107">大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。</span><span class="sxs-lookup"><span data-stu-id="14d27-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="14d27-108">使用 OData，客户端可在实体关系上导航。</span><span class="sxs-lookup"><span data-stu-id="14d27-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="14d27-109">在给定产品的情况下，您可以找到该供应商。</span><span class="sxs-lookup"><span data-stu-id="14d27-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="14d27-110">您还可以创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="14d27-110">You can also create or remove relationships.</span></span> <span data-ttu-id="14d27-111">例如，可以设置产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="14d27-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="14d27-112">本教程演示如何在 ASP.NET Web API 中支持这些操作。</span><span class="sxs-lookup"><span data-stu-id="14d27-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="14d27-113">本教程基于[使用 WEB API 2 创建 OData V3 终结点](creating-an-odata-endpoint.md)教程。</span><span class="sxs-lookup"><span data-stu-id="14d27-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="14d27-114">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="14d27-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="14d27-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="14d27-115">Web API 2</span></span>
> - <span data-ttu-id="14d27-116">OData 版本3</span><span class="sxs-lookup"><span data-stu-id="14d27-116">OData Version 3</span></span>
> - <span data-ttu-id="14d27-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="14d27-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="14d27-118">添加供应商实体</span><span class="sxs-lookup"><span data-stu-id="14d27-118">Add a Supplier Entity</span></span>

<span data-ttu-id="14d27-119">首先，我们需要将新的实体类型添加到 OData 源。</span><span class="sxs-lookup"><span data-stu-id="14d27-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="14d27-120">我们将添加一个 `Supplier` 类。</span><span class="sxs-lookup"><span data-stu-id="14d27-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="14d27-121">此类使用实体键的字符串。</span><span class="sxs-lookup"><span data-stu-id="14d27-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="14d27-122">在实践中，这种做法可能不如使用整数键常见。</span><span class="sxs-lookup"><span data-stu-id="14d27-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="14d27-123">但值得注意的是，OData 如何处理除整数以外的其他密钥类型。</span><span class="sxs-lookup"><span data-stu-id="14d27-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="14d27-124">接下来，我们将通过向 `Product` 类添加 `Supplier` 属性来创建一个关系：</span><span class="sxs-lookup"><span data-stu-id="14d27-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="14d27-125">将新的**DbSet**添加到 `ProductServiceContext` 类中，以便实体框架将 `Supplier` 表包括在数据库中。</span><span class="sxs-lookup"><span data-stu-id="14d27-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="14d27-126">在 WebApiConfig.cs 中，将 "供应商" 实体添加到 EDM 模型：</span><span class="sxs-lookup"><span data-stu-id="14d27-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="14d27-127">导航属性</span><span class="sxs-lookup"><span data-stu-id="14d27-127">Navigation Properties</span></span>

<span data-ttu-id="14d27-128">若要获取产品的供应商，客户端将发送 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="14d27-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="14d27-129">此处的 "供应商" 是 `Product` 类型的导航属性。</span><span class="sxs-lookup"><span data-stu-id="14d27-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="14d27-130">在这种情况下，`Supplier` 引用单个项，但导航属性还可以返回集合（一对多或多对多关系）。</span><span class="sxs-lookup"><span data-stu-id="14d27-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="14d27-131">若要支持此请求，请将以下方法添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="14d27-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="14d27-132">*Key*参数是产品的键。</span><span class="sxs-lookup"><span data-stu-id="14d27-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="14d27-133">此方法在此示例中&#8212;返回相关实体，即一个 `Supplier` 实例。</span><span class="sxs-lookup"><span data-stu-id="14d27-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="14d27-134">方法名称和参数名称都是重要的。</span><span class="sxs-lookup"><span data-stu-id="14d27-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="14d27-135">通常，如果导航属性名为 "X"，则需要添加一个名为 "GetX" 的方法。</span><span class="sxs-lookup"><span data-stu-id="14d27-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="14d27-136">此方法必须采用一个名为 "*key*" 的参数，该参数与父项的键的数据类型匹配。</span><span class="sxs-lookup"><span data-stu-id="14d27-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="14d27-137">还必须在*key*参数中包含 **[FromOdataUri]** 属性。</span><span class="sxs-lookup"><span data-stu-id="14d27-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="14d27-138">此属性告知 Web API 在分析来自请求 URI 的密钥时使用 OData 语法规则。</span><span class="sxs-lookup"><span data-stu-id="14d27-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="14d27-139">创建和删除链接</span><span class="sxs-lookup"><span data-stu-id="14d27-139">Creating and Deleting Links</span></span>

<span data-ttu-id="14d27-140">OData 支持在两个实体之间创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="14d27-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="14d27-141">在 OData 术语中，关系是一个 "链接"。</span><span class="sxs-lookup"><span data-stu-id="14d27-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="14d27-142">每个链接都有一个 URI，其形式为*entity*/$links/*entity*。</span><span class="sxs-lookup"><span data-stu-id="14d27-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="14d27-143">例如，从产品到供应商的链接如下所示：</span><span class="sxs-lookup"><span data-stu-id="14d27-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="14d27-144">若要创建新链接，客户端会将 POST 请求发送到链接 URI。</span><span class="sxs-lookup"><span data-stu-id="14d27-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="14d27-145">请求正文是目标实体的 URI。</span><span class="sxs-lookup"><span data-stu-id="14d27-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="14d27-146">例如，假设有一个供应商的密钥为 "CTSO"。</span><span class="sxs-lookup"><span data-stu-id="14d27-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="14d27-147">若要创建从 "Product （1）" 到 "CTSO"）的链接，客户端将发送如下请求：</span><span class="sxs-lookup"><span data-stu-id="14d27-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="14d27-148">若要删除链接，客户端会将删除请求发送到链接 URI。</span><span class="sxs-lookup"><span data-stu-id="14d27-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="14d27-149">**创建链接**</span><span class="sxs-lookup"><span data-stu-id="14d27-149">**Creating Links**</span></span>

<span data-ttu-id="14d27-150">若要允许客户端创建产品供应商链接，请将以下代码添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="14d27-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="14d27-151">该方法采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="14d27-151">This method takes three parameters:</span></span>

- <span data-ttu-id="14d27-152">*key*：父实体（产品）的键</span><span class="sxs-lookup"><span data-stu-id="14d27-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="14d27-153">*navigationProperty*：导航属性的名称。</span><span class="sxs-lookup"><span data-stu-id="14d27-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="14d27-154">在此示例中，唯一有效的导航属性为 "供应商"。</span><span class="sxs-lookup"><span data-stu-id="14d27-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="14d27-155">*link*：相关实体的 OData URI。</span><span class="sxs-lookup"><span data-stu-id="14d27-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="14d27-156">此值取自请求正文。</span><span class="sxs-lookup"><span data-stu-id="14d27-156">This value is taken from the request body.</span></span> <span data-ttu-id="14d27-157">例如，链接 URI 可以是 "`http://localhost/odata/Suppliers('CTSO')`，这意味着 ID =" CTSO "的供应商。</span><span class="sxs-lookup"><span data-stu-id="14d27-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="14d27-158">方法使用链接查找供应商。</span><span class="sxs-lookup"><span data-stu-id="14d27-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="14d27-159">如果找到匹配的供应商，则方法将设置 `Product.Supplier` 属性，并将结果保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="14d27-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="14d27-160">最难的部分是分析链接 URI。</span><span class="sxs-lookup"><span data-stu-id="14d27-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="14d27-161">基本上，需要模拟将 GET 请求发送到该 URI 的结果。</span><span class="sxs-lookup"><span data-stu-id="14d27-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="14d27-162">以下帮助器方法显示了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="14d27-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="14d27-163">方法调用 Web API 路由进程，并返回表示已分析 OData 路径的**ODataPath**实例。</span><span class="sxs-lookup"><span data-stu-id="14d27-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="14d27-164">对于链接 URI，其中一个段应为实体键。</span><span class="sxs-lookup"><span data-stu-id="14d27-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="14d27-165">（如果不是，则客户端发送了错误的 URI。）</span><span class="sxs-lookup"><span data-stu-id="14d27-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="14d27-166">**删除链接**</span><span class="sxs-lookup"><span data-stu-id="14d27-166">**Deleting Links**</span></span>

<span data-ttu-id="14d27-167">若要删除链接，请将以下代码添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="14d27-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="14d27-168">在此示例中，导航属性是单个 `Supplier` 实体。</span><span class="sxs-lookup"><span data-stu-id="14d27-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="14d27-169">如果导航属性是集合，则用于删除链接的 URI 必须包含相关实体的键。</span><span class="sxs-lookup"><span data-stu-id="14d27-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="14d27-170">例如：</span><span class="sxs-lookup"><span data-stu-id="14d27-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="14d27-171">此请求从客户1中删除订单1。</span><span class="sxs-lookup"><span data-stu-id="14d27-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="14d27-172">在这种情况下，DeleteLink 方法将具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="14d27-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="14d27-173">*RelatedKey*参数为相关实体提供密钥。</span><span class="sxs-lookup"><span data-stu-id="14d27-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="14d27-174">因此，在 `DeleteLink` 方法中，按*键*参数查找主实体，通过*relatedKey*参数查找相关实体，然后删除关联。</span><span class="sxs-lookup"><span data-stu-id="14d27-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="14d27-175">可能需要实现 `DeleteLink`的两个版本，具体取决于您的数据模型。</span><span class="sxs-lookup"><span data-stu-id="14d27-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="14d27-176">Web API 将根据请求 URI 调用正确的版本。</span><span class="sxs-lookup"><span data-stu-id="14d27-176">Web API will call the correct version based on the request URI.</span></span>

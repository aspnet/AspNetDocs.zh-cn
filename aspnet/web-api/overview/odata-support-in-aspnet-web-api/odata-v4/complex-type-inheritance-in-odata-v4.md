---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 使用ASP.NET Web API 的 OData v4 中的复杂类型继承 |微软文档
author: rick-anderson
description: 根据 OData v4 规范，复杂类型可以从另一种复杂类型继承。 （复杂类型是无键的结构化类型。Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543595"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="836d3-104">使用ASP.NET Web API 的 OData v4 中的复杂类型继承</span><span class="sxs-lookup"><span data-stu-id="836d3-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="836d3-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="836d3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="836d3-106">根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，复杂类型可以从另一种复杂类型继承。</span><span class="sxs-lookup"><span data-stu-id="836d3-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="836d3-107">（*复杂*类型是无键的结构化类型。Web API OData 5.3 支持复杂的类型继承。</span><span class="sxs-lookup"><span data-stu-id="836d3-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="836d3-108">本主题演示如何构建具有复杂继承类型的实体数据模型 （EDM）。</span><span class="sxs-lookup"><span data-stu-id="836d3-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="836d3-109">有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="836d3-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="836d3-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="836d3-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="836d3-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="836d3-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="836d3-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="836d3-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="836d3-113">模型层次结构</span><span class="sxs-lookup"><span data-stu-id="836d3-113">Model Hierarchy</span></span>

<span data-ttu-id="836d3-114">为了说明复杂的类型继承，我们将使用以下类层次结构。</span><span class="sxs-lookup"><span data-stu-id="836d3-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="836d3-115">`Shape`是一种抽象的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="836d3-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="836d3-116">`Rectangle``Triangle`和`Circle`是从 派生`Shape`的复杂类型，并且`RoundRectangle`派生自`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="836d3-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="836d3-117">`Window`是实体类型，包含实例`Shape`。</span><span class="sxs-lookup"><span data-stu-id="836d3-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="836d3-118">下面是定义这些类型的 CLR 类。</span><span class="sxs-lookup"><span data-stu-id="836d3-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="836d3-119">构建 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="836d3-119">Build the EDM Model</span></span>

<span data-ttu-id="836d3-120">要创建 EDM，可以使用**ODataConventionModelBuilder**，它推断出 CLR 类型的继承关系。</span><span class="sxs-lookup"><span data-stu-id="836d3-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="836d3-121">您还可以使用**ODataModelBuilder**显式构建 EDM。</span><span class="sxs-lookup"><span data-stu-id="836d3-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="836d3-122">这需要更多的代码，但使您能够对 EDM 进行更多的控制。</span><span class="sxs-lookup"><span data-stu-id="836d3-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="836d3-123">这两个示例创建相同的 EDM 架构。</span><span class="sxs-lookup"><span data-stu-id="836d3-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="836d3-124">元数据文档</span><span class="sxs-lookup"><span data-stu-id="836d3-124">Metadata Document</span></span>

<span data-ttu-id="836d3-125">下面是 OData 元数据文档，显示复杂的类型继承。</span><span class="sxs-lookup"><span data-stu-id="836d3-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="836d3-126">从元数据文档中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="836d3-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="836d3-127">复杂`Shape`类型是抽象的。</span><span class="sxs-lookup"><span data-stu-id="836d3-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="836d3-128">`Triangle`和`Rectangle``Circle`复合类型具有基类型`Shape`。</span><span class="sxs-lookup"><span data-stu-id="836d3-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="836d3-129">类型`RoundRectangle`具有基类型`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="836d3-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="836d3-130">铸造复杂类型</span><span class="sxs-lookup"><span data-stu-id="836d3-130">Casting Complex Types</span></span>

<span data-ttu-id="836d3-131">现在支持对复杂类型的强制转换。</span><span class="sxs-lookup"><span data-stu-id="836d3-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="836d3-132">例如，以下查询将 转换为`Shape`。 `Rectangle`</span><span class="sxs-lookup"><span data-stu-id="836d3-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="836d3-133">下面是响应负载：</span><span class="sxs-lookup"><span data-stu-id="836d3-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]

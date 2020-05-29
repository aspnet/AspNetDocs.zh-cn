---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: 使用 Web API 2.2 的 OData v4 中的包含 |Microsoft Docs
author: rick-anderson
description: 通常，仅当实体封装在实体集内时，才能访问该实体。 但 OData v4 提供两个附加选项：单一实例和 Con .。。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172999"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="68d7e-104">使用 Web API 2.2 的 OData v4 中的包容</span><span class="sxs-lookup"><span data-stu-id="68d7e-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="68d7e-105">作者： Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="68d7e-105">by Jinfu Tan</span></span>

> <span data-ttu-id="68d7e-106">通常，仅当实体封装在实体集内时，才能访问该实体。</span><span class="sxs-lookup"><span data-stu-id="68d7e-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="68d7e-107">但 OData v4 提供了两个额外的选项，即 Singleton 和包容，两者都支持 WebAPI 2.2。</span><span class="sxs-lookup"><span data-stu-id="68d7e-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="68d7e-108">本主题说明如何在 WebApi 2.2 的 OData 终结点中定义包含。</span><span class="sxs-lookup"><span data-stu-id="68d7e-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="68d7e-109">有关包含的详细信息，请参阅包含的内容[为 OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/)。</span><span class="sxs-lookup"><span data-stu-id="68d7e-109">For more information about containment, see [Containment is coming with OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span></span> <span data-ttu-id="68d7e-110">若要在 Web API 中创建 OData V4 终结点，请参阅[使用 ASP.NET Web API 2.2 创建 odata V4 终结点](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="68d7e-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="68d7e-111">首先，我们将使用此数据模型在 OData 服务中创建包含域模型：</span><span class="sxs-lookup"><span data-stu-id="68d7e-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![数据模型](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="68d7e-113">帐户包含许多 PaymentInstruments （PI），但我们未定义 PI 的实体集。</span><span class="sxs-lookup"><span data-stu-id="68d7e-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="68d7e-114">相反，只能通过帐户访问 Pi。</span><span class="sxs-lookup"><span data-stu-id="68d7e-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="68d7e-115">可以从[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)下载本主题中使用的解决方案。</span><span class="sxs-lookup"><span data-stu-id="68d7e-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="68d7e-116">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="68d7e-116">Defining the data model</span></span>

1. <span data-ttu-id="68d7e-117">定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="68d7e-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="68d7e-118">`Contained`特性用于包含导航属性。</span><span class="sxs-lookup"><span data-stu-id="68d7e-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="68d7e-119">基于 CLR 类型生成 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="68d7e-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="68d7e-120">`ODataConventionModelBuilder`如果将 `Contained` 特性添加到相应的导航属性中，则将处理生成 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="68d7e-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="68d7e-121">如果该属性是集合类型，则 `GetCount(string NameContains)` 还将创建一个函数。</span><span class="sxs-lookup"><span data-stu-id="68d7e-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="68d7e-122">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="68d7e-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="68d7e-123">`ContainsTarget`属性指示导航属性是一个包含。</span><span class="sxs-lookup"><span data-stu-id="68d7e-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="68d7e-124">定义包含实体集控制器</span><span class="sxs-lookup"><span data-stu-id="68d7e-124">Define the containing entity set controller</span></span>

<span data-ttu-id="68d7e-125">包含的实体没有自己的控制器;操作是在包含实体集控制器中定义的。</span><span class="sxs-lookup"><span data-stu-id="68d7e-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="68d7e-126">在此示例中，有一个 AccountsController，但没有 PaymentInstrumentsController。</span><span class="sxs-lookup"><span data-stu-id="68d7e-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="68d7e-127">如果 OData 路径为4个或更多个段，则只能使用特性路由，如 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 以上控制器中所示。</span><span class="sxs-lookup"><span data-stu-id="68d7e-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="68d7e-128">否则，特性和常规路由都适用：例如， `GetPayInPIs(int key)` 匹配 `GET ~/Accounts(1)/PayinPIs` 。</span><span class="sxs-lookup"><span data-stu-id="68d7e-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="68d7e-129">*感谢在本文的原始内容中 Leo 的。*</span><span class="sxs-lookup"><span data-stu-id="68d7e-129">*Thanks to Leo Hu for the original content of this article.*</span></span>

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
# <a name="containment-in-odata-v4-using-web-api-22"></a>使用 Web API 2.2 的 OData v4 中的包容

作者： Jinfu Tan

> 通常，仅当实体封装在实体集内时，才能访问该实体。 但 OData v4 提供了两个额外的选项，即 Singleton 和包容，两者都支持 WebAPI 2.2。

本主题说明如何在 WebApi 2.2 的 OData 终结点中定义包含。 有关包含的详细信息，请参阅包含的内容[为 OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/)。 若要在 Web API 中创建 OData V4 终结点，请参阅[使用 ASP.NET Web API 2.2 创建 odata V4 终结点](create-an-odata-v4-endpoint.md)。

首先，我们将使用此数据模型在 OData 服务中创建包含域模型：

![数据模型](odata-containment-in-web-api-22/_static/image1.png)

帐户包含许多 PaymentInstruments （PI），但我们未定义 PI 的实体集。 相反，只能通过帐户访问 Pi。

可以从[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)下载本主题中使用的解决方案。

## <a name="defining-the-data-model"></a>定义数据模型

1. 定义 CLR 类型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`特性用于包含导航属性。
2. 基于 CLR 类型生成 EDM 模型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder`如果将 `Contained` 特性添加到相应的导航属性中，则将处理生成 EDM 模型。 如果该属性是集合类型，则 `GetCount(string NameContains)` 还将创建一个函数。

    生成的元数据将如下所示：

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`属性指示导航属性是一个包含。

## <a name="define-the-containing-entity-set-controller"></a>定义包含实体集控制器

包含的实体没有自己的控制器;操作是在包含实体集控制器中定义的。 在此示例中，有一个 AccountsController，但没有 PaymentInstrumentsController。

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

如果 OData 路径为4个或更多个段，则只能使用特性路由，如 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 以上控制器中所示。 否则，特性和常规路由都适用：例如， `GetPayInPIs(int key)` 匹配 `GET ~/Accounts(1)/PayinPIs` 。

*感谢在本文的原始内容中 Leo 的。*

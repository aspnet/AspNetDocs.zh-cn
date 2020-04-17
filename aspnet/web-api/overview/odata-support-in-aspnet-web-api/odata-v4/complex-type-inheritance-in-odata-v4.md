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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>使用ASP.NET Web API 的 OData v4 中的复杂类型继承

由[微软](https://github.com/microsoft)

> 根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，复杂类型可以从另一种复杂类型继承。 （*复杂*类型是无键的结构化类型。Web API OData 5.3 支持复杂的类型继承。
> 
> 本主题演示如何构建具有复杂继承类型的实体数据模型 （EDM）。 有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>模型层次结构

为了说明复杂的类型继承，我们将使用以下类层次结构。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`是一种抽象的复杂类型。 `Rectangle``Triangle`和`Circle`是从 派生`Shape`的复杂类型，并且`RoundRectangle`派生自`Rectangle`。 `Window`是实体类型，包含实例`Shape`。

下面是定义这些类型的 CLR 类。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>构建 EDM 模型

要创建 EDM，可以使用**ODataConventionModelBuilder**，它推断出 CLR 类型的继承关系。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

您还可以使用**ODataModelBuilder**显式构建 EDM。 这需要更多的代码，但使您能够对 EDM 进行更多的控制。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

这两个示例创建相同的 EDM 架构。

## <a name="metadata-document"></a>元数据文档

下面是 OData 元数据文档，显示复杂的类型继承。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

从元数据文档中，您可以看到：

- 复杂`Shape`类型是抽象的。
- `Triangle`和`Rectangle``Circle`复合类型具有基类型`Shape`。
- 类型`RoundRectangle`具有基类型`Rectangle`。

## <a name="casting-complex-types"></a>铸造复杂类型

现在支持对复杂类型的强制转换。 例如，以下查询将 转换为`Shape`。 `Rectangle`

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

下面是响应负载：

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]

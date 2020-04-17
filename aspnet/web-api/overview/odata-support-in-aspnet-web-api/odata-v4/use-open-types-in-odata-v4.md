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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>oData v4 中的打开类型，具有ASP.NET Web API

由[微软](https://github.com/microsoft)

> 在 OData v4 中，除了类型定义中声明的任何属性外，*开放类型*是包含动态属性的结构化类型。 打开类型可让您为数据模型增加灵活性。 本教程演示如何在 Web API OData ASP.NET中使用开放类型。
> 
> 本教程假定您已经知道如何在ASP.NET Web API 中创建 OData 终结点。 如果没有，请首先读取["创建 OData v4 终结点](create-an-odata-v4-endpoint.md)"。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API OData 5.3
> - OData v4

首先，一些 OData 术语：

- 实体类型：具有键的结构化类型。
- 复杂类型：没有键的结构化类型。
- 打开类型：具有动态属性的类型。 实体类型和复杂类型都可以打开。

动态属性的值可以是基元类型、复杂类型或枚举类型;因此，动态属性的值可以是基元类型、复杂类型或枚举类型。或任何这些类型的集合。 有关打开类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。

## <a name="install-the-web-odata-libraries"></a>安装 Web OData 库

使用 NuGet 包管理器安装最新的 Web API OData 库。 从“程序包管理器控制台”窗口：

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>定义 CLR 类型

首先将 EDM 模型定义为 CLR 类型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

创建实体数据模型 （EDM） 时，

- `Category`是枚举类型。
- `Address`是一种复杂的类型。 （它没有密钥，因此它不是实体类型。
- `Customer`是实体类型。 （它有一个键。
- `Press`是一种开放的复杂类型。
- `Book`是打开的实体类型。

要创建打开类型，CLR 类型必须具有类型 属性`IDictionary<string, object>`，该属性包含动态属性。

## <a name="build-the-edm-model"></a>构建 EDM 模型

如果使用**ODataConventionModelBuilder**创建 EDM，`Press`并且`Book`根据`IDictionary<string, object>`属性的存在自动添加为打开类型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

您还可以使用**ODataModelBuilder**显式构建 EDM。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>添加 OData 控制器

接下来，添加 OData 控制器。 在本教程中，我们将使用一个简化的控制器，该控制器仅支持 GET 和 POST 请求，并使用内存中列表来存储实体。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

请注意，第一`Book`个实例没有动态属性。 第二`Book`个实例具有以下动态属性：

- "已发布"：原始类型
- "作者"：基元类型的集合
- "其他类别"：枚举类型的集合。

此外，该`Press``Book`实例的属性具有以下动态属性：

- "博客"：原始类型
- "地址"：复杂类型

## <a name="query-the-metadata"></a>查询元数据

要获取 OData 元数据文档，请向`~/$metadata`发送 GET 请求。 响应正文应如下所示：

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

从元数据文档中，您可以看到：

- 对于`Book`和`Press`类型，`OpenType`属性的值为 true。 `Customer`和`Address`类型没有此属性。
- 实体`Book`类型具有三个声明属性：ISBN、标题和新闻。 OData 元数据不包括 CLR`Book.Properties`类中的属性。
- 同样，`Press`复杂类型只有两个声明的属性：名称和类别。 元数据不包括来自 CLR`Press.DynamicProperties`类的属性。

## <a name="query-an-entity"></a>查询实体

要将 ISBN 的书等于"978-0-7356-7942-9"，请向`~/Books('978-0-7356-7942-9')`发送 GET 请求。 响应正文应类似于以下内容。 （缩进使其更具可读性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

请注意，动态属性与声明的属性一致。

## <a name="post-an-entity"></a>从实体开始发布

要添加图书实体，请向`~/Books`发送 POST 请求。 客户端可以在请求负载中设置动态属性。

下面是一个示例请求。 请注意"价格"和"已发布"属性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

如果在控制器方法中设置了断点，则可以看到 Web API 将这些属性添加到字典中`Properties`。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>其他资源

[O数据打开类型示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)

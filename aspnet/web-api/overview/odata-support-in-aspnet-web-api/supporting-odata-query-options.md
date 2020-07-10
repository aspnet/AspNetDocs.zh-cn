---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2-ASP.NET 4.x 中支持的 OData 查询选项
author: MikeWasson
description: 概述 "代码示例" 显示 ASP.NET 4.x ASP.NET Web API 2 中支持的 OData 查询选项。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188605"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中支持的 OData 查询选项

作者： [Mike Wasson](https://github.com/MikeWasson)

本概述与代码示例演示了 ASP.NET Web API 2 for ASP.NET 4.x 中支持的 OData 查询选项。 

OData 定义可用于修改 OData 查询的参数。 客户端将这些参数发送到请求 URI 的查询字符串中。 例如，若要对结果进行排序，客户端将使用 $orderby 参数：

`http://localhost/Products?$orderby=Name`

OData 规范调用这些参数*查询选项*。 可以为项目中的任何 Web API 控制器启用 OData 查询选项 &#8212; 控制器无需成为 OData 终结点。 这为你提供了一种简便的方法来向任意 Web API 应用程序添加功能，如筛选和排序。

在启用查询选项之前，请阅读[OData 安全指南](odata-security-guidance.md)主题。

- [启用 OData 查询选项](#enable)
- [示例查询](#examples)
- [服务器驱动的分页](#server-paging)
- [限制查询选项](#limiting_query_options)
- [直接调用查询选项](#ODataQueryOptions)
- [查询验证](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>启用 OData 查询选项

Web API 支持以下 OData 查询选项：

| 选项 | 说明 |
| --- | --- |
| $expand | 以内联方式展开相关实体。 |
| $filter | 根据布尔条件筛选结果。 |
| $inlinecount | 通知服务器在响应中包括匹配实体的总数。  (适用于服务器端分页。 )  |
| $orderby | 对结果进行排序。 |
| $select | 选择要包括在响应中的属性。 |
| $skip | 跳过前 n 个结果。 |
| $top | 仅返回结果的前 n 个。 |

若要使用 OData 查询选项，则必须显式启用它们。 你可以为整个应用程序全局启用它们，也可以为特定控制器或特定操作启用它们。

若要全局启用 OData 查询选项，请在启动时调用**HttpConfiguration**类上的**EnableQuerySupport** ：

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**EnableQuerySupport**方法为返回**IQueryable**类型的任何控制器操作全局启用查询选项。 如果你不希望为整个应用程序启用查询选项，则可以通过将 **[可查询]** 特性添加到操作方法来为特定控制器操作启用查询选项。

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>查询示例

本部分介绍使用 OData 查询选项可以使用的查询类型。 有关查询选项的特定详细信息，请参阅[www.odata.org](http://www.odata.org/)上的 OData 文档。

有关 $expand 和 $select 的信息，请参阅[$Value OData 中的使用 $select、$expand 和 ASP.NET Web API](using-select-expand-and-value.md)。

**客户端驱动的分页**

对于大型实体集，客户端可能需要限制结果的数目。 例如，客户端一次可能会显示10个条目，其中包含 "下一步" 链接以获取下一页结果。 为此，客户端使用 $top 和 $skip 选项。

`http://localhost/Products?$top=10&$skip=20`

$Top 选项提供返回的最大项数，而 $skip 选项提供要跳过的项数。 前面的示例提取条目21到30。

**筛选**

$Filter 选项允许客户端通过应用布尔表达式来筛选结果。 筛选器表达式非常强大;它们包括逻辑运算符和算术运算符、字符串函数和日期函数。

| 返回类别等于 "玩具" 的所有产品。 | `http://localhost/Products?$filter=Category`eq "玩具" |
| --- | --- |
| 返回价格小于10的所有产品。 | `http://localhost/Products?$filter=Price`lt 10 |
| 逻辑运算符：返回价格 >= 5 并且价格 <= 15 的所有产品。 | `http://localhost/Products?$filter=Price`ge 5 和价格 le 15 |
| 字符串函数：返回名称中包含 "zz" 的所有产品。 | `http://localhost/Products?$filter=substringof('zz',Name)` |
| 日期函数：在2005后返回包含 ReleaseDate 的所有产品。 | `http://localhost/Products?$filter=year(ReleaseDate)`gt 2005 |

**排序**

若要对结果进行排序，请使用 $orderby 筛选器。

| 按价格排序。 | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| 按价格降序排序 (最高到最低) 。 | `http://localhost/Products?$orderby=Price desc` |
| 按类别排序，然后按价格在类别中按降序排序。 | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>服务器驱动的分页

如果数据库包含数百万条记录，则不希望在一个有效负载中发送所有记录。 若要防止出现这种情况，服务器可以限制在单个响应中发送的条目数。 若要启用服务器分页，请设置可**查询**属性中的**PageSize**属性。 值为要返回的最大项数。

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

如果控制器返回 OData 格式，则响应正文将包含指向下一页数据的链接：

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

客户端可以使用此链接获取下一页。 若要了解结果集中的总项数，客户端可以设置值为 "allpages" 的 $inlinecount 查询选项。

`http://localhost/Products?$inlinecount=allpages`

值 "allpages" 指示服务器在响应中包含总计数：

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> 下一页链接和内联计数都需要 OData 格式。 原因是 OData 在响应正文中定义了用于保存链接和计数的特殊字段。

对于非 OData 格式，仍可以支持下一页链接和内联计数，方法是在**PageResult &lt; T &gt; **对象中将查询结果括起来。 但是，它需要更多代码。 以下是示例：

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

下面是一个示例 JSON 响应：

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>限制查询选项

查询选项为客户端授予了对服务器上运行的查询的大量控制。 在某些情况下，出于安全或性能方面的原因，可能需要限制可用选项。 **[可查询]** 特性具有此的一些内置属性。 下面是一些示例。

仅允许 $skip 和 $top 支持分页，无其他操作：

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

仅允许按某些属性排序，以防止对未在数据库中编制索引的属性进行排序：

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

允许 "eq" 逻辑函数，但不允许其他逻辑函数：

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

不允许任何算术运算符：

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

可以通过构造**QueryableAttribute**实例并将其传递给**EnableQuerySupport**函数，全局限制选项：

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>直接调用查询选项

您可以直接在控制器中调用查询选项，而不是使用 " **[可查询]** " 属性。 为此，请将**ODataQueryOptions**参数添加到控制器方法。 在这种情况下，不需要 **[可查询]** 特性。

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Web API 从 URI 查询字符串填充**ODataQueryOptions** 。 若要应用查询，请将**IQueryable**传递到**ApplyTo**方法。 方法返回另一个**IQueryable**。

对于高级方案，如果没有**IQueryable**查询提供程序，可以检查**ODataQueryOptions**并将查询选项转换为另一种形式。  (例如，请参阅 RaghuRam Nadiminti 的博客文章[将 OData 查询转换为 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中还包括一个[示例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。 ) 

<a id="query-validation"></a>
## <a name="query-validation"></a>查询验证

[可查询 **]** 特性将在执行查询前对其进行验证。 验证步骤是在**QueryableAttribute. ValidateQuery**方法中执行的。 您还可以自定义验证过程。

另请参阅[OData 安全指南](odata-security-guidance.md)。

首先，重写在**web.config**命名空间中定义的一个验证程序类。 例如，下面的验证程序类禁用 $orderby 选项的 "desc" 选项。

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

将 **[可查询]** 特性的子类用于重写**ValidateQuery**方法。

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

然后，设置自定义属性全局或每个控制器：

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

如果直接使用**ODataQueryOptions** ，请在选项上设置验证程序：

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]

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
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188605"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="1bc81-103">ASP.NET Web API 2 中支持的 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="1bc81-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1bc81-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1bc81-105">本概述与代码示例演示了 ASP.NET Web API 2 for ASP.NET 4.x 中支持的 OData 查询选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="1bc81-106">OData 定义可用于修改 OData 查询的参数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="1bc81-107">客户端将这些参数发送到请求 URI 的查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="1bc81-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="1bc81-108">例如，若要对结果进行排序，客户端将使用 $orderby 参数：</span><span class="sxs-lookup"><span data-stu-id="1bc81-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="1bc81-109">OData 规范调用这些参数 *查询选项*。</span><span class="sxs-lookup"><span data-stu-id="1bc81-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="1bc81-110">可以为项目中的任何 Web API 控制器启用 OData 查询选项 &#8212; 控制器无需成为 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="1bc81-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="1bc81-111">这为你提供了一种简便的方法来向任意 Web API 应用程序添加功能，如筛选和排序。</span><span class="sxs-lookup"><span data-stu-id="1bc81-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="1bc81-112">在启用查询选项之前，请阅读 [OData 安全指南](odata-security-guidance.md)主题。</span><span class="sxs-lookup"><span data-stu-id="1bc81-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="1bc81-113">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="1bc81-114">示例查询</span><span class="sxs-lookup"><span data-stu-id="1bc81-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="1bc81-115">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="1bc81-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="1bc81-116">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="1bc81-117">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="1bc81-118">查询验证</span><span class="sxs-lookup"><span data-stu-id="1bc81-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="1bc81-119">启用 OData 查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-119">Enabling OData Query Options</span></span>

<span data-ttu-id="1bc81-120">Web API 支持以下 OData 查询选项：</span><span class="sxs-lookup"><span data-stu-id="1bc81-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="1bc81-121">选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-121">Option</span></span> | <span data-ttu-id="1bc81-122">说明</span><span class="sxs-lookup"><span data-stu-id="1bc81-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1bc81-123">$expand</span><span class="sxs-lookup"><span data-stu-id="1bc81-123">$expand</span></span> | <span data-ttu-id="1bc81-124">以内联方式展开相关实体。</span><span class="sxs-lookup"><span data-stu-id="1bc81-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="1bc81-125">$filter</span><span class="sxs-lookup"><span data-stu-id="1bc81-125">$filter</span></span> | <span data-ttu-id="1bc81-126">根据布尔条件筛选结果。</span><span class="sxs-lookup"><span data-stu-id="1bc81-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="1bc81-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="1bc81-127">$inlinecount</span></span> | <span data-ttu-id="1bc81-128">通知服务器在响应中包括匹配实体的总数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="1bc81-129"> (适用于服务器端分页。 ) </span><span class="sxs-lookup"><span data-stu-id="1bc81-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="1bc81-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="1bc81-130">$orderby</span></span> | <span data-ttu-id="1bc81-131">对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="1bc81-131">Sorts the results.</span></span> |
| <span data-ttu-id="1bc81-132">$select</span><span class="sxs-lookup"><span data-stu-id="1bc81-132">$select</span></span> | <span data-ttu-id="1bc81-133">选择要包括在响应中的属性。</span><span class="sxs-lookup"><span data-stu-id="1bc81-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="1bc81-134">$skip</span><span class="sxs-lookup"><span data-stu-id="1bc81-134">$skip</span></span> | <span data-ttu-id="1bc81-135">跳过前 n 个结果。</span><span class="sxs-lookup"><span data-stu-id="1bc81-135">Skips the first n results.</span></span> |
| <span data-ttu-id="1bc81-136">$top</span><span class="sxs-lookup"><span data-stu-id="1bc81-136">$top</span></span> | <span data-ttu-id="1bc81-137">仅返回结果的前 n 个。</span><span class="sxs-lookup"><span data-stu-id="1bc81-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="1bc81-138">若要使用 OData 查询选项，则必须显式启用它们。</span><span class="sxs-lookup"><span data-stu-id="1bc81-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="1bc81-139">你可以为整个应用程序全局启用它们，也可以为特定控制器或特定操作启用它们。</span><span class="sxs-lookup"><span data-stu-id="1bc81-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="1bc81-140">若要全局启用 OData 查询选项，请在启动时调用**HttpConfiguration**类上的**EnableQuerySupport** ：</span><span class="sxs-lookup"><span data-stu-id="1bc81-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="1bc81-141">**EnableQuerySupport**方法为返回**IQueryable**类型的任何控制器操作全局启用查询选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="1bc81-142">如果你不希望为整个应用程序启用查询选项，则可以通过将 **[可查询]** 特性添加到操作方法来为特定控制器操作启用查询选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="1bc81-143">查询示例</span><span class="sxs-lookup"><span data-stu-id="1bc81-143">Example Queries</span></span>

<span data-ttu-id="1bc81-144">本部分介绍使用 OData 查询选项可以使用的查询类型。</span><span class="sxs-lookup"><span data-stu-id="1bc81-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="1bc81-145">有关查询选项的特定详细信息，请参阅 [www.odata.org](http://www.odata.org/)上的 OData 文档。</span><span class="sxs-lookup"><span data-stu-id="1bc81-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="1bc81-146">有关 $expand 和 $select 的信息，请参阅 [$Value OData 中的使用 $select、$expand 和 ASP.NET Web API](using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="1bc81-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="1bc81-147">**客户端驱动的分页**</span><span class="sxs-lookup"><span data-stu-id="1bc81-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="1bc81-148">对于大型实体集，客户端可能需要限制结果的数目。</span><span class="sxs-lookup"><span data-stu-id="1bc81-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="1bc81-149">例如，客户端一次可能会显示10个条目，其中包含 "下一步" 链接以获取下一页结果。</span><span class="sxs-lookup"><span data-stu-id="1bc81-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="1bc81-150">为此，客户端使用 $top 和 $skip 选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="1bc81-151">$Top 选项提供返回的最大项数，而 $skip 选项提供要跳过的项数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="1bc81-152">前面的示例提取条目21到30。</span><span class="sxs-lookup"><span data-stu-id="1bc81-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="1bc81-153">**筛选**</span><span class="sxs-lookup"><span data-stu-id="1bc81-153">**Filtering**</span></span>

<span data-ttu-id="1bc81-154">$Filter 选项允许客户端通过应用布尔表达式来筛选结果。</span><span class="sxs-lookup"><span data-stu-id="1bc81-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="1bc81-155">筛选器表达式非常强大;它们包括逻辑运算符和算术运算符、字符串函数和日期函数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="1bc81-156">返回类别等于 "玩具" 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="1bc81-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="1bc81-157">`http://localhost/Products?$filter=Category` eq "玩具"</span><span class="sxs-lookup"><span data-stu-id="1bc81-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="1bc81-158">返回价格小于10的所有产品。</span><span class="sxs-lookup"><span data-stu-id="1bc81-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="1bc81-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="1bc81-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="1bc81-160">逻辑运算符：返回价格 >= 5 并且价格 <= 15 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="1bc81-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="1bc81-161">`http://localhost/Products?$filter=Price` ge 5 和价格 le 15</span><span class="sxs-lookup"><span data-stu-id="1bc81-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="1bc81-162">字符串函数：返回名称中包含 "zz" 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="1bc81-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="1bc81-163">日期函数：在2005后返回包含 ReleaseDate 的所有产品。</span><span class="sxs-lookup"><span data-stu-id="1bc81-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="1bc81-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="1bc81-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="1bc81-165">**排序**</span><span class="sxs-lookup"><span data-stu-id="1bc81-165">**Sorting**</span></span>

<span data-ttu-id="1bc81-166">若要对结果进行排序，请使用 $orderby 筛选器。</span><span class="sxs-lookup"><span data-stu-id="1bc81-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="1bc81-167">按价格排序。</span><span class="sxs-lookup"><span data-stu-id="1bc81-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="1bc81-168">按价格降序排序 (最高到最低) 。</span><span class="sxs-lookup"><span data-stu-id="1bc81-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="1bc81-169">按类别排序，然后按价格在类别中按降序排序。</span><span class="sxs-lookup"><span data-stu-id="1bc81-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="1bc81-170">服务器驱动的分页</span><span class="sxs-lookup"><span data-stu-id="1bc81-170">Server-Driven Paging</span></span>

<span data-ttu-id="1bc81-171">如果数据库包含数百万条记录，则不希望在一个有效负载中发送所有记录。</span><span class="sxs-lookup"><span data-stu-id="1bc81-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="1bc81-172">若要防止出现这种情况，服务器可以限制在单个响应中发送的条目数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="1bc81-173">若要启用服务器分页，请设置可**查询**属性中的**PageSize**属性。</span><span class="sxs-lookup"><span data-stu-id="1bc81-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="1bc81-174">值为要返回的最大项数。</span><span class="sxs-lookup"><span data-stu-id="1bc81-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="1bc81-175">如果控制器返回 OData 格式，则响应正文将包含指向下一页数据的链接：</span><span class="sxs-lookup"><span data-stu-id="1bc81-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="1bc81-176">客户端可以使用此链接获取下一页。</span><span class="sxs-lookup"><span data-stu-id="1bc81-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="1bc81-177">若要了解结果集中的总项数，客户端可以设置值为 "allpages" 的 $inlinecount 查询选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="1bc81-178">值 "allpages" 指示服务器在响应中包含总计数：</span><span class="sxs-lookup"><span data-stu-id="1bc81-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="1bc81-179">下一页链接和内联计数都需要 OData 格式。</span><span class="sxs-lookup"><span data-stu-id="1bc81-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="1bc81-180">原因是 OData 在响应正文中定义了用于保存链接和计数的特殊字段。</span><span class="sxs-lookup"><span data-stu-id="1bc81-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="1bc81-181">对于非 OData 格式，仍可以支持下一页链接和内联计数，方法是在\*\*PageResult &lt; T &gt; \*\*对象中将查询结果括起来。</span><span class="sxs-lookup"><span data-stu-id="1bc81-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="1bc81-182">但是，它需要更多代码。</span><span class="sxs-lookup"><span data-stu-id="1bc81-182">However, it requires a bit more code.</span></span> <span data-ttu-id="1bc81-183">以下是示例：</span><span class="sxs-lookup"><span data-stu-id="1bc81-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="1bc81-184">下面是一个示例 JSON 响应：</span><span class="sxs-lookup"><span data-stu-id="1bc81-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="1bc81-185">限制查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-185">Limiting the Query Options</span></span>

<span data-ttu-id="1bc81-186">查询选项为客户端授予了对服务器上运行的查询的大量控制。</span><span class="sxs-lookup"><span data-stu-id="1bc81-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="1bc81-187">在某些情况下，出于安全或性能方面的原因，可能需要限制可用选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="1bc81-188">**[可查询]** 特性具有此的一些内置属性。</span><span class="sxs-lookup"><span data-stu-id="1bc81-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="1bc81-189">下面是一些示例。</span><span class="sxs-lookup"><span data-stu-id="1bc81-189">Here are some examples.</span></span>

<span data-ttu-id="1bc81-190">仅允许 $skip 和 $top 支持分页，无其他操作：</span><span class="sxs-lookup"><span data-stu-id="1bc81-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="1bc81-191">仅允许按某些属性排序，以防止对未在数据库中编制索引的属性进行排序：</span><span class="sxs-lookup"><span data-stu-id="1bc81-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="1bc81-192">允许 "eq" 逻辑函数，但不允许其他逻辑函数：</span><span class="sxs-lookup"><span data-stu-id="1bc81-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="1bc81-193">不允许任何算术运算符：</span><span class="sxs-lookup"><span data-stu-id="1bc81-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="1bc81-194">可以通过构造 **QueryableAttribute** 实例并将其传递给 **EnableQuerySupport** 函数，全局限制选项：</span><span class="sxs-lookup"><span data-stu-id="1bc81-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="1bc81-195">直接调用查询选项</span><span class="sxs-lookup"><span data-stu-id="1bc81-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="1bc81-196">您可以直接在控制器中调用查询选项，而不是使用 " **[可查询]** " 属性。</span><span class="sxs-lookup"><span data-stu-id="1bc81-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="1bc81-197">为此，请将 **ODataQueryOptions** 参数添加到控制器方法。</span><span class="sxs-lookup"><span data-stu-id="1bc81-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="1bc81-198">在这种情况下，不需要 **[可查询]** 特性。</span><span class="sxs-lookup"><span data-stu-id="1bc81-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="1bc81-199">Web API 从 URI 查询字符串填充 **ODataQueryOptions** 。</span><span class="sxs-lookup"><span data-stu-id="1bc81-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="1bc81-200">若要应用查询，请将 **IQueryable** 传递到 **ApplyTo** 方法。</span><span class="sxs-lookup"><span data-stu-id="1bc81-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="1bc81-201">方法返回另一个 **IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="1bc81-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="1bc81-202">对于高级方案，如果没有 **IQueryable** 查询提供程序，可以检查 **ODataQueryOptions** 并将查询选项转换为另一种形式。</span><span class="sxs-lookup"><span data-stu-id="1bc81-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="1bc81-203"> (例如，请参阅 RaghuRam Nadiminti 的博客文章 [将 OData 查询转换为 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中还包括一个 [示例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。 ) </span><span class="sxs-lookup"><span data-stu-id="1bc81-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="1bc81-204">查询验证</span><span class="sxs-lookup"><span data-stu-id="1bc81-204">Query Validation</span></span>

<span data-ttu-id="1bc81-205">[可查询 **]** 特性将在执行查询前对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="1bc81-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="1bc81-206">验证步骤是在 **QueryableAttribute. ValidateQuery** 方法中执行的。</span><span class="sxs-lookup"><span data-stu-id="1bc81-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="1bc81-207">您还可以自定义验证过程。</span><span class="sxs-lookup"><span data-stu-id="1bc81-207">You can also customize the validation process.</span></span>

<span data-ttu-id="1bc81-208">另请参阅 [OData 安全指南](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="1bc81-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="1bc81-209">首先，重写在 **web.config** 命名空间中定义的一个验证程序类。</span><span class="sxs-lookup"><span data-stu-id="1bc81-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="1bc81-210">例如，下面的验证程序类禁用 $orderby 选项的 "desc" 选项。</span><span class="sxs-lookup"><span data-stu-id="1bc81-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="1bc81-211">将 **[可查询]** 特性的子类用于重写 **ValidateQuery** 方法。</span><span class="sxs-lookup"><span data-stu-id="1bc81-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="1bc81-212">然后，设置自定义属性全局或每个控制器：</span><span class="sxs-lookup"><span data-stu-id="1bc81-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="1bc81-213">如果直接使用 **ODataQueryOptions** ，请在选项上设置验证程序：</span><span class="sxs-lookup"><span data-stu-id="1bc81-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]

---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的属性路由 |微软文档
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675389"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的属性路由

由[迈克·瓦森](https://github.com/MikeWasson)

*路由*是 Web API 将 URI 与操作匹配的方式。 Web API 2 支持一种称为*属性路由*的新型路由。 顾名思义，属性路由使用属性来定义路由。 属性路由使您能够对 Web API 中的 URI 进行更多控制。 例如，您可以轻松地创建描述资源层次结构的 URI。

早期路由样式（称为基于约定的路由）仍完全支持。 事实上，您可以将这两种技术合并到同一项目中。

本主题演示如何启用属性路由，并介绍属性路由的各种选项。 有关使用属性路由的端到端教程，请参阅[在 Web API 2 中使用属性路由创建 REST API。](create-a-rest-api-with-attribute-routing.md)

## <a name="prerequisites"></a>先决条件

[视觉工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版

或者，使用 NuGet 包管理器安装必要的包。 从 Visual Studio 中的 **"工具**"菜单中，选择**NuGet 包管理器**，然后选择 **"包管理器控制台**"。 在包管理器控制台窗口中输入以下命令：

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>为什么选择属性路由？

Web API 的第一个版本使用了*基于约定的*路由。 在这种类型的路由中，定义一个或多个路由模板，这些模板基本上是参数化字符串。 当框架收到请求时，它将 URI 与路由模板匹配。 有关基于约定的路由的详细信息，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

基于约定的路由的一个优点是模板在一个位置定义，并且路由规则在所有控制器之间一致应用。 遗憾的是，基于约定的路由很难支持 RESTful API 中常见的某些 URI 模式。 例如，资源通常包含子资源：客户有订单，电影有演员，书籍有作者，等等。 创建反映这些关系的 URI 是很自然的：

`/customers/1/orders`

这种类型的 URI 很难使用基于约定的路由创建。 尽管可以做到这一点，但如果您有许多控制器或资源类型，则结果不会很好地扩展。

使用属性路由，为此 URI 定义路由非常简单。 只需向控制器操作添加属性：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

下面是一些其他模式，属性路由使容易。

**API 版本控制**

在此示例中，"/api/v1/产品"将路由到与"/api/v2/产品"不同的控制器。

`/api/v1/products`
`/api/v2/products`

**重载 URI 段**

在此示例中，"1"是订单号，但"挂起"映射到集合。

`/orders/1`
`/orders/pending`

**多种参数类型**

在此示例中，"1"是订单号，但"2013/06/16"指定日期。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>启用属性路由

要启用属性路由，请在配置期间调用**MapHttpAttributeRoutes。** 此扩展方法在**System.Web.http.Http 配置扩展**类中定义。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

属性路由可以与[基于约定的](routing-in-aspnet-web-api.md)路由组合使用。 要定义基于约定的路由，请调用**MapHttpRoute**方法。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

有关配置 Web API 的详细信息，请参阅[配置ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意：从 Web API 1 迁移

在 Web API 2 之前，Web API 项目模板生成了如下所示的代码：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

如果启用了属性路由，则此代码将引发异常。 如果将现有 Web API 项目升级为使用属性路由，请确保将此配置代码更新为以下内容：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 有关详细信息，请参阅[使用托管ASP.NET配置 Web API。](../advanced/configuring-aspnet-web-api.md#webhost)

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>添加路由属性

下面是使用属性定义的路由的示例：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

字符串&quot;客户/[客户 Id]/订单&quot;是路由的 URI 模板。 Web API 尝试将请求 URI 与模板匹配。 在此示例中，"客户"和"订单"是文本段，"[客户 Id]"是一个变量参数。 以下 URI 将匹配此模板：

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

您可以使用[约束](#constraints)来限制匹配，本主题稍后将介绍。

请注意，&quot;工艺路线模板中的&quot;{customerId} 参数与 方法中的*customerId*参数的名称匹配。 当 Web API 调用控制器操作时，它尝试绑定路由参数。 例如，如果 URI 是`http://example.com/customers/1/orders`，Web API 会尝试在操作中将值"1"绑定到*customerId*参数。

URI 模板可以具有多个参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

没有任何路由属性的控制器方法都使用基于约定的路由。 这样，可以将两种类型的路由合并到同一项目中。

## <a name="http-methods"></a>HTTP 方法

Web API 还根据请求的 HTTP 方法（GET、POST 等）选择操作。 默认情况下，Web API 查找与控制器方法名称开头不区分大小写的匹配。 例如，名为的`PutCustomers`控制器方法与 HTTP PUT 请求匹配。

您可以通过使用以下任何属性修饰方法来重写此约定：

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

下面的示例将 CreateBook 方法映射到 HTTP POST 请求。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

对于所有其他 HTTP 方法（包括非标准方法），请使用**AcceptVerbs**属性，该属性采用 HTTP 方法的列表。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>路由前缀

通常，控制器中的路由都以相同的前缀开头。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

您可以使用 **[RoutePrefix]** 属性为整个控制器设置公共前缀：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

在方法属性上使用波浪线 （*） 来覆盖路由前缀：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

路由前缀可以包括参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>路由约束

通过路由约束，您可以限制路由模板中的参数的匹配方式。 一般语法是&quot;[参数：约束&quot;] 。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

此处，仅当 URI 的 ID&quot;&quot;段是整数时，才会选择第一个路由。 否则，将选择第二个路由。

下表列出了支持的约束。

| 约束 | 说明 | 示例 |
| --- | --- | --- |
| alpha | 匹配大写或小写拉丁字母字符（a-z，A-Z） | [x：阿尔法] |
| bool | 匹配布尔值。 | {x：布尔] |
| datetime | 匹配**日期时间**值。 | [x：日期时间] |
| Decimal | 匹配十进制值。 | [x：十进制] |
| double | 匹配 64 位浮点值。 | [x：双] |
| FLOAT | 匹配 32 位浮点值。 | [x：浮动] |
| guid | 匹配 GUID 值。 | {x：吉德] |
| int | 匹配 32 位整数值。 | {x：int} |
| 长度 | 将字符串与指定长度或指定长度范围内的字符串匹配。 | [x：长度（6）][x：长度（1，20）] |
| long | 匹配 64 位整数值。 | [x：长] |
| max | 匹配具有最大值的整数。 | {x：最大（10）] |
| 最大长度 | 匹配具有最大长度的字符串。 | {x：最大长度（10）] |
| min | 匹配具有最小值的整数。 | {x：min（10）] |
| 最小长度 | 匹配长度最小的字符串。 | {x：最小长度（10）] |
| range | 匹配值范围内的整数。 | [x：范围（10，50）] |
| regex | 匹配正则表达式。 | {x：regex（\d{3}-d{3}-\d{4}$）] |

请注意，某些约束（如&quot;最小&quot;值）在括号中采用参数。 您可以将多个约束应用于参数，由冒号分隔。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>自定义路由约束

您可以通过实现**IHttpRoute 约束**接口来创建自定义路由约束。 例如，以下约束将参数限制为非零整数值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

以下代码演示如何注册约束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

现在，您可以在路由中应用约束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

您还可以通过实现**IInline 约束解析器**接口来替换整个**默认内联约束解析器**类。 这样做将替换所有内置约束，除非您的**IInline 约束解析器**的实现专门添加它们。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>可选 URI 参数和默认值

您可以通过向路由参数添加问号来使 URI 参数成为可选参数。 如果路由参数是可选的，则必须为方法参数定义默认值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

在此示例中，`/api/books/locale/1033`并`/api/books/locale`返回相同的资源。

或者，您可以在工艺路线模板中指定默认值，如下所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

这几乎与前一个示例相同，但在应用默认值时，行为有细微差异。

- 在第一个示例（"{lcid：int？}"）中，默认值 1033 直接分配给方法参数，因此参数将具有此精确值。
- 在第二个示例（"{lcid：int=1033}）中，"1033"的默认值通过模型绑定过程。 默认模型绑定器将"1033"转换为数值 1033。 但是，您可以插入自定义模型活页夹，这可能执行不同操作。

（在大多数情况下，除非您管道中有自定义模型绑定器，否则这两个窗体将等效。

<a id="route-names"></a>
## <a name="route-names"></a>路由名称

在 Web API 中，每个路由都有一个名称。 路由名称可用于生成链接，因此您可以在 HTTP 响应中包含链接。

要指定路由名称，请在属性上设置**Name**属性。 下面的示例演示如何设置路由名称，以及生成链接时如何使用路由名称。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>路线订单

当框架尝试将 URI 与路由匹配时，它会按特定顺序评估路由。 要指定订单，请在工艺路线属性上设置**Order**属性。 首先计算较低的值。 默认订单值为零。

以下是确定总排序的方式：

1. 比较工艺路线属性的**Order**属性。
2. 查看工艺路线模板中的每个 URI 段。 对于每个段，顺序如下：

    1. 字段。
    2. 具有约束的路由参数。
    3. 路由参数没有约束。
    4. 具有约束的通配符参数段。
    5. 通配符参数段没有约束。
3. 在连接的情况下，路由由路由模板的区分大小写序字符串比较[（OrdinalIgnoreCase）](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)排序。

以下是一个示例。 假设您定义了以下控制器：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

这些路线按如下方式排序。

1. 订单/详细信息
2. 订单/{id}
3. 订单/[客户名称]
4. 订单/*\*日期*
5. 订单/待定

请注意，"详细信息"是文本段，出现在"{id}"之前，但"挂起"显示最后，因为**Order**属性为 1。 （此示例假定没有名为"详细信息"或"挂起"的客户。 通常，尽量避免不明确的路线。 在此示例中，更好的`GetByCustomer`路由模板是"客户/[客户名称]"

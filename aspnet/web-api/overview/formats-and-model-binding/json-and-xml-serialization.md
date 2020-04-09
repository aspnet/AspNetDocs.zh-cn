---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API 中的 JSON 和 XML 序列化 - ASP.NET 4.x
author: MikeWasson
description: 描述ASP.NET 4.x ASP.NET Web API 中的 JSON 和 XML for物质。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675831"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API 中的 JSON 和 XML 序列化

由[迈克·瓦森](https://github.com/MikeWasson)

本文介绍了ASP.NET Web API 中的 JSON 和 XML 等事。

在 Web API ASP.NET，*媒体类型的前物质*是一个对象，可以：

- 从 HTTP 消息正文读取 CLR 对象
- 将 CLR 对象写入 HTTP 消息正文

Web API 为 JSON 和 XML 提供媒体类型。 默认情况下，框架将这些处理件插入到管道中。 客户端可以在 HTTP 请求的"接受"标头中请求 JSON 或 XML。

## <a name="contents"></a>目录

- [JSON 媒体类型](#json_media_type_formatter)

    - [只读属性](#json_readonly)
    - [日期](#json_dates)
    - [缩进](#json_indenting)
    - [骆驼外壳](#json_camelcasing)
    - [匿名和弱类型对象](#json_anon)
- [XML 媒体类型前物质](#xml_media_type_formatter)

    - [只读属性](#xml_readonly)
    - [日期](#xml_dates)
    - [缩进](#xml_indenting)
    - [设置每类型 XML 序列化器](#xml_pertype)
- [删除 JSON 或 XML 前物质](#removing_the_json_or_xml_formatter)
- [处理圆形对象引用](#handling_circular_object_references)
- [测试对象序列化](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON 媒体类型

JSON 格式由**JsonMediaTypeFormatter**类提供。 默认情况下 **，JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库执行序列化。 Json.NET是第三方开源项目。

如果您愿意，可以将**JsonMediaTypeFormatter**类配置为使用**数据合同Jon序列化器**，而不是Json.NET。 为此，将**UseDataContractJson 序列化器**属性设置为**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON 序列化

本节使用默认[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化器描述 JSON formatter 的一些特定行为。 这不是要全面记录Json.NET图书馆;有关详细信息，请参阅[Json.NET文档](http://james.newtonking.com/projects/json/help/)。

#### <a name="what-gets-serialized"></a>什么是序列化？

默认情况下，所有公共属性和字段都包含在序列化的 JSON 中。 要省略属性或字段，请使用**JsonIgnore**属性来修饰它。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

如果您更喜欢&quot;选择加入&quot;的方法，请使用**DataContract**属性修饰类。 如果存在此属性，则忽略成员，除非它们具有 Data**成员**。 您还可以使用 Data**成员**序列化私有成员。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>只读属性

默认情况下，只读属性将序列化。

<a id="json_dates"></a>
### <a name="dates"></a>日期

默认情况下，Json.NET以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式写入日期。 UTC（协调通用时间）中的日期用"Z"后缀书写。 本地时间中的日期包括时区偏移量。 例如：

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

默认情况下，Json.NET保留时区。 您可以通过设置 DateTimeZone 处理属性来覆盖此功能：

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

如果您更喜欢使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)（`"\/Date(ticks)\/"`） 而不是 ISO 8601，请使用序列化器设置上设置**DateFormat 处理**属性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>缩进

要编写缩进的 JSON，请将 **"格式化"** 设置设置为 **"格式化"。**

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>骆驼外壳

要使用 camel 大小写写入 JSON 属性名称，而不更改数据模型，请在序列化器上设置**CamelCasePropertyNames合同解析器**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>匿名和弱类型对象

操作方法可以返回匿名对象并将其序列化到 JSON。 例如：

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

响应消息正文将包含以下 JSON：

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

如果 Web API 从客户端接收结构松散的 JSON 对象，则可以将请求正文反序列化为**Newtonsoft.Json.Linq.JObject**类型。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

但是，通常最好使用强类型数据对象。 然后，您无需自行分析数据，并且得到了模型验证的好处。

XML 序列化程序不支持匿名类型或**JObject**实例。 如果将这些功能用于 JSON 数据，则应从管道中删除 XML formatter，如本文后面所述。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML 媒体类型前物质

XML 格式由**XmlMediaTypeFormatter**类提供。 默认情况下 **，XmlMediaTypeFormatter**使用**数据合同序列化器**类执行序列化。

如果您愿意，可以将**XmlMediaTypeFormatter**配置为使用 Xml**序列化器**而不是**数据合同序列化器**。 为此，将**UseXml 序列化器**属性设置为**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer**类支持比**DataContract 序列化器**更窄的类型集，但提供了对生成的 XML 的更多控制。 如果需要匹配现有的 XML 架构，请考虑使用**Xml 序列化器**。

### <a name="xml-serialization"></a>XML 序列化

本节使用默认**的数据合同序列程序**描述 XML 前物的一些特定行为。

默认情况下，数据合同序列化器的操作方式如下：

- 所有公共读/写属性和字段都将序列化。 要省略属性或字段，请使用**IgnoreData成员**属性来修饰它。
- 私有成员和保护成员不序列化。
- 只读属性不序列化。 （但是，只读集合属性的内容是序列化的。
- 类和成员名称在 XML 中写入，与类声明中显示的完全相同。
- 使用默认的 XML 命名空间。

如果需要对序列化进行更多控制，可以使用**DataContract**属性修饰类。 当存在此属性时，类将序列化如下：

- &quot;选择加入&quot;方法：默认情况下不序列化属性和字段。 要序列化属性或字段，请使用**Data成员**属性来修饰它。
- 要序列化私有或受保护成员，请使用**Data成员**属性装饰它。
- 只读属性不序列化。
- 要更改类名称在 XML 中的显示方式，在**DataContract**属性中设置*Name*参数。
- 要更改成员名称在 XML 中的显示方式，在**DataMs 属性**中设置*Name*参数。
- 要更改 XML 命名空间，在**DataContract**类中设置*命名空间*参数。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>只读属性

只读属性不序列化。 如果只读属性具有支持专用字段，则可以使用**Data"成员"** 属性标记私有字段。 此方法需要类上的**DataContract**属性。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日期

日期以 ISO 8601 格式书写。 例如， &quot;2012-05-23T20：21：37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>缩进

要编写缩进的 XML，请将**缩进**属性设置为**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>设置每类型 XML 序列化器

您可以为不同的 CLR 类型设置不同的 XML 序列化器。 例如，您可能有一个特定的数据对象，该对象需要**XmlSerializer**来进行向后兼容性。 您可以为此对象使用**Xml 序列化器**，并继续将**数据合同序列化器用于其他类型的数据合同序列化器**。

要为特定类型设置 XML 序列化器，请调用**Set 序列化器**。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

您可以指定**Xml 序列化器**或任何派生自**XmlObject 序列化器**的对象。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>删除 JSON 或 XML 前物质

如果不想使用，可以从事件列表中删除 JSON 事件或 XML 前物质。 这样做的主要原因是：

- 将 Web API 响应限制为特定媒体类型。 例如，您可能决定仅支持 JSON 响应，并删除 XML 前一部分。
- 将默认前物质替换为自定义前物质。 例如，您可以将 JSON 事件替换为您自己的 JSON 事件的自定义实现。

以下代码演示如何删除默认的事务。 从在 Global.asax 中定义的**应用程序\_启动**方法调用此。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>处理圆形对象引用

默认情况下，JSON 和 XML formatters 将所有对象写入值。 如果两个属性引用同一对象，或者如果同一对象在集合中出现两次，则 formatter 将序列化该对象两次。 如果对象图包含周期，则这是一个特殊问题，因为序列化器在检测到图形中的循环时将引发异常。

请考虑以下对象模型和控制器。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

调用此操作将导致 formatter 引发异常，该异常将转换为客户端的状态代码 500（内部服务器错误）响应。

要在 JSON 中保留对象引用，请将以下代码添加到 Global.asax 文件中**的应用程序\_启动**方法：

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

现在控制器操作将返回如下所示的 JSON：

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

请注意，序列化器向这&quot;两&quot;个对象添加$id属性。 此外，它检测 Employ.Department 属性创建一个循环，因此它将值替换为&quot;对象引用：{ $ref&quot;：1&quot;&quot;}。

> [!NOTE]
> 对象引用在 JSON 中不是标准引用。 在使用此功能之前，请考虑客户端是否能够分析结果。 最好只是从图形中删除循环。 例如，在此示例中，从"员工"回部门的链接并不真正是必需的。

要在 XML 中保留对象引用，有两个选项。 更简单的选项是`[DataContract(IsReference=true)]`添加到模型类。 *IsReference 参数*启用对象引用。 请记住 **，DataContract**使序列化选择加入，因此您还需要向属性添加**Data成员**属性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

现在，前物质将生成类似于以下内容的 XML：

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

如果要避免模型类的属性，还有另一个选项：创建新的类型特定的**DataContract 序列化器**实例，并在构造函数中将*保留对象引用*设置为**true。** 然后，将此实例设置为 XML 媒体类型前物质上的每种类型序列化器。 以下代码演示如何执行此操作：

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>测试对象序列化

在设计 Web API 时，测试数据对象如何序列化非常有用。 无需创建控制器或调用控制器操作即可执行此操作。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

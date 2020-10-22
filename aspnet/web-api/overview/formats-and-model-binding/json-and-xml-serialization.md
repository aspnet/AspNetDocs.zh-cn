---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API-ASP.NET 4.x 中的 JSON 和 XML 序列化
author: MikeWasson
description: 描述 ASP.NET 4.x 的 ASP.NET Web API 中的 JSON 和 XML 格式化程序。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345165"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API 中的 JSON 和 XML 序列化

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍 ASP.NET Web API 中的 JSON 和 XML 格式化程序。

在 ASP.NET Web API 中， *媒体类型格式化程序* 是一个对象，该对象可：

- 从 HTTP 消息正文中读取 CLR 对象
- 将 CLR 对象写入 HTTP 消息正文

Web API 为 JSON 和 XML 提供了媒体类型格式化程序。 默认情况下，框架将这些格式化程序插入管道。 客户端可以在 HTTP 请求的 Accept 标头中请求 JSON 或 XML。

## <a name="contents"></a>目录

- [JSON Media-Type 格式化程序](#json_media_type_formatter)

    - [只读属性](#json_readonly)
    - [日期](#json_dates)
    - [缩进](#json_indenting)
    - [Camel 大小写](#json_camelcasing)
    - [匿名和 Weakly-Typed 对象](#json_anon)
- [XML Media-Type 格式化程序](#xml_media_type_formatter)

    - [只读属性](#xml_readonly)
    - [日期](#xml_dates)
    - [缩进](#xml_indenting)
    - [设置 Per-Type XML 序列化程序](#xml_pertype)
- [删除 JSON 或 XML 格式化程序](#removing_the_json_or_xml_formatter)
- [处理循环对象引用](#handling_circular_object_references)
- [测试对象序列化](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Media-Type 格式化程序

JSON 格式由 **JsonMediaTypeFormatter** 类提供。 默认情况下， **JsonMediaTypeFormatter** 使用 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 库来执行序列化。 Json.NET 是第三方开源项目。

如果需要，可以将 **JsonMediaTypeFormatter** 类配置为使用 **DataContractJsonSerializer** 而不是 Json.NET。 为此，请将 **UseDataContractJsonSerializer** 属性设置为 **true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON 序列化

本部分介绍使用默认 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 序列化程序的 JSON 格式化程序的某些特定行为。 这并不是 Json.NET 库的综合文档;有关详细信息，请参阅 [Json.NET 文档](http://james.newtonking.com/projects/json/help/)。

#### <a name="what-gets-serialized"></a>序列化的内容是什么？

默认情况下，所有公共属性和字段均包括在序列化的 JSON 中。 若要忽略某个属性或字段，请使用 **JsonIgnore** 属性修饰它。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

如果更喜欢 &quot; 选择加入 &quot; 方法，请使用 **DataContract** 特性修饰类。 如果该属性存在，则将忽略成员，除非它们具有 **DataMember**。 你还可以使用 **DataMember** 来序列化私有成员。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Read-Only 属性

默认情况下，将对只读属性进行序列化。

<a id="json_dates"></a>
### <a name="dates"></a>日期

默认情况下，Json.NET 以 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 格式编写日期。 UTC 格式的日期 (使用 "Z" 后缀编写协调通用时间) 。 本地时间中的日期包括时区偏移量。 例如：

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

默认情况下，Json.NET 保留时区。 可以通过设置 DateTimeZoneHandling 属性来重写此：

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

如果希望使用 [MICROSOFT JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) ，而不是使用 ISO 8601，请在序列化程序设置上设置 **DateFormatHandling** 属性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>缩进

若要写入缩进的 JSON，请将 **格式** 设置设置为 "格式设置" **。缩进**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Camel 大小写

若要以 camel 大小写形式编写 JSON 属性名称，而不更改数据模型，请在序列化程序上设置 **CamelCasePropertyNamesContractResolver** ：

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>匿名和 Weakly-Typed 对象

操作方法可以返回匿名对象并将其序列化为 JSON。 例如：

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

响应消息正文将包含以下 JSON：

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

如果 web API 从客户端接收松散结构化的 JSON 对象，则可以将请求正文反序列化为 ** 上的Newtonsoft.Js。JObject** 类型。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

但是，使用强类型化数据对象通常更好。 然后，你无需自行分析数据，并获得模型验证的优势。

XML 序列化程序不支持匿名类型或 **JObject** 实例。 如果对 JSON 数据使用这些功能，则应该从管道中删除 XML 格式化程序，如本文后面部分所述。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML Media-Type 格式化程序

XML 格式由 **XmlMediaTypeFormatter** 类提供。 默认情况下， **XmlMediaTypeFormatter** 使用 **DataContractSerializer** 类来执行序列化。

如果需要，可以将 **XmlMediaTypeFormatter** 配置为使用 **XmlSerializer** ，而不是 **DataContractSerializer**。 为此，请将 **UseXmlSerializer** 属性设置为 **true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer**类支持比**DataContractSerializer**更窄的类型集，但可以更好地控制生成的 XML。 如果需要匹配现有的 XML 架构，请考虑使用 **XmlSerializer** 。

### <a name="xml-serialization"></a>XML 序列化

本部分介绍使用默认 **DataContractSerializer**的 XML 格式化程序的某些特定行为。

默认情况下，DataContractSerializer 的行为如下所示：

- 所有公共读/写属性和字段均被序列化。 若要忽略某个属性或字段，请使用 **IgnoreDataMember** 属性修饰它。
- 不序列化私有和受保护的成员。
- 只读属性不会序列化。 但 (会序列化只读集合属性的内容。 ) 
- 类和成员名称在 XML 中以与它们在类声明中显示的完全相同的方式编写。
- 使用默认的 XML 命名空间。

如果需要对序列化进行更多控制，则可以用 **DataContract** 特性修饰类。 如果该属性存在，则按如下方式序列化类：

- &quot;选择采用 &quot; 方法：默认情况下不序列化属性和字段。 若要序列化属性或字段，请使用 **DataMember** 特性修饰它。
- 若要序列化私有或受保护成员，请使用 **DataMember** 特性来修饰它。
- 只读属性不会序列化。
- 若要更改类名称在 XML 中的显示方式，请在**DataContract**属性中设置*name*参数。
- 若要更改成员名称在 XML 中的显示方式，请设置**DataMember**特性中的*name*参数。
- 若要更改 XML 命名空间，请在**DataContract**类中设置*namespace*参数。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Read-Only 属性

只读属性不会序列化。 如果只读属性有一个后备私有字段，则可以使用 **DataMember** 特性标记该私有字段。 此方法需要类的 **DataContract** 特性。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日期

日期是采用 ISO 8601 格式编写的。 例如， &quot; 2012-05-23T20：21： 37.9116538 z &quot; 。

<a id="xml_indenting"></a>
### <a name="indenting"></a>缩进

若要写入缩进的 XML，请将 " **缩进** " 属性设置为 **true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>设置 Per-Type XML 序列化程序

可以为不同的 CLR 类型设置不同的 XML 序列化程序。 例如，你可能有一个需要 **XmlSerializer** 来实现向后兼容的特定数据对象。 可以为此对象使用 **XmlSerializer** ，并继续对其他类型使用 **DataContractSerializer** 。

若要设置特定类型的 XML 序列化程序，请调用 **SetSerializer**。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

可以指定 **XmlSerializer** 或从 **XmlObjectSerializer**派生的任何对象。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>删除 JSON 或 XML 格式化程序

如果不想使用 JSON 格式化程序或格式化程序列表中的 XML 格式化程序，则可以将其删除。 执行此操作的主要原因是：

- 若要将 web API 响应限制为特定媒体类型，请使用。 例如，你可能决定仅支持 JSON 响应，并删除 XML 格式化程序。
- 将默认格式化程序替换为自定义格式化程序。 例如，你可以将 JSON 格式化程序替换为你自己的 JSON 格式化程序的自定义实现。

下面的代码演示如何删除默认的格式化程序。 从 global.asax 中定义的 **应用程序 \_ 启动** 方法调用此方法。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>处理循环对象引用

默认情况下，JSON 和 XML 格式化程序将所有对象都作为值写入。 如果两个属性引用同一个对象，或者如果同一对象出现在集合中两次，则格式化程序会将对象序列化两次。 如果你的对象图包含循环，这是一个特殊的问题，因为序列化程序在检测到关系图中的循环时将引发异常。

请考虑以下对象模型和控制器。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

调用此操作将导致格式化程序引发异常，该异常转换为状态代码 500 (内部服务器错误) 对客户端的响应。

若要在 JSON 中保留对象引用，请将以下代码添加到 global.asax 文件中的 **Application \_ Start** 方法：

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

现在，控制器操作将返回如下所示的 JSON：

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

请注意，序列化程序将 &quot; $id &quot; 属性添加到这两个对象。 此外，它还检测 Employee. 部门属性创建了一个循环，因此它会将值替换为对象引用： { &quot; $ref &quot; ： &quot; 1 &quot; }。

> [!NOTE]
> 对象引用在 JSON 中不是标准引用。 使用此功能之前，请考虑客户端是否能够分析结果。 最好是从图形中删除循环。 例如，在此示例中，不需要从 Employee 返回到部门的链接。

若要在 XML 中保留对象引用，您有两种选择。 更简单的选项是添加 `[DataContract(IsReference=true)]` 到模型类。 *IsReference*参数启用对象引用。 请记住， **DataContract** 使序列化选择加入，因此还需要向属性中添加 **DataMember** 特性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

现在格式化程序生成的 XML 类似于以下内容：

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

如果您想要避免使用您的模型类上的属性，可以使用另一个选项：创建新的特定于类型的 **DataContractSerializer** 实例，并在构造函数中将 *preserveObjectReferences* 设置为 **true** 。 然后，将此实例设置为 XML 媒体类型格式化程序上的每个类型的序列化程序。 下面的代码演示如何执行此操作：

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>测试对象序列化

设计 web API 时，测试如何序列化数据对象非常有用。 无需创建控制器或调用控制器操作即可执行此操作。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

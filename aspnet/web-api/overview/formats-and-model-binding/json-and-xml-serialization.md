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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="7a2c9-103">ASP.NET Web API 中的 JSON 和 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="7a2c9-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="7a2c9-104">由[迈克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7a2c9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7a2c9-105">本文介绍了ASP.NET Web API 中的 JSON 和 XML 等事。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="7a2c9-106">在 Web API ASP.NET，*媒体类型的前物质*是一个对象，可以：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="7a2c9-107">从 HTTP 消息正文读取 CLR 对象</span><span class="sxs-lookup"><span data-stu-id="7a2c9-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="7a2c9-108">将 CLR 对象写入 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="7a2c9-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="7a2c9-109">Web API 为 JSON 和 XML 提供媒体类型。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="7a2c9-110">默认情况下，框架将这些处理件插入到管道中。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="7a2c9-111">客户端可以在 HTTP 请求的"接受"标头中请求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="7a2c9-112">目录</span><span class="sxs-lookup"><span data-stu-id="7a2c9-112">Contents</span></span>

- [<span data-ttu-id="7a2c9-113">JSON 媒体类型</span><span class="sxs-lookup"><span data-stu-id="7a2c9-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="7a2c9-114">只读属性</span><span class="sxs-lookup"><span data-stu-id="7a2c9-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="7a2c9-115">日期</span><span class="sxs-lookup"><span data-stu-id="7a2c9-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="7a2c9-116">缩进</span><span class="sxs-lookup"><span data-stu-id="7a2c9-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="7a2c9-117">骆驼外壳</span><span class="sxs-lookup"><span data-stu-id="7a2c9-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="7a2c9-118">匿名和弱类型对象</span><span class="sxs-lookup"><span data-stu-id="7a2c9-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="7a2c9-119">XML 媒体类型前物质</span><span class="sxs-lookup"><span data-stu-id="7a2c9-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="7a2c9-120">只读属性</span><span class="sxs-lookup"><span data-stu-id="7a2c9-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="7a2c9-121">日期</span><span class="sxs-lookup"><span data-stu-id="7a2c9-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="7a2c9-122">缩进</span><span class="sxs-lookup"><span data-stu-id="7a2c9-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="7a2c9-123">设置每类型 XML 序列化器</span><span class="sxs-lookup"><span data-stu-id="7a2c9-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="7a2c9-124">删除 JSON 或 XML 前物质</span><span class="sxs-lookup"><span data-stu-id="7a2c9-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="7a2c9-125">处理圆形对象引用</span><span class="sxs-lookup"><span data-stu-id="7a2c9-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="7a2c9-126">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="7a2c9-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="7a2c9-127">JSON 媒体类型</span><span class="sxs-lookup"><span data-stu-id="7a2c9-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="7a2c9-128">JSON 格式由**JsonMediaTypeFormatter**类提供。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="7a2c9-129">默认情况下 **，JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库执行序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="7a2c9-130">Json.NET是第三方开源项目。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="7a2c9-131">如果您愿意，可以将**JsonMediaTypeFormatter**类配置为使用**数据合同Jon序列化器**，而不是Json.NET。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="7a2c9-132">为此，将**UseDataContractJson 序列化器**属性设置为**true**：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="7a2c9-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="7a2c9-133">JSON Serialization</span></span>

<span data-ttu-id="7a2c9-134">本节使用默认[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化器描述 JSON formatter 的一些特定行为。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="7a2c9-135">这不是要全面记录Json.NET图书馆;有关详细信息，请参阅[Json.NET文档](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="7a2c9-136">什么是序列化？</span><span class="sxs-lookup"><span data-stu-id="7a2c9-136">What Gets Serialized?</span></span>

<span data-ttu-id="7a2c9-137">默认情况下，所有公共属性和字段都包含在序列化的 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="7a2c9-138">要省略属性或字段，请使用**JsonIgnore**属性来修饰它。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="7a2c9-139">如果您更喜欢&quot;选择加入&quot;的方法，请使用**DataContract**属性修饰类。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="7a2c9-140">如果存在此属性，则忽略成员，除非它们具有 Data**成员**。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="7a2c9-141">您还可以使用 Data**成员**序列化私有成员。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="7a2c9-142">只读属性</span><span class="sxs-lookup"><span data-stu-id="7a2c9-142">Read-Only Properties</span></span>

<span data-ttu-id="7a2c9-143">默认情况下，只读属性将序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="7a2c9-144">日期</span><span class="sxs-lookup"><span data-stu-id="7a2c9-144">Dates</span></span>

<span data-ttu-id="7a2c9-145">默认情况下，Json.NET以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式写入日期。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="7a2c9-146">UTC（协调通用时间）中的日期用"Z"后缀书写。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="7a2c9-147">本地时间中的日期包括时区偏移量。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="7a2c9-148">例如：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="7a2c9-149">默认情况下，Json.NET保留时区。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="7a2c9-150">您可以通过设置 DateTimeZone 处理属性来覆盖此功能：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="7a2c9-151">如果您更喜欢使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)（`"\/Date(ticks)\/"`） 而不是 ISO 8601，请使用序列化器设置上设置**DateFormat 处理**属性：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="7a2c9-152">缩进</span><span class="sxs-lookup"><span data-stu-id="7a2c9-152">Indenting</span></span>

<span data-ttu-id="7a2c9-153">要编写缩进的 JSON，请将 **"格式化"** 设置设置为 **"格式化"。**</span><span class="sxs-lookup"><span data-stu-id="7a2c9-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="7a2c9-154">骆驼外壳</span><span class="sxs-lookup"><span data-stu-id="7a2c9-154">Camel Casing</span></span>

<span data-ttu-id="7a2c9-155">要使用 camel 大小写写入 JSON 属性名称，而不更改数据模型，请在序列化器上设置**CamelCasePropertyNames合同解析器**：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="7a2c9-156">匿名和弱类型对象</span><span class="sxs-lookup"><span data-stu-id="7a2c9-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="7a2c9-157">操作方法可以返回匿名对象并将其序列化到 JSON。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="7a2c9-158">例如：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="7a2c9-159">响应消息正文将包含以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="7a2c9-160">如果 Web API 从客户端接收结构松散的 JSON 对象，则可以将请求正文反序列化为**Newtonsoft.Json.Linq.JObject**类型。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="7a2c9-161">但是，通常最好使用强类型数据对象。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="7a2c9-162">然后，您无需自行分析数据，并且得到了模型验证的好处。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="7a2c9-163">XML 序列化程序不支持匿名类型或**JObject**实例。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="7a2c9-164">如果将这些功能用于 JSON 数据，则应从管道中删除 XML formatter，如本文后面所述。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="7a2c9-165">XML 媒体类型前物质</span><span class="sxs-lookup"><span data-stu-id="7a2c9-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="7a2c9-166">XML 格式由**XmlMediaTypeFormatter**类提供。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="7a2c9-167">默认情况下 **，XmlMediaTypeFormatter**使用**数据合同序列化器**类执行序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="7a2c9-168">如果您愿意，可以将**XmlMediaTypeFormatter**配置为使用 Xml**序列化器**而不是**数据合同序列化器**。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="7a2c9-169">为此，将**UseXml 序列化器**属性设置为**true**：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="7a2c9-170">**XmlSerializer**类支持比**DataContract 序列化器**更窄的类型集，但提供了对生成的 XML 的更多控制。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="7a2c9-171">如果需要匹配现有的 XML 架构，请考虑使用**Xml 序列化器**。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="7a2c9-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="7a2c9-172">XML Serialization</span></span>

<span data-ttu-id="7a2c9-173">本节使用默认**的数据合同序列程序**描述 XML 前物的一些特定行为。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="7a2c9-174">默认情况下，数据合同序列化器的操作方式如下：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="7a2c9-175">所有公共读/写属性和字段都将序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="7a2c9-176">要省略属性或字段，请使用**IgnoreData成员**属性来修饰它。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="7a2c9-177">私有成员和保护成员不序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="7a2c9-178">只读属性不序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="7a2c9-179">（但是，只读集合属性的内容是序列化的。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="7a2c9-180">类和成员名称在 XML 中写入，与类声明中显示的完全相同。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="7a2c9-181">使用默认的 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-181">A default XML namespace is used.</span></span>

<span data-ttu-id="7a2c9-182">如果需要对序列化进行更多控制，可以使用**DataContract**属性修饰类。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="7a2c9-183">当存在此属性时，类将序列化如下：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="7a2c9-184">&quot;选择加入&quot;方法：默认情况下不序列化属性和字段。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="7a2c9-185">要序列化属性或字段，请使用**Data成员**属性来修饰它。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="7a2c9-186">要序列化私有或受保护成员，请使用**Data成员**属性装饰它。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="7a2c9-187">只读属性不序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="7a2c9-188">要更改类名称在 XML 中的显示方式，在**DataContract**属性中设置*Name*参数。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="7a2c9-189">要更改成员名称在 XML 中的显示方式，在**DataMs 属性**中设置*Name*参数。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="7a2c9-190">要更改 XML 命名空间，在**DataContract**类中设置*命名空间*参数。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="7a2c9-191">只读属性</span><span class="sxs-lookup"><span data-stu-id="7a2c9-191">Read-Only Properties</span></span>

<span data-ttu-id="7a2c9-192">只读属性不序列化。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="7a2c9-193">如果只读属性具有支持专用字段，则可以使用**Data"成员"** 属性标记私有字段。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="7a2c9-194">此方法需要类上的**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="7a2c9-195">日期</span><span class="sxs-lookup"><span data-stu-id="7a2c9-195">Dates</span></span>

<span data-ttu-id="7a2c9-196">日期以 ISO 8601 格式书写。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="7a2c9-197">例如， &quot;2012-05-23T20：21：37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="7a2c9-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="7a2c9-198">缩进</span><span class="sxs-lookup"><span data-stu-id="7a2c9-198">Indenting</span></span>

<span data-ttu-id="7a2c9-199">要编写缩进的 XML，请将**缩进**属性设置为**true**：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="7a2c9-200">设置每类型 XML 序列化器</span><span class="sxs-lookup"><span data-stu-id="7a2c9-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="7a2c9-201">您可以为不同的 CLR 类型设置不同的 XML 序列化器。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="7a2c9-202">例如，您可能有一个特定的数据对象，该对象需要**XmlSerializer**来进行向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="7a2c9-203">您可以为此对象使用**Xml 序列化器**，并继续将**数据合同序列化器用于其他类型的数据合同序列化器**。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="7a2c9-204">要为特定类型设置 XML 序列化器，请调用**Set 序列化器**。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="7a2c9-205">您可以指定**Xml 序列化器**或任何派生自**XmlObject 序列化器**的对象。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="7a2c9-206">删除 JSON 或 XML 前物质</span><span class="sxs-lookup"><span data-stu-id="7a2c9-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="7a2c9-207">如果不想使用，可以从事件列表中删除 JSON 事件或 XML 前物质。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="7a2c9-208">这样做的主要原因是：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="7a2c9-209">将 Web API 响应限制为特定媒体类型。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="7a2c9-210">例如，您可能决定仅支持 JSON 响应，并删除 XML 前一部分。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="7a2c9-211">将默认前物质替换为自定义前物质。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="7a2c9-212">例如，您可以将 JSON 事件替换为您自己的 JSON 事件的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="7a2c9-213">以下代码演示如何删除默认的事务。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="7a2c9-214">从在 Global.asax 中定义的**应用程序\_启动**方法调用此。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="7a2c9-215">处理圆形对象引用</span><span class="sxs-lookup"><span data-stu-id="7a2c9-215">Handling Circular Object References</span></span>

<span data-ttu-id="7a2c9-216">默认情况下，JSON 和 XML formatters 将所有对象写入值。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="7a2c9-217">如果两个属性引用同一对象，或者如果同一对象在集合中出现两次，则 formatter 将序列化该对象两次。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="7a2c9-218">如果对象图包含周期，则这是一个特殊问题，因为序列化器在检测到图形中的循环时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="7a2c9-219">请考虑以下对象模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="7a2c9-220">调用此操作将导致 formatter 引发异常，该异常将转换为客户端的状态代码 500（内部服务器错误）响应。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="7a2c9-221">要在 JSON 中保留对象引用，请将以下代码添加到 Global.asax 文件中**的应用程序\_启动**方法：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="7a2c9-222">现在控制器操作将返回如下所示的 JSON：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="7a2c9-223">请注意，序列化器向这&quot;两&quot;个对象添加$id属性。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="7a2c9-224">此外，它检测 Employ.Department 属性创建一个循环，因此它将值替换为&quot;对象引用：{ $ref&quot;：1&quot;&quot;}。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="7a2c9-225">对象引用在 JSON 中不是标准引用。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="7a2c9-226">在使用此功能之前，请考虑客户端是否能够分析结果。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="7a2c9-227">最好只是从图形中删除循环。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="7a2c9-228">例如，在此示例中，从"员工"回部门的链接并不真正是必需的。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="7a2c9-229">要在 XML 中保留对象引用，有两个选项。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="7a2c9-230">更简单的选项是`[DataContract(IsReference=true)]`添加到模型类。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="7a2c9-231">*IsReference 参数*启用对象引用。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="7a2c9-232">请记住 **，DataContract**使序列化选择加入，因此您还需要向属性添加**Data成员**属性：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="7a2c9-233">现在，前物质将生成类似于以下内容的 XML：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="7a2c9-234">如果要避免模型类的属性，还有另一个选项：创建新的类型特定的**DataContract 序列化器**实例，并在构造函数中将*保留对象引用*设置为**true。**</span><span class="sxs-lookup"><span data-stu-id="7a2c9-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="7a2c9-235">然后，将此实例设置为 XML 媒体类型前物质上的每种类型序列化器。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="7a2c9-236">以下代码演示如何执行此操作：</span><span class="sxs-lookup"><span data-stu-id="7a2c9-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="7a2c9-237">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="7a2c9-237">Testing Object Serialization</span></span>

<span data-ttu-id="7a2c9-238">在设计 Web API 时，测试数据对象如何序列化非常有用。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="7a2c9-239">无需创建控制器或调用控制器操作即可执行此操作。</span><span class="sxs-lookup"><span data-stu-id="7a2c9-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

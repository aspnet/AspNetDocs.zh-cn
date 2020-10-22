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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="ebfed-103">ASP.NET Web API 中的 JSON 和 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="ebfed-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="ebfed-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ebfed-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ebfed-105">本文介绍 ASP.NET Web API 中的 JSON 和 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="ebfed-106">在 ASP.NET Web API 中， *媒体类型格式化程序* 是一个对象，该对象可：</span><span class="sxs-lookup"><span data-stu-id="ebfed-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="ebfed-107">从 HTTP 消息正文中读取 CLR 对象</span><span class="sxs-lookup"><span data-stu-id="ebfed-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="ebfed-108">将 CLR 对象写入 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="ebfed-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="ebfed-109">Web API 为 JSON 和 XML 提供了媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="ebfed-110">默认情况下，框架将这些格式化程序插入管道。</span><span class="sxs-lookup"><span data-stu-id="ebfed-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="ebfed-111">客户端可以在 HTTP 请求的 Accept 标头中请求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="ebfed-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="ebfed-112">目录</span><span class="sxs-lookup"><span data-stu-id="ebfed-112">Contents</span></span>

- [<span data-ttu-id="ebfed-113">JSON Media-Type 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="ebfed-114">只读属性</span><span class="sxs-lookup"><span data-stu-id="ebfed-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="ebfed-115">日期</span><span class="sxs-lookup"><span data-stu-id="ebfed-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="ebfed-116">缩进</span><span class="sxs-lookup"><span data-stu-id="ebfed-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="ebfed-117">Camel 大小写</span><span class="sxs-lookup"><span data-stu-id="ebfed-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="ebfed-118">匿名和 Weakly-Typed 对象</span><span class="sxs-lookup"><span data-stu-id="ebfed-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="ebfed-119">XML Media-Type 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="ebfed-120">只读属性</span><span class="sxs-lookup"><span data-stu-id="ebfed-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="ebfed-121">日期</span><span class="sxs-lookup"><span data-stu-id="ebfed-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="ebfed-122">缩进</span><span class="sxs-lookup"><span data-stu-id="ebfed-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="ebfed-123">设置 Per-Type XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="ebfed-124">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="ebfed-125">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="ebfed-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="ebfed-126">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="ebfed-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="ebfed-127">JSON Media-Type 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="ebfed-128">JSON 格式由 **JsonMediaTypeFormatter** 类提供。</span><span class="sxs-lookup"><span data-stu-id="ebfed-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="ebfed-129">默认情况下， **JsonMediaTypeFormatter** 使用 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 库来执行序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="ebfed-130">Json.NET 是第三方开源项目。</span><span class="sxs-lookup"><span data-stu-id="ebfed-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="ebfed-131">如果需要，可以将 **JsonMediaTypeFormatter** 类配置为使用 **DataContractJsonSerializer** 而不是 Json.NET。</span><span class="sxs-lookup"><span data-stu-id="ebfed-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="ebfed-132">为此，请将 **UseDataContractJsonSerializer** 属性设置为 **true**：</span><span class="sxs-lookup"><span data-stu-id="ebfed-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="ebfed-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="ebfed-133">JSON Serialization</span></span>

<span data-ttu-id="ebfed-134">本部分介绍使用默认 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 序列化程序的 JSON 格式化程序的某些特定行为。</span><span class="sxs-lookup"><span data-stu-id="ebfed-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="ebfed-135">这并不是 Json.NET 库的综合文档;有关详细信息，请参阅 [Json.NET 文档](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="ebfed-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="ebfed-136">序列化的内容是什么？</span><span class="sxs-lookup"><span data-stu-id="ebfed-136">What Gets Serialized?</span></span>

<span data-ttu-id="ebfed-137">默认情况下，所有公共属性和字段均包括在序列化的 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="ebfed-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="ebfed-138">若要忽略某个属性或字段，请使用 **JsonIgnore** 属性修饰它。</span><span class="sxs-lookup"><span data-stu-id="ebfed-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="ebfed-139">如果更喜欢 &quot; 选择加入 &quot; 方法，请使用 **DataContract** 特性修饰类。</span><span class="sxs-lookup"><span data-stu-id="ebfed-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="ebfed-140">如果该属性存在，则将忽略成员，除非它们具有 **DataMember**。</span><span class="sxs-lookup"><span data-stu-id="ebfed-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="ebfed-141">你还可以使用 **DataMember** 来序列化私有成员。</span><span class="sxs-lookup"><span data-stu-id="ebfed-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="ebfed-142">Read-Only 属性</span><span class="sxs-lookup"><span data-stu-id="ebfed-142">Read-Only Properties</span></span>

<span data-ttu-id="ebfed-143">默认情况下，将对只读属性进行序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="ebfed-144">日期</span><span class="sxs-lookup"><span data-stu-id="ebfed-144">Dates</span></span>

<span data-ttu-id="ebfed-145">默认情况下，Json.NET 以 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 格式编写日期。</span><span class="sxs-lookup"><span data-stu-id="ebfed-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="ebfed-146">UTC 格式的日期 (使用 "Z" 后缀编写协调通用时间) 。</span><span class="sxs-lookup"><span data-stu-id="ebfed-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="ebfed-147">本地时间中的日期包括时区偏移量。</span><span class="sxs-lookup"><span data-stu-id="ebfed-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="ebfed-148">例如：</span><span class="sxs-lookup"><span data-stu-id="ebfed-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="ebfed-149">默认情况下，Json.NET 保留时区。</span><span class="sxs-lookup"><span data-stu-id="ebfed-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="ebfed-150">可以通过设置 DateTimeZoneHandling 属性来重写此：</span><span class="sxs-lookup"><span data-stu-id="ebfed-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="ebfed-151">如果希望使用 [MICROSOFT JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) ，而不是使用 ISO 8601，请在序列化程序设置上设置 **DateFormatHandling** 属性：</span><span class="sxs-lookup"><span data-stu-id="ebfed-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="ebfed-152">缩进</span><span class="sxs-lookup"><span data-stu-id="ebfed-152">Indenting</span></span>

<span data-ttu-id="ebfed-153">若要写入缩进的 JSON，请将 **格式** 设置设置为 "格式设置" **。缩进**：</span><span class="sxs-lookup"><span data-stu-id="ebfed-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="ebfed-154">Camel 大小写</span><span class="sxs-lookup"><span data-stu-id="ebfed-154">Camel Casing</span></span>

<span data-ttu-id="ebfed-155">若要以 camel 大小写形式编写 JSON 属性名称，而不更改数据模型，请在序列化程序上设置 **CamelCasePropertyNamesContractResolver** ：</span><span class="sxs-lookup"><span data-stu-id="ebfed-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="ebfed-156">匿名和 Weakly-Typed 对象</span><span class="sxs-lookup"><span data-stu-id="ebfed-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="ebfed-157">操作方法可以返回匿名对象并将其序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="ebfed-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="ebfed-158">例如：</span><span class="sxs-lookup"><span data-stu-id="ebfed-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="ebfed-159">响应消息正文将包含以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="ebfed-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="ebfed-160">如果 web API 从客户端接收松散结构化的 JSON 对象，则可以将请求正文反序列化为 \*\* 上的Newtonsoft.Js。JObject\*\* 类型。</span><span class="sxs-lookup"><span data-stu-id="ebfed-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="ebfed-161">但是，使用强类型化数据对象通常更好。</span><span class="sxs-lookup"><span data-stu-id="ebfed-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="ebfed-162">然后，你无需自行分析数据，并获得模型验证的优势。</span><span class="sxs-lookup"><span data-stu-id="ebfed-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="ebfed-163">XML 序列化程序不支持匿名类型或 **JObject** 实例。</span><span class="sxs-lookup"><span data-stu-id="ebfed-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="ebfed-164">如果对 JSON 数据使用这些功能，则应该从管道中删除 XML 格式化程序，如本文后面部分所述。</span><span class="sxs-lookup"><span data-stu-id="ebfed-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="ebfed-165">XML Media-Type 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="ebfed-166">XML 格式由 **XmlMediaTypeFormatter** 类提供。</span><span class="sxs-lookup"><span data-stu-id="ebfed-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="ebfed-167">默认情况下， **XmlMediaTypeFormatter** 使用 **DataContractSerializer** 类来执行序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="ebfed-168">如果需要，可以将 **XmlMediaTypeFormatter** 配置为使用 **XmlSerializer** ，而不是 **DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ebfed-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="ebfed-169">为此，请将 **UseXmlSerializer** 属性设置为 **true**：</span><span class="sxs-lookup"><span data-stu-id="ebfed-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="ebfed-170">**XmlSerializer**类支持比**DataContractSerializer**更窄的类型集，但可以更好地控制生成的 XML。</span><span class="sxs-lookup"><span data-stu-id="ebfed-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="ebfed-171">如果需要匹配现有的 XML 架构，请考虑使用 **XmlSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="ebfed-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="ebfed-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="ebfed-172">XML Serialization</span></span>

<span data-ttu-id="ebfed-173">本部分介绍使用默认 **DataContractSerializer**的 XML 格式化程序的某些特定行为。</span><span class="sxs-lookup"><span data-stu-id="ebfed-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="ebfed-174">默认情况下，DataContractSerializer 的行为如下所示：</span><span class="sxs-lookup"><span data-stu-id="ebfed-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="ebfed-175">所有公共读/写属性和字段均被序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="ebfed-176">若要忽略某个属性或字段，请使用 **IgnoreDataMember** 属性修饰它。</span><span class="sxs-lookup"><span data-stu-id="ebfed-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="ebfed-177">不序列化私有和受保护的成员。</span><span class="sxs-lookup"><span data-stu-id="ebfed-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="ebfed-178">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="ebfed-179">但 (会序列化只读集合属性的内容。 ) </span><span class="sxs-lookup"><span data-stu-id="ebfed-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="ebfed-180">类和成员名称在 XML 中以与它们在类声明中显示的完全相同的方式编写。</span><span class="sxs-lookup"><span data-stu-id="ebfed-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="ebfed-181">使用默认的 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="ebfed-181">A default XML namespace is used.</span></span>

<span data-ttu-id="ebfed-182">如果需要对序列化进行更多控制，则可以用 **DataContract** 特性修饰类。</span><span class="sxs-lookup"><span data-stu-id="ebfed-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="ebfed-183">如果该属性存在，则按如下方式序列化类：</span><span class="sxs-lookup"><span data-stu-id="ebfed-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="ebfed-184">&quot;选择采用 &quot; 方法：默认情况下不序列化属性和字段。</span><span class="sxs-lookup"><span data-stu-id="ebfed-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="ebfed-185">若要序列化属性或字段，请使用 **DataMember** 特性修饰它。</span><span class="sxs-lookup"><span data-stu-id="ebfed-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="ebfed-186">若要序列化私有或受保护成员，请使用 **DataMember** 特性来修饰它。</span><span class="sxs-lookup"><span data-stu-id="ebfed-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="ebfed-187">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="ebfed-188">若要更改类名称在 XML 中的显示方式，请在**DataContract**属性中设置*name*参数。</span><span class="sxs-lookup"><span data-stu-id="ebfed-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="ebfed-189">若要更改成员名称在 XML 中的显示方式，请设置**DataMember**特性中的*name*参数。</span><span class="sxs-lookup"><span data-stu-id="ebfed-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="ebfed-190">若要更改 XML 命名空间，请在**DataContract**类中设置*namespace*参数。</span><span class="sxs-lookup"><span data-stu-id="ebfed-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="ebfed-191">Read-Only 属性</span><span class="sxs-lookup"><span data-stu-id="ebfed-191">Read-Only Properties</span></span>

<span data-ttu-id="ebfed-192">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="ebfed-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="ebfed-193">如果只读属性有一个后备私有字段，则可以使用 **DataMember** 特性标记该私有字段。</span><span class="sxs-lookup"><span data-stu-id="ebfed-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="ebfed-194">此方法需要类的 **DataContract** 特性。</span><span class="sxs-lookup"><span data-stu-id="ebfed-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="ebfed-195">日期</span><span class="sxs-lookup"><span data-stu-id="ebfed-195">Dates</span></span>

<span data-ttu-id="ebfed-196">日期是采用 ISO 8601 格式编写的。</span><span class="sxs-lookup"><span data-stu-id="ebfed-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="ebfed-197">例如， &quot; 2012-05-23T20：21： 37.9116538 z &quot; 。</span><span class="sxs-lookup"><span data-stu-id="ebfed-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="ebfed-198">缩进</span><span class="sxs-lookup"><span data-stu-id="ebfed-198">Indenting</span></span>

<span data-ttu-id="ebfed-199">若要写入缩进的 XML，请将 " **缩进** " 属性设置为 **true**：</span><span class="sxs-lookup"><span data-stu-id="ebfed-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="ebfed-200">设置 Per-Type XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="ebfed-201">可以为不同的 CLR 类型设置不同的 XML 序列化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="ebfed-202">例如，你可能有一个需要 **XmlSerializer** 来实现向后兼容的特定数据对象。</span><span class="sxs-lookup"><span data-stu-id="ebfed-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="ebfed-203">可以为此对象使用 **XmlSerializer** ，并继续对其他类型使用 **DataContractSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="ebfed-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="ebfed-204">若要设置特定类型的 XML 序列化程序，请调用 **SetSerializer**。</span><span class="sxs-lookup"><span data-stu-id="ebfed-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="ebfed-205">可以指定 **XmlSerializer** 或从 **XmlObjectSerializer**派生的任何对象。</span><span class="sxs-lookup"><span data-stu-id="ebfed-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="ebfed-206">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="ebfed-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="ebfed-207">如果不想使用 JSON 格式化程序或格式化程序列表中的 XML 格式化程序，则可以将其删除。</span><span class="sxs-lookup"><span data-stu-id="ebfed-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="ebfed-208">执行此操作的主要原因是：</span><span class="sxs-lookup"><span data-stu-id="ebfed-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="ebfed-209">若要将 web API 响应限制为特定媒体类型，请使用。</span><span class="sxs-lookup"><span data-stu-id="ebfed-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="ebfed-210">例如，你可能决定仅支持 JSON 响应，并删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="ebfed-211">将默认格式化程序替换为自定义格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="ebfed-212">例如，你可以将 JSON 格式化程序替换为你自己的 JSON 格式化程序的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="ebfed-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="ebfed-213">下面的代码演示如何删除默认的格式化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="ebfed-214">从 global.asax 中定义的 **应用程序 \_ 启动** 方法调用此方法。</span><span class="sxs-lookup"><span data-stu-id="ebfed-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="ebfed-215">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="ebfed-215">Handling Circular Object References</span></span>

<span data-ttu-id="ebfed-216">默认情况下，JSON 和 XML 格式化程序将所有对象都作为值写入。</span><span class="sxs-lookup"><span data-stu-id="ebfed-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="ebfed-217">如果两个属性引用同一个对象，或者如果同一对象出现在集合中两次，则格式化程序会将对象序列化两次。</span><span class="sxs-lookup"><span data-stu-id="ebfed-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="ebfed-218">如果你的对象图包含循环，这是一个特殊的问题，因为序列化程序在检测到关系图中的循环时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="ebfed-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="ebfed-219">请考虑以下对象模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="ebfed-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="ebfed-220">调用此操作将导致格式化程序引发异常，该异常转换为状态代码 500 (内部服务器错误) 对客户端的响应。</span><span class="sxs-lookup"><span data-stu-id="ebfed-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="ebfed-221">若要在 JSON 中保留对象引用，请将以下代码添加到 global.asax 文件中的 **Application \_ Start** 方法：</span><span class="sxs-lookup"><span data-stu-id="ebfed-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="ebfed-222">现在，控制器操作将返回如下所示的 JSON：</span><span class="sxs-lookup"><span data-stu-id="ebfed-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="ebfed-223">请注意，序列化程序将 &quot; $id &quot; 属性添加到这两个对象。</span><span class="sxs-lookup"><span data-stu-id="ebfed-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="ebfed-224">此外，它还检测 Employee. 部门属性创建了一个循环，因此它会将值替换为对象引用： { &quot; $ref &quot; ： &quot; 1 &quot; }。</span><span class="sxs-lookup"><span data-stu-id="ebfed-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="ebfed-225">对象引用在 JSON 中不是标准引用。</span><span class="sxs-lookup"><span data-stu-id="ebfed-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="ebfed-226">使用此功能之前，请考虑客户端是否能够分析结果。</span><span class="sxs-lookup"><span data-stu-id="ebfed-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="ebfed-227">最好是从图形中删除循环。</span><span class="sxs-lookup"><span data-stu-id="ebfed-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="ebfed-228">例如，在此示例中，不需要从 Employee 返回到部门的链接。</span><span class="sxs-lookup"><span data-stu-id="ebfed-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="ebfed-229">若要在 XML 中保留对象引用，您有两种选择。</span><span class="sxs-lookup"><span data-stu-id="ebfed-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="ebfed-230">更简单的选项是添加 `[DataContract(IsReference=true)]` 到模型类。</span><span class="sxs-lookup"><span data-stu-id="ebfed-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="ebfed-231">*IsReference*参数启用对象引用。</span><span class="sxs-lookup"><span data-stu-id="ebfed-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="ebfed-232">请记住， **DataContract** 使序列化选择加入，因此还需要向属性中添加 **DataMember** 特性：</span><span class="sxs-lookup"><span data-stu-id="ebfed-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="ebfed-233">现在格式化程序生成的 XML 类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="ebfed-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="ebfed-234">如果您想要避免使用您的模型类上的属性，可以使用另一个选项：创建新的特定于类型的 **DataContractSerializer** 实例，并在构造函数中将 *preserveObjectReferences* 设置为 **true** 。</span><span class="sxs-lookup"><span data-stu-id="ebfed-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="ebfed-235">然后，将此实例设置为 XML 媒体类型格式化程序上的每个类型的序列化程序。</span><span class="sxs-lookup"><span data-stu-id="ebfed-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="ebfed-236">下面的代码演示如何执行此操作：</span><span class="sxs-lookup"><span data-stu-id="ebfed-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="ebfed-237">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="ebfed-237">Testing Object Serialization</span></span>

<span data-ttu-id="ebfed-238">设计 web API 时，测试如何序列化数据对象非常有用。</span><span class="sxs-lookup"><span data-stu-id="ebfed-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="ebfed-239">无需创建控制器或调用控制器操作即可执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ebfed-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

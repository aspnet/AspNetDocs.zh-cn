---
title: ASP.NET Core Web API 中的自定义格式化程序
author: rick-anderson
description: 了解如何为 ASP.NET Core 中的 Web API 创建和使用自定义格式化程序。
ms.author: tdykstra
ms.date: 02/08/2017
uid: web-api/advanced/custom-formatters
ms.openlocfilehash: 2861a15a80725dcc237d33313a24822cf8aa9c7e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033194"
---
# <a name="custom-formatters-in-aspnet-core-web-api"></a>ASP.NET Core Web API 中的自定义格式化程序

作者：[Tom Dykstra](https://github.com/tdykstra)

ASP.NET Core MVC 使用 JSON 或 XML，为 Web API 中的数据交换提供内置支持。 本文展示如何通过创建自定义格式化程序，添加对其他格式的支持。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="when-to-use-custom-formatters"></a>何时使用自定义格式化程序

如果希望[内容协商](xref:web-api/advanced/formatting#content-negotiation)过程支持内置格式化程序（JSON 和 XML）所不支持的内容类型，可使用自定义格式化程序。

例如，如果 Web API 的某些客户端可以处理 [Protobuf](https://github.com/google/protobuf) 格式，你可能想在这些客户端上使用 Protobuf，因为它更高效。 或者，你可能希望 Web API 使用 [vCard](https://wikipedia.org/wiki/VCard) 格式发送联系人姓名和地址，这种格式经常用于交换联系人数据。 本文提供的示例应用可实现简单的 vCard 格式化程序。

## <a name="overview-of-how-to-use-a-custom-formatter"></a>有关如何使用自定义格式化程序的概述

创建和使用自定义格式化程序的步骤如下：

* 如果想对要发送到客户端的数据进行序列化，则创建输出格式化程序类。
* 如果想对从客户端接收的数据进行反序列化，则创建输入格式化程序类。
* 将格式化程序的实例添加到 [MvcOptions](/dotnet/api/microsoft.aspnetcore.mvc.mvcoptions) 中的 `InputFormatters` 和 `OutputFormatters` 集合。

以下部分针对其中每个步骤提供了指南和代码示例。

## <a name="how-to-create-a-custom-formatter-class"></a>如何创建自定义格式化程序类

若要创建格式化程序，请执行以下操作：

* 从相应的基类中派生类。
* 在构造函数中指定有效的媒体类型和编码。
* 重写 `CanReadType`/`CanWriteType` 方法
* 重写 `ReadRequestBodyAsync`/`WriteResponseBodyAsync` 方法
  
### <a name="derive-from-the-appropriate-base-class"></a>从相应的基类中派生

对于文本媒体类型（例如，vCard），从 [TextInputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) 或 [TextOutputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) 基类派生。

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

有关输入格式化程序示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)。

对于二进制类型，从 [InputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.inputformatter) 或 [OutputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.outputformatter) 基类派生。

### <a name="specify-valid-media-types-and-encodings"></a>指定有效的媒体类型和编码

在构造函数中，通过添加到 `SupportedMediaTypes` 和 `SupportedEncodings` 集合来指定有效的媒体类型和编码。

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

有关输入格式化程序示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)。

> [!NOTE]
> 不能在格式化程序类中执行构造函数依赖关系注入。 例如，不能通过向构造函数添加记录器参数来获取记录器。 若要访问服务，必须使用传递到方法的上下文对象。 [下面](#read-write)的代码示例展示了如何执行此操作。

### <a name="override-canreadtypecanwritetype"></a>重写 CanReadType/CanWriteType

通过重写 `CanReadType` 或 `CanWriteType` 方法，指定可反序列化为或从其序列化的类型。 例如，可能只能从 `Contact` 类型创建 vCard 文本，反之亦然。

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

有关输入格式化程序示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)。

#### <a name="the-canwriteresult-method"></a>CanWriteResult 方法

在某些情况下，必须重写 `CanWriteResult`，而不是 `CanWriteType`。 如果满足以下条件，则使用 `CanWriteResult`：

* 操作方法返回模型类。
* 具有可能在运行时返回的派生类。
* 需要知道操作在运行时返回了哪个派生类。

例如，假设操作方法签名返回 `Person` 类型，但它可能返回从 `Person` 派生的 `Student` 或 `Instructor` 类型。 如果希望格式化程序仅处理 `Student` 对象，请检查提供给 `CanWriteResult` 方法的上下文对象中的[对象](/dotnet/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object)类型。 请注意，当操作方法返回 `IActionResult` 时，不必使用 `CanWriteResult`；在这种情况下，`CanWriteType` 方法可接收运行时类型。

<a id="read-write"></a>
### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a>重写 ReadRequestBodyAsync/WriteResponseBodyAsync

实际的反序列化或序列化工作在 `ReadRequestBodyAsync` 或 `WriteResponseBodyAsync` 中执行。 以下示例中突出显示的行展示了如何从依赖关系注入容器中获取服务（不能从构造函数参数中获取它们）。

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

有关输入格式化程序示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)。

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a>如何将 MVC 配置为使用自定义格式化程序

若要使用自定义格式化程序，请将格式化程序类的实例添加到 `InputFormatters` 或 `OutputFormatters` 集合。

[!code-csharp[](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

按格式化程序的插入顺序对其进行计算。 第一个优先。

## <a name="next-steps"></a>后续步骤

* [GitHub 上的纯文本格式化程序示例代码。](https://github.com/aspnet/Entropy/tree/master/samples/Mvc.Formatters)
* [此文档的示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample)，它可实现简单的 vCard 输入和输出格式化程序。 该应用可读取和写入与以下示例类似的 vCard：

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

若要查看 vCard 输出，请运行该应用程序，并向 `http://localhost:63313/api/contacts/`（从 Visual Studio 运行时）或 `http://localhost:5000/api/contacts/`（从命令行运行时）发送具有 Accept 标头“text/vcard”的 Get 请求。

若要将 vCard 添加到内存中联系人集合，请向相同的 URL 发送具有 Content-Type 标头“text/vcard”且正文中包含 vCard 文本的 Post 请求，格式化方式与上面的示例类似。

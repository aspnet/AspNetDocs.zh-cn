---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: 了解 ASP.NET AJAX Web 服务 |Microsoft Docs
author: scottcate
description: Web 服务是 .NET framework 的有机组成部分，它提供跨平台的解决方案，以便在分布式系统之间交换数据。 尽管 Web .。。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2020
ms.locfileid: "86162747"
---
# <a name="understanding-aspnet-ajax-web-services"></a>了解 ASP.NET AJAX Web 服务

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web 服务是 .NET framework 的有机组成部分，它提供跨平台的解决方案，以便在分布式系统之间交换数据。 尽管 Web 服务通常用于允许不同的操作系统、对象模型和编程语言来发送和接收数据，但它们也可用于将数据动态注入到 ASP.NET AJAX 页面，或将数据从页面发送到后端系统。 所有这些操作都可以完成，无需采取回发操作。

## <a name="calling-web-services-with-aspnet-ajax"></a>通过 ASP.NET AJAX 调用 Web 服务

Dan Wahlin

Web 服务是 .NET framework 的有机组成部分，它提供跨平台的解决方案，以便在分布式系统之间交换数据。 尽管 Web 服务通常用于允许不同的操作系统、对象模型和编程语言来发送和接收数据，但它们也可用于将数据动态注入到 ASP.NET AJAX 页面，或将数据从页面发送到后端系统。 所有这些操作都可以完成，无需采取回发操作。

尽管 ASP.NET AJAX UpdatePanel 控件提供了一种简单的方法来实现 AJAX 启用任何 ASP.NET 页，但有时你可能需要在不使用 UpdatePanel 的情况下动态访问服务器上的数据。 在本文中，你将了解如何通过在 ASP.NET AJAX 页面中创建和使用 Web 服务来完成此操作。

本文重点介绍 core ASP.NET AJAX 扩展中提供的功能，以及 ASP.NET AJAX 工具包中名为 AutoCompleteExtender 的启用了 Web 服务的控件。 涉及的主题包括定义启用 AJAX 的 Web 服务、创建客户端代理以及通过 JavaScript 调用 Web 服务。 你还将了解如何直接将 Web 服务调用 ASP.NET 到页面方法。

## <a name="web-services-configuration"></a>Web 服务配置

当使用 Visual Studio 2008 创建新的网站项目时，web.config 文件中有一些新的新增内容，这些新的内容可能不熟悉 Visual Studio 早期版本中的用户。 其中一些修改将 "asp" 前缀映射到 ASP.NET AJAX 控件，以便它们可用于页面，而其他项则可定义所需的 HttpHandlers 和 HttpModules。 列表1显示 `<httpHandlers>` 影响 Web 服务调用 web.config 中对元素所做的修改。 用于处理 .asmx 调用的默认 HttpHandler 将被删除，并替换为位于 System.Web.Extensions.dll 程序集中的 ScriptHandlerFactory 类。 System.Web.Extensions.dll 包含 ASP.NET AJAX 使用的所有核心功能。

**列表1。ASP.NET AJAX Web Service 处理程序配置**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

这种 HttpHandler 的替换是为了允许使用 JavaScript Web 服务代理从 ASP.NET AJAX 页面向 .NET Web 服务发出 JavaScript 对象表示法 (JSON) 调用。 ASP.NET AJAX 将 JSON 消息发送到 Web 服务，而不是标准简单对象访问协议 (SOAP) 调用通常与 Web 服务相关联。 这将导致整体的请求和响应消息。 它还允许对数据进行更高效的客户端处理，因为 ASP.NET AJAX JavaScript 库经过优化，可使用 JSON 对象。 列表2和列表3显示了序列化为 JSON 格式的 Web 服务请求和响应消息的示例。 清单2中显示的请求消息传递值为 "华南" 的国家/地区参数，而列表3中的响应消息传递客户对象的数组及其相关属性。

**清单2。序列化为 JSON 的 Web 服务请求消息**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]操作名称定义为 web 服务的 URL 的一部分; 此外，请求消息并不总是通过 JSON 提交。Web 服务可以利用 ScriptMethod 属性，并将 UseHttpGet 参数设置为 true，这将导致通过查询字符串参数传递参数。*

**列表3。序列化为 JSON 的 Web 服务响应消息**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

在下一部分中，你将了解如何创建能够处理 JSON 请求消息和响应简单和复杂类型的 Web 服务。

## <a name="creating-ajax-enabled-web-services"></a>创建启用 AJAX 的 Web 服务

ASP.NET AJAX framework 提供了几种不同的方法来调用 Web 服务。 可以使用 AutoCompleteExtender 控件 (在 ASP.NET AJAX 工具包) 或 JavaScript 中可用。 但是，在调用服务之前，您必须启用 AJAX，以便客户端脚本代码可以调用它。

无论你是否对 ASP.NET Web 服务都不熟悉，都可以轻松地创建和启用 AJAX 的服务。 自2002的初始版本以来，.NET framework 支持创建 ASP.NET Web 服务，ASP.NET AJAX 扩展提供了基于 .NET framework 的默认功能集构建的其他 AJAX 功能。 Visual Studio .NET 2008 Beta 2 内置了对创建 .asmx Web 服务文件的支持，并自动从 System.web 类的类中派生关联的代码。 在将方法添加到类中时，必须应用 WebMethod 特性，以便 Web 服务使用者调用这些方法。

列表4显示了一个将 WebMethod 属性应用于名为 GetCustomersByCountry 的方法 ( # A1 的示例。

**列表4。在 Web 服务中使用 WebMethod 属性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry ( # A1 方法接受国家/地区参数并返回客户对象数组。 传递给方法的国家/地区值将转发到业务层类，后者又会调用数据层类从数据库中检索数据，使用数据填充客户对象属性并返回数组。

## <a name="using-the-scriptservice-attribute"></a>使用 ScriptService 特性

在添加 WebMethod 特性时，将允许将标准 SOAP 消息发送到 Web 服务的客户端调用 GetCustomersByCountry ( # A1 方法，而不允许从现成的 ASP.NET AJAX 应用程序调用 JSON。 若要允许进行 JSON 调用，必须将 ASP.NET AJAX 扩展的属性应用于 `ScriptService` Web 服务类。 这使 Web 服务可以发送使用 JSON 格式化的响应消息，并允许客户端脚本通过发送 JSON 消息来调用服务。

列表5显示了一个将 ScriptService 属性应用于名为 CustomersService 的 Web 服务类的示例。

**列表5。使用 ScriptService 属性通过 AJAX 启用 Web 服务**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 特性用作标记，该标记指示可以从 AJAX 脚本代码中调用它。 它不会实际处理在幕后发生的任何 JSON 序列化或反序列化任务。 web.config) 和其他相关类中配置的 ScriptHandlerFactory (进行批量处理。

## <a name="using-the-scriptmethod-attribute"></a>使用 ScriptMethod 特性

ScriptService 特性是唯一必须在 .NET Web 服务中定义的 ASP.NET AJAX 特性，以便 ASP.NET AJAX 页可以使用该特性。 但是，另一个名为 ScriptMethod 的属性也可以直接应用于服务中的 Web 方法。 ScriptMethod 定义了三个属性 `UseHttpGet` ，包括、 `ResponseFormat` 和 `XmlSerializeString` 。 更改这些属性的值在以下情况下很有用：当 web 方法接受的请求类型需要更改为获取时，当 Web 方法需要以或对象的形式返回原始 XML 数据时， `XmlDocument` `XmlElement` 或应始终将从服务返回的数据序列化为 XML 而不是 JSON。

当 Web 方法应接受 GET 请求而不是 POST 请求时，可以使用 UseHttpGet 属性。 使用 URL，并将 Web 方法输入参数转换为 QueryString 参数来发送请求。 UseHttpGet 属性默认为 false，只应 `true` 在已知操作安全时设置为，并且不会将敏感数据传递到 Web 服务。 列表6显示了在 UseHttpGet 属性中使用 ScriptMethod 属性的示例。

**清单6。结合使用 ScriptMethod 属性和 UseHttpGet 属性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

下面显示了在列表6中所示的 HttpGetEcho Web 方法被调用时发送的标头示例：

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

除了允许 Web 方法接受 HTTP GET 请求之外，还可以在需要从服务而不是 JSON 返回 XML 响应时使用 ScriptMethod 属性。 例如，Web 服务可以从远程站点检索 RSS 源，并将其作为 Xml 或 XmlElement 对象返回。 然后，可以在客户端上处理 XML 数据。

列表7显示了使用 ResponseFormat 属性来指定应从 Web 方法返回 XML 数据的示例。

**列表7。结合使用 ScriptMethod 属性和 ResponseFormat 属性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 属性还可以与 XmlSerializeString 属性一起使用。 XmlSerializeString 属性的默认值为 false，这意味着，当属性设置为时，所有返回类型（从 Web 方法返回的字符串除外）将序列化为 XML `ResponseFormat` `ResponseFormat.Xml` 。 当 `XmlSerializeString` 设置为时 `true` ，从 Web 方法返回的所有类型将序列化为包含字符串类型的 XML。 如果 ResponseFormat 属性的值 `ResponseFormat.Json` 为 XmlSerializeString，则将忽略该属性的值。

列表8显示了使用 XmlSerializeString 属性强制将字符串序列化为 XML 的示例。

**列表8。结合使用 ScriptMethod 属性和 XmlSerializeString 属性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

下面显示了通过调用列表8中所示的 GetXmlString Web 方法返回的值：

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

尽管默认 JSON 格式最大程度地减少了请求和响应消息的总大小，并且通过跨浏览器方式 ASP.NET AJAX 客户端更容易地使用，但当 Internet Explorer 5 或更高版本的客户端应用程序需要从 Web 方法返回 XML 数据时，可以使用 ResponseFormat 和 XmlSerializeString 属性。

## <a name="working-with-complex-types"></a>使用复杂类型

列表5显示了从 Web 服务返回名为 Customer 的复杂类型的示例。 Customer 类在内部定义多个不同的简单类型作为属性，如 FirstName 和 LastName。 在支持 AJAX 的 Web 方法上用作输入参数或返回类型的复杂类型在发送到客户端之前会自动序列化为 JSON。 不过，默认情况下，嵌套的复杂类型 (在另一类型中内部定义的类型) 默认情况下，客户端不能作为独立对象提供给客户端。

如果 Web 服务使用的嵌套复杂类型还必须在客户端页中使用，则可以将 ASP.NET AJAX GenerateScriptType 特性添加到 Web 服务。 例如，"列表 9" 中所示的 CustomerDetails 类包含***表示嵌套复杂类型***的 "地址" 和 "性别" 属性。

**列表9。此处所示的 CustomerDetails 类包含两个嵌套的复杂类型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

列表9中所示的 CustomerDetails 类中定义的地址和性别对象将不会自动在客户端上使用，因为它们是嵌套类型 (Address 是类，而性别是) 的枚举。 在 Web 服务中使用的嵌套类型必须在客户端上可用的情况下，可以使用前面提到的 GenerateScriptType 属性 (参阅列出 10) 。 如果从服务返回不同的嵌套复杂类型，则可以多次添加此特性。 它可以直接应用于 Web 服务类，也可以应用于特定的 Web 方法。

**列表10。使用 GenerateScriptService 属性定义应该可供客户端使用的嵌套类型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

通过将 `GenerateScriptType` 特性应用于 Web 服务，地址和性别类型将自动可供客户端 ASP.NET AJAX JavaScript 代码使用。 列表11中显示了自动生成并通过在 Web 服务中添加 GenerateScriptType 属性发送到客户端的 JavaScript 示例。 本文稍后将介绍如何使用嵌套的复杂类型。

**列表11。ASP.NET AJAX 页面提供的嵌套复杂类型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

现在，你已了解如何创建 Web 服务并使其可供 ASP.NET AJAX 页面访问，接下来让我们看看如何创建和使用 JavaScript 代理，以便可以检索数据或将数据发送到 Web 服务。

## <a name="creating-javascript-proxies"></a>创建 JavaScript 代理

 ( .NET 或其他) 平台调用标准 Web 服务通常涉及到创建一个代理对象，以防止发送 SOAP 请求和响应消息的复杂性。 使用 ASP.NET AJAX Web 服务调用，可以创建 JavaScript 代理并使用它轻松调用服务，而不必担心序列化和反序列化 JSON 消息。 可以使用 ASP.NET AJAX ScriptManager 控件自动生成 JavaScript 代理。

可以通过使用 ScriptManager 的 "服务" 属性来创建可以调用 Web 服务的 JavaScript 代理。 使用此属性可以定义一个或多个服务，ASP.NET AJAX 页可以异步调用该服务来发送或接收数据，而无需回发操作。 可以使用 ASP.NET AJAX 控件定义服务 `ServiceReference` ，并将 Web 服务 URL 分配给控件的 `Path` 属性。 列表12显示了引用名为 CustomersService 的服务的示例。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**列表12。定义 ASP.NET AJAX 页中使用的 Web 服务。**

通过 ScriptManager 控件添加对 CustomersService 的引用会导致 JavaScript 代理动态生成并由页面引用。 代理通过使用脚本标记进行嵌入 &lt; &gt; ，并通过调用 CustomersService 文件并将可通过/js 追加到末尾来进行动态加载。 下面的示例演示在 web.config 中禁用调试后，如何在页面中嵌入 JavaScript 代理：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]如果你想要查看生成的实际 JavaScript 代理代码，你可以在 Internet Explorer 的 "地址" 框中键入所需 .Net Web 服务的 URL，并将可通过/js 追加到其末尾。*

如果在 web.config 中启用了调试，则会在页面中嵌入 JavaScript 代理的调试版本，如下所示：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager 创建的 JavaScript 代理也可以直接嵌入到页面中，而不是使用 &lt; 脚本 &gt; 标记的 src 属性进行引用。 为此，可以将 ServiceReference 控件的 InlineScript 属性设置为 true， (默认值为 false) 。 当代理不在多个页面之间共享，并且想要减少对服务器进行的网络调用时，这会很有用。 如果 InlineScript 设置为 true，则浏览器将不会缓存代理脚本，因此，在 ASP.NET AJAX 应用程序中多个页面使用代理的情况下，建议使用默认值 false。 下面显示了使用 InlineScript 属性的示例：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>使用 JavaScript 代理

使用 ScriptManager 控件引用 ASP.NET AJAX 页面后，就可以对 Web 服务进行调用，并可以使用回调函数处理返回的数据。 Web 服务将通过引用其命名空间来调用 (如果存在) 、类名称和 Web 方法名称。 传递给 Web 服务的任何参数均可与处理返回数据的回调函数一起定义。

列表13中显示了使用 JavaScript 代理调用名为 GetCustomersByCountry ( Web 方法的示例。 当最终用户单击页面上的按钮时，将调用 GetCustomersByCountry ( # A1 函数。

**列表13。使用 JavaScript 代理调用 Web 服务。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

此调用引用在服务中定义的 InterfaceTraining 命名空间、CustomersService 类和 GetCustomersByCountry Web 方法。 它传递从 textbox 获取的国家/地区值，以及一个名为 OnWSRequestComplete 的回调函数，该函数应在异步 Web 服务调用返回时调用。 OnWSRequestComplete 处理从服务返回的客户对象的数组，并将它们转换为该页中显示的表。 从调用生成的输出如图1所示。

[![通过对 Web 服务进行异步 AJAX 调用来获取绑定的数据。](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**图 1**：通过对 Web 服务进行异步 AJAX 调用获得的绑定数据。   ([单击查看全尺寸图像](understanding-asp-net-ajax-web-services/_static/image3.png)) 

JavaScript 代理还可以在应调用 Web 方法但代理不应等待响应的情况下，对 Web 服务进行单向调用。 例如，你可能想要调用 Web 服务来启动进程（例如工作流），而不是等待来自服务的返回值。 如果需要对服务进行单向调用，则只需省略列表13中所示的回调函数。 由于未定义回调函数，因此代理对象将不会等待 Web 服务返回数据。

## <a name="handling-errors"></a>处理错误

对 Web 服务的异步回调可能会遇到各种类型的错误，例如网络关闭、Web 服务不可用或返回异常。 幸运的是，ScriptManager 生成的 JavaScript 代理对象允许定义多个回调，以处理前面所示的成功回调。 错误回调函数可在调用 Web 方法的标准回调函数之后立即定义，如列表14中所示。

**列表14。定义错误回调函数并显示错误。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

在调用 Web 服务时出现的任何错误都将触发 OnWSRequestFailed ( # A1 回调函数，该函数接受一个表示错误的对象作为参数。 Error 对象公开几个不同的函数来确定错误的原因，以及调用是否超时。列表14显示了使用不同错误函数的示例，图2显示了函数生成的输出示例。

[![通过调用 ASP.NET AJAX 错误函数生成的输出。](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**图 2**：通过调用 ASP.NET AJAX 错误函数生成的输出。   ([单击查看全尺寸图像](understanding-asp-net-ajax-web-services/_static/image6.png)) 

## <a name="handling-xml-data-returned-from-a-web-service"></a>处理从 Web 服务返回的 XML 数据

之前，你已了解 Web 方法如何通过使用 ScriptMethod 属性及其 ResponseFormat 属性返回原始 XML 数据。 当 ResponseFormat 设置为 ResponseFormat.Xml 时，从 Web 服务返回的数据将序列化为 XML 而不是 JSON。 当需要将 XML 数据直接传递到客户端以便使用 JavaScript 或 XSLT 进行处理时，这会很有用。 目前，Internet Explorer 5 或更高版本提供了最佳的客户端对象模型，用于分析和筛选 XML 数据，因为它是对 MSXML 的内置支持。

从 Web 服务检索 XML 数据与检索其他数据类型没有什么不同。 首先调用 JavaScript 代理来调用适当的函数并定义回调函数。 调用返回后，可以处理回调函数中的数据。

列表15显示了一个示例，该示例调用名为 GetRssFeed 的 Web 方法 ( # A1，该方法返回 XmlElement 对象。 GetRssFeed ( # A1 接受一个参数，表示要检索的 RSS 源的 URL。

**列表15。使用从 Web 服务返回的 XML 数据。**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

此示例将 URL 传递到 RSS 源，并在 OnWSRequestComplete ( # A1 函数中处理返回的 XML 数据。 OnWSRequestComplete ( # A1 首先检查浏览器是否为 Internet Explorer，以确定 MSXML 分析器是否可用。 如果是，则使用 XPath 语句来查找 &lt; &gt; RSS 源中的所有项标记。 然后循环访问每个项，并 &lt; &gt; 定位并处理关联的标题和 &lt; 链接标记， &gt; 以显示每个项的数据。 图3显示了一个示例，该示例是从通过 JavaScript 代理向 GetRssFeed ( # A1 Web 方法发出 ASP.NET AJAX 调用而生成的。

## <a name="handling-complex-types"></a>处理复杂类型

Web 服务接受或返回的复杂类型会自动通过 JavaScript 代理公开。 但是，不能在客户端上直接访问嵌套的复杂类型，除非 GenerateScriptType 属性应用到前面所述的服务。 为什么要在客户端使用嵌套的复杂类型？

若要回答此问题，假设 ASP.NET AJAX 页面显示客户数据并允许最终用户更新客户的地址。 如果 Web 服务指定的地址类型 (在 CustomerDetails 类中定义的复杂类型) 可以发送到客户端，则可以将更新过程划分为单独的函数，以便更好地重复使用代码。

[![从调用返回 RSS 数据的 Web 服务创建的输出。](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**图 3**：从调用返回 RSS 数据的 Web 服务创建的输出。   ([单击查看全尺寸图像](understanding-asp-net-ajax-web-services/_static/image9.png)) 

列表16显示了客户端代码示例，该代码调用在模型命名空间中定义的地址对象，使用更新的数据填充该对象，并将其分配给 CustomerDetails 对象的 Address 属性。 然后，将 CustomerDetails 对象传递给 Web 服务进行处理。

**列出的16。使用嵌套的复杂类型**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>创建和使用页面方法

Web 服务提供了向各种客户端（包括 ASP.NET AJAX 页面）公开可重复使用的服务的绝佳方式。 但是，在某些情况下，页面需要检索不是由其他页面使用或共享的数据。 在这种情况下，创建 .asmx 文件以允许页访问数据可能看起来像多余，因为该服务仅由单个页面使用。

ASP.NET AJAX 提供了另一种机制，用于进行类似 Web 服务的调用，而无需创建独立的 .asmx 文件。 这是通过使用一种称为 "页面方法" 的技术来完成的。 页面方法是静态 (在 VB.NET 中共享的) 方法，这些方法直接嵌入在应用了 WebMethod 特性的页或代码旁置文件中。 通过应用 WebMethod 特性，可以使用一个名为 PageMethods 的特殊 JavaScript 对象调用，该对象在运行时动态创建。 PageMethods 对象充当代理，用于阻止 JSON 序列化/反序列化过程。 请注意，若要使用 PageMethods 对象，必须将 ScriptManager 的 EnablePageMethods 属性设置为 true。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

列表17显示了一个示例，说明如何在 ASP.NET 的代码旁置类中定义两个页面方法。 这些方法从网站的应用代码文件夹中的业务层类检索数据 \_ 。

**列出17。定义页面方法。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

当 ScriptManager 检测到页中存在 Web 方法时，它会生成一个对前面提到的 PageMethods 对象的动态引用。 调用 Web 方法的方法是：引用 PageMethods 类，后跟方法的名称和应传递的任何必要参数数据。 列表18显示了调用上述两个 page 方法的示例。

**列出18。调用带有 PageMethods JavaScript 对象的页面方法。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

使用 PageMethods 对象与使用 JavaScript 代理对象非常类似。 首先指定应传递给 page 方法的所有参数数据，然后定义应在异步调用返回时调用的回调函数。 还可以指定失败回调 (引用列表14，以) 处理失败的示例。

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 和 ASP.NET AJAX 工具包

)  (提供的 ASP.NET AJAX 工具包 [http://ajax.asp.net](http://ajax.asp.net) 提供了可用于访问 Web 服务的多个控件。 具体而言，该工具包包含一个名为 `AutoCompleteExtender` 的有用控件，该控件可用于调用 Web 服务并在页中显示数据，而无需编写任何 JavaScript 代码。

AutoCompleteExtender 控件可用于扩展文本框的现有功能，帮助用户更轻松地找到要查找的数据。 当他们在文本框中键入时，控件可用于查询 Web 服务并动态显示文本框下方的结果。 图4显示了使用 AutoCompleteExtender 控件显示支持应用程序的客户 id 的示例。 当用户在文本框中键入不同的字符时，将根据输入的内容在其下方显示不同的项。 然后，用户可以选择所需的客户 id。

在 ASP.NET AJAX 页中使用 AutoCompleteExtender 要求将 AjaxControlToolkit.dll 程序集添加到网站的 bin 文件夹中。 添加工具包程序集后，您将需要在 web.config 中引用该程序集，使其包含的控件可用于应用程序中的所有页。 可以通过在 web.config 的 controls 标记中添加以下标记来完成此 &lt; &gt; 操作：

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

如果只需要在特定页面中使用控件，则可以通过将 Reference 指令添加到页面顶部来引用它，如下所示，而不是更新 web.config：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![使用 AutoCompleteExtender 控件。](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**图 4**：使用 AutoCompleteExtender 控件。   ([单击查看全尺寸图像](understanding-asp-net-ajax-web-services/_static/image12.png)) 

将网站配置为使用 ASP.NET AJAX 工具包后，可以将 AutoCompleteExtender 控件添加到页面中，就像添加常规的 ASP.NET 服务器控件一样。 列表19显示了使用控件调用 Web 服务的示例。

**列出19。使用 ASP.NET AJAX 工具包 AutoCompleteExtender 控件。**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender 具有多个不同的属性，包括在服务器控件上找到的标准 ID 和 runat 属性。 除此之外，它还允许您定义最终用户在对 Web 服务进行数据查询之前键入的字符数。 当在文本框中键入字符时，列表19中显示的 MinimumPrefixLength 属性会导致调用服务。 你需要小心设置此值，因为每次用户键入一个字符时，将调用 Web 服务来搜索与文本框中的字符匹配的值。 将分别使用 ServicePath 和 ServiceMethod 属性定义要调用的 Web 服务以及目标 Web 方法。 最后，TargetControlID 属性标识将 AutoCompleteExtender 控件挂钩到的文本框。

正在调用的 Web 服务必须按前面所述应用 ScriptService 属性，并且目标 Web 方法必须接受名为 prefixText 的两个参数和 count。 PrefixText 参数表示由最终用户键入的字符，count 参数表示 (默认值为 10) 时返回多少项。 列表20显示了 GetCustomerIDs Web 方法的示例，该方法由前面的列表19中所示的 AutoCompleteExtender 控件调用。 Web 方法调用一个业务层方法，该方法又调用一个数据层方法，该方法可处理对数据的筛选并返回匹配结果。 数据层方法的代码显示在列表21中。

**列表20。筛选从 AutoCompleteExtender 控件发送的数据。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**列表21。基于最终用户输入来筛选结果。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>结论

ASP.NET AJAX 提供了对调用 Web 服务的出色支持，无需编写大量的自定义 JavaScript 代码来处理请求和响应消息。 在本文中，你已了解如何通过 AJAX 启用 .NET Web 服务来处理 JSON 消息，以及如何使用 ScriptManager 控件定义 JavaScript 代理。 你还了解了如何使用 JavaScript 代理来调用 Web 服务、处理简单和复杂类型并处理故障。 最后，你已了解了如何使用页面方法来简化创建和发出 Web 服务调用的过程，以及 AutoCompleteExtender 控件如何向最终用户键入信息。 尽管 ASP.NET AJAX 中提供的 UpdatePanel 当然会对许多 AJAX 程序员做出选择，因为它是简单的，但了解如何通过 JavaScript 代理调用 Web 服务在许多应用程序中都很有用。

## <a name="bio"></a>个人简介

Dan Wahlin (Microsoft 最有价值的 ASP.NET 和 XML Web Services 专业人员) 是 .NET 开发讲师和体系结构顾问，提供 () 的界面技术培训 [http://www.interfacett.com](http://www.interfacett.com) 。 Dan 构建了 XML for ASP.NET 开发人员网站 ([www.XMLforASP.NET](http://www.XMLforASP.NET)) ，位于 INETA 演讲者的局上，并发表了几个会议。 Dan 共同创作的专业 Windows 责任 (Wrox) ，ASP.NET：技巧，教程和代码 (Sam) ，ASP.NET 1.1 有问必答解决方案，专业 ASP.NET 2.0 AJAX (Wrox) ，ASP.NET 2.0 MVP 黑客和为 ASP.NET 开发人员编写的 XML (Sams) 。 当他不编写代码、文章或书籍时，Dan 喜欢撰写和录制音乐，并通过他的妻子和孩子玩高尔夫和篮球。

Scott Cate 已使用 Microsoft Web 技术，因为1997，是 myKB.com ([www.myKB.com](http://www.myKB.com)) 的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 或[ScottCate.com](http://ScottCate.com)上的博客联系 Scott

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-localization.md)
> [下一页](understanding-asp-net-ajax-debugging-capabilities.md)

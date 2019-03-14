---
title: ASP.NET Core 中的模型绑定
author: tdykstra
description: 了解 ASP.NET Core MVC 中的模型绑定如何将 HTTP 请求中的数据映射到操作方法参数。
ms.assetid: 0be164aa-1d72-4192-bd6b-192c9c301164
ms.author: tdykstra
ms.date: 11/13/2018
uid: mvc/models/model-binding
ms.openlocfilehash: 1dc9b41328ed78440622acc1865b6f088d394403
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037044"
---
# <a name="model-binding-in-aspnet-core"></a>ASP.NET Core 中的模型绑定

作者：[Rachel Appel](https://github.com/rachelappel)

## <a name="introduction-to-model-binding"></a>模型绑定简介

ASP.NET Core MVC 中的模型绑定将 HTTP 请求中的数据映射到操作方法参数。 这些参数可能是简单类型的参数，如字符串、整数或浮点数，也可能是复杂类型的参数。 这是 MVC 的一项强大功能，因为不管数据的大小和复杂性，将传入数据映射到对应位置都是经常重复的方案。 MVC 通过将绑定抽象出来解决了这一问题，使开发者不必在每个应用中重写同一代码的稍微不同版本。 向类型转换器代码写入自己的文本不仅繁琐乏味，而且容易出错。

## <a name="how-model-binding-works"></a>模型绑定的工作原理

当 MVC 收到 HTTP 请求时，它会将此请求路由到控制器的特定操作方法。 它基于路由数据中的内容决定要运行的操作方法，然后将 HTTP 请求中的值绑定到该操作方法的参数。 以下列 URL 为例：

`http://contoso.com/movies/edit/2`

由于路由模板为 `{controller=Home}/{action=Index}/{id?}`，因此，`movies/edit/2` 将路由到 `Movies` 控制器及其 `Edit` 操作方法。 此外，它还接受名为 `id` 的可选参数。 操作方法的代码应如下所示：

```csharp
public IActionResult Edit(int? id)
   ```

注意:URL 路由中的字符串不区分大小写。

MVC 将尝试按名称将请求数据绑定到操作参数。 MVC 将使用参数名称和其公共可设置属性的名称查找每个参数的值。 在以上示例中，唯一的操作参数名为 `id`，MVC 会将此参数绑定到路由值中具有相同名称的值。 除路由值外，MVC 还会绑定来自请求各个部分的数据，并按一定顺序执行此操作。 下面是一个数据源列表（按模型绑定查看的顺序排列）：

1. `Form values`：这些是在 HTTP 请求使用 POST 方法的窗体值。 （包括 jQuery POST 请求）。

2. `Route values`：通过提供的路由值集[路由](xref:fundamentals/routing)

3. `Query strings`：URI 查询字符串部分。

<!-- DocFX BUG
The link works but generates an error when building with DocFX
@fundamentals/routing
[Routing](xref:fundamentals/routing)
-->

注意:窗体值、 路由数据和查询字符串存储为名称 / 值对。

由于模型绑定请求名为 `id` 的键，而窗体值中没有任何名为 `id` 的键，因此，它将转到路由值以查找该键。 在本示例中，该键是一个匹配项。 发生绑定，并且值被转换为整数 2。 使用 Edit(string id) 的同一请求将转换为字符串“2”。

到目前为止，示例使用的都是简单类型。 在 MVC 中，简单类型是任何 .NET 基元类型或包含字符串类型转换器的类型。 如果操作方法的参数是一个属性为简单类型和复杂类型的类，如 `Movie` 类型，则 MVC 的模型绑定仍可对其进行妥善处理。 它使用反射和递归来遍历查找匹配项的复杂类型的属性。 模型绑定查找模式 parameter_name.property_name 以将值绑定到属性 。 如果未找到此窗体的匹配值，它将尝试仅使用属性名称进行绑定。 对于诸如 `Collection` 类型的类型，模型绑定将查找 parameter_name[index] 或仅 [index] 的匹配项。 对于 `Dictionary` 类型，模型绑定的处理方法与之类似，即请求 parameter_name[key] 或仅 [key]（只要键是简单类型）。 受支持的键匹配字段名称 HTML 和针对相同模型类型生成的标记帮助程序。 这样就可以启用往返值，以便用户仍能方便地输入内容来填充窗体字段，例如当创建或编辑的绑定数据未通过验证时。

若要实现模型绑定，该类必须具有要绑定的公共默认构造函数和公共可写属性。 发生模型绑定时，在使用公共默认构造函数对类进行实例化后才可设置属性。

绑定参数时，模型绑定将停止查找具有该名称的值并向前移动以绑定下一个参数。 否则，默认模型绑定行为将根据参数的类型将参数设置为其默认值：

* `T[]`：类型的数组除外`byte[]`，绑定类型的参数设置`T[]`到`Array.Empty<T>()`。 `byte[]` 类型的数组设置为 `null`。

* 引用类型：绑定的默认构造函数中创建类的实例，而无需设置属性。 但是，模型绑定将 `string` 参数设置为 `null`。

* 可为 null 类型：可以为 null 的类型设置为`null`。 在上面的示例中，模型绑定将 `id` 设置为 `null`，因为其类型为 `int?`。

* 值类型：可以为非 null 值类型的类型`T`设置为`default(T)`。 例如，模型绑定将参数 `int id` 设置为 0。 请考虑使用模型验证或可以为 null 的类型，而不是依赖于默认值。

如果绑定失败，MVC 不会引发错误。 接受用户输入的每个操作均应检查 `ModelState.IsValid` 属性。

注意:在控制器的每个条目`ModelState`属性是`ModelStateEntry`包含`Errors`属性。 很少需要自行查询此集合。 请改用 `ModelState.IsValid`。

此外，MVC 在执行模型绑定时必须考虑一些特殊数据类型：

* `IFormFile`, `IEnumerable<IFormFile>`:一个或多个已上传的文件的 HTTP 请求的一部分。

* `CancellationToken`：用于取消异步控制器中的活动。

这些类型可绑定到操作参数或类类型的属性。

模型绑定完成后，将发生[验证](validation.md)。 对于绝大多数开发方案，默认模型绑定效果极佳。 它还可以扩展，因此如果你有特殊需求，则可自定义内置行为。

## <a name="customize-model-binding-behavior-with-attributes"></a>通过特性自定义模型绑定行为

MVC 包含多种特性，可用于将其默认模型绑定行为定向到不同的源。 例如，可以使用 `[BindRequired]` 或 `[BindNever]` 特性指定属性是否需要绑定，或绑定是否根本不应发生。 或者，可以替代默认数据源，并指定模型绑定器的数据源。 下面是模型绑定特性的列表：

* `[BindRequired]`：如果无法发生绑定，此属性将添加模型状态错误。

* `[BindNever]`：指示模型绑定器从不绑定到此参数。

* `[FromHeader]`, `[FromQuery]`, `[FromRoute]`, `[FromForm]`:使用这些特性指定你想要应用的确切绑定源。

* `[FromServices]`：此特性使用[依赖关系注入](../../fundamentals/dependency-injection.md)以从服务绑定参数。

* `[FromBody]`：使用已配置的格式化程序绑定请求正文中的数据。 基于请求的内容类型，选择格式化程序。

* `[ModelBinder]`：用于替代默认模型联编程序，绑定源和名称。

需要替代模型绑定的默认行为时，特性是非常有用的工具。

## <a name="customize-model-binding-and-validation-globally"></a>全局自定义模型绑定和验证

由 [ModelMetadata](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.modelmetadata) 驱动模型绑定和验证系统的行为，该行为描述：

* 如何绑定模型。
* 如何验证类型及其属性。

通过向 [MvcOptions.ModelMetadataDetailsProviders](/dotnet/api/microsoft.aspnetcore.mvc.mvcoptions.modelmetadatadetailsproviders#Microsoft_AspNetCore_Mvc_MvcOptions_ModelMetadataDetailsProviders) 添加详细信息提供程序，可以全局配置系统行为的各个方面。 MVC 有一些内置的详细信息提供程序，可通过它们配置禁用模型绑定或验证某些类型等行为。

若要禁用对特定类型的所有模型的模型绑定，请在 `Startup.ConfigureServices` 中添加 [ExcludeBindingMetadataProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.metadata.excludebindingmetadataprovider)。 例如，禁用对 `System.Version` 类型的所有模型的模型绑定：

```csharp
services.AddMvc().AddMvcOptions(options =>
    options.ModelMetadataDetailsProviders.Add(
        new ExcludeBindingMetadataProvider(typeof(System.Version))));
```

要禁用对特定类型的属性的验证，请在 `Startup.ConfigureServices` 中添加 [SuppressChildValidationMetadataProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.suppresschildvalidationmetadataprovider)。 例如，禁用对 `System.Guid` 类型的属性的验证：

```csharp
services.AddMvc().AddMvcOptions(options =>
    options.ModelMetadataDetailsProviders.Add(
        new SuppressChildValidationMetadataProvider(typeof(System.Guid))));
```

## <a name="bind-formatted-data-from-the-request-body"></a>绑定请求正文中的带格式数据

请求数据可以有各种格式，包括 JSON、XML 和许多其他格式。 使用 [FromBody] 特性指示要将参数绑定到请求正文中的数据时，MVC 会使用一组已配置的格式化程序基于请求数据的内容类型对请求数据进行处理。 默认情况下，MVC 包括用于处理 JSON 数据的 `JsonInputFormatter` 类，但你可以添加用于处理 XML 和其他自定义格式的其他格式化程序。

> [!NOTE]
> 对于用 `[FromBody]` 修饰的每个操作，最多可以有一个参数。 ASP.NET Core MVC 运行时向格式化程序委托读取请求流的责任。 读取参数的请求流后，通常不能为绑定其他 `[FromBody]` 参数而再次读取请求流。

> [!NOTE]
> `JsonInputFormatter` 为默认格式化程序且基于 [Json.NET](https://www.newtonsoft.com/json)。

除非有特性应用于 ASP.NET Core，否则它将基于 [Content-Type](https://www.w3.org/Protocols/rfc1341/4_Content-Type.html) 标头和参数类型来选择输入格式化程序。 如果想要使用 XML 或其他格式，则必须在 Startup.cs 文件中配置该格式，但可能必须先使用 NuGet 获取对 `Microsoft.AspNetCore.Mvc.Formatters.Xml` 的引用。 启动代码应如下所示：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddXmlSerializerFormatters();
   }
```

Startup.cs 文件中的代码包含具有 `services` 参数的 `ConfigureServices` 方法，此方法可用于为 ASP.NET Core 应用生成服务。 在此示例中，我们将添加 XML 格式化程序作为 MVC 将为此应用提供的服务。 通过传递给 `AddMvc` 方法的 `options` 参数，可在应用启动后添加和管理筛选器、格式化程序和其他 MVC 系统选项。 然后，将 `Consumes` 特性应用于控制器类或操作方法，以使用所需格式。

### <a name="custom-model-binding"></a>自定义模型绑定

可通过编写自己的自定义模型绑定器来扩展模型绑定。 详细了解[自定义模型绑定](../advanced/custom-model-binding.md)。

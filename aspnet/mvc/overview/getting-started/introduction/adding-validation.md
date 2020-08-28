---
uid: mvc/overview/getting-started/introduction/adding-validation
title: 正在添加验证 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044345"
---
# <a name="adding-validation"></a>添加验证

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本部分中，你将向模型中添加验证逻辑 `Movie` ，并确保每当用户尝试使用应用程序创建或编辑电影时，都会强制执行验证规则。

## <a name="keeping-things-dry"></a>使东西干燥

ASP.NET MVC 的核心设计原则之一 [是 (](http://en.wikipedia.org/wiki/Don't_repeat_yourself) &quot; 不要自我重复 &quot;) 。 ASP.NET MVC 鼓励您仅指定一次功能或行为，然后让它在应用程序中的任何位置进行反映。 这会减少需要编写的代码量，并使编写的代码更少出错并且更易于维护。

ASP.NET MVC 和实体框架 Code First 提供的验证支持是有效的操作原理示例。 您可以以声明方式在模型类)  (中指定验证规则，并在应用程序中的任何位置强制执行规则。

让我们看看如何在电影应用程序中利用此验证支持。

## <a name="adding-validation-rules-to-the-movie-model"></a>向影片模型添加验证规则

首先向类添加一些验证逻辑 `Movie` 。

打开 Movie.cs 文件**。 请注意， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 命名空间不包含 `System.Web` 。 DataAnnotations 提供了一组内置验证特性，可通过声明方式应用于任何类或属性。  (它还包含格式属性（如 [数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) ），这些属性可帮助进行格式设置，而不提供任何验证。 ) 

现在， `Movie` 请更新类以利用内置 [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 、 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)和 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 验证属性。 将 `Movie` 类替换为以下内容：

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

[`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)特性设置字符串的最大长度，并对数据库设置此限制，因此数据库架构将更改。 在**服务器资源管理器**中右键单击**电影**表，然后单击 "**打开表定义**"：

![](adding-validation/_static/image1.png)

在上面的图像中，可以看到所有字符串字段均设置为 [NVARCHAR (MAX) ](https://technet.microsoft.com/library/ms186939.aspx)。 我们将使用迁移来更新架构。 生成解决方案，然后打开 " **包管理器控制台** " 窗口并输入以下命令：

[!code-console[Main](adding-validation/samples/sample2.cmd)]

此命令完成后，Visual Studio 会打开类文件，该文件 `DbMigration` 用 () 指定的名称定义新的派生类 `DataAnnotations` ，在 `Up` 方法中，你可以看到更新架构约束的代码：

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

该 `Genre` 字段不再为 null (也就是说，你必须输入值) 。 此 `Rating` 字段的最大长度为5， `Title` 最大长度为60。 上的最小长度为 3 `Title` ，而上的范围 `Price` 未创建架构更改。

检查电影架构：

![](adding-validation/_static/image2.png)

字符串字段显示新的长度限制，并且不再被 `Genre` 视为可以为 null。

验证特性指定要对应用这些特性的模型属性强制执行的行为。 `Required` 和 `MinimumLength` 特性表示属性必须有值；但用户可输入空格来满足此验证。 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性用于限制可以输入的字符。 在上述代码中，`Genre` 和 `Rating` 仅可使用字母（禁用空格、数字和特殊字符）。 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)特性将值限制在指定的范围内。 `StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。 值类型 (如 `decimal, int, float, DateTime`) 本质上是必需的，不需要 `Required` 属性。

Code First 确保在应用程序将更改保存到数据库中之前，强制执行在模型类上指定的验证规则。 例如，当调用方法时，以下代码将引发 [DbEntityValidationException](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) 异常 `SaveChanges` ，因为缺少几个必需 `Movie` 的属性值：

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

上面的代码引发了以下异常：

*对一个或多个实体的验证失败。有关更多详细信息，请参阅 "EntityValidationErrors" 属性。*

验证规则由 .NET Framework 自动强制实施有助于提高应用程序的可靠性。 同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 中的验证错误 UI

运行应用程序并导航到 */Movies* URL。

单击 " **新建** " 链接以添加新电影。 使用无效值填写表单。 当 jQuery 客户端验证检测到错误时，会显示一条错误消息。

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> 若要支持使用逗号 ( "，" ) 对于小数点的非英语区域设置的 jQuery 验证，必须按本教程前面所述包含 NuGet 全球化。

请注意窗体自动使用红色边框颜色突出显示包含无效数据的文本框，并在每个文本框旁边发出适当的验证错误消息。 客户端（使用 JavaScript 和 jQuery）和服务器端（若用户禁用 JavaScript）都必定会遇到这些错误。

一个真正的好处是，您无需更改 `MoviesController` 类或 *创建的 cshtml* 视图中的单个代码行即可启用此验证 UI。 在本教程前面创建的控制器和视图会自动选取验证规则，这些规则是通过在 `Movie` 模型类的属性上使用验证特性所指定的。 使用 `Edit` 操作方法测试验证后，即已应用相同的验证。

存在客户端验证错误时，不会将表单数据发送到服务器。 可以通过使用 [fiddler 工具](http://fiddler2.com/fiddler2/)或 IE [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)，在 HTTP Post 方法中放置一个断点来验证这一点。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在 "创建视图" 和 "创建操作" 方法中进行验证

你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。 下一列表显示了 `Create` 类中的方法的 `MovieController` 外观。 在本教程的前面部分中创建它们的方式没有改变。

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

第一个 (HTTP GET) `Create` 操作方法显示初始的“创建”表单。 第二个 (`[HttpPost]`) 版本处理表单发布。 第二 `Create` 种方法 (`HttpPost` 版本) 检查 `ModelState.IsValid` 以查看电影是否有任何验证错误。 获取此属性将计算已应用于对象的任何验证特性。 如果对象具有验证错误，则方法将重新出现 `Create` 窗体。 如果没有错误，此方法则将新电影保存在数据库中。 在我们的电影示例中， **当在客户端检测到验证错误时，不会将窗体发布到服务器; 第二**种 `Create` **方法永远不会被调用**。 如果在浏览器中禁用 JavaScript，则会禁用客户端验证，并且 HTTP POST `Create` 方法将获取 `ModelState.IsValid` 以检查电影是否有任何验证错误。

可以在 `HttpPost Create` 方法中设置断点，并验证方法从未被调用，客户端验证在检测到存在验证错误时不会提交表单数据。 如果在浏览器中禁用 JavaScript，然后提交错误的表单，将触发断点。 在没有 JavaScript 的情况下仍然可以进行完整的验证。 下图显示了如何在 Internet Explorer 中禁用 JavaScript。

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

以下图片显示如何在 FireFox 浏览器中禁用 JavaScript。

![](adding-validation/_static/image7.png)

以下图片显示如何在 Chrome 浏览器中禁用 JavaScript。

![](adding-validation/_static/image8.png)

下面是在本教程的前面部分中基架的 *Create.* view 模板。 以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

请注意，代码如何使用 `Html.EditorFor` helper 来输出 `<input>` 每个属性的元素 `Movie` 。 此帮助器旁边的调用 `Html.ValidationMessageFor` 帮助程序方法。 这两个帮助器方法使用由控制器传递到视图的模型对象 (在这种情况下，) 的 `Movie` 对象。 它们会自动查找在模型上指定的验证属性，并根据需要显示错误消息。

此方法真正好的一点是：无论是控制器还是 `Create` 视图模板都不知道强制实施的实际验证规则或显示的特定错误消息。 仅可在 `Movie` 类中指定验证规则和错误字符串。 这些相同的验证规则自动应用于 `Edit` 视图和可能创建用于编辑模型的任何其他视图模板。

如果要在以后更改验证逻辑，可以通过向模型添加验证特性来在一个位置执行此操作， (在此示例中， `movie` 类) 。 无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。 这使代码非常简洁，并且更易于维护和改进。 这意味着你将完全遵守 *晾干* 原则。

## <a name="using-datatype-attributes"></a>使用 DataType 特性

打开 Movie.cs 文件并检查 `Movie` 类。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间除了提供内置的验证特性集外，还提供格式特性。 我们已将 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 枚举值应用于发布日期和价格字段。 下面的代码演示 `ReleaseDate` `Price` 具有相应特性的和属性 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 。

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性只为视图引擎提供提示，以便为数据 (设置格式，并为 `<a>` URL 和电子邮件提供之类的属性 `<a href="mailto:EmailAddress.com">` 。 您可以使用 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 属性来验证数据的格式。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性用于指定比数据库内部类型更具体的数据类型，它们***不***是验证特性。 在此示例中，我们只想跟踪日期，而不是日期和时间。 [DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供多种数据类型，例如*日期、时间、PhoneNumber、货币、EmailAddress*等。 应用程序还可通过 `DataType` 特性自动提供类型特定的功能。 例如， `mailto:` 可以为[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)创建链接，并且可以在支持[HTML5](http://html5.org/)的浏览器中为[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供日期选择器。 数据 [类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 属性发出 html 5 [数据](http://ejohn.org/blog/html-5-data-attributes/) * (发音* 为 html 5 浏览器可以理解的) 属性。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性不提供任何验证。

`DataType.Date` 不指定显示日期的格式。 默认情况下，数据字段根据服务器的 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)按默认格式显示。

`DisplayFormat` 特性用于显式指定日期格式：

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

此 `ApplyFormatInEditMode` 设置指定当在文本框中显示值进行编辑时，还应应用指定的格式设置。  (您可能不希望为某些字段（例如，对于货币值），您可能不希望文本框中的货币符号用于编辑。 ) 

您可以单独使用 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 属性，但通常最好使用 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 属性。 `DataType`属性传达数据的*语义*，而不是在屏幕上呈现数据的语义，并提供以下不需要的优点 `DisplayFormat` ：

- 浏览器可以启用 HTML5 功能 (例如，显示日历控件、区域设置相应的货币符号、电子邮件链接等 ) 。
- 默认情况下，浏览器将根据 [区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)使用正确的格式呈现数据。
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性可以使 MVC 选择正确的字段模板来呈现数据 (如果[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)使用字符串模板) 。 有关详细信息，请参阅 Brad Wilson 的 [ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。 尽管 (是为 MVC 2 编写的，但本文仍适用于当前版本的 ASP.NET MVC。 ) 

如果将 `DataType` 属性与日期字段一起使用，则还必须指定属性，以 `DisplayFormat` 确保字段在 Chrome 浏览器中正确呈现。 有关详细信息，请参阅 [此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。

> [!NOTE]
> jQuery 验证不能使用 [范围](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 属性和 [日期时间](https://msdn.microsoft.com/library/system.datetime.aspx)。 例如，以下代码将始终显示客户端验证错误，即便日期在指定的范围内：
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> 你将需要禁用 jQuery 日期验证，以将 [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 属性与 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)一起使用。 通常不是在模型中编译硬日期的最佳做法，因此不建议使用 [范围](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 属性和 [日期时间](https://msdn.microsoft.com/library/system.datetime.aspx) 。

以下代码显示组合在一行上的特性：

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。

> [!div class="step-by-step"]
> [上一页](adding-a-new-field.md)
> [下一页](examining-the-details-and-delete-methods.md)

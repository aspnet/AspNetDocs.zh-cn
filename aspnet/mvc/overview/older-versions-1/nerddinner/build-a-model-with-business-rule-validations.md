---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证构建模型 |微软文档
author: rick-anderson
description: 步骤 3 演示如何创建模型，可用于查询和更新 NerdDinner 应用程序的数据库。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541632"
---
# <a name="build-a-model-with-business-rule-validations"></a>生成具有业务规则验证功能的模型

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第3步，该教程演示如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。
> 
> 步骤 3 演示如何创建模型，可用于查询和更新 NerdDinner 应用程序的数据库。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-3-building-the-model"></a>神经晚餐步骤 3： 构建模型

在模型视图控制器框架中，术语"模型"是指表示应用程序数据的对象，以及与其集成验证和业务规则的相应域逻辑。 该模型在许多方面是基于 MVC 的应用程序的"心脏"，稍后我们将看到从根本上推动它的行为。

ASP.NET MVC 框架支持使用任何数据访问技术，开发人员可以从各种丰富的 .NET 数据选项中进行选择以实施其模型，包括：LINQ 到实体、LINQ 到 SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM，或者只是原始ADO.NET数据阅读器或数据集集。

对于我们的NerdDinner应用程序，我们将使用LINQ到SQL来创建一个与数据库设计相当一致的简单模型，并添加一些自定义验证逻辑和业务规则。 然后，我们将实现一个存储库类，该类可帮助从应用程序的其余部分提取数据持久性实现，并使我们能够轻松地对其进行单元测试。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ 到 SQL 是作为 .NET 3.5 的一部分而附带的 ORM（对象关系映射器）。

LINQ 到 SQL 提供了一种将数据库表映射到 .NET 类的简单方法，我们可以针对它编写代码。 对于我们的NerdDinner应用程序，我们将用它来将数据库中的晚餐和RSVP表映射到晚餐和RSVP类。 晚餐和 RSVP 表的列将对应于"晚餐"和"RSVP"类的属性。 每个 Dinner 和 RSVP 对象将表示数据库中的 Dinner 或 RSVP 表中的单独行。

LINQ 到 SQL 允许我们避免手动构造 SQL 语句来检索和更新具有数据库数据的 Dinner 和 RSVP 对象。 相反，我们将定义 Dinner 和 RSVP 类、它们如何映射到/从数据库映射以及它们之间的关系。 然后，LINQ 到 SQL 将负责生成适当的 SQL 执行逻辑，以便在运行时交互使用它们时使用。

我们可以在 VB 和 C# 中使用 LINQ 语言支持来编写表达性查询，从数据库中检索 Dinner 和 RSVP 对象。 这最大限度地减少了我们需要编写的数据代码量，并允许我们构建真正干净的应用程序。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>将 LINQ 添加到 SQL 类到我们的项目

我们将从右键单击项目中的"模型"文件夹开始，然后选择 **"添加新&gt;项目**"菜单命令：

![](build-a-model-with-business-rule-validations/_static/image1.png)

这将弹出"添加新项目"对话框。 我们将按"数据"类别进行筛选，并在其中选择"LINQ 到 SQL 类"模板：

![](build-a-model-with-business-rule-validations/_static/image2.png)

我们将为项目命名为"NerdDinner"，然后单击"添加"按钮。 Visual Studio 将在我们的 #Model 目录下添加 NerdDinner.dbml 文件，然后打开 LINQ 到 SQL 对象关系设计器：

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>使用 LINQ 创建到 SQL 的数据模型类

LINQ 到 SQL 使我们能够从现有数据库架构快速创建数据模型类。 为此，我们将在服务器资源管理器中打开 NerdDinner 数据库，并选择要在其中建模的表：

![](build-a-model-with-business-rule-validations/_static/image4.png)

然后，我们可以将表拖到 LINQ 到 SQL 设计器表面。 当我们执行此操作 LINQ 到 SQL 时，将使用表的架构（具有映射到数据库表列的类属性）自动创建 Dinner 和 RSVP 类：

![](build-a-model-with-business-rule-validations/_static/image5.png)

默认情况下，LINQ 到 SQL 设计器在基于数据库架构创建类时自动"复数"表和列名称。 例如：我们上面示例中的"Dinners"表产生了一个"Dinner"类。 此类命名有助于使我们的模型与 .NET 命名约定保持一致，我通常发现让设计器修复这一点很方便（尤其是在添加大量表时）。 但是，如果您不喜欢设计器生成的类或属性的名称，则始终可以重写它并将其更改为所需的任何名称。 可以通过在设计器内编辑实体/属性名称，或通过属性网格对其进行修改来执行此操作。

默认情况下，LINQ 到 SQL 设计器还会检查表的主键/外键关系，并基于这些关系自动在它创建的不同模型类之间创建默认的"关系关联"。 例如，当我们将 Dinner 和 RSVP 表拖到 LINQ 到 SQL 设计器时，根据 RSVP 表对 Dinners 表具有外键（由设计器中的箭头指示）推断两者之间存在一对多关系关联：

![](build-a-model-with-business-rule-validations/_static/image6.png)

上述关联将导致 LINQ 到 SQL 向 RSVP 类添加强类型"Dinner"属性，开发人员可以使用该属性访问与给定 RSVP 关联的 Dinner。 它还会导致 Dinner 类具有"RSVP"集合属性，使开发人员能够检索和更新与特定 Dinner 关联的 RSVP 对象。

下面您可以看到 Visual Studio 中一个智能感知示例，当我们创建新的 RSVP 对象并将其添加到 Dinner 的 RSVP 集合中时。 请注意 LINQ 到 SQL 如何在 Dinner 对象上自动添加"RSV"集合：

![](build-a-model-with-business-rule-validations/_static/image7.png)

通过将 RSVP 对象添加到 Dinner 的 RSVP 集合中，我们告诉 LINQ 到 SQL 来关联数据库中的 Dinner 和 RSVP 行之间的外键关系：

![](build-a-model-with-business-rule-validations/_static/image8.png)

如果您不喜欢设计器建模或命名表关联的方式，则可以重写它。 只需单击设计器中的关联箭头，并通过属性网格访问其属性以重命名、删除或修改它。 但是，对于我们的 NerdDinner 应用程序，默认关联规则非常适合我们构建的数据模型类，我们可以只使用默认行为。

### <a name="nerddinnerdatacontext-class"></a>内德晚餐数据上下文类

Visual Studio 将自动创建 .NET 类，这些类表示使用 LINQ 到 SQL 设计器定义的模型和数据库关系。 还将为添加到解决方案的每个 LINQ 到 SQL 设计器文件生成 LINQ 到 SQL DataContext 类。 由于我们将 LINQ 命名为 SQL 类项"NerdDinner"，因此创建的数据上下文类将称为"NerdDinnerDataContext"。 此 NerdDinnerDataContext 类是我们与数据库交互的主要方式。

我们的 NerdDinnerDataContext 类公开了两个属性 - "Dinners" 和"RSVPs" - 它们表示我们在数据库中建模的两个表。 我们可以使用 C# 针对这些属性编写 LINQ 查询，以便从数据库中查询和检索 Dinner 和 RSVP 对象。

以下代码演示如何实例化 NerdDinnerDataContext 对象，并针对该对象执行 LINQ 查询，以获取将来发生的一系列 Dinner。 Visual Studio 在编写 LINQ 查询时提供完整的无意义，从它返回的对象是强类型，并且还支持智能感知：

![](build-a-model-with-business-rule-validations/_static/image9.png)

除了允许我们查询晚餐和RSVP对象外，NerdDinnerDataContext 还会自动跟踪我们随后对我们通过它检索的晚餐和 RSVP 对象所做的任何更改。 我们可以使用此功能轻松地将更改保存回数据库 - 而无需编写任何显式 SQL 更新代码。

例如，下面的代码演示如何使用 LINQ 查询从数据库中检索单个 Dinner 对象，更新两个 Dinner 属性，然后将更改保存回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上面代码中的 NerdDinnerDataContext 对象自动跟踪我们对从该对象检索到的 Dinner 对象所做的属性更改。 当我们调用"提交更改（）"方法时，它将对数据库执行适当的 SQL"UPDATE"语句，以保留更新的值。

### <a name="creating-a-dinnerrepository-class"></a>创建晚餐存储库类

对于小型应用程序，有时让控制器直接针对 LINQ 到 SQL DataContext 类工作，并将 LINQ 查询嵌入到控制器中，这有时很好。 但是，随着应用程序变得越来越大，此方法在维护和测试方面变得繁琐起来。 它还可能导致我们在多个位置复制相同的 LINQ 查询。

使应用程序更易于维护和测试的一种方法是使用"存储库"模式。 存储库类有助于封装数据查询和持久性逻辑，并从应用程序抽象数据持久性的实现详细信息。 除了使应用程序代码更简洁之外，使用存储库模式还可以使将来更轻松地更改数据存储实现，并且它可以帮助简化应用程序单元测试，而无需真正的数据库。

对于我们的NerdDinner应用程序，我们将定义一个带有以下签名的 DinnerRepository 类：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注意：在本章的后面部分，我们将从此类中提取 IDinnerRepository 接口，并在我们的控制器上启用依赖项注入。不过，首先，我们将开始简单，只是直接与 DinnerRepository 类一起工作。*

要实现此类，我们将右键单击我们的"模型"文件夹，然后选择 **"添加新&gt;项目**"菜单命令。 在"添加新项目"对话框中，我们将选择"类"模板并将文件命名为"DinnerRepository.cs"：

![](build-a-model-with-business-rule-validations/_static/image10.png)

然后，我们可以使用以下代码实现我们的 DinnerRepository 类：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>使用 DinnerRepository 类检索、更新、插入和删除

现在，我们已经创建了 DinnerRepository 类，让我们看一些代码示例，这些示例演示了我们可以执行的常见任务：

#### <a name="querying-examples"></a>查询示例

以下代码使用 DinnerID 值检索单个晚餐：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

下面的代码检索所有即将举办的晚餐，并在它们上循环：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>插入和更新示例

下面的代码演示了添加两个新晚餐。 在调用"Save（）"方法之前，不会将存储库的添加/修改提交到数据库。 LINQ 到 SQL 会自动包装数据库事务中的所有更改 ， 因此，当我们的存储库保存时，要么发生所有更改，要么这些更改都不会发生：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

下面的代码检索现有的 Dinner 对象，并修改其上的两个属性。 当我们的存储库上调用"Save（））"方法时，更改将提交回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

下面的代码检索晚餐，然后向其中添加 RSVP。 它使用 LINQ 到 SQL 为我们创建的 Dinner 对象上的 RSVP 集合来这样做（因为数据库中两者之间存在主键/外键关系）。 当在存储库上调用"Save（））"方法时，此更改将作为新的 RSVP 表行保留回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>删除示例

下面的代码检索现有的 Dinner 对象，然后将其标记为要删除。 在存储库上调用"Save（））"方法时，它将将删除提交回数据库：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>将验证和业务规则逻辑与模型类集成

集成验证和业务规则逻辑是任何处理数据的应用程序的关键部分。

#### <a name="schema-validation"></a>架构验证

使用 LINQ 到 SQL 设计器定义模型类时，数据模型类中属性的数据类型对应于数据库表的数据类型。 例如：如果 Dinners 表中的"EventDate"列是"日期时间"，则 LINQ 创建的 SQL 数据模型类的类型为"DateTime"（这是内置的 .NET 数据类型）。 这意味着，如果您尝试从代码为其分配整数或布尔，则收到编译错误，如果尝试在运行时隐式将无效字符串类型转换为该字符串类型，则会自动引发错误。

LINQ 到 SQL 还会在使用字符串时自动处理转义 SQL 值，这有助于在使用字符串时防止 SQL 注入攻击。

#### <a name="validation-and-business-rule-logic"></a>验证和业务规则逻辑

架构验证作为第一步非常有用，但很少足够。 大多数实际方案都需要能够指定更丰富的验证逻辑，该验证逻辑可以跨越多个属性，执行代码，并且通常了解模型的状态（例如：它是在创建/更新/删除，还是处于特定于域的状态（如"存档"）。 有多种不同的模式和框架可用于定义验证规则并将其应用于模型类，并且有几个基于 .NET 的框架可用于帮助实现此。 您可以在mVC应用程序中使用几乎任何ASP.NET。

为了我们的 NerdDinner 应用程序，我们将使用相对简单和直接的模式，在其中我们公开 IsValid 属性和 GetRule侵犯（） 方法在我们的 Dinner 模型对象上。 IsValid 属性将返回真或假，具体取决于验证和业务规则是否都有效。 GetRule违反（） 方法将返回任何规则错误的列表。

我们将通过在我们的项目中添加"部分类"来实现"有效"和 GetRule违反（）） 我们的晚餐模型。 部分类可用于向 VS 设计器维护的类（如 LINQ 生成的到 SQL 设计器生成的 Dinner 类）添加方法/属性/事件，并帮助避免工具混乱我们的代码。 我们可以通过右键单击 #Model 文件夹，将新的部分类添加到项目中，然后选择"添加新项目"菜单命令。 然后，我们可以在"添加新项目"对话框中选择"类"模板，并将其命名为Dinner.cs。

![](build-a-model-with-business-rule-validations/_static/image11.png)

单击"添加"按钮会将Dinner.cs文件添加到我们的项目中，并在 IDE 中打开该文件。 然后，我们可以使用以下代码实现基本的规则/验证实施框架：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

有关上述代码的一些说明：

- Dinner 类以"部分"关键字为开头 - 这意味着其中包含的代码将与 LINQ 生成/维护的类组合到 SQL 设计器并编译为单个类。
- RuleRuleRule 类是一个帮助类，我们将添加到项目中，允许我们提供有关规则违反的更多详细信息。
- 晚餐.GetRule违反（）方法会导致评估我们的验证和业务规则（我们将很快实施它们）。 然后，它返回一系列规则冲突对象，这些对象提供有关任何规则错误的更多详细信息。
- Dinner.IsValid 属性提供了一个方便的帮助程序属性，用于指示 Dinner 对象是否具有任何活动的规则冲突。 开发人员可以随时使用 Dinner 对象主动检查它（并且不会引发异常）。
- Dinner.OnValidate（） 部分方法是 LINQ 到 SQL 提供的一个挂钩，它允许我们在即将在数据库中持久化 Dinner 对象的任何时间收到通知。 上述 OnValidate（） 实现可确保在保存之前没有规则违反规则。 如果处于无效状态，它将引发异常，这将导致 LINQ 到 SQL 中止事务。

此方法提供了一个简单的框架，我们可以将验证和业务规则集成到其中。 现在，让我们将以下规则添加到我们的 GetRule 违反（） 方法：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

我们使用 C# 的"收益回报"功能来返回任何规则违反规则的序列。 上面的前六个规则检查只是强制说，我们 Dinner 上的字符串属性不能为空或为空。 最后一条规则更有趣一点，并调用 PhoneValidator.IsValidNumber（） 帮助器方法，我们可以添加到我们的项目中，以验证 ContactPhone 号码格式是否与 Dinner 的国家/地区匹配。

我们可以使用 。NET 的正则表达式支持实现此电话验证支持。 下面是一个简单的电话验证器实现，我们可以添加到我们的项目，使我们能够添加特定于国家/地区的 Regex 模式检查：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>处理验证和业务逻辑冲突

现在，我们已经添加了上述验证和业务规则代码，每当我们尝试创建或更新 Dinner 时，都将评估和强制执行验证逻辑规则。

开发人员可以编写如下代码，以主动确定 Dinner 对象是否有效，并检索其中所有冲突的列表，而不会引发任何异常：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

如果我们尝试将 Dinner 保存为无效状态，则当我们在 Dinner 存储库上调用 Save（） 方法时，将引发异常。 这是因为 LINQ 到 SQL 在保存晚餐更改之前自动调用我们的 Dinner.OnValidate（） 部分方法，并且我们在晚餐中添加了代码。OnValidate（） 如果晚餐中存在任何违反规则的行为，则引发异常。 我们可以捕获此异常并被动检索要修复的违规列表：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

由于验证和业务规则在我们的模型层中实现，而不是 UI 层内，因此它们将在应用程序中的所有方案中应用和使用。 我们以后可以更改或添加业务规则，并让所有与我们的 Dinner 对象一起使用的代码都遵守它们。

在一个位置灵活地更改业务规则，而不使这些更改波及整个应用程序和 UI 逻辑，是编写良好的应用程序的标志，也是 MVC 框架有助于鼓励的好处。

### <a name="next-step"></a>下一步

现在，我们有一个模型，我们可以用于查询和更新我们的数据库。

现在，让我们向项目添加一些控制器和视图，可用于构建围绕它的 HTML UI 体验。

> [!div class="step-by-step"]
> [上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 迭代#4 = 使应用程序松散耦合 （C#） |微软文档
author: rick-anderson
description: 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 预测...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542360"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>迭代 4 – 使应用程序松散耦合 (C#)

由[微软](https://github.com/microsoft)

[下载代码](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 例如，我们重构应用程序以使用存储库模式和依赖项注入模式。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>构建联系人管理ASP.NET MVC 应用程序 （C#）

在本系列教程中，我们从头到尾构建整个联系人管理应用程序。 通过联系人管理器应用程序，您可以存储联系人信息 （姓名、电话号码和电子邮件地址） 人员列表。

我们通过多次迭代构建应用程序。 每次迭代时，我们都会逐步改进应用程序。 此多迭代方法的目标是使您能够了解每次更改的原因。

- 迭代#1 - 创建应用程序。 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。

- 迭代#2 - 使应用程序看起来不错。 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。

- 迭代#3 - 添加表单验证。 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证电子邮件地址和电话号码。

- 迭代#4 - 使应用程序松散耦合。 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 例如，我们重构应用程序以使用存储库模式和依赖项注入模式。

- 迭代#5 - 创建单元测试。 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。

- 迭代#6 - 使用测试驱动开发。 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代#7 - 添加Ajax功能。 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。

## <a name="this-iteration"></a>此迭代

在 Contact Manager 应用程序的第四个迭代中，我们重构应用程序以使应用程序更松散耦合。 当应用程序松散耦合时，可以在应用程序一个部分修改代码，而无需修改应用程序其他部分中的代码。 松散耦合的应用程序对更改更具弹性。

目前，Contact Manager 应用程序使用的所有数据访问和验证逻辑都包含在控制器类中。 这是个坏主意。 每当需要修改应用程序的一个部分时，您都有可能将 Bug 引入应用程序的另一部分。 例如，如果修改验证逻辑，则有在数据访问或控制器逻辑中引入新 Bug 的风险。

> [!NOTE] 
> 
> （SRP），类不应有超过一个更改的原因。 混合控制器、验证和数据库逻辑严重违反了单一责任原则。

可能需要修改应用程序的原因有多种。 您可能需要向应用程序添加新功能，可能需要修复应用程序中的 Bug，或者可能需要修改应用程序的实现方式。 应用程序很少是静态的。 它们往往随着时间的推移而生长和变异。

例如，假设您决定更改实现数据访问层的方式。 现在，联系人管理器应用程序使用 Microsoft 实体框架访问数据库。 但是，您可能决定迁移到新的或替代的数据访问技术，如ADO.NET数据服务或 NHibernate。 但是，由于数据访问代码不与验证和控制器代码隔离，因此如果不修改与数据访问没有直接关系的其他代码，就无法修改应用程序中的数据访问代码。

另一方面，当应用程序耦合松散时，您可以对应用程序的一个部分进行更改，而无需接触应用程序的其他部分。 例如，无需修改验证或控制器逻辑即可切换数据访问技术。

在此迭代中，我们利用了多种软件设计模式，使我们能够将我们的 Contact Manager 应用程序重构为更松散耦合的应用程序。 完成后，联系人管理器不会执行以前未执行的任何操作。 但是，我们将来能够更轻松地更改应用程序。

> [!NOTE] 
> 
> 重构是重写应用程序的过程，这样它不会丢失任何现有功能。

## <a name="using-the-repository-software-design-pattern"></a>使用存储库软件设计模式

我们的第一个变化是利用称为存储库模式的软件设计模式。 我们将使用存储库模式将数据访问代码与应用程序的其余部分隔离开来。

实现存储库模式需要我们完成以下两个步骤：

1. 创建接口
2. 创建实现接口的具体类

首先，我们需要创建一个接口来描述我们需要执行的所有数据访问方法。 IContactManager存储库接口包含在清单1中。 此界面描述了五种方法：创建联系人、删除联系人、编辑联系人、获取联系人和列表联系人（）。

**清单 1 - 型号\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

接下来，我们需要创建一个实现 IContactManagerRepository 接口的具体类。 由于我们使用 Microsoft 实体框架访问数据库，因此我们将创建一个名为实体联系人管理器存储库的新类。 此类包含在清单 2 中。

**清单2 - 模型_实体联系人管理器存储库.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

请注意，实体联系人管理器存储库类实现了 IContactManager 存储库接口。 类实现该接口描述的所有五种方法。

您可能想知道为什么我们需要处理一个接口。 为什么我们需要同时创建接口和实现它的类？

除了一个例外，我们应用程序的其余部分将与接口而不是具体类进行交互。 我们将调用 IContactManagerRepository 接口公开的方法，而不是调用实体ContactManagerRepository类公开的方法。

这样，我们可以使用新类实现接口，而无需修改应用程序的其余部分。 例如，在未来某个日期，我们可能想要实现实现 IContactManagerRepository 接口的数据服务联系人管理器存储库类。 DataServicesContactManagerManagerRepository 类可能使用ADO.NET数据服务来访问数据库而不是 Microsoft 实体框架。

如果我们的应用程序代码是根据 IContactManagerRepository 接口而不是具体的 EntityContactManagerManagerRepository 类编程的，那么我们可以切换具体类，而无需修改我们代码的任何其余部分。 例如，我们可以从实体联系人管理器存储库类切换到 DataServicesContactManagerManagerRepository 类，而无需修改我们的数据访问或验证逻辑。

针对接口（抽象）而不是具体类进行编程使我们的应用程序更具弹性，从而对更改进行编程。

> [!NOTE] 
> 
> 您可以通过选择菜单选项"重构"，提取界面，从 Visual Studio 中的特定类快速创建界面。 例如，您可以先创建实体联系人管理器存储库类，然后使用提取接口自动生成 IContactManagerRepository 接口。

## <a name="using-the-dependency-injection-software-design-pattern"></a>使用依赖项注入软件设计模式

现在，我们已经将数据访问代码迁移到单独的存储库类，我们需要修改我们的联系人控制器才能使用此类。 我们将利用称为依赖注入的软件设计模式，在我们的控制器中使用存储库类。

修改后的联系人控制器包含在清单 3 中。

**清单3 - 控制器\联系控制器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

请注意，清单 3 中的联系人控制器有两个构造函数。 第一个构造函数将 IContactManagerRepository 接口的具体实例传递给第二个构造函数。 联系人控制器类使用*构造函数依赖项注入*。

使用实体联系人管理器存储库类的唯一位置位于第一个构造函数中。 类的其余部分使用 IContactManagerRepository 接口，而不是具体的实体联系人管理器存储库类。

这样，将来可以轻松切换 IContactManagerRepository 类的实现。 如果要使用 DataServicesContact存储库类而不是实体联系人管理器存储库类，只需修改第一个构造函数。

构造函数依赖项注入也使联系人控制器类非常可测试。 在单元测试中，您可以通过通过 IContactManagerRepository 类的模拟实现来实例化联系人控制器。 在下一次迭代中，当我们为联系人管理器应用程序构建单元测试时，依赖项注入的此功能对我们非常重要。

> [!NOTE] 
> 
> 如果要将 Contact 控制器类与 IContactManagerRepository 接口的特定实现完全分离，则可以利用支持依赖项注入的框架，如结构映射或 Microsoft 实体框架 （MEF）。 通过利用依赖项注入框架，您无需在代码中引用具体类。

## <a name="creating-a-service-layer"></a>创建服务层

您可能已经注意到，我们的验证逻辑仍然与清单 3 中修改后的控制器类中的控制器逻辑混合在一起。 出于隔离数据访问逻辑的一个个好主意，最好隔离我们的验证逻辑。

为了解决此问题，我们可以创建一个单独的[*服务层*](http://martinfowler.com/eaaCatalog/serviceLayer.html)。 服务层是一个单独的层，我们可以插入控制器和存储库类之间。 服务层包含我们的业务逻辑，包括我们所有的验证逻辑。

联系人管理器服务包含在清单 4 中。 它包含来自联系人控制器类的验证逻辑。

**清单4 - 型号_联系管理器服务.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

请注意，联系人管理器服务的构造函数需要验证字典。 服务层通过此验证字典与控制器层通信。 在讨论修饰器模式时，我们将在下一节中详细讨论验证词典。

此外，请注意，联系人管理器服务实现了 IContactManager 服务接口。 您应该始终努力针对接口而不是具体类进行编程。 联系人管理器应用程序中的其他类不直接与联系人管理器服务类交互。 相反，除了一个例外，联系人管理器应用程序的其余部分根据 IContactManager 服务接口进行编程。

IContactManager 服务接口包含在清单 5 中。

**清单5 - 型号_IContactManager服务.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

修改后的联系人控制器类包含在清单 6 中。 请注意，联系人控制器不再与联系人管理器存储库进行交互。 相反，联系人控制器与联系人管理器服务进行交互。 每个图层都尽可能与其他图层隔离。

**清单 6 - 控制器\联系控制器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

我们的应用程序不再违反单一责任原则 （SRP）。 清单6中的联系人控制器除控制应用程序执行流外，已被剥夺了所有责任。 所有验证逻辑都已从"联系人"控制器中删除，并推送到服务层。 所有数据库逻辑都已推送到存储库层。

## <a name="using-the-decorator-pattern"></a>使用修饰器模式

我们希望能够将服务层与控制器层完全分离。 原则上，我们应该能够在与控制器层分开的程序集中编译我们的服务层，而无需添加对 MVC 应用程序的引用。

但是，我们的服务层需要能够将验证错误消息传递回控制器层。 我们如何使服务层在不耦合控制器和服务层的情况下通信验证错误消息？ 我们可以利用一个软件设计模式，称为[装饰模式](http://en.wikipedia.org/wiki/Decorator_pattern)。

控制器使用名为 ModelState 的 ModelState 字典来表示验证错误。 因此，您可能受诱惑将 ModelState 从控制器层传递到服务层。 但是，在服务层中使用 ModelState 将使服务层依赖于ASP.NET MVC 框架的功能。 这将很糟糕，因为有一天，您可能希望将服务层与 WPF 应用程序一起使用，而不是使用ASP.NET MVC 应用程序。 在这种情况下，您不希望引用ASP.NET MVC 框架来使用 ModelState字典类。

修饰器模式使您能够在新类中包装现有类，以实现接口。 我们的联系人管理器项目包括清单 7 中包含的 ModelStateWrapper 类。 ModelStateWrapper 类实现清单 8 中的接口。

**清单7 - 模型_验证_模型状态包装器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**清单8 - 模型_验证_验证字典.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

如果您仔细查看清单 5，您将看到 ContactManager 服务层专用 IValidationa 字典界面。 联系人管理器服务不依赖于 ModelState 字典类。 当联系人控制器创建 ContactManager 服务时，控制器将像这样包装其 ModelState：

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>总结

在此迭代中，我们没有向联系人管理器应用程序添加任何新功能。 此迭代的目标是重构联系人管理器应用程序，以便更易于维护和修改。

首先，我们实现了存储库软件设计模式。 我们将所有数据访问代码迁移到单独的 ContactManager 存储库类。

我们还将验证逻辑与控制器逻辑隔离开来。 我们创建了一个单独的服务层，其中包含我们所有的验证代码。 控制器层与服务层交互，服务层与存储库层交互。

创建服务层时，我们利用修饰器模式将 ModelState 与服务层隔离开来。 在我们的服务层中，我们根据 I验证词典接口而不是 ModelState 进行了编程。

最后，我们利用了名为依赖项注入模式的软件设计模式。 此模式使我们能够针对接口（抽象）而不是具体类进行编程。 实现依赖项注入设计模式也使我们的代码更具可测试性。 在下一个迭代中，我们将单元测试添加到项目中。

> [!div class="step-by-step"]
> [上一页](iteration-3-add-form-validation-cs.md)
> [下一页](iteration-5-create-unit-tests-cs.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 迭代#5 = 创建单元测试 （VB） |微软文档
author: rick-anderson
description: 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟我们的数据模型类，并为 o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: cc5425de86e7481894fbea242fa555b5598167f6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542334"
---
# <a name="iteration-5--create-unit-tests-vb"></a>迭代 5 — 创建单元测试 (VB)

由[微软](https://github.com/microsoft)

[下载代码](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建 MVC 应用程序 （VB） ASP.NET联系人管理

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

在 Contact Manager 应用程序的上一次迭代中，我们将应用程序重构为更松散耦合。 我们将应用程序划分为不同的控制器、服务和存储库层。 每个层通过接口与层交互。

我们重构了应用程序，使应用程序更易于维护和修改。 例如，如果需要使用新的数据访问技术，我们可以简单地更改存储库层而不接触控制器或服务层。 通过使联系人管理器松散耦合，我们使应用程序对更改更具弹性。

但是，当我们需要向联系人管理器应用程序添加新功能时，会发生什么情况？ 或者，当我们修复 Bug 时会发生什么情况？ 编写代码的可悲但经过充分验证的事实是，每当您触摸代码时，都会产生引入新 Bug 的风险。

例如，一天好，您的经理可能会要求您向联系人管理器添加新功能。 她希望您添加对联系人组的支持。 她希望您允许用户将联系人组织成"朋友"、"业务"等组。

为了实现此新功能，您需要修改联系人管理器应用程序的所有三个层。 您需要向控制器、服务层和存储库添加新功能。 一旦开始修改代码，您就可能会破坏以前起作用的功能。

像上次迭代中所做的那样，将应用程序重构为单独的层是一件好事。 这是一件好事，因为它使我们能够对整个层进行更改，而无需接触应用程序的其余部分。 但是，如果要使层中的代码更易于维护和修改，则需要为代码创建单元测试。

使用单元测试来测试单个代码单元。 这些代码单位小于整个应用程序层。 通常，使用单元测试来验证代码中的特定方法的行为方式是否达到预期。 例如，您将为 ContactManager 服务类公开的 CreateContact（） 方法创建单元测试。

应用程序单元测试工作就像安全网一样。 每当修改应用程序中的代码时，都可以运行一组单元测试，以检查修改是否破坏了现有功能。 单元测试使代码可以安全地修改。 单元测试使应用程序中的所有代码都更具更改的弹性。

在此迭代中，我们将单元测试添加到我们的联系人管理器应用程序中。 这样，在下一次迭代中，我们可以将联系人组添加到我们的应用程序中，而不必担心破坏现有功能。

> [!NOTE] 
> 
> 有多种单元测试框架，包括 NUnit、xUnit.net 和 MbUnit。 在本教程中，我们使用 Visual Studio 附带的单位测试框架。 但是，您可以同样轻松地使用这些替代框架之一。

## <a name="what-gets-tested"></a>测试内容

在理想情况下，所有代码都将由单元测试覆盖。 在完美的世界，你会有完美的安全网。 您将能够修改应用程序中的任何代码行，并通过执行单元测试立即知道更改是否中断了现有功能。

然而，我们并不生活在一个完美的世界。 实际上，在编写单元测试时，您专注于为业务逻辑编写测试（例如，验证逻辑）。 特别是，您*不会*为数据访问逻辑或视图逻辑编写单元测试。

为了有用，单元测试必须非常快速地执行。 您可以轻松地为应用程序累积数百（甚至数千个）单元测试。 如果单元测试需要很长时间才能运行，则可以避免执行它们。 换句话说，对于日常编码目的，长时间运行单元测试是无用的。

因此，您通常不会为与数据库交互的代码编写单元测试。 对实时数据库运行数百个单元测试将太慢。 相反，您模拟数据库并编写与模拟数据库交互的代码（我们讨论下面嘲笑数据库）。

出于类似的原因，您通常不会为视图编写单元测试。 为了测试视图，必须启动 Web 服务器。 由于旋转 Web 服务器是一个相对缓慢的过程，因此不建议为视图创建单元测试。

如果视图包含复杂的逻辑，则应考虑将逻辑移动到帮助程序方法中。 您可以为在不旋转 Web 服务器的情况下执行的 Helper 方法编写单元测试。

> [!NOTE] 
> 
> 虽然编写数据访问逻辑或视图逻辑的测试在编写单元测试时不是个好主意，但这些测试在构建功能或集成测试时可能非常有价值。

> [!NOTE] 
> 
> ASP.NET MVC 是 Web 窗体视图引擎。 虽然 Web 窗体视图引擎依赖于 Web 服务器，但其他视图引擎可能不是。

## <a name="using-a-mock-object-framework"></a>使用模拟对象框架

构建单元测试时，您几乎总是需要利用模拟对象框架。 模拟对象框架使您能够为应用程序中的类创建模拟和存根。

例如，可以使用 Mock Object 框架生成存储库类的模拟版本。 这样，您可以在单元测试中使用模拟存储库类而不是真正的存储库类。 使用模拟存储库使您能够在执行单元测试时避免执行数据库代码。

可视化工作室不包括模拟对象框架。 但是，有几种商业和开源模拟对象框架可用于 .NET 框架：

1. Moq - 此框架在开源 BSD 许可证下可用。 你可以从[https://code.google.com/p/moq/](https://code.google.com/p/moq/)下载莫克。
2. 犀牛模拟 - 此框架可在开源 BSD 许可证下提供。 你可以从[http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)下载犀牛模拟。
3. 类型隔离器 - 这是一个商业框架。 可以从 下载试用版[http://www.typemock.com/](http://www.typemock.com/)。

在本教程中，我决定使用 Moq。 但是，您可以同样轻松地使用 Rhino Mocks 或 Typemock 隔离器为联系人管理器应用程序创建 Mock 对象。

在使用 Moq 之前，您需要完成以下步骤：

1. .
2. 在解压缩下载之前，请确保右键单击文件并单击标记为 **"取消阻止"** 的按钮（参见图 1）。
3. 解压缩下载。
4. 通过选择菜单选项 **"项目"，添加引用**以打开 **"添加参考"** 对话框，将对 Moq 程序集的引用添加到测试项目。 在"浏览"选项卡下，浏览到解压缩 Moq 的文件夹，然后选择 Moq.dll 程序集。 单击 **"确定"** 按钮（参见图 2）。

[![解除阻止莫克](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**图 01**： 取消阻止 Moq（[单击以查看全尺寸图像](iteration-5-create-unit-tests-vb/_static/image2.png)）

[![添加 Moq 后的引用](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**图 02**： 添加 Moq（[单击以查看全尺寸图像](iteration-5-create-unit-tests-vb/_static/image4.png)）后的参考

## <a name="creating-unit-tests-for-the-service-layer"></a>为服务层创建单元测试

让我们首先为联系人管理器应用程序的服务层创建一组单元测试。 我们将使用这些测试来验证我们的验证逻辑。

在 ContactManager.测试项目中创建名为"模型"的新文件夹。 接下来，右键单击"模型"文件夹并选择 **"添加、新建测试**"。 将显示图 3 所示**的"添加新测试**"对话框。 选择**单元测试**模板并命名新的测试联系人管理器服务测试.vb。 单击 **"确定"** 按钮将新测试添加到测试项目。

> [!NOTE] 
> 
> 通常，您希望测试项目的文件夹结构与 ASP.NET MVC 项目的文件夹结构匹配。 例如，将控制器测试放在控制器文件夹中，在模型文件夹中放置模型测试，等等。

[![型号_联系管理器服务测试.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**图 03**：型号_ContactManagerServiceTest.cs（[单击以查看全尺寸图像](iteration-5-create-unit-tests-vb/_static/image6.png)）

最初，我们要测试 ContactManager 服务类公开的 CreateContact（） 方法。 我们将创建以下五个测试：

- 创建联系人（） - 当有效的联系人传递给方法时，创建联系人（） 的测试返回该值为 true。
- 创建联系人需要先名（） - 测试当缺少名字的联系人传递给 CreateContact（） 方法时，错误消息是否添加到模型状态。
- 创建联系人需要LastName（） - 测试当缺少姓氏的联系人传递给 CreateContact（） 方法时，将错误消息添加到模型状态。
- 创建联系人无效电话（） - 测试当电话号码无效的联系人传递给 CreateContact（） 方法时，错误消息是否添加到模型状态。
- 创建联系人无效电子邮件（） - 测试当具有无效电子邮件地址的联系人传递给 CreateContact（） 方法时，错误消息是否添加到模型状态。

第一个测试验证有效的联系人未生成验证错误。 其余的测试检查每个验证规则。

这些测试的代码包含在清单 1 中。

**清单 1 - 型号_联系管理器服务测试.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

由于我们使用清单 1 中的 Contact 类，因此我们需要将对 Microsoft 实体框架的引用添加到我们的测试项目中。 添加对系统.Data.实体程序集的引用。

清单1包含一个名为初始化（）的方法，该方法用 [测试初始化] 属性进行修饰。 在运行每个单元测试之前自动调用此方法（在每个单元测试之前调用此方法 5 次）。 初始化（）方法创建具有以下代码行的模拟存储库：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

此代码行使用 Moq 框架从 IContactManagerRepository 接口生成模拟存储库。 使用模拟存储库而不是实际的实体联系人管理器存储库，以避免在运行每个单元测试时访问数据库。 模拟存储库实现 IContactManagerRepository 接口的方法，但这些方法实际上不执行任何操作。

> [!NOTE] 
> 
> 使用 Moq 框架时，mockRepository 和\_\_mockRepository.Object 区别是有区别的。 前者是指 Mock（IContactManagerRepository）类，该类包含用于指定模拟存储库如何执行的方法。 后者是指实现 IContactManager存储库接口的实际模拟存储库。

创建 ContactManagerService 类的实例时，模拟存储库在初始化（） 方法中使用。 所有单独的单元测试都使用此联系人管理器服务类的此实例。

清单1包含与每个单元测试对应的五种方法。 这些方法中的每一个都用 [TestMethod] 属性进行修饰。 运行单元测试时，将调用具有此属性的任何方法。 换句话说，使用 [TestMethod] 属性修饰的任何方法都是单元测试。

第一个单元测试名为 CreateContact（），验证在将 Contact 类的有效实例传递给该方法时调用 CreateContact（） 返回该值为 true。 测试创建 Contact 类的实例，调用 CreateContact（） 方法，并验证 CreateContact（） 返回该值为 true。

其余测试验证当使用无效的 Contact 调用 CreateContact（） 方法时，该方法将返回 false，并且预期的验证错误消息将添加到模型状态。 例如，"创建联系人需求名称（）"测试将创建联系人类的实例，该类的 FirstName 属性具有空字符串。 接下来，使用无效的联系人调用 CreateContact（） 方法。 最后，测试验证 CreateContact（） 返回 false，并且模型状态包含预期的验证错误消息"需要名字"。

您可以通过选择菜单选项 **"测试"、"运行"、"解决方案中的所有测试"（CTRL+R、A）** 来在清单 1 中运行单元测试。 测试结果显示在"测试结果"窗口中（参见图 4）。

[![测试结果](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**图 04**： 测试结果 （[单击以查看全尺寸图像](iteration-5-create-unit-tests-vb/_static/image8.png)）

## <a name="creating-unit-tests-for-controllers"></a>为控制器创建单元测试

ASP.NET MVC 应用程序控制用户交互流。 测试控制器时，要测试控制器是否返回正确的操作结果并查看数据。 您可能还希望测试控制器是否与模型类以预期的方式交互。

例如，清单 2 包含联系人控制器 Create（） 方法的两个单元测试。 第一个单元测试验证当有效的联系人传递到 Create（） 方法时，Create（） 方法重定向到 Index 操作。 换句话说，当传递有效的联系人时，Create（） 方法应返回表示索引操作的重定向到RouteResult。

在测试控制器层时，我们不想测试 ContactManager 服务层。 因此，我们在初始化方法中使用以下代码模拟服务层：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

在 CreateValidContact（） 单元测试中，我们用以下代码行模拟调用服务层 CreateContact（） 方法的行为：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

此代码行在调用其 CreateContact（） 方法时，会导致模拟 ContactManager 服务返回该值 true。 通过模拟服务层，我们可以测试控制器的行为，而无需在服务层中执行任何代码。

第二个单元测试验证 Create（） 操作在将无效联系人传递给方法时是否返回"创建"视图。 我们使服务层 CreateContact（） 方法使用以下代码行返回错误值：

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

如果 Create（） 方法按预期方式进行，则当服务层返回值为 false 时，它应返回"创建"视图。 这样，控制器可以在"创建"视图中显示验证错误消息，并且用户有机会更正无效的"联系人"属性。

如果计划为控制器生成单元测试，则需要从控制器操作中返回显式视图名称。 例如，不要返回如下所示的视图：

返回视图（）

相反，返回视图如下所示：

返回视图（"创建"）

如果在返回视图时不是显式，则 ViewResult.ViewName 属性将返回一个空字符串。

**清单2 - 控制器_联系控制器测试.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>总结

在此迭代中，我们为联系人管理器应用程序创建了单元测试。 我们可以随时运行这些单元测试，以验证我们的应用程序是否仍按预期方式运行。 单元测试作为我们应用程序的安全网，使我们能够在未来安全地修改我们的应用程序。

我们创建了两组单元测试。 首先，我们通过为服务层创建单元测试来测试验证逻辑。 接下来，我们通过为控制器层创建单元测试来测试流量控制逻辑。 在测试服务层时，我们通过模拟存储库层将服务层的测试与存储库层隔离开来。 测试控制器层时，我们通过模拟服务层来隔离控制器层的测试。

在下一次迭代中，我们修改联系人管理器应用程序，以便它支持联系人组。 我们将使用称为测试驱动开发的软件设计过程将这项新功能添加到我们的应用程序中。

> [!div class="step-by-step"]
> [上一页](iteration-4-make-the-application-loosely-coupled-vb.md)
> [下一页](iteration-6-use-test-driven-development-vb.md)

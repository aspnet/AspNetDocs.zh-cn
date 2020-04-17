---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |微软文档
author: rick-anderson
description: 步骤 12 演示如何开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心进行更改...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541463"
---
# <a name="enable-automated-unit-testing"></a>启用自动单元测试

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第12步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。
> 
> 步骤 12 演示如何开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心在未来对应用程序进行更改和改进。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-12-unit-testing"></a>神经晚餐步骤 12：单元测试

让我们开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心在未来对应用程序进行更改和改进。

### <a name="why-unit-test"></a>为什么选择单元测试？

在一天早上上班时，你突然闪现出一些关于你正在处理的应用程序的灵感。 您意识到，您可以实现一个更改，这将使应用程序显著更好地。 它可能是清理代码、添加新功能或修复 Bug 的重构。

当你到达计算机时，您面临的问题是"进行这种改进有多安全？ 如果做出改变有副作用或破坏某些东西呢？ 更改可能很简单，只需几分钟即可实现，但如果手动测试所有应用程序方案需要数小时，该怎么办？ 如果您忘记覆盖场景，而损坏的应用程序投入生产，该怎么办？ 做出这种改进真的值得付出所有努力吗？

自动单元测试可以提供一个安全网，使您能够持续增强应用程序，并避免害怕您正在处理的代码。 通过自动测试来快速验证功能，使您能够自信地编写代码，并使您能够做出改进，否则您可能觉得这样做并不自在。 它们还有助于创建更可维护且使用寿命更长的解决方案，从而获得更高的投资回报。

ASP.NET MVC 框架使单元测试应用程序功能变得简单自然。 它还支持测试驱动开发 （TDD） 工作流，支持基于测试优先的开发。

### <a name="nerddinnertests-project"></a>内德晚餐.测试项目

当我们在本教程开始时创建 NerdDinner 应用程序时，系统会提示我们进行一个对话框，询问我们是否希望创建一个单元测试项目以配合应用程序项目：

![](enable-automated-unit-testing/_static/image1.png)

我们保留了"是，创建一个单元测试项目"单选按钮 -导致"NerdDinner.Test"项目被添加到我们的解决方案中：

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.测试项目引用 NerdDinner 应用程序项目程序集，并使我们能够轻松地向其添加自动测试，以验证应用程序功能。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>为我们的晚餐模型类创建单元测试

让我们向 NerdDinner.测试项目添加一些测试，以验证我们在构建模型层时创建的 Dinner 类。

我们将首先在我们的测试项目中创建一个名为"模型"的新文件夹，我们将在这里放置与模型相关的测试。 然后，我们将右键单击该文件夹并选择 **"添加-&gt;新测试"** 菜单命令。 这将弹出"添加新测试"对话框。

我们将选择创建"单元测试"并将其命名为"DinnerTest.cs"：

![](enable-automated-unit-testing/_static/image3.png)

当我们单击"ok"按钮 Visual Studio 会向项目添加（并打开）DinnerTest.cs文件时：

![](enable-automated-unit-testing/_static/image4.png)

默认的 Visual Studio 单元测试模板内有一堆样板代码，我觉得有点乱。 让我们清理它，以便只包含以下代码：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上面的 DinnerTest 类上的 [TestClass] 属性将其标识为包含测试的类以及可选的测试初始化和拆解代码。 我们可以通过在其中添加具有 [TestMethod] 属性的公共方法来定义其中的测试。

下面是我们将添加的两个测试中的第一个，即锻炼我们的晚餐课程。 第一个测试验证，如果新晚餐的创建没有正确设置所有属性，则我们的晚餐无效。 第二个测试验证我们的晚餐是否有效，当晚餐具有具有有效值的所有属性设置时：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

您在上面会注意到我们的测试名称非常明确（而且有些详细）。 我们这样做是因为我们可能最终创建数百或数千个小测试，我们希望能够轻松快速确定每个测试程序的意图和行为（尤其是在查看测试运行程序中的失败列表时）。 测试名称应以测试的功能命名。 上面我们使用的是"名词\_应该\_动词"命名模式。

我们使用"AAA"测试模式构建测试，该模式代表"安排、操作、断言"：

- 排列：设置正在测试的装置
- 操作：锻炼被测试的单位并捕获结果
- 断言：验证行为

当我们编写测试时，我们希望避免让单个测试执行太多操作。 相反，每个测试应只验证一个概念（这将使确定故障原因变得更加容易）。 一个好的准则是尝试每个测试只有一个断言语句。 如果在测试方法中有多个断言语句，请确保它们都用于测试同一概念。 如有疑问，再做一次测试。

### <a name="running-tests"></a>正在运行测试

Visual Studio 2008 专业版（和更高版本）包括一个内置测试运行程序，可用于在 IDE 中运行 Visual Studio 单元测试项目。 我们可以选择解决方案菜单**中的"&gt;测试-&gt;运行-所有测试**"命令（或键入 Ctrl R，A）来运行我们所有的单元测试。 或者，我们可以将光标定位到特定的测试类或测试方法中，并使用**当前上下文菜单中的&gt;测试运行&gt;测试**命令（或键入 Ctrl R、T）来运行单元测试的子集。

让我们将光标定位在 DinnerTest 类中，并键入"Ctrl R，T"以运行我们刚刚定义的两个测试。 当我们执行此操作时，Visual Studio 中将显示一个"测试结果"窗口，我们将看到其中列出的测试运行结果：

![](enable-automated-unit-testing/_static/image5.png)

*注意：默认情况下，VS 测试结果窗口不显示"类名称"列。您可以通过在"测试结果"窗口中右键单击并使用"添加/删除列"菜单命令来添加此内容。*

我们的两个测试只用了一小部分时间就可以运行了，正如您所看到的，它们都通过了。 现在，我们可以通过创建验证特定规则验证的其他测试来扩展它们，并涵盖我们添加到 Dinner 类的两种帮助方法 - IsUserHost（） 和 IsUser 注册（）。 为 Dinner 类提供所有这些测试将使将来向该课程添加新业务规则和验证变得更加简单和安全。 我们可以将新的规则逻辑添加到 Dinner，然后在几秒钟内验证它是否没有破坏我们以前的任何逻辑功能。

请注意，使用描述性测试名称如何便于快速了解每个测试正在验证的内容。 我建议使用 **"工具-&gt;选项"** 菜单命令，打开测试工具-&gt;测试执行配置屏幕，并选中"双击失败或不确定的单位测试结果显示测试中的失败点"复选框。 这将允许您双击测试结果窗口中的故障，并立即跳转到断言失败。

### <a name="creating-dinnerscontroller-unit-tests"></a>创建晚餐控制器单元测试

现在，让我们创建一些单元测试，以验证我们的 DinnersController 功能。 我们将从右键单击测试项目中的"控制器"文件夹开始，然后选择 **"&gt;新增测试"** 菜单命令。 我们将创建一个"单元测试"并将其命名为"DinnersControllerTest.cs"。

我们将创建两种测试方法，以验证 DinnersController 上的细节（） 操作方法。 第一个将验证在请求现有晚餐时是否返回了视图。 第二个将验证在请求不存在的晚餐时是否返回"未找到"视图：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上述代码编译干净。 但是，当我们运行测试时，它们都失败：

![](enable-automated-unit-testing/_static/image6.png)

如果我们查看错误消息，我们将看到测试失败的原因是因为我们的 DinnersRepository 类无法连接到数据库。 我们的 NerdDinner 应用程序使用连接字符串到本地 SQL Server Express 文件，该文件位于\_NerdDinner 应用程序项目的 #App 数据目录下。 由于我们的 NerdDinner.测试项目编译并运行在不同的目录中，然后以应用程序项目运行，因此连接字符串的相对路径位置不正确。

*我们可以*通过将 SQL Express 数据库文件复制到测试项目来解决此问题，然后在测试项目的 App.config 中向它添加适当的测试连接字符串。 这将使上述测试解除阻止并运行。

但是，使用真实数据库的单位测试代码带来了许多挑战。 具体来说：

- 它显著减慢了单元测试的执行时间。 运行测试所需的时间越长，执行测试的可能性就越小。 理想情况下，您希望单元测试能够在几秒钟内运行，并且让它像编译项目一样自然地完成。
- 它在测试中使设置和清理逻辑复杂化。 您希望每个单元测试都隔离并独立于其他测试（没有副作用或依赖项）。 在对真实数据库工作时，您必须注意状态并在测试之间重置它。

让我们来看看一种称为"依赖注入"的设计模式，它可以帮助我们解决这些问题，并避免使用真实数据库作为测试的需要。

### <a name="dependency-injection"></a>依赖关系注入

现在，晚餐控制器与晚餐存储库类紧密地"耦合"。 "耦合"是指类显式依赖于另一个类才能工作的情况：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

由于 DinnerRepository 类需要访问数据库，因此 DinnersController 类在 DinnerRepository 上的紧密耦合依赖关系最终要求我们有一个数据库才能测试 DinnersController 操作方法。

我们可以采用称为"依赖注入"的设计模式来克服这一问题，这种方法在使用依赖项（如提供数据访问的存储库类）中不再隐式创建。 相反，依赖项可以显式传递给使用构造函数参数使用它们的类。 如果使用接口定义依赖项，则我们可以灵活地通过单元测试方案的"假"依赖项实现。 这使我们能够创建实际上不需要访问数据库的特定于测试的依赖项实现。

为了看到此操作，让我们使用 DinnersController 实现依赖项注入。

#### <a name="extracting-an-idinnerrepository-interface"></a>提取 IDinner 存储库界面

我们的第一步是创建一个新的 IDinnerRepository 接口，该接口封装了控制器检索和更新 Dinner 所需的存储库合同。

我们可以手动定义此接口协定，通过右键单击 #Model 文件夹，然后选择 **"添加-&gt;新项目"** 菜单命令并创建名为 IDinnerRepository.cs的新接口。

或者，我们可以使用内置于 Visual Studio 专业版（和更高版本）的重构工具，从现有的 DinnerRepository 类中自动提取和创建我们的界面。 要使用 VS 提取此接口，只需将光标放在 DinnerRepository 类的文本编辑器中，然后右键单击并选择 **"重构-&gt;提取界面"** 菜单命令：

![](enable-automated-unit-testing/_static/image7.png)

这将启动"提取接口"对话框，并提示我们创建接口的名称。 它将默认为 IDinnerRepository，并自动选择现有 DinnerRepository 类上的所有公共方法以添加到接口：

![](enable-automated-unit-testing/_static/image8.png)

当我们单击"确定"按钮时，Visual Studio 将为我们的应用程序添加新的 IDinnerRepository 界面：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

我们现有的 DinnerRepository 类将被更新，以便实现接口：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>更新晚餐控制器以支持构造函数注入

现在，我们将更新 DinnersController 类以使用新接口。

目前，晚餐控制器是硬编码的，因此其"晚餐存储库"字段始终是一个晚餐存储库类：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

我们将更改它，以便"晚餐存储库"字段是 IDinner 存储库类型，而不是晚餐存储库。 然后，我们将添加两个公共 DinnersController 构造函数。 其中一个构造函数允许将 IDinnerRepository 作为参数传递。 另一个是使用我们现有的 DinnerRepository 实现的默认构造函数：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

由于默认情况下ASP.NET MVC 使用默认构造函数创建控制器类，因此运行时的 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。

但是，我们现在可以更新我们的单元测试，以便使用参数构造函数在"假"晚餐存储库实现中传递。 此"假"晚餐存储库不需要访问真实数据库，而是使用内存中的示例数据。

#### <a name="creating-the-fakedinnerrepository-class"></a>创建假晚餐存储库类

让我们创建一个假晚餐存储库类。

我们将首先在我们的NerdDinner.测试项目中创建一个"Fakes"目录，然后向它添加新的FakeDinnerRepository类（右键单击该文件夹并选择 **"添加-&gt;新类**"）：

![](enable-automated-unit-testing/_static/image9.png)

我们将更新代码，以便 FakeDinnerRepository 类实现 IDinnerRepository 接口。 然后，我们可以右键单击它并选择"实现接口 IDinnerRepository"上下文菜单命令：

![](enable-automated-unit-testing/_static/image10.png)

这将导致 Visual Studio 自动将所有 IDinnerRepository 接口成员添加到我们的 FakeDinnerRepository 类，并包含默认的"存分之外"实现：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

然后，我们可以更新 FakeDinnerRepository 实现，以处理作为构造函数参数传递给&lt;它的&gt;内存中列表晚餐集合：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

我们现在有一个假的 IDinnerRepository 实现，它不需要数据库，而是可以处理存储中晚餐对象列表。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>将假晚餐存储库与单元测试一起使用

让我们返回到由于数据库不可用而较早失败的 DinnersController 单元测试。 我们可以更新测试方法，使用以下代码将填充在内存中晚餐数据样本的假晚餐存储库更新给 DinnersController：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

现在，当我们运行这些测试时，它们都通过了：

![](enable-automated-unit-testing/_static/image11.png)

最重要的是，它们只需一小部分秒才能运行，并且不需要任何复杂的设置/清理逻辑。 我们现在可以单元测试所有我们的 DinnersController 操作方法代码（包括列表、分页、详细信息、创建、更新和删除），而无需连接到真正的数据库。

| **侧主题：依赖项注入框架** |
| --- |
| 执行手动依赖项注入（如上所示）工作正常，但随着应用程序中依赖项和组件数量的增加，维护起来确实变得更加困难。 .NET 存在多个依赖项注入框架，可帮助提供更多依赖项管理灵活性。 这些框架有时也称为"控制反转"（IoC） 容器，它们提供了机制，支持在运行时指定依赖项并将其传递给对象（通常使用构造函数注入）的额外配置支持级别。 .NET 中一些较流行的 OSS 依赖项注入 / IOC 框架包括：AutoFac、Ninject、Spring.NET、结构映射和温莎。 ASP.NET MVC 公开扩展 API，使开发人员能够参与控制器的解析和实例化，并使依赖项注入/IoC 框架能够安全地集成到此过程中。 使用 DI/IOC 框架还将使我们能够从 DinnersController 中删除默认构造函数 ， 这将完全消除它和 DinnerRepository 之间的耦合。 我们不会使用依赖注入/IOC框架与我们的NerdDinner应用程序。 但是，如果NerdDinner代码库和功能的增长，我们可以考虑未来的问题。 |

### <a name="creating-edit-action-unit-tests"></a>创建编辑操作单元测试

现在，让我们创建一些单元测试，以验证 DinnersController 的编辑功能。 我们将首先测试我们的编辑操作的 HTTP-GET 版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

我们将创建一个测试，以验证在请求有效晚餐时，由 DinnerFormViewModel 对象支持的视图是否呈现回：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

但是，当我们运行测试时，我们会发现它失败，因为当 Edit 方法访问User.Identity.Name属性以执行 Dinner.Is托管By（） 检查时，将引发一个空引用异常。

控制器基类上的 User 对象封装有关登录用户的详细信息，并在运行时创建控制器时由ASP.NET MVC 填充。 由于我们在 Web 服务器环境之外测试 DinnersController，所以未设置用户对象（因此为空引用异常）。

### <a name="mocking-the-useridentityname-property"></a>模拟User.Identity.Name属性

模拟框架使我们能够动态创建支持测试的从属对象的假版本，从而使测试更容易。 例如，我们可以在"编辑"操作测试中使用模拟框架动态创建一个用户对象，我们的 DinnersController 可用于查找模拟用户名。 这将避免在运行测试时引发空引用。

有许多 .NET 模拟框架可用于ASP.NET MVC（您可以在此处查看它们的列表： [http://www.mockframeworks.com/](http://www.mockframeworks.com/) 为了测试我们的NerdDinner应用程序，我们将使用一个开源模拟框架，称为"Moq"，可以从免费下载[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)。

下载后，我们将在 NerdDinner.测试项目中向 Moq.dll 程序集添加参考：

![](enable-automated-unit-testing/_static/image12.png)

然后，我们将向测试类添加"创建 DinnerSControllerA（用户名）"帮助器方法，该方法以用户名作为参数，然后"模拟"DinnersController 实例上的User.Identity.Name属性：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

上面，我们使用 Moq 创建一个模拟对象，该对象伪造了控制器上下文对象（ASP.NET MVC 传递给控制器类以公开运行时对象（如用户、请求、响应和会话）。 我们在 Mock 上调用"setupGet"方法，以指示 ControllerContext 上的HttpContext.User.Identity.Name属性应返回我们传递给帮助器方法的用户名字符串。

我们可以模拟任意数量的控制器上下文属性和方法。 为了说明这一点，我还为 Request.Is 验证属性添加了 SetupGet（） 调用（下面测试实际上不需要它，但这有助于说明如何模拟请求属性）。 完成后，我们将控制器上下文模拟的实例分配给 DinnersController，我们的帮助器方法返回。

现在，我们可以编写使用此帮助器方法测试涉及不同用户的编辑方案的单位测试：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

现在，当我们运行测试时，他们通过：

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>测试更新模型（）方案

我们创建了涵盖"编辑"操作的 HTTP-GET 版本的测试。 现在，让我们创建一些测试来验证编辑操作的 HTTP-POST 版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

我们支持此操作方法的有趣新测试方案是它在 Controller 基类上使用 UpdateModel（） 帮助器方法。 我们使用此帮助器方法将表单发布值绑定到我们的 Dinner 对象实例。

下面是两个测试，它们演示如何为 UpdateModel（） 帮助器方法提供表单发布值。 我们将通过创建和填充 FormCollection 对象来执行此操作，然后将其分配给控制器上的"ValueProvider"属性。

第一个测试验证在成功保存浏览器时是否重定向到详细信息操作。 第二个测试验证，当发布无效输入时，操作会再次用错误消息重新显示编辑视图。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>测试总结

我们介绍了单元测试控制器类中涉及的核心概念。 我们可以使用这些技术轻松创建数百个简单的测试，以验证我们应用程序的行为。

由于我们的控制器和模型测试不需要真正的数据库，因此它们非常快速且易于运行。 我们将能够在数秒内执行数百个自动测试，并立即获得反馈，了解我们所做的更改是否违反了某些内容。 这将有助于我们有信心不断改进、重构和改进我们的应用程序。

我们将测试作为本章的最后一个主题进行介绍，但不是因为测试是您在开发过程结束时应该做的！ 相反，您应该在开发过程中尽早编写自动化测试。 这样做使您能够在开发时立即获得反馈，帮助您仔细考虑应用程序的用例方案，并指导您设计应用程序时要牢记干净的分层和耦合。

本书的后一章将讨论测试驱动开发 （TDD）以及如何将其与 mVC ASP.NET一起使用。 TDD 是一种迭代编码实践，您首先编写生成的代码将满足的测试。 使用 TDD，您首先创建一个测试，以验证即将实现的功能。 首先编写单元测试有助于确保您清楚地了解该功能及其应该如何工作。 只有在编写测试（并且已验证测试失败）后，您才会实现测试验证的实际功能。 由于您已经花时间考虑了该功能应该如何工作的用例，因此您将更好地了解这些要求以及如何最好地实现这些要求。 完成实现后，您可以重新运行测试，并立即获得有关该功能是否正常工作的反馈。 我们将在第 10 章中介绍 TDD。

### <a name="next-step"></a>下一步

一些最后的总结评论。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)

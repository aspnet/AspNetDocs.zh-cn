---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 迭代#6 = 使用测试驱动开发 （C#） |微软文档
author: rick-anderson
description: 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: d0e8f30a075cc79c7410ffe1b8bf02da2bd44443
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542321"
---
# <a name="iteration-6--use-test-driven-development-c"></a>迭代 6 – 使用测试驱动开发 (C#)

由[微软](https://github.com/microsoft)

[下载代码](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中，我们添加联系人组。

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

在 Contact Manager 应用程序的上一次迭代中，我们创建了单元测试，为我们的代码提供一个安全网。 创建单元测试的动机是使我们的代码对更改更具弹性。 通过单元测试，我们可以愉快地对我们的代码进行任何更改，并立即知道我们是否破坏了现有功能。

在此迭代中，我们将单元测试用于完全不同的目的。 在此迭代中，我们将单元测试用作称为*测试驱动开发*的应用程序设计理念的一部分。 练习测试驱动开发时，首先编写测试，然后针对测试编写代码。

更确切地说，在练习测试驱动开发时，在创建代码时完成三个步骤（红色/绿色/重构）：

1. 编写失败的单元测试（红色）
2. 编写通过单元测试的代码（绿色）
3. 重构代码（重构）

首先，编写单元测试。 单元测试应表达您希望代码如何的行为的意图。 首次创建单元测试时，单元测试应失败。 测试应失败，因为您尚未编写满足测试的任何应用程序代码。

接下来，您只编写足够的代码，以便单元测试通过。 目标是以最懒、最懒、最快的方式编写代码。 不应浪费时间考虑应用程序的体系结构。 相反，您应该专注于编写满足单元测试表达的意图所需的最小代码量。

最后，在编写了足够的代码后，您可以退后一步考虑应用程序的整体体系结构。 在此步骤中，您利用软件设计模式（如存储库模式）重写（重构）代码，以便代码更可维护。 您可以在此步骤中无所畏惧地重写代码，因为单元测试涵盖了您的代码。

实践测试驱动开发会带来许多好处。 首先，测试驱动的开发迫使您专注于实际需要编写的代码。 由于您始终专注于编写足够的代码以通过特定的测试，因此您无法游荡到杂草中，并编写大量永远不会使用的代码。

其次，"测试第一"设计方法迫使您从如何使用代码的角度编写代码。 换句话说，在练习测试驱动开发时，您会不断从用户的角度编写测试。 因此，测试驱动的开发可以产生更清洁、更易懂的 API。

最后，测试驱动的开发迫使您编写单元测试，作为编写应用程序的正常过程的一部分。 随着项目截止时间的临近，测试通常是窗口外的第一件事。 另一方面，在实践测试驱动开发时，您更有可能对编写单元测试具有道德性，因为测试驱动开发使单元测试成为构建应用程序过程的核心。

> [!NOTE] 
> 
> 要了解有关测试驱动开发的更多内容，我建议您阅读 Michael Feathers 的书，**以有效使用旧代码**。

在此迭代中，我们将向联系人管理器应用程序添加新功能。 我们添加对联系人组的支持。 您可以使用"联系人组"将联系人组织到"业务"和"朋友"组等类别中。

我们将遵循测试驱动开发过程，将这项新功能添加到我们的应用程序中。 我们将首先编写单元测试，并针对这些测试编写所有代码。

## <a name="what-gets-tested"></a>测试内容

正如我们在上一次迭代中讨论的那样，您通常不会为数据访问逻辑或视图逻辑编写单元测试。 您不会为数据访问逻辑编写单元测试，因为访问数据库的操作相对较慢。 您不为视图逻辑编写单元测试，因为访问视图需要旋转 Web 服务器，这是一个相对较慢的操作。 除非测试可以快速一遍又一遍地执行，否则不应编写单元测试

由于测试驱动开发由单元测试驱动，所以我们最初侧重于编写控制器和业务逻辑。 我们避免触摸数据库或视图。 在本教程结束之前，我们不会修改数据库或创建视图。 我们从可以测试的内容开始。

## <a name="creating-user-stories"></a>创建用户情景

练习测试驱动开发时，您总是从编写测试开始。 这立即提出了一个问题：你如何决定先写什么测试？ 要回答这个问题，你应该编写一组[**用户情景**](http://en.wikipedia.org/wiki/User_stories)。

用户情景是软件要求的非常简短（通常是一个句子）描述。 它应该是从用户的角度编写的对需求的非技术描述。

以下是描述新的联系人组功能所需的功能的用户情景集：

1. 用户可以查看联系人组的列表。
2. 用户可以创建新的联系人组。
3. 用户可以删除现有的联系人组。
4. 创建新联系人时，用户可以选择联系人组。
5. 用户可以在编辑现有联系人时选择联系人组。
6. 联系人组列表显示在"索引"视图中。
7. 当用户单击联系人组时，将显示匹配联系人的列表。

请注意，客户完全可以理解此用户情景列表。 没有提到技术实施细节。

在构建应用程序的过程中，用户情景集可能会变得更加精细。 您可以将用户情景分解为多个情景（要求）。 例如，您可能决定创建新的联系人组应涉及验证。 提交没有名称的联系人组应返回验证错误。

创建用户情景列表后，即可编写第一个单元测试。 我们将首先创建用于查看联系人组列表的单位测试。

## <a name="listing-contact-groups"></a>列出联系人组

我们的第一个用户故事是，用户应该能够查看联系人组的列表。 我们需要用测试来表达这个故事。

通过右键单击 ContactManager.测试项目中的控制器文件夹、选择 **"添加、新建测试**"并选择单元测试模板来创建新**的单元测试**（参见图 1）。 GroupControllerTest.cs为新单元测试命名，然后单击 **"确定**"按钮。

[![添加组控制器测试单元测试](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**图 01**： 添加组控制器测试单元测试（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image2.png)）

我们的第一个单元测试包含在清单 1 中。 此测试验证组控制器的 Index（） 方法是否返回一组组。 测试验证在视图数据中返回组的集合。

**清单 1 - 控制器\组控制器测试.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

当您首次在 Visual Studio 中键入清单 1 中的代码时，您将获得大量红色波浪线。 我们尚未创建组控制器或组类。

此时，我们甚至不能构建应用程序，因此无法执行第一个单元测试。 很好 这算作一个失败的测试。 因此，我们现在有权开始编写应用程序代码。 我们需要编写足够的代码来执行我们的测试。

清单 2 中的组控制器类包含通过单元测试所需的最小代码。 Index（） 操作返回静态编码的组列表（组类在清单 3 中定义）。

**清单2 - 控制器\组控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**清单3 - 模型_组.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

将 GroupController 和组类添加到项目中后，我们的第一个单元测试将成功完成（参见图 2）。 我们已经做了通过考试所需的最低工作。 是时候庆祝了。

[![成功！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**图02：** 成功！（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image4.png)）

## <a name="creating-contact-groups"></a>创建联系人组

现在，我们可以转到第二个用户情景。 我们需要能够创建新的联系组。 我们需要用测试来表达这个意图。

清单4中的测试验证，使用新组调用 Create（） 方法会将组添加到 Index（） 方法返回的组列表中。 换句话说，如果我创建了一个新组，那么我应该能够从 Index（） 方法返回的组列表中恢复新组。

**清单4 - 控制器\组控制器测试.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

清单4中的测试使用新的联系人组调用组控制器 Create（） 方法。 接下来，测试验证调用组控制器 Index（） 方法返回视图中的新组数据。

清单 5 中修改后的组控制器包含通过新测试所需的最小更改。

**清单5 - 控制器\组控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>清单 5 中的组控制器具有新的 Create（） 操作。 此操作将组添加到组的集合中。 请注意，已修改 Index（） 操作以返回组集合的内容。

再次，我们执行了通过单元测试所需的最低工作量。 对组控制器进行这些更改后，所有单元测试都通过。

## <a name="adding-validation"></a>添加验证

在用户情景中未明确说明此要求。 但是，要求集团有名称是合理的。 否则，将联系人组织到组中将不是很有用。

清单6包含表示此意图的新测试。 此测试验证尝试创建组而不提供名称会导致模型状态的验证错误消息。

**清单6 - 控制器\组控制器测试.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

为了满足此测试，我们需要向组类添加 Name 属性（请参阅清单 7）。 此外，我们需要向组控制器的 Create（） 操作添加一点验证逻辑（参见清单 8）。

**清单7 - 模型_组.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**清单8 - 控制器\组控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

请注意，组控制器 Create（） 操作现在同时包含验证和数据库逻辑。 目前，组控制器使用的数据库仅包含内存中的集合。

## <a name="time-to-refactor"></a>重构时间

红色/绿色/重构的第三步是重构部分。 此时，我们需要从代码中退后一步，考虑如何重构应用程序以改进其设计。 重构阶段是我们认真思考实现软件设计原则和模式的最佳方式的阶段。

我们可以自由地修改我们的代码，我们选择以任何方式改进代码的设计。 我们有一个单元测试安全网，以防止我们破坏现有功能。

现在，从良好的软件设计来看，我们的集团控制器是一团糟。 组控制器包含一堆的验证和数据访问代码。 为了避免违反单一责任原则，我们需要将这些关注分为不同的类别。

我们的重构组控制器类包含在清单 9 中。 控制器已修改为使用 ContactManager 服务层。 这与我们与联系人控制器一起使用的服务层相同。

清单10包含添加到 ContactManager 服务层以支持验证、列出和创建组的新方法。 IContactManager 服务接口已更新，以包括新方法。

清单11包含一个新的 FakeContactManagerManager存储库类，该类实现了 IContactManagerRepository 接口。 与同时实现 IContactManagerRepository 接口的实体联系人管理器存储库类不同，我们新的 FakeContactManagerManagerRepository 类不与数据库通信。 FakeContactManagerManagerRepository 类使用内存中集合作为数据库的代理。 我们将在单元测试中将此类用作假存储库层。

**清单 9 - 控制器\组控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**清单 10 - 控制器\联系管理器服务.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**清单11 - 控制器\假联系人管理器存储库.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

修改 IContactManager 存储库界面需要用于在实体联系人管理器存储库类中实现 CreateGroup（） 和列表组（）方法。 最懒惰和最快的方法是添加如下所示的存根方法：   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

最后，对应用程序设计的这些更改要求我们对单元测试进行一些修改。 现在，在执行单元测试时，我们需要使用假联系人管理器存储库。 更新后的 GroupControllerTest 类包含在清单 12 中。

**清单12 - 控制器\组控制器测试.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

在我们进行所有这些更改后，我们再次通过所有单元测试。 我们已经完成了整个红色/绿色/重构周期。 我们已经实现了前两个用户情景。 现在，我们支持用户情景中表达的要求单元测试。 实现其余用户情景涉及重复相同的红色/绿色/重构周期。

## <a name="modifying-our-database"></a>修改我们的数据库

不幸的是，尽管我们满足了单元测试表达的所有要求，但我们的工作并没有完成。 我们仍然需要修改我们的数据库。

我们需要创建新的组数据库表。 执行以下步骤:

1. 在"服务器资源管理器"窗口中，右键单击"表"文件夹并选择菜单选项 **"添加新表**"。
2. 输入下表设计器中描述的两列。
3. 将 Id 列标记为主键和标识列。
4. 单击软盘的图标，保存具有名称组的新表。

<a id="0.11_table01"></a>

| **列名** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| ID | int | False |
| “属性” | nvarchar(50) | False |

接下来，我们需要从"联系人"表中删除所有数据（否则，我们将无法在"联系人"和"组"表之间创建关系）。 执行以下步骤:

1. 右键单击"联系人"表并选择菜单选项 **"显示表数据**"。
2. 删除所有行。

接下来，我们需要定义组数据库表和现有联系人数据库表之间的关系。 执行以下步骤:

1. 双击服务器资源管理器窗口中的"联系人"表以打开表设计器。
2. 向名为 GroupId 的"联系人"表添加新整数列。
3. 单击"关系"按钮以打开"外键关系"对话框（参见图 3）。
4. 单击“添加”按钮。
5. 单击"表和列规范"按钮旁边的省略号按钮。
6. 在"表和列"对话框中，选择组作为主键表，选择 Id 作为主键列。 选择"联系人"作为外键表，将 GroupId 作为外键列（参见图 4）。 单击“确定”按钮。
7. 在 **"插入"和"更新规范"** 下，选择**删除规则**的值 **"级联**"。
8. 单击"关闭"按钮以关闭"外键关系"对话框。
9. 单击"保存"按钮将更改保存到"联系人"表。

[![创建数据库表关系](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**图 03**： 创建数据库表关系 （[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image6.png)）

[![指定表关系](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**图 04**：指定表关系（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image8.png)）

### <a name="updating-our-data-model"></a>更新我们的数据模型

接下来，我们需要更新数据模型以表示新的数据库表。 执行以下步骤:

1. 双击"模型"文件夹中的 ContactManagerModel.edmx 文件以打开实体设计器。
2. 右键单击"设计器"曲面，然后从数据库中选择菜单选项 **"更新模型**"。
3. 在"更新向导"中，选择"组"表并单击"完成"按钮（参见图 5）。
4. 右键单击"组实体"并选择菜单选项 **"重命名**"。 将*组*实体的名称更改为*组*（单数）。
5. 右键单击显示在"联系人"实体底部的"组导航属性"。 将*组*导航属性的名称更改为*组*（单数）。

[![从数据库更新实体框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**图 05**：从数据库更新实体框架模型（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image10.png)）

完成这些步骤后，数据模型将同时表示"联系人"和"组"表。 实体设计器应显示两个实体（参见图 6）。

[![实体设计器显示组和联系人](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**图 06**： 实体设计器显示组和联系人（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image12.png)）

### <a name="creating-our-repository-classes"></a>创建我们的存储库类

接下来，我们需要实现我们的存储库类。 在此迭代过程中，我们在编写代码以满足单元测试的同时，向 IContactManagerRepository 界面添加了几种新方法。 IContactManager存储库界面的最终版本包含在清单14中。

**清单14 - 型号\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

我们实际上尚未实现与使用联系人组相关的任何方法。 目前，实体联系人管理器存储库类具有 IContactManagerRepository 界面中列出的每个联系人组方法的存根方法。 例如，ListGroups（） 方法当前如下所示：

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

存根方法使我们能够编译应用程序并通过单元测试。 但是，现在是时候实际实现这些方法了。 实体联系人管理器存储库类的最终版本包含在清单 13 中。

**清单13 - 模型_实体联系人管理器存储库.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>创建视图

使用默认ASP.NET视图引擎时，ASP.NET MVC 应用程序。 因此，您不会创建视图以响应特定的单元测试。 但是，由于没有视图的应用程序将毫无用处，因此，如果不创建和修改 Contact Manager 应用程序中的视图，我们就无法完成此迭代。

我们需要创建以下用于管理联系人组的新视图（参见图 7）：

- 视图_组\索引.aspx - 显示联系人组列表
- 视图\组\删除.aspx - 显示用于删除联系人组的确认表单

[![组索引视图](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**图 07**： 组索引视图（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image14.png)）

我们需要修改以下现有视图，以便它们包括联系人组：

- 视图\Home_Create.aspx
- 视图\主页\编辑.aspx
- 视图\主页\索引.aspx

通过查看本教程附带的 Visual Studio 应用程序，可以查看修改后的视图。 例如，图 8 说明了联系人索引视图。

[![联系人索引视图](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**图 08**： 联系人索引视图（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image16.png)）

## <a name="summary"></a>总结

在此迭代中，我们遵循测试驱动的开发应用程序设计方法，向 Contact Manager 应用程序添加了新功能。 我们首先创建一组用户情景。 我们创建了一组单元测试，这些测试对应于用户情景表达的要求。 最后，我们编写的代码足够满足单元测试表达的要求。

完成编写足够的代码以满足单元测试表达的要求后，我们更新了数据库和视图。 我们将新的组表添加到我们的数据库中，并更新了实体框架数据模型。 我们还创建并修改了一组视图。

在下一次迭代（最后迭代）中，我们重写应用程序以利用Ajax。 通过使用Ajax，我们将提高联系人管理器应用程序的响应性和性能。

> [!div class="step-by-step"]
> [上一页](iteration-5-create-unit-tests-cs.md)
> [下一页](iteration-7-add-ajax-functionality-cs.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 迭代#3 = 添加表单验证 （VB） |微软文档
author: rick-anderson
description: 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证了 emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ee2f40996873a7af2eaa255edd5f157c3fefb29
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542386"
---
# <a name="iteration-3--add-form-validation-vb"></a>迭代 3 – 添加表单验证 (VB)

由[微软](https://github.com/microsoft)

[下载代码](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证电子邮件地址和电话号码。

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

在联系人管理器应用程序的第二次迭代中，我们添加基本表单验证。 我们防止人员提交联系人而不输入所需表单字段的值。 我们还验证电话号码和电子邮件地址（参见图 1）。

[![“新建项目”对话框](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**图 01**： 具有验证的窗体 （[单击以查看全尺寸图像](iteration-3-add-form-validation-vb/_static/image2.png)）

在此迭代中，我们将验证逻辑直接添加到控制器操作中。 通常，这不是向ASP.NET MVC 应用程序添加验证的建议方法。 更好的方法是将应用程序的验证逻辑放在单独的[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。 在下一次迭代中，我们将重构联系人管理器应用程序，以使应用程序更具可维护性。

在此迭代中，为了简单化，我们手动编写所有验证代码。 我们可以利用验证框架，而不是自己编写验证代码。 例如，可以使用 Microsoft 企业库验证应用程序块 （VAB） 来实现ASP.NET MVC 应用程序的验证逻辑。 要了解有关验证应用程序块的更多，请参阅：

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>将验证添加到创建视图

让我们首先向"创建"视图添加验证逻辑。 幸运的是，由于我们使用 Visual Studio 生成了"创建"视图，因此"创建"视图已包含显示验证消息所需的所有用户界面逻辑。 "创建"视图包含在清单 1 中。

**清单 1 - [视图]联系人\创建.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

字段验证错误类用于设置 Html.验证Message（） 帮助程序呈现的输出的样式。 输入验证错误类用于设置 Html.TextBox（） 帮助程序呈现的文本框（输入）的样式。 验证摘要错误类用于设置 Html.验证摘要（） 帮助程序呈现的无序列表的样式。

> [!NOTE] 
> 
> 您可以修改本节中描述的样式表类，以自定义验证错误消息的外观。

## <a name="adding-validation-logic-to-the-create-action"></a>将验证逻辑添加到创建操作

现在，"创建"视图从不显示验证错误消息，因为我们尚未编写逻辑来生成任何消息。 为了显示验证错误消息，您需要将错误消息添加到 ModelState。

> [!NOTE] 
> 
> 当将表单字段的值分配给属性时，UpdateModel（） 方法会自动将错误消息添加到 ModelState。 例如，如果您尝试将字符串"apple"分配给接受 DateTime 值的 DateDate 属性，则 UpdateModel（） 方法将错误添加到 ModelState。

清单 2 中修改的 Create（） 方法包含一个新部分，用于在新联系人插入数据库之前验证 Contact 类的属性。

**清单2 - 控制器\联系控制器.vb（通过验证创建）**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

验证部分强制实施四个不同的验证规则：

- FirstName 属性的长度必须大于零（它不能仅由空格组成）
- LastName 属性的长度必须大于零（它不能仅由空格组成）
- 如果 Phone 属性具有值（长度大于 0），则 Phone 属性必须匹配正则表达式。
- 如果 Email 属性的值（长度大于 0），则 Email 属性必须与正则表达式匹配。

当存在验证规则冲突时，在 AddModelError（） 方法的帮助下，将一条错误消息添加到 ModelState。 将消息添加到 ModelState 时，会提供属性的名称和验证错误消息的文本。 此错误消息由 Html.验证摘要（） 和 Html.验证消息（） 帮助器方法显示在视图中。

执行验证规则后，将检查 ModelState 的"IsValid"属性。 将任何验证错误消息添加到 ModelState 时，"IsValid"属性将返回 false。 如果验证失败，则使用错误消息重新显示"创建"窗体。

> [!NOTE] 
> 
> 我收到用于验证从正则表达式存储库的电话号码和电子邮件地址的正则表达式，[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>将验证逻辑添加到编辑操作

编辑（） 操作更新联系人。 Edit（） 操作需要执行与 Create（） 操作完全相同的验证。 我们不应复制相同的验证代码，而应重构联系人控制器，以便 Create（） 和 Edit（） 操作调用相同的验证方法。

修改后的联系人控制器类包含在清单 3 中。 此类具有在 Create（） 和 Edit（） 操作中调用的新验证联系人（） 方法。

**清单3 - 控制器\联系控制器.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>总结

在此迭代中，我们将基本表单验证添加到我们的联系人管理器应用程序中。 我们的验证逻辑可防止用户提交新联系人或编辑现有联系人，而不提供 NameName 和 LASTName 属性的值。 此外，用户必须提供有效的电话号码和电子邮件地址。

在此迭代中，我们以最简单的方式将验证逻辑添加到我们的联系人管理器应用程序中。 但是，从长期来看，将验证逻辑混合到控制器逻辑中将给我们带来问题。 随着时间的推移，我们的应用程序将更难维护和修改。

在下一次迭代中，我们将重构我们的验证逻辑和数据库访问逻辑的控制器。 我们将利用多种软件设计原则，使我们能够创建一个更松散耦合、更可维护的应用程序。

> [!div class="step-by-step"]
> [上一页](iteration-2-make-the-application-look-nice-vb.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-vb.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 迭代#2 = 使应用程序看起来不错 （VB） |微软文档
author: rick-anderson
description: 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a97958db442c48bd696f6414f7226127984bc34
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542425"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>迭代 2 – 使应用程序外表美观 (VB)

由[微软](https://github.com/microsoft)

[下载代码](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建 MVC 应用程序 （VB） ASP.NET联系人管理

在本系列教程中，我们从头到尾构建整个联系人管理应用程序。 通过联系人管理器应用程序，您可以存储联系人信息（姓名、电话号码和电子邮件地址）以存储人员列表。

我们通过多次迭代构建应用程序。 每次迭代时，我们都会逐步改进应用程序。 此多迭代方法的目标是使您能够了解每次更改的原因。

- 迭代#1 = 创建应用程序。 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。

- 迭代#2 = 使应用程序看起来不错。 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。

- 迭代#3 = 添加表单验证。 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证电子邮件地址和电话号码。

- 迭代#4 = 使应用程序松散耦合。 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 例如，我们重构应用程序以使用存储库模式和依赖项注入模式。

- 迭代#5 = 创建单元测试。 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。

- 迭代#6 = 使用测试驱动开发。 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代#7 = 添加 Ajax 功能。 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。

## <a name="this-iteration"></a>此迭代

此迭代的目标是改进联系人管理器应用程序的外观。 目前，联系人管理器使用默认ASP.NET MVC 视图母版页和级联样式表（参见图 1）。 这些看起来并不坏，但我不希望联系人管理器看起来像所有其他ASP.NET MVC 网站。 我想用自定义文件替换这些文件。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**图 01**： ASP.NET mVC 应用程序的默认外观（[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image2.png)）

在此迭代中，我讨论了改进应用程序可视化设计的两种方法。 首先，我将向您展示如何利用ASP.NET MVC 设计库下载免费ASP.NET MVC 设计模板。 ASP.NET MVC 设计库使您能够创建专业 Web 应用程序，而无需进行任何工作。

我决定不再使用联系人管理器应用程序ASP.NET MVC 设计库中的模板。 相反，我有一个专业的设计公司创造的定制设计。 在本教程的第二部分中，我解释了我如何与一家专业设计公司合作，创建最终ASP.NET MVC 设计。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 设计库

ASP.NET MVC 设计库是微软提供的免费资源。 ASP.NET MVC 库位于以下地址：

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 设计库托管一组免费网站设计，这些设计专为ASP.NET MVC 项目中使用而创建。 设计由社区成员上传。 参观画廊的参观者可以投票选出他们最喜欢的设计（参见图2）。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**图02**： ASP.NET MVC 设计库 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image4.png)）

在写本教程时，画廊中最受欢迎的设计是大卫·豪瑟设计的10月。 您可以通过完成以下步骤，为 mVC 项目ASP.NET使用此设计：

1. 单击 **"下载**"按钮将 10 月.zip 文件下载到您的计算机。
2. 右键单击下载的 10 月.zip 文件，然后单击 **"取消阻止"** 按钮（参见图 3）。
3. 解压缩文件到名为 10 月的文件夹。
4. 从 10 月文件夹中的 DesignTemplate 文件夹中选择所有文件，右键单击文件，然后选择菜单选项 **"复制**"。
5. 右键单击可视化工作室解决方案资源管理器窗口中的 ContactManager 项目节点，然后选择菜单选项 **"粘贴**"（参见图 4）。
6. 选择"可视化工作室"菜单选项 **"编辑、查找和替换"、"快速替换**"，*并将其替换为**联系人管理器*（参见图 5）。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**图 03**： 取消阻止从 Web 下载的文件 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image6.png)）

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**图 04**： 解决方案资源管理器中的覆盖文件 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image8.png)）

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**图 05**： 将 [项目名称] 替换为联系人管理器 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image10.png)）

完成这些步骤后，Web 应用程序将使用新设计。 图 6 中的页面说明了使用 10 月设计的联系人管理器应用程序的外观。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**图 06**： 使用 10 月模板联系经理 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image12.png)）

## <a name="creating-a-custom-aspnet-mvc-design"></a>创建自定义ASP.NET MVC 设计

ASP.NET MVC 设计库具有多种设计风格。 库为您提供了一种无痛的方式来自定义ASP.NET MVC 应用程序的外观。 当然，画廊有很大的优势是完全自由的。

但是，您可能需要为您的网站创建完全独特的设计。 在这种情况下，与网站设计公司合作是有意义的。 我决定采用这种方法来设计联系人管理器应用程序。

我压缩了迭代#1的联系人管理器，并将项目发送给了设计公司。 他们没有视觉工作室（羞辱他们！ 他们能够从网站免费下载 Microsoft 可视化 Web[https://www.asp.net](https://www.asp.net)开发人员，并在可视化 Web 开发人员中打开联系人管理器应用程序。 几天后，他们制作了图7中的设计。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**图07**： ASP.NET MVC 联系人管理器设计 （[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image14.png)）

新的设计由两个主要文件组成：一个新的级联样式表文件和一个新的视图母版页文件。 视图母版页包含ASP.NET MVC 应用程序中的视图的布局和共享内容。 例如，视图母版页包括图 7 中显示的标题、导航选项卡和页脚。 我用新的 Site.Master 文件在"视图"和"共享"文件夹中重写了现有的 Site.Master 视图母版页，

设计公司还创建了一个新的级联样式表和一组图像。 我把这些新文件放在内容文件夹中，并覆盖了现有的 Site.css 文件。 应将所有静态内容放在"内容"文件夹中。

请注意，联系人管理器的新设计包括用于编辑和删除联系人的图像。 联系人的 HTML 表中，每个联系人旁边都会显示"编辑"和"删除"图像。

最初，这些链接是使用 HTML 呈现的。操作链接（） 帮助程序如下所示：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink（） 方法不支持图像（出于安全原因，方法 HTML 对链接文本进行编码）。 因此，我将对 Html.ActionLink（） 的调用替换为对 Url.Action（） 的调用，如下所示：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink（） 方法呈现整个 HTML 超链接。 另一方面，Url.Action（） 方法只呈现没有&lt;&gt;标记的 URL。

此外，请注意，新设计包括所选选项卡和未选中选项卡。 例如，在图 8 中，选择了 **"创建新联系人"** 选项卡，并且未选择"**我的联系人**"选项卡。

[![“新建项目”对话框](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**图 08**：选定和未选中的选项卡（[单击以查看全尺寸图像](iteration-2-make-the-application-look-nice-vb/_static/image16.png)）

为了支持呈现所选选项卡和未选中选项卡，我创建了一个名为 MenuItemHelper 的自定义 HTML 帮助程序。 此帮助&lt;器方法呈现一个 li&gt;标记或&lt;li class="&gt;选定"标记，具体取决于当前控制器和操作是否与传递给帮助程序的控制器和操作名称相对应。 菜单项目帮助程序的代码包含在清单 1 中。

**清单1 = 帮助者\菜单项目帮助程序.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper 在内部使用 TagBuilder 类来&lt;构建&gt;li HTML 标记。 TagBuilder 类是一个非常有用的实用程序类，您可以随时构建新的 HTML 标记时使用该类。 它包括添加属性、添加 CSS 类、生成 Id 和修改标记的内部 HTML 的方法。

## <a name="summary"></a>总结

在此迭代中，我们改进了ASP.NET MVC 应用程序的可视化设计。 首先，您将被介绍到ASP.NET MVC 设计库。 您学习了如何从ASP.NET MVC 设计库中下载免费设计模板，这些模板可用于ASP.NET MVC 应用程序中。

接下来，我们将讨论如何通过修改默认级联样式表文件和母版视图页文件来创建自定义设计。 为了支持新设计，我们不得不对我们的联系人管理器应用程序进行一些小的更改。 例如，我们添加了一个名为 MenuItemHelper 的新 HTML 帮助程序，该助手显示所选和未选中的选项卡。

在下一个迭代中，我们将处理非常重要的验证主题。 我们将验证代码添加到我们的应用程序中，以便用户在未提供所需值（如人员姓名和姓氏）的情况下无法创建新联系人。

> [!div class="step-by-step"]
> [上一页](iteration-1-create-the-application-vb.md)
> [下一页](iteration-3-add-form-validation-vb.md)

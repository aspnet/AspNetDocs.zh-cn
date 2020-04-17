---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: 使用数据注释验证器 （C#） 进行验证 |微软文档
author: rick-anderson
description: 利用数据注释模型绑定器在 mVC 应用程序中执行验证ASP.NET。 了解如何使用不同类型的验证器...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542672"
---
# <a name="validation-with-the-data-annotation-validators-c"></a>使用数据注释验证程序进行验证 (C#)

由[微软](https://github.com/microsoft)

> 利用数据注释模型绑定器在 mVC 应用程序中执行验证ASP.NET。 了解如何使用不同类型的验证器属性，并在 Microsoft 实体框架中使用它们。

在本教程中，您将了解如何使用数据注释验证器在 ASP.NET MVC 应用程序中执行验证。 使用数据注释验证器的优点是，它们仅通过向类属性添加一个或多个属性（如"必需"或"字符串长度"属性）即可执行验证。

在使用数据注释验证器之前，必须下载数据注释模型绑定器。 您可以通过[单击此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)从 CodePlex 网站下载数据注释模型粘合剂示例。

请务必了解，数据注释模型绑定器不是 Microsoft ASP.NET MVC 框架的正式部分。 尽管数据注释模型活页夹是由 Microsoft ASP.NET MVC 团队创建的，但 Microsoft 不会为本教程中介绍和使用的数据注释模型粘合剂提供官方产品支持。

## <a name="using-the-data-annotation-model-binder"></a>使用数据注释模型绑定器

为了在ASP.NET MVC 应用程序中使用数据注释模型绑定器，首先需要添加对 Microsoft.Web.Mvc.Dataannotations.dll 程序集和 System.组件模型.Datathethe.dll 程序集的引用。 选择菜单选项 **"项目"，添加参考**。 接下来，单击 **"浏览"** 选项卡并浏览到下载（并解压缩）数据注释模型装订器示例的位置（参见**图 1）。**

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**图 1**： 添加对数据注释模型装订器的引用 （[单击以查看全尺寸图像](validation-with-the-data-annotation-validators-cs/_static/image3.png)）

同时选择 Microsoft.Web.Mvc.Data注释.dll 程序集和系统.组件模型.DataAnnotations.dll 程序集，然后单击 **"确定"** 按钮。

不能使用系统.组件模型.Data注释.dll 程序集包含在 .NET 框架服务包 1 与数据注释模型绑定器。 您必须使用系统版本.组件模型.Data注释.dll 程序集包含在数据注释模型装订器示例下载中。

最后，您需要在 Global.asax 文件中注册 DataAnnotations 模型绑定器。 将以下代码行添加到应用程序\_Start（） 事件处理程序，以便应用程序\_Start（） 方法如下所示：

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

此代码行将 ataAnnotationsModelBinder 注册为整个ASP.NET MVC 应用程序的默认模型活页夹。

## <a name="using-the-data-annotation-validator-attributes"></a>使用数据注释验证器属性

使用数据注释模型装订器时，可以使用验证器属性执行验证。 系统.组件模型.Data注释命名空间包括以下验证器属性：

- 范围 – 使您能够验证属性的值是否介于指定的值范围之间。
- 正则表达式 – 使您能够验证属性的值是否与指定的正则表达式模式匹配。
- 必需 = 使您能够根据需要标记属性。
- 字符串长度 – 使您能够为字符串属性指定最大长度。
- 验证 = 所有验证器属性的基类。

> [!NOTE] 
> 
> 如果任何标准验证器未满足验证需求，则始终可以选择通过从基本验证属性继承新的验证器属性来创建自定义验证器属性。

**清单1**中的"产品"类说明了如何使用这些验证器属性。 名称、说明和单价属性按要求进行标记。 Name 属性的字符串长度必须小于 10 个字符。 最后，UnitPrice 属性必须匹配表示货币金额的正则表达式模式。

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**清单1**：型号\产品.cs

"产品"类说明了如何使用一个附加属性：显示名称属性。 在错误消息中显示属性时，显示Name 属性允许您修改属性的名称。 您可以显示错误消息"需要价格"，而不是显示错误消息"需要价格"

> [!NOTE] 
> 
> 如果要完全自定义验证器显示的错误消息，则可以将自定义错误消息分配给验证器的 ErrorMessage 属性，如下所示：`<Required(ErrorMessage:="This field needs a value!")>`

您可以将**清单 1**中的"产品"类与**清单 2**中的 Create（） 控制器操作一起使用。 当模型状态包含任何错误时，此控制器操作重新显示"创建"视图。

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**清单2**：控制器\产品控制器.vb

最后，您可以通过右键单击 Create（） 操作并选择菜单选项 **"添加视图**"来在**清单 3**中创建视图。 创建以 Product 类为模型类的强类型视图。 从视图内容下拉列表中**选择"创建**"（参见**图 2**）。

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**图 2**： 添加创建视图

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**清单3**：视图\产品\创建.aspx

> [!NOTE] 
> 
> 从"**添加视图"** 菜单选项生成的"创建窗体"中删除"Id"字段。 由于 Id 字段对应于标识列，因此您不希望允许用户输入此字段的值。

如果提交表单以创建产品，并且未输入所需字段的值，则将显示**图 3**中的验证错误消息。

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**图 3**：缺少必填字段

如果输入无效的货币金额，则将显示**图 4**中的错误消息。

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**图4**：无效货币金额

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>将数据注释验证器与实体框架一起使用

如果使用 Microsoft 实体框架生成数据模型类，则无法将验证器属性直接应用于类。 由于实体框架设计器生成模型类，因此下次在设计器中进行任何更改时，将对模型类所做的任何更改都将被覆盖。

如果要将验证器与实体框架生成的类一起使用，则需要创建元数据类。 将验证器应用于元数据类，而不是将验证器应用于实际类。

例如，假设您已使用实体框架创建了 Movie 类（参见**图 5**）。 此外，假设您要使影片标题和导演属性成为所需的属性。 在这种情况下，您可以在**清单 4**中创建部分类和元数据类。

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**图 5**： 实体框架生成的影片类

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**清单4**： 模型_电影.cs

**清单4**中的文件包含名为"电影"和"MovieMetaData"的两个类。 "影片"类是部分类。 它对应于数据模型.Designer.vb 文件中包含的实体框架生成的部分类。

目前，.NET 框架不支持部分属性。 因此，无法通过将验证器属性应用于**清单 4**中文件中定义的 Movie 类的属性，从而将验证器属性应用于 DataModel.designer.vb 文件中定义的 Movie 类的属性。

请注意，影片部分类用指向 MovieMetaData 类的元数据类型属性进行修饰。 MovieMetaData 类包含影片类属性的代理属性。

验证器属性应用于 MovieMetaData 类的属性。 标题、控制器和日期释放属性都标记为必需属性。 必须为 Director 属性分配包含少于 5 个字符的字符串。 最后，显示Name 属性应用于 Date 下达属性，以显示错误消息，如"需要发布日期发布"字段。 而不是错误"需要日期释放字段"。

> [!NOTE] 
> 
> 请注意，MovieMetaData 类中的代理属性不需要表示与 Movie 类中的相应属性相同的类型。 例如，Director 属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。

**图 6**中的页面演示了在为 Movie 属性输入无效值时返回的错误消息。

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**图 6**： 使用验证器与实体框架 （[单击以查看全尺寸图像](validation-with-the-data-annotation-validators-cs/_static/image14.png)）

## <a name="summary"></a>总结

在本教程中，您学习了如何使用数据注释模型绑定器在ASP.NET MVC 应用程序中执行验证。 您学习了如何使用不同类型的验证器属性，如"必需"和"字符串长度"属性。 在使用 Microsoft 实体框架时，您还学习了如何使用这些属性。

> [!div class="step-by-step"]
> [上一页](validating-with-a-service-layer-cs.md)
> [下一页](creating-model-classes-with-the-entity-framework-vb.md)

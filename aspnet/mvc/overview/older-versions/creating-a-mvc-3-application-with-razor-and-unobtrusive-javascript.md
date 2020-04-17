---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和不显眼的 JavaScript 创建 MVC 3 应用程序 |微软文档
author: rick-anderson
description: 用户列表示例 Web 应用程序演示了使用 Razor 视图引擎创建ASP.NET MVC 3 应用程序是多么简单。 示例应用程序...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542451"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>使用 Razor 和非介入性 JavaScript 创建 MVC 3 应用程序

由[微软](https://github.com/microsoft)

> 用户列表示例 Web 应用程序演示了使用 Razor 视图引擎创建ASP.NET MVC 3 应用程序是多么简单。 该示例应用程序演示如何使用带有 ASP.NET mVC 版本 3 和 Visual Studio 2010 的新 Razor 视图引擎来创建虚构的用户列表网站，该网站包含创建、显示、编辑和删除用户等功能。
> 
> 本教程介绍为生成用户列表示例而采取的步骤ASP.NET MVC 3 应用程序。 带有 C# 和 VB 源代码的可视化工作室项目可随同本主题：[下载](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。 如果您对本教程有疑问，请将其发布到[MVC 论坛](https://forums.asp.net/1146.aspx)。

## <a name="overview"></a>概述

您将构建的应用程序是一个简单的用户列表网站。 用户可以输入、查看和更新用户信息。

![示例站点](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

您可以[在此处](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)下载 VB 和 C# 已完成的项目。

## <a name="creating-the-web-application"></a>创建 Web 应用程序

要开始本教程，请打开 Visual Studio 2010 并使用ASP.NET *MVC 3 Web 应用程序*模板创建新项目。 命名应用程序&quot;Mvc3Razor&quot;。

[![新的 MVC 3 项目](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

在新**ASP.NET MVC 3 项目**对话框中，选择 Internet**应用程序**，选择 Razor 视图引擎，然后单击"**确定**"。

![新ASP.NET MVC 3 项目对话框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

在本教程中，您将不使用ASP.NET成员资格提供程序，因此您可以删除与登录和成员资格关联的所有文件。 在**解决方案资源管理器中**，删除以下文件和目录：

- *控制器\帐户控制器*
- *模型_帐户模型*
- *视图\共享\\_LogOnPartial*
- *视图\帐户*（以及此目录中的所有文件）

![索伦·Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

编辑<em>\_Layout.cshtml</em>文件，并将命名`<div>``logindisplay`的元素内的标记替换为消息<em>&quot;</em>"登录禁用"。&quot; 下面的示例显示了新的标记：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>添加模型

在 **"解决方案资源管理器"** 中，右键单击 *"模型"* 文件夹，选择 **"添加**"，然后单击 **"类**"。

![新用户 Mdl 类](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

命名类 `UserModel`。 将*UserModel*文件的内容替换为以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

类`UserModel`表示用户。 类的每个成员都使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的["必需"](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性进行批注。 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的属性为 Web 应用程序提供自动客户端和服务器端验证。

打开类`HomeController`并添加指令`using`，以便您可以访问 和`UserModel``Users`类：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

声明之后`HomeController`，添加以下注释和对`Users`类的引用：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

该`Users`类是一个简化的内存数据存储，您将在本教程中使用。 在实际应用程序中，您将使用数据库来存储用户信息。 `HomeController`该文件的前几行显示在以下示例中：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

生成应用程序，以便用户模型在下一步中可供基架向导使用。

## <a name="creating-the-default-view"></a>创建默认视图

下一步是添加一个操作方法和视图来显示用户。

删除现有的*视图\Home_索引*文件。 您将创建新*的 Index*文件以显示用户。

在`HomeController`类中，将`Index`方法的内容替换为以下代码：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

右键单击方法内`Index`，然后单击"**添加视图**"。

![添加视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

选择"**创建强类型视图**"选项。 对于**查看数据类**，请选择**Mvc3Razor.Model.UserModel**。 （如果您没有看到**Mvc3Razor.Models.UserModel**在 **"查看数据"类**框中，则需要生成项目。确保视图引擎设置为**Razor**。 将 **"查看内容**"设置为 **"列表**"，然后单击"**添加**"。

![添加索引视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新视图会自动对传递给`Index`视图的用户数据基脚架。 检查新生成的*视图\Home_Index*文件。 **"创建新**"、"**编辑**"、"**详细信息**"和 **"删除**"链接不起作用，但页面的其余部分正常工作。 运行页面。 您将看到用户列表。

![索引页](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

打开*Index.cshtml*文件，用`ActionLink`以下代码替换**编辑**、**详细信息**和**删除**的标记：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

用户名用作 ID，用于在 **"编辑**"、"**详细信息****"和"删除**"链接中查找所选记录。

## <a name="creating-the-details-view"></a>创建详细信息视图

下一步是添加操作`Details`方法和视图，以便显示用户详细信息。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

将以下`Details`方法添加到主控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

右键单击方法内`Details`，然后选择<strong>"添加视图</strong>"。 验证<strong>"查看数据类"</strong>框是否包含<strong>Mvc3Razor.Model.UserModel</strong><em>。</em> 将<strong>"查看内容"</strong>设置为<strong>"详细信息</strong>"，然后单击"<strong>添加</strong>"。

![添加详细信息视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

运行应用程序并选择详细信息链接。 自动基架显示模型中的每个属性。

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>创建编辑视图

将以下`Edit`方法添加到主控制器。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

添加视图与前面的步骤一样，但将 **"查看内容"** 设置为 **"编辑**"。

![添加编辑视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

运行应用程序并编辑其中一个用户的名字和姓氏。 如果违反了已应用于`DataAnnotation``UserModel`类的任何约束，则在提交表单时，将看到服务器代码生成的验证错误。 例如，如果在提交表单时将名字&quot;Ann&quot; &quot;更改为&quot;A，则窗体上将显示以下错误：

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

在本教程中，您将用户名视为主键。 因此，无法更改用户名属性。 在*Edit.cshtml*文件中，在`Html.BeginForm`语句之后，将用户名设置为隐藏字段。 这将导致在模型中传递该属性。 以下代码片段显示语句的位置`Hidden`：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

将`TextBoxFor`用户名的`ValidationMessageFor`和 标记替换为`DisplayFor`调用。 该方法`DisplayFor`将该属性显示为只读元素。 下面的示例演示了完整标记。 原始`TextBoxFor`和`ValidationMessageFor`调用用 Razor 开头注释和结束注释字符 （）`@* *@`注释出来

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>启用客户端验证

要在 ASP.NET MVC 3 中启用客户端验证，必须设置两个标志，并且必须包含三个 JavaScript 文件。

打开应用程序的*Web.config*文件。 在`that ClientValidationEnabled`应用程序`UnobtrusiveJavaScriptEnabled`设置中验证并设置为 true。 root *Web.config*文件中的以下片段显示了正确的设置：

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

设置为`UnobtrusiveJavaScriptEnabled`true 可实现不显眼的 Ajax 和不显眼的客户端验证。 使用不显眼的验证时，验证规则将转换为 HTML5 属性。 HTML5 属性名称只能包含小写字母、数字和破折号。

设置为`ClientValidationEnabled`true 启用客户端验证。 通过在应用程序*Web.config 文件中*设置这些密钥，您可以为整个应用程序启用客户端验证和不显眼的 JavaScript。 您还可以使用以下代码在单个视图或控制器方法中启用或禁用这些设置：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

您还需要在呈现的视图中包含多个 JavaScript 文件。 在所有视图中包含 JavaScript 的一种简单方法是将它们添加到*视图_共享\\_Layout.cshtml*文件中。 将`<head>` * \_Layout.cshtml*文件的元素替换为以下代码：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

前两个 jQuery 脚本由 Microsoft Ajax 内容交付网络 （CDN） 托管。 通过利用 Microsoft Ajax CDN，您可以显著提高应用程序的第一热性能。

运行应用程序并单击编辑链接。 在浏览器中查看页面的源。 浏览器源显示窗体`data-val`的许多属性（用于数据验证）。 启用客户端验证和不显眼的 JavaScript 时，具有客户端验证规则的输入字段包含该`data-val="true"`属性以触发不显眼的客户端验证。 例如，模型中的`City`字段用["必需"](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性进行修饰，这将导致以下示例中显示的 HTML：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

对于每个客户端验证规则，将添加具有窗体`data-val-rulename="message"`的属性。 使用前面`City`显示的字段示例，所需的客户端验证规则将生成`data-val-required`该属性，并且消息&quot;"城市"字段是必需的。&quot; 运行应用程序，编辑其中一个用户，并清除该`City`字段。 当您选项卡出字段时，您将看到客户端验证错误消息。

![城市需要](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同样，对于客户端验证规则中的每个参数，将添加具有窗体`data-val-rulename-paramname=paramvalue`的属性。 例如，`FirstName`使用[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性对属性进行批号，并指定最小长度为 3 和最大长度为 8。 命名的`length`数据验证规则具有参数名称`max`和参数值 8。 下面显示了在编辑其中一个用户时为`FirstName`字段生成的 HTML：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

有关不显眼的客户端验证的详细信息，请参阅 brad Wilson 博客[中ASP.NET MVC 3 中的"不显眼客户端验证](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)"条目。

> [!NOTE]
> 在ASP.NET MVC 3 测试版中，有时需要提交表单才能启动客户端验证。 对于最终版本，可能会更改此情况。

## <a name="creating-the-create-view"></a>创建视图

下一步是添加操作`Create`方法和视图，以便使用户能够创建新用户。 将以下`Create`方法添加到主控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

添加视图与前面的步骤一样，但将 **"视图内容"** 设置为 **"创建**"。

![创建视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

运行应用程序，选择 **"创建**"链接，然后添加新用户。 该方法`Create`会自动利用客户端和服务器端验证。 尝试输入包含空白的用户名，如&quot;Ben X&quot;。 当您从用户名字段中选项卡外时，将显示客户端验证错误 （`White space is not allowed`） 。

## <a name="add-the-delete-method"></a>添加删除方法

要完成本教程，请向主控制器`Delete`添加以下方法：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

添加`Delete`视图，如前面的步骤，**将"查看内容"** 设置为 **"删除**"。

![删除视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

现在，您拥有一个简单但功能齐全ASP.NET MVC 3 应用程序，并具有验证功能。

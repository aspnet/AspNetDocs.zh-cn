---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 创建自定义 AJAX 控制工具包控制扩展器 （C#） |微软文档
author: rick-anderson
description: 自定义扩展程序使您能够自定义和扩展ASP.NET控件的功能，而无需创建新类。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543023"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>创建自定义 AJAX 控件工具包控件扩展程序 (C#)

由[微软](https://github.com/microsoft)

> 自定义扩展程序使您能够自定义和扩展ASP.NET控件的功能，而无需创建新类。

在本教程中，您将了解如何创建自定义 AJAX 控件工具包控件扩展器。 我们创建一个简单但有用的新扩展器，当您在 TextBox 中键入文本时，将按钮的状态从禁用更改为启用。 阅读本教程后，您将能够使用自己的控件扩展器扩展ASP.NET AJAX 工具包。

您可以使用可视化工作室或可视化 Web 开发人员创建自定义控件扩展器（请确保您具有最新版本的可视化 Web 开发人员）。

## <a name="overview-of-the-disabledbutton-extender"></a>禁用按钮扩展器概述

我们的新控制扩展器被命名为禁用按钮扩展器。 此扩展器将有三个属性：

- 目标控制ID - 控件扩展的文本框。
- 目标ButtonIID - 已禁用或启用的按钮。
- 禁用文本 - 最初显示在按钮中的文本。 开始键入时，按钮将显示按钮文本属性的值。

将"禁用按钮扩展器"挂到文本框和按钮控件。 键入任何文本之前，将禁用"按钮"，文本框和按钮如下所示：

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)）

开始键入文本后，将启用"按钮"，文本框和按钮如下所示：

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)）

要创建我们的控件扩展器，我们需要创建以下三个文件：

- DisabledButtonExtender.cs - 此文件是服务器端控制类，用于管理创建扩展器，并允许您在设计时设置属性。 它还定义可以在扩展器上设置的属性。 这些属性可通过代码和设计时间访问，并匹配在禁用ButtonBehavior.js文件中定义的属性。
- 禁用ButtonBehavior.js -- 此文件是您将添加所有客户端脚本逻辑的位置。
- DisabledButtonDesigner.cs - 此类启用设计时功能。 如果希望控件扩展器与可视化工作室/可视化 Web 开发人员设计器正确工作，则需要此类。

因此，控件扩展器由服务器端控件、客户端行为和服务器端设计器类组成。 您将在以下部分了解如何创建所有三个这些文件。

## <a name="creating-the-custom-extender-website-and-project"></a>创建自定义扩展器网站和项目

第一步是在可视化工作室/可视化 Web 开发人员中创建类库项目和网站。 我们将在类库项目中创建自定义扩展器，并在网站中测试自定义扩展器。

让我们从网站开始。 按照以下步骤创建网站：

1. 选择菜单选项 **"文件，新建网站**"。
2. 选择**ASP.NET网站**模板。
3. 命名新的*网站网站1。*
4. 单击“确定”**** 按钮。

接下来，我们需要创建包含控件扩展器代码的类库项目：

1. 选择菜单选项 **"文件、添加、新项目**"。
2. 选择**类库**模板。
3. 使用名称 **"自定义扩展器**"为新类库命名。
4. 单击“确定”**** 按钮。

完成这些步骤后，解决方案资源管理器窗口应类似于图 1。

[![网站和类库项目的解决方案](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**图01：** 包含网站和类库项目的解决方案（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)）

接下来，您需要向类库项目添加所有必要的程序集引用：

1. 右键单击"自定义扩展器"项目并选择菜单选项 **"添加参考**"。
2. 选择 .NET 选项卡。
3. 添加对下列程序集的引用：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. 系统.Web.扩展.设计.dll
4. 选择“浏览”按钮。
5. 添加对 AjaxControlToolkit.dll 程序集的引用。 此程序集位于下载 AJAX 控制工具包的文件夹中。

完成这些步骤后，类库项目参考文件夹应类似于图 2。

[![具有所需引用的引用文件夹](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**图 02**：引用具有所需引用的文件夹（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)）

## <a name="creating-the-custom-control-extender"></a>创建自定义控件扩展器

现在，我们已经有了类库，我们可以开始构建扩展器控件。 让我们从自定义扩展器控件类的裸骨开始（参见清单 1）。

**清单 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

关于清单1中的控件扩展器类，您注意到几件事。 首先，请注意，类从基扩展器控制库类继承。 所有 AJAX 控制工具包扩展器控件都源自此基类。 例如，基类包括作为每个控件扩展器的必需属性的 TargetID 属性。

接下来，请注意，该类包含以下与客户端脚本相关的两个属性：

- Web 资源 - 使文件作为嵌入资源包含在程序集中。
- 客户端脚本资源 - 导致从程序集检索脚本资源。

WebResource 属性用于在编译自定义扩展器时将 MyControlBehavior.js JavaScript 文件嵌入到程序集中。 当在网页中使用自定义扩展器时，客户端脚本资源属性用于从程序集中检索 MyControlBehavior.js 脚本。

为了使 Web 资源和客户端脚本资源属性正常工作，必须将 JavaScript 文件编译为嵌入式资源。 在解决方案资源管理器窗口中选择文件，打开属性表，并将值 *"嵌入资源"* 分配给 **"生成操作"** 属性。

请注意，控件扩展器还包括一个 TargetControlType 属性。 此属性用于指定由控件扩展器扩展的控件类型。 在清单 1 中，控件扩展器用于扩展 TextBox。

最后，请注意，自定义扩展器包含名为 MyProperty 的属性。 属性使用扩展器控制属性属性进行标记。 GetPropertyValue（） 和 SetPropertyValue（） 方法用于将属性值从服务器端控件扩展器传递到客户端行为。

让我们继续实现我们的禁用按钮扩展器的代码。 此扩展器的代码可在清单 2 中找到。

**清单2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

清单2中的"禁用按钮扩展器"具有两个属性，分别命名为 TargetButtonID 和"禁用文本"。 应用于 TargetButtonID 属性的 IDReference 属性可防止您将 Button 控件 ID 以外的任何内容分配给此属性。

WebResource 和 ClientScriptResource 属性将位于名为"禁用ButtonBehavior.js"的文件中的客户端行为与此扩展器相关联。 我们将在下一节中讨论此 JavaScript 文件。

## <a name="creating-the-custom-extender-behavior"></a>创建自定义扩展程序行为

控件扩展器的客户端组件称为行为。 禁用和启用按钮的实际逻辑包含在"禁用按钮"行为中。 该行为的 JavaScript 代码包含在清单 3 中。

**清单 3 - 禁用Button.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

清单3中的 JavaScript 文件包含名为"禁用Button行为"的客户端类。 此类，与其服务器端孪生一样，包括名为 TargetButtonID 和禁用文本的两个属性，您可以使用\_GetTargetButtonID/设置\_TargetButtonID 进行访问，并获得\_禁用文本/集\_禁用文本。

初始化（） 方法将键up事件处理程序与行为的目标元素关联。 每次在与此行为关联的 TextBox 中键入字母时，键 up 处理程序都会执行。 键up 处理程序启用或禁用按钮，具体取决于与该行为关联的 TextBox 是否包含任何文本。

请记住，您必须将清单 3 中的 JavaScript 文件编译为嵌入式资源。 在解决方案资源管理器窗口中选择文件，打开属性表，并将值 *"嵌入资源"* 分配给**生成操作**属性（参见图 3）。 此选项在可视化工作室和可视化 Web 开发人员中都可用。

[![将 JavaScript 文件添加为嵌入式资源](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**图 03**： 将 JavaScript 文件添加为嵌入式资源（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)）

## <a name="creating-the-custom-extender-designer"></a>创建自定义扩展程序设计器

我们需要创建最后一个类来完成扩展器。 我们需要在清单4中创建设计器类。 此类是使扩展器在可视化工作室/可视化 Web 开发人员设计器中正确运行所必需的。

**清单4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

将清单 4 中的设计器与"已禁用Button 扩展器"与"设计器"属性相关联。您需要将 Designer 属性应用于禁用Button扩展器类，如下所示：

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>使用自定义扩展器

现在，我们已经完成了创建禁用按钮控件扩展器，是时候在我们的ASP.NET网站使用它了。 首先，我们需要将自定义扩展器添加到工具箱中。 执行以下步骤:

1. 通过双击解决方案资源管理器窗口中的页面打开ASP.NET页。
2. 右键单击工具箱并选择菜单选项 **"选择项目**"。
3. 在"选择工具箱项目"对话框中，浏览到"自定义扩展器.dll"程序集。
4. 单击"**确定"** 按钮关闭对话框。

完成这些步骤后，禁用 Button 控件扩展器应显示在工具箱中（参见图 4）。

[![工具箱中的禁用按钮](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**图 04**： 工具箱中的禁用按钮（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)）

接下来，我们需要创建一个新的ASP.NET页。 执行以下步骤:

1. 创建新ASP.NET页面名为"显示禁用按钮.aspx"。
2. 将脚本管理器拖到页面上。
3. 将文本框控件拖到页面上。
4. 将"按钮"控件拖到页面上。
5. 在"属性"窗口中，将按钮 ID 属性更改为值<em>btnSave，</em>将文本属性更改为*值\*"保存*"。

我们创建了一个包含标准ASP.NET文本框和按钮控件的页面。

接下来，我们需要使用禁用按钮扩展器扩展 TextBox 控件：

1. 选择 **"添加扩展器**"任务选项以打开扩展程序向导对话框（参见图 5）。 请注意，该对话框包括我们的自定义禁用按钮扩展器。
2. 选择"禁用按钮扩展器"，然后单击 **"确定**"按钮。

[![扩展器向导对话框](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**图 05**： 扩展器向导对话框（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)）

最后，我们可以设置禁用按钮扩展器的属性。 您可以通过修改 TextBox 控件的属性来修改禁用Button扩展器的属性：

1. 选择设计器中的文本框。
2. 在"属性"窗口中，展开扩展器节点（参见图 6）。
3. 将"*保存到*禁用文本"属性的值和值*btnSave*分配给 TargetButtonID 属性。

[![设置扩展器属性](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**图 06**：设置扩展器属性（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)）

当您运行页面（通过点击 F5）时，按钮控件最初被禁用。 一旦您开始将文本输入到 TextBox 中，按钮控件即启用（参见图 7）。

[![禁用按钮扩展器正在操作中](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**图 07**： 禁用按钮扩展器在操作中（[单击以查看全尺寸图像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)）

## <a name="summary"></a>总结

本教程的目的是说明如何使用自定义扩展器控件扩展 AJAX 控件工具包。 在本教程中，我们创建了一个简单的禁用按钮控件扩展器。 我们通过创建禁用Button扩展器类、禁用Button行为 JavaScript 行为和禁用ButtonDesigner类实现了此扩展程序。 每当创建自定义控件扩展器时，都会遵循一组类似的步骤。

> [!div class="step-by-step"]
> [上一页](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [下一页](get-started-with-the-ajax-control-toolkit-vb.md)

---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 实体框架基架和迁移 |Microsoft Docs
author: rick-anderson
description: 如果你熟悉 ASP.NET MVC 4 控制器方法，或者已完成 &quot; 帮助程序、窗体和验证 &quot; Hands-On lab，你应该知道 .。。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 58aafe862f56ab13bf5a6bf8908a3baf582a08ff
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105268"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework 基架和迁移

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

如果你熟悉 ASP.NET MVC 4 控制器方法，或者已完成了 &quot; 帮助程序、窗体和验证 &quot; Hands-On 实验室，你应该注意到，许多用于创建、更新、列出和删除任何数据实体的逻辑都在整个应用程序中重复。 请不要说，如果您的模型有多个要操作的类，您可能会花费相当长的时间来编写 POST，并为每个实体操作以及每个视图获取操作方法。

在此实验室中，您将学习如何使用 ASP.NET MVC 4 基架自动生成应用程序 CRUD 的基线 (创建、读取、更新和删除) 。 从一个简单的模型类开始，而无需编写一行代码，你将创建一个包含所有 CRUD 操作的控制器以及所有必要的视图。 生成并运行简单解决方案后，将生成应用程序数据库以及用于数据操作的 MVC 逻辑和视图。

此外，你将了解在整个应用程序中使用实体框架迁移执行模型更新的难易程度如何。 实体框架迁移，你可以在模型发生了简单的步骤之后修改数据库。 为此，你将能够更有效地构建和维护 web 应用程序，利用 ASP.NET MVC 4 的最新功能。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从 [Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。 [ASP.NET MVC 4 实体框架基架和迁移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)中提供了此实验室特定的项目。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本 Hands-On 实验室中，您将学习如何：

- 将 ASP.NET 基架用于控制器中的 CRUD 操作。
- 使用实体框架迁移更改数据库模型。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>必备知识

你必须具有以下项才能完成此实验室：

- 适用于 Web 或高级 ([的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)阅读[附录 A](#AppendixA) ，以获取有关如何) 安装它的说明。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>设置

**安装代码片段**

为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。 若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi** 文件。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录 &quot; [B：使用代码片段](#AppendixB) &quot; 。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

以下练习将 Hands-On 实验室：

1. [将 ASP.NET MVC 4 基架用于实体框架迁移](#Exercise1)

> [!NOTE]
> 此练习附带了一个 **结束** 文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **30 分钟**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>练习1：将 ASP.NET MVC 4 基架用于实体框架迁移

ASP.NET MVC 基架提供一种以标准化方式生成 CRUD 操作的快速方法，从而创建必要的逻辑来使应用程序与数据库层交互。

在此练习中，您将学习如何将 ASP.NET MVC 4 基架与 code first 一起使用以创建 CRUD 方法。 然后，你将学习如何使用实体框架迁移来更新数据库中应用更改的模型。

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>任务 1-使用基架创建新的 ASP.NET MVC 4 项目

1. 如果尚未打开，请启动 **Visual Studio 2012**。
2. 选择 **文件 |新项目**。 在 "新建项目" 对话框的 " **Visual c #" 下，|Web** 部分，选择 " **ASP.NET MVC 4 Web 应用程序**"。 将项目命名为 " **MVC4andEFMigrations** "，并将 "位置" 设置为 " **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** "。 将 **解决方案名称** 设置为 " **开始** "，并确保选中 " **创建解决方案的目录** "。 单击“确定”。

    !["新建 ASP.NET MVC 4 项目" 对话框](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png ""新建 ASP.NET MVC 4 项目" 对话框")

    *"新建 ASP.NET MVC 4 项目" 对话框*
3. 在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **Internet 应用程序** " 模板，并确保 **Razor** 为所选的 **视图引擎**。 单击“确定”以创建该项目  。

    ![New ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet 应用程序")

    *New ASP.NET MVC 4 Internet 应用程序*
4. 在解决方案资源管理器中，右键单击 " **模型** "，然后选择 " **添加 |** 用于创建 (POCO) 的简单类人员的类。 将其命名为 **Person** 并单击 **"确定"**。
5. 打开 Person 类并插入以下属性。

     (代码片段- *ASP.NET MVC 4 和实体框架 Ex1 Person Properties*) 

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. 单击 " **生成" |生成解决方案** 以保存更改并生成项目。

    ![构建应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "生成应用程序")

    *生成应用程序*
7. 在解决方案资源管理器中，右键单击 "控制器" 文件夹，然后选择 " **添加 |控制器**。
8. 将控制器命名为 " *PersonController* "，并完成具有以下值的 " **基架" 选项** 。

   1. 在 " **模板** " 下拉列表中，选择 **包含读/写操作和视图的 MVC 控制器，并使用实体框架** 选项。
   2. 在 " **模型类** " 下拉列表中，选择 **Person** 类。
   3. 在 "**数据上下文类**" 列表中，选择 " **&lt; 新建数据上下文 &gt; ...**"。 选择任意名称并单击 **"确定"**。
   4. 在 " **视图** " 下拉列表中，确保选择 " **Razor** "。

      ![添加具有基架的人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "添加具有基架的人员控制器")

      *添加具有基架的人员控制器*
9. 单击 " **添加** " 以创建具有基架的人员的新控制器。 你现在已经生成控制器操作以及视图。

    ![创建具有基架的人员控制器之后](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "创建具有基架的人员控制器之后")

    *创建具有基架的人员控制器之后*
10. 打开 **PersonController** 类。 请注意，已自动生成完整的 CRUD 操作方法。

   ![在人员控制器中](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "在人员控制器中")

   *在人员控制器中*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>任务 2-运行应用程序

此时，数据库尚未创建。 在此任务中，您将首次运行应用程序并测试 CRUD 操作。 将随 Code First 动态创建数据库。

1. 按 **F5** 运行该应用程序。
2. 在浏览器中，将 **/Person** 添加到 URL 以打开 Person 页面。

    ![应用程序首次运行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "应用程序首次运行")

    *应用程序：首次运行*
3. 现在，你将浏览人员页面并测试 CRUD 操作。

    1. 单击 " **新建** " 以添加新人员。 输入名字和姓氏，然后单击 " **创建**"。

        ![添加新人员](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "添加新人员")

        *添加新人员*
    2. 在用户的列表中，可以删除、编辑或添加项。

        ![人员列表](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人员列表")

        *人员列表*
    3. 单击 " **详细信息** " 打开人员的详细信息。

        ![人员的详细信息](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人员的详细信息")

        *人员的详细信息*
4. 关闭浏览器并返回到 Visual Studio。 请注意，在整个应用程序中为 person 实体创建了整个 CRUD-从模型到视图-无需编写一行代码！

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>任务 3-使用实体框架迁移更新数据库

在此任务中，您将使用实体框架迁移来更新数据库。 通过使用实体框架迁移功能，您将发现更改模型并反映数据库中的更改是多么简单。

1. 打开包管理器控制台。 选择“工具” > “NuGet 包管理器” > “包管理器控制台”。
2. 在“包管理器控制台”中，输入以下命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![启用迁移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "启用迁移")

    *启用迁移*

    Enable-Migration 命令创建 **迁移** 文件夹，其中包含用于初始化数据库的脚本。

    ![迁移文件夹](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "迁移文件夹")

    *迁移文件夹*
3. 打开 "迁移" 文件夹中的 **Configuration.cs** 文件。 找到类构造函数并将 **AutomaticMigrationsEnabled** 值更改为 *true*。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. 打开 Person 类并为人员的中间名添加一个属性。 通过此新属性，您将更改模型。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. 选择 **生成 |** 用于生成应用程序的菜单上的 "生成解决方案"。

    ![构建应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "生成应用程序")

    *构建应用程序*
6. 在“包管理器控制台”中，输入以下命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    此命令会在数据对象中查找更改，然后将添加必要的命令来相应地修改数据库。

    ![添加中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "添加中间名")

    *添加中间名*
7.  (可选) 可以运行以下命令，以使用差异更新生成 SQL 脚本。 这将允许您手动更新数据库 (在这种情况下，不需要) 或应用其他数据库中的更改：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![生成 SQL 脚本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "生成 SQL 脚本")

    *生成 SQL 脚本*

    ![SQL 脚本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 脚本更新")

    *SQL 脚本更新*
8. 在 "程序包管理器控制台" 中，输入以下命令以更新数据库：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![更新数据库](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新数据库")

    *更新数据库*

    这 **将在 Person 表中** 添加 **MiddleName** 列以与 **Person** 类的当前定义匹配。
9. 更新数据库后，右键单击 "控制器" 文件夹，然后选择 " **添加 |** 如果) ，控制器将再次添加人员控制器 (完成。 这将更新添加新属性的现有方法和视图。

    ![添加控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "添加控制器更新")

    *更新控制器*
10. 单击“添加” 。 然后，选择 " **覆盖 PersonController.cs** 的值" 和 " **覆盖关联的视图** "，然后单击 **"确定"**。

   ![添加控制器覆盖](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *更新控制器*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-运行应用程序

1. 按 **F5** 运行该应用程序。
2. 打开 **/Person**。 请注意，数据已保留，而中间名称列已添加。

    ![添加的中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "添加的中间名")

    *添加的中间名*
3. 如果单击 " **编辑**"，则可以将中间名添加到当前用户。

    ![中间名版本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中间名版本")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

在本 Hands-On 实验室中，你已学习了使用任何模型类通过 ASP.NET MVC 4 基架创建 CRUD 操作的简单步骤。 然后，你已了解如何通过使用实体框架迁移，在应用程序中执行端到端更新（从数据库到视图）。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

你可以使用 Microsoft Web 平台安装程序安装 **Web Microsoft Visual Studio Express 2012** 或其他 &quot; Express &quot; 版本。 **[](https://www.microsoft.com/web/downloads/platform.aspx)** 以下说明将指导你完成使用 *Microsoft Web 平台安装程序* 安装 *Visual studio Express 2012 for Web* 的步骤。

1. 转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并 &quot; <em>使用 WINDOWS Azure SDK 搜索产品 Visual Studio Express 2012 for Web</em> &quot; 。
2. 单击 " **立即安装**"。 如果你没有 **Web 平台安装程序** ，则会重定向到 "下载并安装"。
3. **Web 平台安装程序** 打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 " **我接受** " 以继续。

    ![接受许可条款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *安装进度*
6. 安装完成后，单击 " **完成**"。

    ![安装完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *安装完成*
7. 单击 " **退出** " 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，单击 "开始撰写 &quot; **VS Express** &quot; "，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 B：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘 (c # 仅) _ 添加代码片段**

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称 (没有空格或连字符) 。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段 (或保留键入内容，直到选择了整个代码段的名称) 。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "开始键入代码片段名称")

_Start 键入代码片段名称 *

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***若要使用鼠标 (c # 添加代码片段，请 Visual Basic 和 XML)** _ 1。 右键单击要插入代码片段的位置。

1. 依次选择 ""、"*插入代码段* **" 和 "我的代码片段"**。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*

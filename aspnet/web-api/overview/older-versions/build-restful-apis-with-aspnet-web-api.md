---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 通过 ASP.NET Web API-ASP.NET 4.x 生成 RESTful Api
author: rick-anderson
description: 动手实验：使用 ASP.NET 4.x 中的 Web API 生成联系人管理器应用程序的简单 REST API。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 72ce313c380547f74d5dc17d1aefbf7cf2da4bea
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105281"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>通过 ASP.NET Web API 生成 RESTful Api

由[Web 训练营团队](https://twitter.com/webcamps)使用

> 动手实验：使用 ASP.NET 4.x 中的 Web API 生成联系人管理器应用程序的简单 REST API。 你还将生成一个使用 API 的客户端。

在最近几年中，它已变得清楚： HTTP 并非仅用于提供 HTML 页面。 它也是一个功能强大的平台，用于生成 Web Api，使用几个谓词 (GET、POST 等) 加上一些简单的概念，如 *uri* 和 *标头*。 ASP.NET Web API 是一组可简化 HTTP 编程的组件。 由于它是在 ASP.NET MVC 运行时的基础上构建的，因此 Web API 会自动处理 HTTP 的低级传输细节。 同时，Web API 自然公开 HTTP 编程模型。 事实上，Web API 的一个目标是 *不* 会抽象出 HTTP 的现实。 因此，Web API 既灵活又易于扩展。  已证明 REST 体系结构样式是利用 HTTP 的有效方法，但它当然不是 HTTP 的唯一有效方法。 联系人管理器将公开 RESTful 以列出、添加和删除联系人，等等。 

此实验室需要基本了解 HTTP、REST，并假定你具有 HTML、JavaScript 和 jQuery 的基本工作知识。
> 
> > [!NOTE]
> > ASP.NET 网站有一个专用于 ASP.NET Web API 框架的区域 [https://asp.net/web-api](https://asp.net/web-api) 。 此站点将继续提供与 Web API 相关的最新信息、示例和新闻，因此，如果想要深入了解如何创建可用于几乎任何设备或开发框架的自定义 Web Api，请经常查看。
> > 
> > 与 ASP.NET MVC 4 类似，ASP.NET Web API，在将服务层与控制器分离时具有很大的灵活性，使您可以很轻松地使用几个可用的依赖项注入框架。 
> 
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从获取 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409) 。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 实现 RESTful Web API
- 从 HTML 客户端调用 API

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>必备知识

完成本动手实验需要以下各项：

- 适用于 Web 或高级 ([的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)阅读[附录 B](#AppendixB) ，了解有关如何) 安装它的说明。

<a id="Setup"></a>
### <a name="setup"></a>设置

**安装代码片段**

为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。 若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi** 文件。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录 &quot; [A：使用代码片段](#AppendixA) &quot; 。

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [练习1：创建 Read-Only Web API](#Exercise1)
2. [练习2：创建读/写 Web API](#Exercise2)
3. [练习3：使用 HTML 客户端中的 Web API](#Exercise3)

> [!NOTE]
> 每个练习都带有一个 **结束** 文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>练习1：创建 Read-Only Web API

在此练习中，您将实现联系人管理器的只读 GET 方法。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>任务 1-创建 API 项目

在此任务中，你将使用新的 ASP.NET web 项目模板创建 Web API web 应用程序。

1. 运行 **Visual Studio 2012 Express For Web**，若要执行此操作，请单击 " **开始** "，然后键入 **VS Express for Web** 然后按 **enter**。
2. 从 " **文件** " 菜单中选择 " **新建项目**"。 选择 **Visual c # |** "项目类型" 树视图中的 "web 项目类型"，然后选择 " **ASP.NET MVC 4 Web 应用程序** " 项目类型。 将项目的 **名称** 设置为 *ContactManager* ，将 **解决方案名称** 设置为 " *开始*"，然后单击 **"确定"**。

    ![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")

    *创建新的 ASP.NET MVC 4.0 Web 应用程序项目*
3. 在 "ASP.NET MVC 4 项目类型" 对话框中，选择 " **WEB API** " 项目类型。 单击“确定”。

    ![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")

    *指定 Web API 项目类型*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>任务 2-创建联系人管理器 API 控制器

在此任务中，将创建 API 方法将驻留的控制器类。

1. 从项目中删除 "**控制器**" 文件夹中名为 " **ValuesController.cs** " 的文件。
2. 右键单击项目中的 " **控制器** " 文件夹，然后选择 " **添加 |** 上下文菜单中的 "控制器"。

    ![向项目添加新控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新控制器")

    *向项目添加新控制器*
3. 在出现的 " **添加控制器** " 对话框中，从 "模板" 菜单中选择 " **空 API 控制器** "。 将 controller 类命名为 **ContactController**。 然后单击 " **添加"。**

    ![使用 "添加控制器" 对话框创建新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 "添加控制器" 对话框创建新的 Web API 控制器")

    *使用 "添加控制器" 对话框创建新的 Web API 控制器*
4. 将以下代码添加到 **ContactController** 中。

     (代码片段- *WEB API Ex01-获取 API 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. 按 **F5** 调试应用程序。 Web API 项目的默认主页应该会出现。

    ![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")

    *ASP.NET Web API 应用程序的默认主页*
6. 在 Internet Explorer 窗口中，按 **F12** 键打开 " **开发人员工具** " 窗口。 单击 " **网络** " 选项卡，然后单击 " **开始捕获** " 按钮，开始将网络流量捕获到该窗口中。

    ![打开 "网络" 选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开 "网络" 选项卡并启动网络捕获")

    *打开 "网络" 选项卡并启动网络捕获*
7. 在浏览器的地址栏中追加 **/api/contact** ，并按 enter。 传输详细信息将出现在 "网络捕获" 窗口中。 请注意，响应的 MIME 类型为 **application/json**。 这说明了默认输出格式为 JSON。

    ![在 "网络" 视图中查看 Web API 请求的输出](build-restful-apis-with-aspnet-web-api/_static/image7.png "在 "网络" 视图中查看 Web API 请求的输出")

    *在 "网络" 视图中查看 Web API 请求的输出*

    > [!NOTE]
    > 此时，Internet Explorer 10 的默认行为将询问用户是否想要保存或打开由 Web API 调用导致的流。 输出将是一个文本文件，其中包含 Web API URL 调用的 JSON 结果。 不要取消对话框以便能够通过 "开发人员工具" 窗口监视响应的内容。
8. 单击 " **中转到详细视图** " 按钮，查看有关此 API 调用响应的详细信息。

    ![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")

    *切换到详细视图*
9. 单击 " **响应正文** " 选项卡以查看实际的 JSON 响应文本。

    ![查看网络监视器中的 JSON 输出文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看网络监视器中的 JSON 输出文本")

    *查看网络监视器中的 JSON 输出文本*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>任务 3-创建联系人模型并增强联系人控制器

在此任务中，将创建 API 方法将驻留的控制器类。

1. 右键单击 " **模型** " 文件夹，然后选择 " **添加 |类 ...** 从上下文菜单中。

    ![向 web 应用程序添加新模型](build-restful-apis-with-aspnet-web-api/_static/image10.png "向 web 应用程序添加新模型")

    *向 web 应用程序添加新模型*
2. 在 " **添加新项** " 对话框中，将新文件命名为 **Contact.cs** ，然后单击 " **添加"。**

    ![创建新的 Contact 类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的 Contact 类文件")

    *创建新的 Contact 类文件*
3. 将以下突出显示的代码添加到 **Contact** 类。

     (代码片段- *WEB API Ex01-Contact 类*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 在 **ContactController** 类中，选择 **Get** 方法的 "方法定义" 中的单词 **字符串**，然后键入 "*联系人*"。 键入单词后，就会在 word **联系人** 的开头显示一个指示器。 按下 **Ctrl** 键并按句点 (。 ) 键，或使用鼠标单击图标以打开代码编辑器中的 "协助" 对话框，以自动填充 "模型" 命名空间的 **using** 指令。

    ![使用 Intellisense 帮助命名空间声明](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *使用 Intellisense 帮助命名空间声明*
5. 修改 **Get** 方法的代码，使其返回联系人模型实例的数组。

     (代码片段- *WEB API Ex01-返回联系人列表*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. 按 **F5** 在浏览器中调试 web 应用程序。 若要查看对 API 的响应输出所做的更改，请执行以下步骤。

   1. 打开浏览器后，如果开发人员工具尚未打开，请按 **F12** 。
   2. 单击 " **网络** " 选项卡。
   3. 按 " **开始捕获** " 按钮。
   4. 将 URL 后缀 **/api/contact** 添加到地址栏中的 url，然后按 **enter** 键。
   5. 按 " **中转到详细视图** " 按钮。
   6. 选择 " **响应正文** " 选项卡。应该会看到一个 JSON 字符串，表示联系人实例的序列化形式。

      ![复杂的 Web API 方法调用的 JSON 序列化输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "复杂的 Web API 方法调用的 JSON 序列化输出")

      *复杂的 Web API 方法调用的 JSON 序列化输出*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>任务 4-将功能提取到服务层

此任务将演示如何将功能提取到服务层，使开发人员可以轻松地将其服务功能与控制器层分开，从而实现实际执行工作的服务的可重用性。

1. 在解决方案根文件夹中创建一个新文件夹并将其命名为 "it **服务**"。 为此，请右键单击 " **ContactManager** 项目"，选择 "**添加**  |  " "**新建文件夹**"，将其命名为 "*服务*"。

    ![正在创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "正在创建服务文件夹")

    *正在创建服务文件夹*
2. 右键单击 " **服务** " 文件夹，然后选择 " **添加 |类 ...** 从上下文菜单中。

    ![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")

    *将新类添加到服务文件夹*
3. 当 " **添加新项** " 对话框出现时，将新类命名为 **contacts.json** ，然后单击 " **添加**"。

    ![创建类文件以包含联系人存储库服务层的代码](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")

    *创建类文件以包含联系人存储库服务层的代码*
4. 向 **ContactRepository.cs** 文件添加 using 指令以包括模型命名空间。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 将以下突出显示的代码添加到 **ContactRepository.cs** 文件，以实现 GetAllContacts 方法。

     (代码片段- *WEB API Ex01-联系库*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. 打开 **ContactController.cs** 文件（如果尚未打开）。
7. 将以下 using 语句添加到文件的命名空间声明部分。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 将以下突出显示的代码添加到 **ContactController.cs** 类，以添加一个私有字段以表示存储库的实例，以便其他类成员可以使用服务实现。

     (代码片段- *WEB API Ex01-联系控制器*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 更改 **Get** 方法，使其能够使用联系人存储库服务。

     (代码片段- *WEB API Ex01-通过存储库返回联系人列表*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. 在 **ContactController** 的 **Get** 方法定义中放置一个断点。

   ![向联系人控制器添加断点](build-restful-apis-with-aspnet-web-api/_static/image17.png "向联系人控制器添加断点")

   *向联系人控制器添加断点*
11. 按 **F5** 运行该应用程序。
12. 当浏览器打开时，按 **F12** 打开开发人员工具。
13. 单击 " **网络** " 选项卡。
14. 单击 " **开始捕获** " 按钮。
15. 在地址栏中附加带有后缀 **/api/contact** 的 URL，然后按 **enter** 加载 api 控制器。
16. **Get** 方法开始执行时，Visual Studio 2012 应中断。

   ![在 Get 方法内中断](build-restful-apis-with-aspnet-web-api/_static/image18.png "在 Get 方法内中断")

   *在 Get 方法内中断*
17. 按 F5 以继续操作。
18. 返回到 Internet Explorer （如果它尚未处于焦点上）。 请注意 "网络捕获" 窗口。

    ![Internet Explorer 中显示 Web API 调用结果的网络视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "Internet Explorer 中显示 Web API 调用结果的网络视图")

    *Internet Explorer 中显示 Web API 调用结果的网络视图*
19. 单击 " **中转到详细视图** " 按钮。
20. 单击 " **响应正文** " 选项卡。请注意 API 调用的 JSON 输出，以及它如何表示服务层检索到的两个联系人。

    ![在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出")

    *在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>练习2：创建读/写 Web API

在此练习中，您将为联系人管理器实现 POST 和 PUT 方法，使其能够使用数据编辑功能。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>任务 1-打开 Web API 项目

在此任务中，你将准备好改进在练习1中创建的 Web API 项目，以便它可以接受用户输入。

1. 运行 **Visual Studio 2012 Express For Web**，若要执行此操作，请单击 " **开始** "，然后键入 **VS Express for Web** 然后按 **enter**。
2. 打开位于 **Source/Ex02-ReadWriteWebAPI/begin/** Folder 的 **begin** 解决方案。 否则，你可以继续使用通过完成前一练习所获得的 **最终** 解决方案。

   1. 如果你打开了提供的 **开始** 解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 " **项目** " 菜单并选择 " **管理 NuGet 包**"。
   2. 在 " **管理 NuGet 包** " 对话框中，单击 " **还原** " 以下载缺少的包。
   3. 最后，通过单击 "**生成**" "生成解决方案" 来生成解决方案  |  。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过指定 Packages.config 文件中的包版本，你将能够在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 打开 **Services/contacts.json** 文件。

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>任务 2-将 Data-Persistence 功能添加到联系人存储库实现

在此任务中，您将补充在练习1中创建的 Web API 项目的 Contacts.json 类，使其可以持久保存并接受用户输入和新的联系人实例。

1. 将以下常量添加到 **contacts.json** 类中，以表示在本练习后面的 web 服务器缓存项密钥名称。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 将构造函数添加到包含以下代码的 **contacts.json** 。

     (代码片段- *Ex02 联系存储库构造函数*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 修改 **GetAllContacts** 方法的代码，如下所示。

     (代码片段- *WEB API Ex02-获取所有联系人*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 此示例用于演示目的，并将 web 服务器的缓存用作存储介质，使多个客户端的值可以同时用于多个客户端，而不是使用会话存储机制或请求存储生存期。 可以使用实体框架、XML 存储或任何其他种类的 web 服务器缓存。
4. 为 **contacts.json** 类实现一个名为 **SaveContact** 的新方法，以便保存联系人。 **SaveContact** 方法应采用单个 **Contact** 参数，并返回指示成功或失败的布尔值。

     (代码片段- *WEB API Ex02-实现 SaveContact 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>练习3：使用 HTML 客户端中的 Web API

在此练习中，您将创建一个 HTML 客户端来调用 Web API。 此客户端将使用 JavaScript 简化与 Web API 的数据交换，并使用 HTML 标记在 web 浏览器中显示结果。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>任务 1-修改索引视图以提供用于显示联系人的 GUI

在此任务中，您将修改 web 应用程序的默认索引视图，以支持在 HTML 浏览器中显示现有联系人列表的要求。

1. 如果尚未打开，请打开 **Visual Studio 2012 Express For Web** 。
2. 打开位于 **Source/Ex03-ConsumingWebAPI/begin/** Folder 的 **begin** 解决方案。 否则，你可以继续使用通过完成前一练习所获得的 **最终** 解决方案。

   1. 如果你打开了提供的 **开始** 解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 " **项目** " 菜单并选择 " **管理 NuGet 包**"。
   2. 在 " **管理 NuGet 包** " 对话框中，单击 " **还原** " 以下载缺少的包。
   3. 最后，通过单击 "**生成**" "生成解决方案" 来生成解决方案  |  。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过指定 Packages.config 文件中的包版本，你将能够在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 打开位于 **Views/Home** 文件夹中的 **索引 cshtml** 文件。
4. 用 id **体** 替换 div 元素中的 HTML 代码，使其类似于以下代码。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 在文件底部添加以下 Javascript 代码，以对 Web API 执行 HTTP 请求。

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. 打开 **ContactController.cs** 文件（如果尚未打开）。
7. 在 **ContactController** 类的 **Get** 方法上放置一个断点。

    ![在 API 控制器的 Get 方法上放置断点](build-restful-apis-with-aspnet-web-api/_static/image21.png "在 API 控制器的 Get 方法上放置断点")

    *在 API 控制器的 Get 方法上放置断点*
8. 按 **F5** 运行项目。 浏览器将加载 HTML 文档。

    > [!NOTE]
    > 确保浏览到应用程序的根 URL。
9. 加载页面并执行 JavaScript 后，断点将被命中，代码执行将在控制器中暂停。

    ![使用 VS Express for Web 调试到 Web API 调用](build-restful-apis-with-aspnet-web-api/_static/image22.png "使用 VS Express for Web 调试到 Web API 调用")

    *使用 Visual Studio 2012 Express for Web 调试到 Web API 调用*
10. 删除断点，然后按 **F5** 或 "调试" 工具栏的 " **继续** " 按钮，继续在浏览器中加载视图。 Web API 调用完成后，会在浏览器中看到从 Web API 调用返回的、显示为列表项的联系人。

    ![在浏览器中显示为列表项的 API 调用结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "在浏览器中显示为列表项的 API 调用结果")

    *在浏览器中显示为列表项的 API 调用结果*
11. 停止调试。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>任务 2-修改索引视图以提供用于创建联系人的 GUI

在此任务中，您将继续修改 MVC 应用程序的索引视图。 将在 HTML 页中添加一个窗体，该页面将捕获用户输入并将其发送到 Web API 来创建新的联系人，并将创建新的 Web API 控制器方法以从 GUI 收集日期。

1. 打开 **ContactController.cs** 文件。
2. 将新方法添加到名为 **Post** 的控制器类，如下面的代码所示。

     (代码片段- *WEB API Ex03-Post 方法*) 

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 在 Visual Studio 中打开 **索引 cshtml** 文件（如果尚未打开）。
4. 将以下 HTML 代码添加到文件中，就在上一个任务中添加的未排序列表之后。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 在文档底部的脚本元素中，添加以下突出显示的代码以处理按钮单击事件，这会使用 HTTP POST 调用将数据发布到 Web API。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. 在 **ContactController.cs** 中，将一个断点置于 **Post** 方法上。
7. 按 **F5** 在浏览器中运行该应用程序。
8. 在浏览器中加载页面后，键入新的联系人名称和 Id，并单击 " **保存** " 按钮。

    ![在浏览器中加载的客户端 HTML 文档](build-restful-apis-with-aspnet-web-api/_static/image24.png "在浏览器中加载的客户端 HTML 文档")

    *在浏览器中加载的客户端 HTML 文档*
9. 调试器窗口在 **Post** 方法中中断时，查看 **contact** 参数的属性。 值应与您在窗体中输入的数据匹配。

    ![要从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "要从客户端发送到 Web API 的联系人对象")

    *要从客户端发送到 Web API 的联系人对象*
10. 在调试器中单步执行方法，直到创建了 **响应** 变量为止。 在调试器的 " **局部变量** " 窗口中进行检查后，您将看到已设置所有属性。

   ![在调试器中创建后的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "在调试器中创建后的响应")

   *在调试器中创建后的响应*
11. 如果按 **F5** 或单击调试器中的 " **继续** "，请求将会完成。 切换回浏览器后，会将新联系人添加到 **contacts.json** 实现存储的联系人列表中。

   ![浏览器反映新联系人实例的创建成功](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映新联系人实例的创建成功")

   *浏览器反映新联系人实例的创建成功*

> [!NOTE]
> 此外，你可以遵循 [附录 C：使用 Web 部署发布 ASP.NET MVC 4 应用程序](#AppendixC)，将此应用程序部署到 Azure。

---

<a id="Summary"></a>
## <a name="summary"></a>总结

此实验室已向你介绍了新的 ASP.NET Web API 框架，以及如何使用框架实现 RESTful Web Api。 从这里，你可以创建一个新的存储库，该存储库使用任意数量的机制和网络连接，而不是在此实验室中作为示例提供的简单数据。 Web API 支持多种附加功能，例如，从以支持 HTTP 和 JSON 或 XML 的任何语言编写的非 HTML 客户端进行通信。 还可以在典型的 web 应用程序之外承载 Web API，还可以创建自己的序列化格式。

ASP.NET 网站有一个专用于 ASP.NET Web API 框架的区域 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api) 。 此站点将继续提供与 Web API 相关的最新信息、示例和新闻，因此，如果想要深入了解如何创建可用于几乎任何设备或开发框架的自定义 Web Api，请经常查看。

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附录 A：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>使用键盘 (仅限 c # 添加代码片段) 

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称 (没有空格或连字符) 。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段 (或保留键入内容，直到选择了整个代码段的名称) 。
5. 按 Tab 键两次，将代码段插入到光标位置。

    ![开始键入代码片段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码片段名称")

    *开始键入代码片段名称*

    ![按 Tab 键以选择突出显示的代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 键以选择突出显示的代码段")

    *按 Tab 键以选择突出显示的代码段*

    ![再次按 Tab 键，代码片段将展开](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 键，代码片段将展开")

    *再次按 Tab 键，代码片段将展开*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>若要使用鼠标 (c # 中添加代码段，请 Visual Basic 和 XML) 

1. 右键单击要插入代码片段的位置。
2. 选择 " **插入** 代码片段"，然后选择 **"我的代码片段"**。
3. 通过单击从列表中选择相关的代码片段。

    ![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

    *右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

    ![通过单击从列表中选择相关的代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "通过单击从列表中选择相关的代码片段")

    *通过单击从列表中选择相关的代码片段*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附录 B：安装 Web Visual Studio Express 2012

你可以使用 Microsoft Web 平台安装程序安装 **Web Microsoft Visual Studio Express 2012** 或其他 &quot; Express &quot; 版本。 **[](https://www.microsoft.com/web/downloads/platform.aspx)** 以下说明将指导你完成使用 *Microsoft Web 平台安装程序* 安装 *Visual studio Express 2012 for Web* 的步骤。

1. 请参阅 [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169) 。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它，并 &quot; <em>使用 Azure SDK 搜索产品 Visual Studio Express 2012 for Web</em> &quot; 。
2. 单击 " **立即安装**"。 如果你没有 **Web 平台安装程序** ，则会重定向到 "下载并安装"。
3. **Web 平台安装程序** 打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 " **我接受** " 以继续。

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *安装进度*
6. 安装完成后，单击 " **完成**"。

    ![安装完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *安装完成*
7. 单击 " **退出** " 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，单击 "开始撰写 &quot; **VS Express** &quot; "，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web 磁贴*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 C：使用 Web 部署发布 ASP.NET MVC 4 应用程序

本附录将演示如何从 Azure 门户创建新网站，以及如何利用 Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>任务 1-从 Azure 门户创建新网站

1. 请使用 [Azure 管理门户](https://manage.windowsazure.com/) ，并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。 你可以在 [此处](https://aka.ms/aspnet-hol-azure)注册。

    ![登录到 Microsoft Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Microsoft Azure 门户")

    *登录到门户*
2. 单击命令栏上的 " **新建** "。

    ![创建新网站](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新网站")

    *创建新网站*
3. 单击 "**计算**  |  **网站"**。 然后选择 " **快速创建** " 选项。 为新网站提供可用 URL，并单击 " **创建** 网站"。

    > [!NOTE]
    > Azure 是在云中运行的 web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Azure。 它不包括设置数据库的步骤。

    ![使用“快速创建”创建新网站](build-restful-apis-with-aspnet-web-api/_static/image41.png "使用“快速创建”创建新网站")

    *使用“快速创建”创建新网站*
4. 请 **等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](build-restful-apis-with-aspnet-web-api/_static/image43.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 " **名称** " 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")

    *打开网站管理页*
7. 在 " **仪表板** " 页的 " **速览** " 部分下，单击 " **下载发布配置文件** " 链接。

    > [!NOTE]
    > *发布配置文件* 包含为每个已启用的发布方法将 web 应用程序发布到 Azure 所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web** 和 **Microsoft Visual Studio 2012** 支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 Azure。

    ![下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，你将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Azure。

    ![正在保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Azure 管理门户中的 **sql 数据库**  |  **服务器**  |  **的仪表板** 上查看订阅中的 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 " **添加** " 按钮创建一个服务器。 记下 **服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的 **允许 IP 地址** 列表中包含本地 ip 地址。 要执行此操作，请单击 " **配置**"，从 " **当前客户端 IP 地址** " 选择 ip 地址，并将其粘贴到 " **起始 Ip 地址** " 和 " **结束 ip 地址** " 文本框中，然后单击 " ![ 添加-客户端-IP 地址-确定" ](build-restful-apis-with-aspnet-web-api/_static/image48.png) 按钮。

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *添加客户端 IP 地址*
3. 将 **客户端 Ip 地址** 添加到 "允许的 IP 地址" 列表中后，单击 " **保存** " 以确认更改。

    ![确认更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *确认更改*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在 **解决方案资源管理器** 中，右键单击网站项目，然后选择 " **发布**"。

    ![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 " **验证连接**"。 验证完成后，单击 " **下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "正在验证连接")

    *正在验证连接*
4. 在 " **设置** " 页的 " **数据库** " 部分下，单击数据库连接的文本框旁边的按钮， (**DefaultConnection**) 。

    ![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 " **服务器名称** " 中，键入您的 SQL 数据库服务器 URL，使用 *tcp：* prefix。
   - 在 " **用户名** " 中键入服务器管理员登录名。
   - 在 " **密码** " 中键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![正在配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 。 系统提示创建数据库时，单击 **"是"**。

    ![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 然后单击“下一步”。

    ![指向 SQL 数据库的连接字符串](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 " **预览** " 页上，单击 " **发布**"。

    ![发布 web 应用程序](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

    ![发布到 Windows Azure 的应用程序](build-restful-apis-with-aspnet-web-api/_static/image59.png "发布到 Windows Azure 的应用程序")

    *已将应用程序发布到 Azure*

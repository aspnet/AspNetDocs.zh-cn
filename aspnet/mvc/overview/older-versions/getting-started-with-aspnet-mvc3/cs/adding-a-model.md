---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: 添加模型 (C#) |Microsoft Docs
author: Rick-Anderson
description: 注意:本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 8cf8693b71509163860c78a87370c4765414fd5d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130340"
---
# <a name="adding-a-model-c"></a>添加模型 (C#)

通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些：[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，请通过单击以下链接安装必备组件：[Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/adding-a-model.md)本教程。

## <a name="adding-a-model"></a>添加模型

在本部分中将添加用于管理数据库中的电影的一些类。 这些类将 ASP.NET MVC 应用程序的"模型"部分。

将使用名为实体框架的.NET Framework 数据访问技术来定义和使用这些模型的类。 实体框架 （通常称为 EF） 支持开发模式称为*Code First*。 代码首先允许你通过编写简单的类来创建模型对象。 （这些也称为是 POCO 类，从"纯旧式 CLR 对象"。）然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。

## <a name="adding-model-classes"></a>添加模型类

在中**解决方案资源管理器**，右键单击 *模型* 文件夹，选择**添加**，然后选择**类**。

![](adding-a-model/_static/image1.png)

名称*类*"电影"。

[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)

添加到以下五个属性`Movie`类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用`Movie`类来表示数据库中的电影。 每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。

在同一文件中，添加以下`MovieDBContext`类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。 `MovieDBContext`派生自`DbContext`实体框架提供的基类。 有关详细信息`DbContext`并`DbSet`，请参阅[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。

若要引用将`DbContext`并`DbSet`，你需要添加以下`using`在文件顶部的语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完整*Movie.cs*文件如下所示。

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>创建的连接字符串和使用 SQL Server Compact

`MovieDBContext`创建的类处理连接到数据库以及映射任务`Movie`数据库记录的对象。 您可能会问的一个问题，是如何指定将连接到的数据库。 您将通过添加中的连接信息来实现*Web.config*应用程序文件。

打开应用程序根目录*Web.config*文件。 (未*Web.config*中的文件*视图*文件夹。)下图显示两者*Web.config*文件; 打开*Web.config*用红线圈出文件。

![](adding-a-model/_static/image4.png)

添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下面的示例显示了一部分*Web.config*文件添加的新连接字符串：

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

这种少量的代码和 XML 是为了表示，并将影片数据存储在数据库中编写所需的一切。

接下来，你将生成一个新`MoviesController`类，该类可以用于显示电影数据并允许用户创建新的影片列表。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)

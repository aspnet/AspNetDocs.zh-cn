---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 通过模型绑定和 web 窗体检索和显示数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-.。。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240740"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>通过模型绑定和 web 窗体检索和显示数据

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 模型绑定模式适用于任何数据访问技术。 在本教程中，你将使用实体框架，但你可以使用你最熟悉的数据访问技术。 从数据绑定服务器控件（例如 GridView、ListView、DetailsView 或 FormView 控件），指定用于选择、更新、删除和创建数据的方法的名称。 在本教程中，您将为 SelectMethod 指定一个值。 
> 
> 在该方法中，将提供用于检索数据的逻辑。 在下一教程中，你将为 UpdateMethod、DeleteMethod 和 InsertMethod 设置值。
>
> 可以在 c # 或 Visual Basic 中[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 和更高版本。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2017 模板略有不同。
> 
> 在本教程中，你将在 Visual Studio 中运行应用程序。 你还可以将应用程序部署到托管提供程序，并使其在 internet 上可用。 Microsoft 为提供最多10个网站的免费 web 托管  
> [免费的 Azure 试用帐户](https://azure.microsoft.com/free/dotnet/)。 有关如何将 Visual Studio web 项目部署到 Azure App Service Web Apps 的信息，请参阅[使用 Visual studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)系列。 该教程还演示了如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Azure SQL 数据库。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> - Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017
>   
> 本教程还适用于 Visual Studio 2012 和 Visual Studio 2013，但用户界面和项目模板有一些不同之处。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，你将：

* 生成数据对象，这些对象反映了学生注册课程的大学
* 从对象生成数据库表
* 用测试数据填充数据库
* 在 web 窗体中显示数据

## <a name="create-the-project"></a>创建项目

1. 在 Visual Studio 2017 中，创建名为**ContosoUniversityModelBinding**的**ASP.NET Web 应用程序（.NET Framework）** 项目。

   ![创建项目](retrieving-data/_static/image19.png)

2. 选择“确定”。 此时将显示用于选择模板的对话框。

   ![选择 web 窗体](retrieving-data/_static/image3.png)

3. 选择 " **Web 窗体**" 模板。 

4. 如有必要，请将身份验证更改为**单独的用户帐户**。 

5. 选择“确定”以创建项目。

## <a name="modify-site-appearance"></a>修改站点外观

   进行一些更改，以自定义站点外观。 
   
   1. 打开站点 .Master 文件。
   
   2. 更改标题以显示**Contoso 大学**，而不是**我的 ASP.NET 应用程序**。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. 将标题文本从**应用程序名称**更改为**Contoso 大学**。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. 更改导航标题链接到站点相应的链接。 
   
      删除**关于**和**联系人**的链接，而不是链接到您将创建的**学生**页面。

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. 保存站点。

## <a name="add-a-web-form-to-display-student-data"></a>添加 web 窗体以显示学生数据

   1. 在**解决方案资源管理器**中，右键单击项目，选择 "**添加**"，然后选择 "**新建项**"。 
   
   2. 在 "**添加新项**" 对话框中，选择 "**带有母版页的 Web 窗体**" 模板，**并将其**命名为 "student"。

      ![创建页面](retrieving-data/_static/image5.png)

   3. 选择 **添加** 。
   
   4. 对于 web 窗体的母版页，选择 "**网站"。**
   
   5. 选择“确定”。

## <a name="add-the-data-model"></a>添加数据模型

在 "**模型**" 文件夹中，添加名为**UniversityModels.cs**的类。

   1. 右键单击 "**模型**"，依次选择 "**添加**"、"**新建项**"。 此时会显示“添加新项”对话框。****

   2. 从左侧导航菜单中，选择 "**代码**"，然后选择 "**类**"。

      ![创建模型类](retrieving-data/_static/image20.png)

   3. 将类命名为**UniversityModels.cs** ，然后选择 "**添加**"。

      在此文件中，定义 `SchoolContext` 、 `Student` 、 `Enrollment` 和 `Course` 类，如下所示：

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext`类派生自 `DbContext` ，它管理数据库连接和数据的更改。

      在 `Student` 类中，请注意应用于 `FirstName` 、 `LastName` 和属性的特性 `Year` 。 本教程将使用这些属性进行数据验证。 若要简化代码，只会将这些属性标记为数据验证特性。 在实际项目中，您将验证特性应用到需要验证的所有属性。

   4. 保存 UniversityModels.cs。

## <a name="set-up-the-database-based-on-classes"></a>基于类设置数据库

本教程使用[Code First 迁移](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)来创建对象和数据库表。 这些表存储有关学生及其课程的信息。

   1. 选择“工具” > “NuGet 包管理器” > “包管理器控制台”。

   2. 在 "**程序包管理器控制台**" 中运行以下命令：  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      如果该命令成功完成，则会出现一条消息，指出已启用了迁移。

      ![启用迁移](retrieving-data/_static/image8.png)

      请注意，已创建一个名为*Configuration.cs*的文件。 `Configuration`类具有 `Seed` 方法，该方法可使用测试数据预先填充数据库表。

## <a name="pre-populate-the-database"></a>预先填充数据库

   1. 打开 Configuration.cs。
   
   2. 将以下代码添加到 `Seed` 方法中。 此外， `using` 为命名空间添加语句 `ContosoUniversityModelBinding. Models` 。

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. 保存 Configuration.cs。

   4. 在 "包管理器控制台" 中，运行命令 "**添加迁移初始**"。

   5. 运行命令**更新-数据库**。

      如果在运行此命令时收到异常，则 `StudentID` 和 `CourseID` 值可能与 `Seed` 方法值不同。 打开这些数据库表并查找和的现有 `StudentID` 值 `CourseID` 。 将这些值添加到用于播种表的代码中 `Enrollments` 。

## <a name="add-a-gridview-control"></a>添加 GridView 控件

如果填充了数据库数据，则可以检索并显示数据。 

1. 打开 "student"。

2. 查找 `MainContent` 占位符。 在该占位符中，添加包含此代码的**GridView**控件。

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   注意事项：
   * 请注意，在 `SelectMethod` GridView 元素中为属性设置的值。 此值指定用于检索在下一步中创建的 GridView 数据的方法。 
   
   * `ItemType`属性设置为 `Student` 前面创建的类。 此设置允许你引用标记中的类属性。 例如， `Student` 类具有一个名为的集合 `Enrollments` 。 您可以使用 `Item.Enrollments` 检索该集合，然后使用[LINQ 语法](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)来检索每个学生注册的信用额度。
   
3. 保存学生 .aspx。

## <a name="add-code-to-retrieve-data"></a>添加代码以检索数据

   在 "student" 代码隐藏文件中，添加为该值指定的方法 `SelectMethod` 。 
   
   1. 打开 Students.aspx.cs。
   
   2. `using`为 `ContosoUniversityModelBinding. Models` 和 `System.Data.Entity` 命名空间添加语句。

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. 添加为指定的方法 `SelectMethod` ：

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include`子句可提高查询性能，但不是必需的。 如果没有 `Include` 子句，则使用[*延迟加载*](https://en.wikipedia.org/wiki/Lazy_loading)来检索数据，这涉及到每次检索相关数据时向数据库发送一个单独的查询。 使用 `Include` 子句时，将使用*预先加载*来检索数据，这意味着单个数据库查询将检索所有相关数据。 如果未使用相关数据，预先加载的效率会降低，因为检索到更多的数据。 但在这种情况下，预先加载可提供最佳性能，因为每个记录都显示了相关数据。

      有关加载相关数据时的性能注意事项的详细信息，请参阅[使用 ASP.NET MVC 应用程序中的实体框架读取相关数据](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)部分中的 "**延迟、预先和显式加载相关**数据" 部分。

      默认情况下，数据按标记为键的属性的值进行排序。 您可以添加 `OrderBy` 子句来指定其他排序值。 在此示例中，默认 `StudentID` 属性用于排序。 在[排序、分页和筛选数据](sorting-paging-and-filtering-data.md)一文中，用户可以选择要排序的列。
 
   4. 保存 Students.aspx.cs。

## <a name="run-your-application"></a>运行应用程序 

运行 web 应用程序（**F5**），并导航到 "**学生**" 页，其中显示了以下内容：

   ![显示数据](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>自动生成模型绑定方法

在学习本系列教程时，只需将代码从教程复制到项目即可。 但是，这种方法的一个缺点是，你可能不会意识到 Visual Studio 提供的功能自动为模型绑定方法生成代码。 在处理自己的项目时，自动代码生成可以节省时间，并帮助你了解如何实现操作。 本部分介绍自动代码生成功能。 本节仅提供信息，并且不包含你在项目中实现所需的任何代码。 

在 `SelectMethod` `UpdateMethod` 标记代码中为、、或属性设置值时 `InsertMethod` `DeleteMethod` ，可以选择 "**创建新方法**" 选项。

![创建方法](retrieving-data/_static/image18.png)

Visual Studio 不仅使用正确的签名在代码隐藏中创建方法，而且还会生成执行代码来执行该操作。 如果首先在 `ItemType` 使用自动代码生成功能之前设置属性，则生成的代码将使用该类型进行操作。 例如，在设置属性时 `UpdateMethod` ，将自动生成以下代码：

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

同样，不需要将此代码添加到您的项目中。 在下一教程中，你将实现用于更新、删除和添加新数据的方法。

## <a name="summary"></a>总结

本教程介绍了如何创建数据模型类，并从这些类生成了数据库。 用测试数据填充数据库表。 你使用了模型绑定从数据库检索数据，然后在 GridView 中显示数据。

在本系列的下一个[教程](updating-deleting-and-creating-data.md)中，你将启用更新、删除和创建数据。

> [!div class="step-by-step"]
> [下一页](updating-deleting-and-creating-data.md)

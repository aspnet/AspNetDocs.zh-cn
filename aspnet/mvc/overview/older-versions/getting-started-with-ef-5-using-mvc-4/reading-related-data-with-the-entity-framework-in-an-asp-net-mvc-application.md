---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架读取相关数据 (5/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 6a3a4978a718ba56446463373ad3525e8b6f0d4a
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984838"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>使用 ASP.NET MVC 应用程序中的实体框架读取相关数据 (第5个，共10个) 

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你已完成 School 数据模型。 在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。

下图是将会用到的页面。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>延迟、预先和显式加载相关数据

实体框架可以通过多种方式将相关数据加载到实体的导航属性中：

- *延迟加载*。 首次读取实体时，不检索相关数据。 然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。 这会导致向数据库发送多个查询，一个用于实体本身，每次必须检索到该实体的相关数据。 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *预先加载*。 读取该实体时，会同时检索相关数据。 此时通常会出现单一联接查询，检索所有必需数据。 使用方法指定预先加载 `Include` 。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *显式加载*。 这类似于延迟加载，只不过是在代码中显式检索相关数据;在访问导航属性时，不会自动发生此情况。 您可以通过获取实体的对象状态管理器项并为 `Collection.Load` 包含单个实体的属性调用集合或方法，手动加载相关数据 `Reference.Load` 。  (在以下示例中，如果要加载 "管理员" 导航属性，则应将替换 `Collection(x => x.Courses)` 为 `Reference(x => x.Administrator)` 。 ) 

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

因为它们不会立即检索属性值，所以延迟加载和显式加载也称为 *延迟加载*。

通常，如果您知道每个检索到的实体都需要相关数据，预先加载可提供最佳性能，因为发送到数据库的单个查询通常比检索的每个实体的单独查询更有效。 例如，在上面的示例中，假设每个部门都有十个相关的课程。 预先加载的示例只会导致单个 (联接) 查询，并单次往返到数据库。 延迟加载和显式加载示例会导致对数据库进行11次查询和十一次往返。 延迟较高时，额外往返数据库对性能尤为不利。

另一方面，在某些情况下，延迟加载更为有效。 预先加载可能会导致生成非常复杂的联接，这 SQL Server 无法有效地处理。 或者，如果需要只为正在处理的一组实体的子集访问实体的导航属性，则延迟加载可能会更好，因为预先加载将检索比你需要的更多的数据。 如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。

通常，仅当关闭延迟加载时才使用显式加载。 一种情况是，在序列化过程中应关闭延迟加载。 延迟加载和序列化不是很好，如果您不小心，在启用延迟加载的情况下，查询的数据可能比预期要大得多。 序列化通常通过访问类型实例上的每个属性来工作。 属性访问会触发延迟加载，并且会序列化这些延迟加载的实体。 然后，序列化过程访问延迟加载的实体的每个属性，这可能会导致更多的延迟加载和序列化。 若要防止此运行时链反应，请在序列化实体之前关闭延迟加载。

默认情况下，数据库上下文类执行延迟加载。 可以通过两种方式来禁用延迟加载：

- 对于特定的导航属性，请 `virtual` 在声明属性时省略关键字。
- 对于所有导航属性，将设置 `LazyLoadingEnabled` 为 `false` 。 例如，你可以将以下代码放在上下文类的构造函数中： 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

延迟加载可以屏蔽导致性能问题的代码。 例如，如果代码不指定预先加载或显式加载，但处理大量实体，并且在每次迭代中使用多个导航属性，则可能会非常低效 (，因为对数据库) 的多次往返。 使用本地 SQL server 进行开发良好的应用程序在迁移到 Azure SQL 数据库时可能会遇到性能问题，因为这会增加延迟和延迟加载。 使用真实的测试负载分析数据库查询将有助于确定是否适合延迟加载。 有关详细信息，请参阅 [揭密实体框架策略：加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx) 和 [使用实体框架将网络延迟减少到 SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx)。

## <a name="create-a-courses-index-page-that-displays-department-name"></a>创建显示部门名称的课程索引页

`Course`实体包括一个导航属性，该属性包含将 `Department` 课程分配到的部门的实体。 若要在课程列表中显示分配的部门的名称，需要 `Name` 从 `Department` 导航属性中的实体获取属性 `Course.Department` 。

`CourseController` `Course` 使用之前对控制器执行的相同选项，为实体类型创建一个名为的控制器 `Student` ，如下图所示 (除了映像以外，上下文类位于 DAL 命名空间中，而不是模型命名空间) ：

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

打开 *Controllers\CourseController.cs* 并查看 `Index` 方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。

打开 *Views\Course\Index.cshtml* ，并将现有代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

已对基架代码进行了如下更改：

- 将标题从 **索引** 更改为 **课程**。
- 将行链接向左移动。
- 在显示属性值的标题 **编号** 下添加了一列 `CourseID` 。 默认情况下 (，主键基架，因为它们对于最终用户没有意义。 但是，在这种情况下，主键是有意义的，并且您想要将其显示。 ) 
- 更改了 **DepartmentID** 的最后一个列标题， (外键的名称到 `Department`) 到 **部门** 的实体。

请注意，对于最后一列，基架代码显示 `Name` `Department` 加载到导航属性中的实体的属性 `Department` ：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

运行页面 (在 Contoso 大学主页上选择 " **课程** " 选项卡，) 查看具有部门名称的列表。

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>创建显示课程和注册的讲师索引页面

在本部分中，你将为实体创建一个控制器和视图，以便 `Instructor` 显示 "讲师索引" 页：

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

该页面通过以下方式读取和显示相关数据：

- 讲师列表显示实体中的相关数据 `OfficeAssignment` 。 `Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。 将对实体使用预先加载 `OfficeAssignment` 。 如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。 在这种情况下，你希望显示所有显示的讲师的办公室分配情况。
- 用户选择一名讲师时，显示相关 `Course` 实体。 `Instructor` 和 `Course` 实体之间存在多对多关系。 你将对 `Course` 实体及其相关实体使用预先加载 `Department` 。 在这种情况下，延迟加载可能更高效，因为你只需要为所选指导员提供课程。 但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。
- 当用户选择某一课程时，将显示该 `Enrollments` 实体集中的相关数据。 `Course` 和 `Enrollment` 实体之间存在一对多的关系。 你将添加 `Enrollment` 实体及其相关实体的显式加载 `Student` 。  (显式加载不是必需的，因为已启用延迟加载，但这会显示如何进行显式加载。 ) 

### <a name="create-a-view-model-for-the-instructor-index-view"></a>为讲师索引视图创建视图模型

"讲师索引" 页显示三个不同的表。 因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。

在 *viewmodel* 文件夹中，创建 *InstructorIndexData.cs* 并将现有代码替换为以下代码：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>添加所选行的样式

若要标记所选的行，需要不同的背景色。 若要为此 UI 提供样式，请将以下突出显示的代码添加 `/* info and errors */` 到 *Content\Site.css* 中的节，如下所示：

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>创建讲师控制器和视图

创建一个 `InstructorController` 控制器，如下图所示：

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

打开 *Controllers\InstructorController.cs* 并 `using` 为命名空间添加语句 `ViewModels` ：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

方法中的基架代码 `Index` 仅为导航属性指定预先加载 `OfficeAssignment` ：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

将方法替换为 `Index` 以下代码，以加载其他相关数据并将其放入视图模型：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

该方法接受可选的路由数据 (`id`) 和查询字符串参数 (`courseID`) 提供选定讲师和所选课程的 ID 值，并将所有所需数据传递给视图。 参数由页面上的“选择”超链接提供。

> [!TIP]
> 
> **路由数据**
> 
> 路由数据是模型绑定器在路由表中指定的 URL 段中找到的数据。 例如，默认路由指定 `controller` 、 `action` 和 `id` 段：
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> 在下面的 URL 中，默认路由映射 `Instructor` 为 `controller` ， `Index` 作为 `action` 和1作为， `id` 它们是路由数据值。
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "？ courseID = 2021" 是一个查询字符串值。 如果将 `id` 作为查询字符串值传递，则模型绑定器也起作用：
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> 这些 Url 是通过 `ActionLink` Razor 视图中的语句创建的。 在下面的代码中， `id` 参数与默认路由匹配，因此 `id` 添加到路由数据。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> 在下面的代码中，与 `courseID` 默认路由中的参数不匹配，因此将其添加为查询字符串。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

代码先创建一个视图模型实例，并在其中放入讲师列表。 此代码为 `Instructor.OfficeAssignment` 和导航属性指定预先加载 `Instructor.Courses` 。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

第二 `Include` 种方法将加载课程，对于加载的每个课程，它会预先加载 `Course.Department` 导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

如前所述，无需预先加载，但会执行此操作来提高性能。 由于视图始终需要 `OfficeAssignment` 实体，因此在同一查询中提取该实体会更有效。 `Course` 在网页中选择了指导员时，实体是必需的，因此，只有在选择了不使用的课程时，预先加载才能比延迟加载更好。

如果选择了指导员 ID，则会从视图模型中的指导员列表中检索所选的指导员。 然后，将 `Courses` `Course` 从该教师导航属性中的实体加载视图模型的属性 `Courses` 。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

`Where`方法返回集合，但在此示例中，传递给该方法的条件仅导致 `Instructor` 返回单个实体。 `Single`方法将集合转换为单个 `Instructor` 实体，这使你能够访问该实体的 `Courses` 属性。

当您知道集合将只有一个项时，对集合使用 [单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 方法。 `Single`如果传递给它的集合为空或有多个项，则该方法将引发异常。 替代项为 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合为空，它将返回默认值 (`null` 在这种情况下) 。 但是，在这种情况下，仍会导致异常 (尝试查找 `Courses` 引用) 上的属性 `null` ，并且异常消息不会明确指出问题的原因。 调用 `Single` 方法时，还可以传递 `Where` 条件，而不是 `Where` 单独调用方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

而不是：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。 然后，将 `Enrollments` `Enrollment` 从该课程的导航属性中的实体加载视图模型的属性 `Enrollments` 。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>修改讲师索引视图

在 *Views\Instructor\Index.cshtml* 中，将现有代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

已对现有代码进行了如下更改：

- 将模型类更改为了 `InstructorIndexData`。
- 将页标题从“索引”更改为了“讲师” 。
- 将行链接列向左移动。
- 删除了 **FullName** 列。
- 添加了仅当不为 null 时才显示的 **Office** 列 `item.OfficeAssignment.Location` `item.OfficeAssignment` 。  (因为这是一对零或一关系，因此可能没有相关的 `OfficeAssignment` 实体。 )  

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- 添加了将动态添加 `class="selectedrow"` 到选定讲师的元素中的代码 `tr` 。 这将使用之前创建的 CSS 类设置所选行的背景色。 在 `valign` 以下教程中，将多行列添加到表中时，属性 (将非常有用。 )  

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- `ActionLink`在每行中的其他链接之前添加了一个新的标签 **选择**，这将导致所选的指导员 ID 发送到 `Index` 方法。

运行应用程序并选择 " **讲师** " 选项卡。 `Location` 当没有相关实体时，此页将显示相关实体的属性 `OfficeAssignment` 和一个空的表单元 `OfficeAssignment` 。

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

在 *Views\Instructor\Index.cshtml* 文件中，在 `table`) 文件末尾 (结束元素之后，添加以下突出显示的代码。 选择指导员后，将显示与讲师相关的课程列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

此代码读取视图模型的 `Courses` 属性以显示课程列表。 它还提供了一个 `Select` 超链接，该超链接将所选课程的 ID 发送到 `Index` 操作方法。

> [!NOTE]
> *Css* 文件由浏览器进行缓存。 如果在运行应用程序时看不到所做的更改，请执行硬刷新 (按住 CTRL 键的同时单击 " **刷新** " 按钮，或按 Ctrl + F5) 。

运行页面并选择一个指导员。 此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在刚刚添加的代码块后，添加以下代码。 选择课程后，代码将显示参与课程的学生列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

此代码读取 `Enrollments` 视图模型的属性，以显示课程中注册的学生列表。

运行页面并选择一个指导员。 然后选择一门课程，查看参与的学生列表及其成绩。

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>添加显式加载

打开 *InstructorController.cs* ，并查看方法如何 `Index` 获取所选课程的注册列表：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

检索到讲师列表时，你为导航属性指定了预先加载， `Courses` 并为 `Department` 每个课程的属性指定了预先加载。 然后，将 `Courses` 集合放入视图模型，此时将 `Enrollments` 从该集合中的一个实体访问导航属性。 由于没有为导航属性指定预先加载 `Course.Enrollments` ，因此该属性中的数据将作为延迟加载的结果出现在页中。

如果在不以任何其他方式更改代码的情况下禁用了延迟加载，则 `Enrollments` 无论该课程实际具有多少注册，属性都将为 null。 在这种情况下，若要加载 `Enrollments` 属性，必须指定预先加载或显式加载。 您已经了解了如何执行预先加载。 若要查看显式加载的示例，请将方法替换 `Index` 为以下代码，以显式加载 `Enrollments` 属性。 更改的代码已突出显示。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

获取所选 `Course` 实体后，新代码将显式加载该课程的 `Enrollments` 导航属性：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

然后，它显式加载每个 `Enrollment` 实体的相关 `Student` 实体：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

请注意，使用 `Collection` 方法加载集合属性，但对于只包含一个实体的属性，则使用 `Reference` 方法。 你现在可以运行讲师索引页面，并且你将看到页面上显示的内容没有任何区别，但你已更改数据的检索方式。

## <a name="summary"></a>总结

现在，你已使用了所有三种方法 (延迟、预先和显式) 将相关数据加载到导航属性。 下一个教程将介绍如何更新相关数据。

可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

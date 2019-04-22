---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 读取相关的数据使用实体框架在 ASP.NET MVC 应用程序 (共 10 个 5) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f86212c1cb559c164342997fb0e4208339b5e3cc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421116"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>读取相关数据使用实体框架在 ASP.NET MVC 应用程序 (5 10 个)

通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


在上一教程中，您将完成学校数据模型。 在本教程将读取并显示相关的数据-即 Entity Framework 加载到导航属性的数据。

下图是将会用到的页面。

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>延迟、 及早计算，和显式加载相关数据

有几种方法，实体框架可以相关的数据加载到实体的导航属性：

- *延迟加载*。 首次读取实体时，不检索相关数据。 然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。 这会导致发送到数据库的多个查询 — 一个用于实体本身，一个必须检索每个相关实体数据的时间。 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *预先加载*。 读取该实体时，会同时检索相关数据。 此时通常会出现单一联接查询，检索所有必需数据。 使用指定预先加载`Include`方法。

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *显式加载*。 这是类似于延迟加载的只不过显式检索相关的数据中的代码;它不会自动发生时您访问导航属性。 加载相关的数据手动通过实体和调用获取对象状态管理器入口`Collection.Load`集合的方法或`Reference.Load`保存单个实体的属性的方法。 (在以下示例中，如果你想要加载管理员导航属性，您会取代`Collection(x => x.Courses)`与`Reference(x => x.Administrator)`。)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

因为它们不立即检索属性值，延迟加载和显式加载也都称为*延迟加载*。

一般情况下，如果您知道你需要相关的数据对于每个实体检索到的预先加载提供最佳性能，因为发送到数据库的单个查询通常比个检索每个实体的单独查询更有效。 例如，在上面的示例中，假设每个系有十个相关的课程。 预先加载示例会导致只需单一 （联接） 查询，将单个往返到数据库。 延迟加载和显式加载示例将同时导致 11 个查询和 11 个往返到数据库。 延迟较高时，额外往返数据库对性能尤为不利。

但是，在某些情况下延迟加载是更高效。 预先加载可能会导致非常复杂的联接为其生成 SQL Server 无法有效地处理它。 或者，如果您需要访问实体的导航属性仅对一组实体的子集进行处理，延迟加载可能会更好地执行，因为预先加载将检索数据超过所需的数据。 如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。

通常会使用显式加载，仅当你已启用延迟加载关闭时。 你应打开延迟加载关闭时的一个方案是在序列化过程。 延迟加载和序列化，不要混合，如果您不小心最终查询更多的数据比预期时延迟加载处于启用状态。 序列化通常可通过访问类型的实例上每个属性。 属性访问触发延迟加载，并为这些延迟加载的实体进行序列化。 然后，序列化过程访问的延迟加载的实体，可能会导致更多的延迟加载和序列化的每个属性。 若要防止此用尽链式反应，启用延迟加载关闭之前序列化实体。

默认情况下，数据库上下文类执行延迟加载。 有两种禁用延迟加载的方法：

- 对于特定的导航属性，省略`virtual`关键字声明的属性时。
- 对于所有导航属性，设置`LazyLoadingEnabled`到`false`。 例如，可以将以下代码放在您的上下文类的构造函数中： 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

延迟加载可以屏蔽会导致性能问题的代码。 例如，（由于与数据库的多个往返） 未指定预先或显式加载，但处理大量的实体并在每次迭代中使用多个导航属性的代码可能是非常低效。 在开发使用本地 SQL 服务器中执行的应用程序可能具有性能问题时增加延迟时间和延迟加载由于移到 Azure SQL 数据库。 分析数据库查询的实际测试负载将有助于确定延迟加载是否适当。 有关详细信息请参阅[揭开面纱实体框架策略：加载相关的数据](https://msdn.microsoft.com/magazine/hh205756.aspx)并[使用 Entity Framework 减少 SQL Azure 的网络延迟](https://msdn.microsoft.com/magazine/gg309181.aspx)。

## <a name="create-a-courses-index-page-that-displays-department-name"></a>创建该显示院系名称的课程索引页

`Course`实体包括导航属性包含`Department`院系的课程将分配到的实体。 若要在课程列表中显示的分配系的名称，您需要获取`Name`属性从`Department`中的实体`Course.Department`导航属性。

创建名为的控制器`CourseController`有关`Course`实体类型，使用之前的相同选项`Student`控制器，如下图中所示 （但与不同的映像，您的上下文类位于 DAL 的命名空间，不是模型命名空间）：

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

打开*Controllers\CourseController.cs*并查看`Index`方法：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。

打开*Views\Course\Index.cshtml*和现有代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

已对基架代码进行了如下更改：

- 更改将标题从**索引**到**课程**。
- 向左移动行链接。
- 添加列标题下的**数量**显示`CourseID`属性值。 （默认情况下，主键不是已搭建基架因为它们通常是向最终用户无意义。 但是，在这种情况下主键是有意义并且你想要显示它。）
- 更改从最后一个列标题**DepartmentID** (到外键的名称`Department`实体) 对**部门**。

请注意，对于最后一列中，基架的代码将显示`Name`的属性`Department`实体加载到`Department`导航属性：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

运行页 (选择**课程**Contoso University 主页上的选项卡) 若要查看包含系名称列表。

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>创建显示课程和注册的讲师索引页

将在本部分中创建一个控制器并查看`Instructor`实体以显示讲师索引页：

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

该页面通过以下方式读取和显示相关数据：

- 讲师列表显示的相关的数据`OfficeAssignment`实体。 `Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。 你将使用预先加载`OfficeAssignment`实体。 如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。 在这种情况下，你希望显示所有显示的讲师的办公室分配情况。
- 当用户选择一名讲师，相关`Course`实体的显示。 `Instructor` 和 `Course` 实体之间存在多对多关系。 你将使用预先加载`Course`实体和其相关`Department`实体。 在这种情况下，可能延迟加载是更高效，因为你需要仅对所选讲师的课程。 但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。
- 当用户选择一门课程时，与相关的数据从`Enrollments`显示实体集。 `Course` 和 `Enrollment` 实体之间存在一对多的关系。 你将添加用于显式加载`Enrollment`实体和其相关`Student`实体。 （显式加载无需因为启用了延迟加载，但这将显示如何执行显式加载。）

### <a name="create-a-view-model-for-the-instructor-index-view"></a>为讲师索引视图创建视图模型

讲师索引页显示了三个不同的表。 因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。

在中*Viewmodel*文件夹中，创建*InstructorIndexData.cs*和现有代码替换为以下代码：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>添加所选行的样式

若要将标记所选的行需要不同的背景色。 若要为此用户界面提供一种样式，请将以下突出显示的代码添加到部分`/* info and errors */`中*Content\Site.css*，如下所示：

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>创建讲师控制器和视图

创建`InstructorController`控制器，如下图中所示：

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

打开*Controllers\InstructorController.cs*并添加`using`语句`ViewModels`命名空间：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

中的基架的代码`Index`方法指定预先加载仅`OfficeAssignment`导航属性：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

替换为`Index`方法与以下代码以加载其他相关数据并将其放在视图模型中：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

该方法接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)，提供 ID 值的所选的讲师和课程，并将所有所需的数据传递给视图。 参数由页面上的“选择”超链接提供。

> [!TIP]
> 
> **路由数据**
> 
> 路由数据是在路由表中指定的 URL 段中找到的模型联编程序的数据。 例如，指定默认路由`controller`， `action`，和`id`段：
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> 在以下 URL，默认路由映射`Instructor`作为`controller`，`Index`作为`action`1 赋`id`; 这些是路由数据值。
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "？ courseID = 2021年"是一个查询字符串值。 如果传递的模型联编程序也能`id`作为查询字符串值：
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> 通过创建 Url `ActionLink` Razor 视图中的语句。 在下面的代码中，`id`参数匹配的默认路由，因此`id`添加到路由数据。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> 在下面的代码，`courseID`不匹配默认路由中的参数，因此，它将添加为查询字符串。
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]


代码先创建一个视图模型实例，并在其中放入讲师列表。 该代码指定预先加载`Instructor.OfficeAssignment`和`Instructor.Courses`导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

第二个`Include`方法加载课程，并为每个课程加载完成了预先加载`Course.Department`导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

正如前面提到，预先加载不是必需的但做是为了提高性能。 由于视图始终需要`OfficeAssignment`实体，它是更有效地在同一查询中提取的。 `Course` 实体是必需的因此预先加载是优于延迟加载，仅当与选中课程更频繁地显示的页中 web 页上，选择一名讲师时。

如果选择了讲师 ID，则从视图模型中的讲师列表检索所选的讲师。 视图模型`Courses`属性然后加载`Course`讲师实体`Courses`导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

`Where`方法将返回一个集合，但在这种情况下只有一个在向该方法传入条件`Instructor`所返回的实体。 `Single`方法将集合转换为一个`Instructor`实体，这将使您可以访问该实体的`Courses`属性。

您使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)集合时知道集合上的方法将具有只有一个项。 `Single`方法将引发异常，如果传递给它的集合为空或多个项。 一种替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它返回默认值 (`null`这种情况下) 是否为空集合。 但是，在这种情况下，仍会引发异常 (尝试查找`Courses`属性上的`null`引用)，和异常消息会清楚指出问题的原因。 当您调用`Single`方法，您还可以传入`Where`条件而不是调用`Where`方法分开：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

而不是：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。 然后，视图模型的`Enrollments`属性加载`Enrollment`从该课程实体`Enrollments`导航属性。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>修改讲师索引视图

在中*Views\Instructor\Index.cshtml*，现有代码替换为以下代码。 突出显示所作更改：

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

已对现有代码进行了如下更改：

- 将模型类更改为了 `InstructorIndexData`。
- 将页标题从“索引”更改为了“讲师”。
- 向左移动行链接列。
- 删除**FullName**列。
- 添加**Office**显示的列`item.OfficeAssignment.Location`仅当`item.OfficeAssignment`不为 null。 (这是一对零或一一关系，因为可能不会有相关`OfficeAssignment`实体。) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- 添加了的代码，将动态添加`class="selectedrow"`到`tr`的所选讲师的元素。 此设置使用前面创建的 CSS 类的所选行的背景色。 (`valign`将多行的列添加到表时，将在以下教程中有用属性。) 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- 添加了新`ActionLink`标记为**选择**之前每个行中的其他链接，这将导致所选的讲师 ID 发送到`Index`方法。

运行应用程序，并选择**讲师**选项卡。页将显示`Location`属性的相关`OfficeAssignment`实体和一个空表单元时有无相关`OfficeAssignment`实体。

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

在中*Views\Instructor\Index.cshtml*文件之后，结束`table`元素 （在文件末尾），添加以下突出显示的代码。 这将显示选择讲师时与讲师相关的课程列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

此代码读取视图模型的 `Courses` 属性以显示课程列表。 它还提供了`Select`发送到所选课程的 ID 的超链接`Index`操作方法。

> [!NOTE]
> *.Css*由浏览器缓存文件。 如果看不到所做的更改，在运行该应用程序时，请执行硬刷新 (单击时按住 CTRL 键**刷新**按钮或按 CTRL + F5)。


运行该页并选择讲师。 此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在刚刚添加的代码块后，添加以下代码。 选择课程后，代码将显示参与课程的学生列表。

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

此代码读取`Enrollments`以便显示学生列表视图模型属性参加该课程。

运行该页并选择讲师。 然后选择一门课程，查看参与的学生列表及其成绩。

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>添加显式加载

打开*InstructorController.cs* ，并查看如何`Index`方法获取所选课程的注册列表：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

当检索讲师列表时，您指定了预先加载`Courses`导航属性和`Department`属性的每个课程。 然后您将放`Courses`集合视图模型中，现在正在访问`Enrollments`从该集合中的一个实体的导航属性。 因为未指定预先加载`Course.Enrollments`导航属性，作为延迟加载结果页中显示来自该属性的数据。

如果无需更改代码以任何方式禁用延迟加载`Enrollments`属性将为 null 而不考虑该课程实际上有多少注册。 在此情况下，若要加载`Enrollments`属性，您将需要指定预先加载还是显式加载。 您所见如何执行预先加载。 若要查看的显式加载示例，请替换`Index`方法显式加载的以下代码替换`Enrollments`属性。 突出显示更改的代码。

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

获取所选后`Course`实体，新代码，显式加载该课程`Enrollments`导航属性：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

然后它显式加载每个`Enrollment`实体的相关`Student`实体：

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

请注意，使用`Collection`方法以加载集合属性，但对于一个属性，保存只是一个实体，你使用`Reference`方法。 现在可以运行讲师索引页，尽管已经更改数据的检索方式，您将看到的页上，显示的内容没有区别。

## <a name="summary"></a>总结

现在，你已使用所有三种方式 （延迟、 及早计算，和显式） 将相关的数据加载到导航属性。 下一个教程将介绍如何更新相关数据。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

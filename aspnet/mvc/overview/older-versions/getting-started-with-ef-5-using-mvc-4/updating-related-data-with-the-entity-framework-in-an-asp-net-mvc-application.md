---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架更新相关数据 (6 （共10个）) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: dcdbd746aaa06d734f0d88b88e8d864e7e4ff5e7
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984928"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>使用 ASP.NET MVC 应用程序中的实体框架更新相关数据 (6 （共10个）) 

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你显示了相关数据;在本教程中，你将更新相关数据。 对于大多数关系，可以通过更新相应的外键字段来实现此目的。 对于多对多关系，实体框架不会直接公开联接表，因此必须在适当的导航属性中显式添加和移除实体。

下图是将会用到的页面。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>自定义课程的创建和编辑页面

创建新的课程实体时，新实体必须与现有院系有关系。 为此，基架代码需包括控制器方法、创建视图和编辑视图，且视图中应包括用于选择院系的下拉列表。 下拉列表设置 `Course.DepartmentID` 外键属性，这就是加载 `Department` 具有相应实体的导航属性所需的全部实体框架 `Department` 。 将用到基架代码，但需对其稍作更改，以便添加错误处理和对下拉列表进行排序。

在 *CourseController.cs* 中，删除四个 `Edit` 和 `Create` 方法，并将其替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList`方法获取按名称排序的所有部门的列表， `SelectList` 为下拉列表创建集合，并将集合传递给属性中的视图 `ViewBag` 。 该方法可以使用可选的 `selectedDepartment` 参数，而调用的代码可以通过该参数来指定呈现下拉列表时被选择的项。 视图将名称传递 `DepartmentID` 给 [ `DropDownList` 帮助](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)者，然后，帮助者知道在对象中查找名为的 `ViewBag` `SelectList` `DepartmentID` 。

`HttpGet` `Create` 方法调用 `PopulateDepartmentsDropDownList` 方法而不设置所选的项，因为对于新课程，尚未建立部门：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` 方法根据已分配给要编辑的课程的部门 ID 设置所选项目：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpPost`和的方法 `Create` 还包括在发生 `Edit` 错误后重新显示该页时设置选定项的代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

此代码可确保在重新显示页面以显示错误消息时，选择的任何部门始终处于选中状态。

在 *Views\Course\Create.cshtml* 中，添加突出显示的代码，以在 " **标题** " 字段之前创建新的课程编号字段。 如前面的教程中所述，默认情况下主键字段不基架，但此主键是有意义的，因此你希望用户能够输入密钥值。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

在 *Views\Course\Edit.cshtml*、 *Views\Course\Delete.cshtml* 和 *Views\Course\Details.cshtml* 中，在 " **标题** " 字段之前添加课程编号字段。 由于它是主键，因此将显示，但不能更改它。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

运行 " **创建** " 页 (显示 "课程索引" 页，然后单击 **"新建)** 并为新课程输入数据：

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

单击“创建”。 将显示 "课程索引" 页，新课程将添加到列表中。 索引页列表中的院系名称来自导航属性，表明已正确建立关系。

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

运行 " **编辑** " 页 (显示 "课程索引" 页，然后单击课程) 上的 " **编辑** "。

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

更改页面上的数据，然后单击“保存”。 将显示 "课程索引" 页和更新的课程数据。

## <a name="adding-an-edit-page-for-instructors"></a>为讲师添加编辑页面

编辑讲师记录时，有时希望能更新讲师的办公室分配。 `Instructor`实体与实体之间存在一对零或一的关系 `OfficeAssignment` ，这意味着你必须处理以下情况：

- 如果用户清除 office 分配，并且它最初具有值，则必须删除并删除该 `OfficeAssignment` 实体。
- 如果用户输入 office 分配值并且它最初为空，则必须创建新 `OfficeAssignment` 实体。
- 如果用户更改了 office 分配的值，则必须更改现有实体中的值 `OfficeAssignment` 。

打开 *InstructorController.cs* 并查看 `HttpGet` `Edit` 方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此处的基架代码不是你所需的代码。 它为下拉列表设置数据，但您需要的是文本框。 将此方法替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

此代码删除 `ViewBag` 语句，并为关联实体添加预先加载 `OfficeAssignment` 。 不能使用方法执行预先加载 `Find` ，因此， `Where` 使用和 `Single` 方法来选择讲师。

将 `HttpPost` `Edit` 方法替换为以下代码。 处理 office 分配更新的：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

该代码执行以下操作：

- 使用 `OfficeAssignment` 导航属性的预先加载从数据库获取当前的 `Instructor` 实体。 这与你在方法中执行的操作相同 `HttpGet` `Edit` 。
- 用模型绑定器中的值更新检索到的 `Instructor` 实体。 使用的 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 重载使你能够将你要包括的属性 *列入* 允许列表。 这可以防止过度发布，如 [第二个教程中所](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)述。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- 如果办公室位置为空，则将 `Instructor.OfficeAssignment` 属性设置为 null，以便删除表中的相关行 `OfficeAssignment` 。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- 将更改保存到数据库。

在 *Views\Instructor\Edit.cshtml* 中，在 `div` " **雇佣日期** " 字段的元素之后，添加一个用于编辑办公室位置的新字段：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

运行页面 (选择 " **讲师** " 选项卡，然后单击讲师) 上的 " **编辑** "。 更改“办公室位置”，然后单击“保存” 。

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>向 "讲师编辑" 页添加课程分配

讲师可能教授任意数量的课程。 现在可以通过使用一组复选框来更改课程分配，从而增强讲师编辑页面的性能，如以下屏幕截图所示：

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

和实体之间的 `Course` 关系 `Instructor` 是多对多，这意味着您不能直接访问联接表。 相反，您将在导航属性中添加和移除实体 `Instructor.Courses` 。

用于更改讲师所对应的课程的 UI 是一组复选框。 该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。 用户可以通过选择或清除复选框来更改课程分配。 如果课程数量很大，您可能想要使用不同的方法来显示视图中的数据，但您可以使用相同的方法来处理导航属性，以便创建或删除关系。

若要为复选框列表的视图提供数据，将使用视图模型类。 在 *viewmodel* 文件夹中创建 *AssignedCourseData.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

在 *InstructorController.cs* 中，将 `HttpGet` `Edit` 方法替换为以下代码。 突出显示所作更改。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。

方法中的代码 `PopulateAssignedCourseData` 读取所有 `Course` 实体，以便使用视图模型类加载课程列表。 对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。 若要在检查是否将课程分配给讲师时创建高效的查找，则分配给讲师的课程将被放入 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 集合。 `Assigned`对于指定讲师的课程，将属性设置为 `true` 。 视图将使用此属性来确定应将哪些复选框显示为选中状态。 最后，将列表传递给属性中的视图 `ViewBag` 。

接下来，添加用户单击“保存”时执行的代码。 将 `HttpPost` `Edit` 方法替换为以下代码，该代码调用更新实体的导航属性的新方法 `Courses` `Instructor` 。 突出显示所作更改。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

由于视图不具有实体集合，因此 `Course` 模型绑定器无法自动更新 `Courses` 导航属性。 你将在新的方法中执行此操作，而不是使用模型联编程序更新课程导航属性 `UpdateInstructorCourses` 。 为此，需要从模型绑定中排除 `Courses` 属性。 这不需要对调用 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 的代码进行任何更改，因为你使用的是 *允许列表* 重载，而 `Courses` 不是包含列表。

如果未选择任何复选框，则中的代码将 `UpdateInstructorCourses` `Courses` 使用空集合初始化导航属性：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。 为便于高效查找，后两个集合存储在 `HashSet` 对象中。

如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

在 *Views\Instructor\Edit.cshtml* 中，通过在字段的元素后添加以下突出显示的代码，添加一个包含复选框数组的 " **课程** " 字段 `div` `OfficeAssignment` ：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

此代码将创建一个具有三列的 HTML 表。 每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。 所有复选框都具有相同的名称 ( "selectedCourses" ) ，这会通知模型绑定器将这些复选框视为组。 `value`每个复选框的属性都设置为 `CourseID.` 页面发布后的值，模型联编程序将一个数组传递到控制器，该控制器 `CourseID` 仅包含所选复选框的值。

最初呈现复选框时，分配给讲师的课程的 `checked` 属性具有属性，这些属性将选择它们 (显示选中) 。

更改课程分配后，你将希望能够在站点返回到页面时验证所做的更改 `Index` 。 因此，您需要在该页面的表中添加一列。 在这种情况下，不需要使用 `ViewBag` 对象，因为您要显示的信息已位于 `Courses` `Instructor` 作为模型传递到页面的实体的导航属性中。

在 *Views\Instructor\Index.cshtml* 中，在 " **Office** " 标题后面添加一个 **课程** 标题，如以下示例中所示：

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

然后，在 "办公室位置详细信息" 单元之后立即添加一个新的详细信息单元：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

运行 " **讲师索引** " 页，查看分配给每位讲师的课程：

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

单击指导员上的 " **编辑** " 以查看 "编辑" 页。

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

更改某些课程分配，并单击 " **保存**"。 所作更改将反映在索引页上。

 注意：在有有限数量的课程时，用于编辑讲师课程数据的方法很有用。 若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。  

## <a name="update-the-delete-method"></a>更新 Delete 方法

更改 HttpPost Delete 方法中的代码，以便在删除指导员时删除任何)  (office 分配记录：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

如果尝试删除以管理员身份分配到部门的指导员，将会出现引用完整性错误。 请参阅 [本教程的当前版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) ，以获取其他代码，此代码将自动从指定为管理员的任何部门删除教师。

## <a name="summary"></a>总结

你现在已经完成了使用相关数据的这一简介。 到目前为止，在这些教程中，您已完成了一系列完整的 CRUD 操作，但您并未处理并发问题。 下一教程将介绍并发性的主题、说明如何处理它，以及如何将并发处理添加到已为一种实体类型编写的代码段。

可以在 [本系列最后一个教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)结尾处找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

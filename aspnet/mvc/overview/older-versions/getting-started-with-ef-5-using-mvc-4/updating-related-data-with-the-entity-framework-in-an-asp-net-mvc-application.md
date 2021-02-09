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
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="92f28-103">使用 ASP.NET MVC 应用程序中的实体框架更新相关数据 (6 （共10个）) </span><span class="sxs-lookup"><span data-stu-id="92f28-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>

<span data-ttu-id="92f28-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="92f28-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="92f28-105">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="92f28-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="92f28-106">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="92f28-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="92f28-107">如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="92f28-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="92f28-108">通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="92f28-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="92f28-109">有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="92f28-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="92f28-110">在上一教程中，你显示了相关数据;在本教程中，你将更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="92f28-110">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="92f28-111">对于大多数关系，可以通过更新相应的外键字段来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="92f28-111">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="92f28-112">对于多对多关系，实体框架不会直接公开联接表，因此必须在适当的导航属性中显式添加和移除实体。</span><span class="sxs-lookup"><span data-stu-id="92f28-112">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="92f28-113">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="92f28-113">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="92f28-116">自定义课程的创建和编辑页面</span><span class="sxs-lookup"><span data-stu-id="92f28-116">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="92f28-117">创建新的课程实体时，新实体必须与现有院系有关系。</span><span class="sxs-lookup"><span data-stu-id="92f28-117">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="92f28-118">为此，基架代码需包括控制器方法、创建视图和编辑视图，且视图中应包括用于选择院系的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="92f28-118">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="92f28-119">下拉列表设置 `Course.DepartmentID` 外键属性，这就是加载 `Department` 具有相应实体的导航属性所需的全部实体框架 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-119">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="92f28-120">将用到基架代码，但需对其稍作更改，以便添加错误处理和对下拉列表进行排序。</span><span class="sxs-lookup"><span data-stu-id="92f28-120">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="92f28-121">在 *CourseController.cs* 中，删除四个 `Edit` 和 `Create` 方法，并将其替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="92f28-121">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="92f28-122">`PopulateDepartmentsDropDownList`方法获取按名称排序的所有部门的列表， `SelectList` 为下拉列表创建集合，并将集合传递给属性中的视图 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-122">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="92f28-123">该方法可以使用可选的 `selectedDepartment` 参数，而调用的代码可以通过该参数来指定呈现下拉列表时被选择的项。</span><span class="sxs-lookup"><span data-stu-id="92f28-123">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="92f28-124">视图将名称传递 `DepartmentID` 给 [ `DropDownList` 帮助](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)者，然后，帮助者知道在对象中查找名为的 `ViewBag` `SelectList` `DepartmentID` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-124">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="92f28-125">`HttpGet` `Create` 方法调用 `PopulateDepartmentsDropDownList` 方法而不设置所选的项，因为对于新课程，尚未建立部门：</span><span class="sxs-lookup"><span data-stu-id="92f28-125">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="92f28-126">`HttpGet` `Edit` 方法根据已分配给要编辑的课程的部门 ID 设置所选项目：</span><span class="sxs-lookup"><span data-stu-id="92f28-126">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="92f28-127">`HttpPost`和的方法 `Create` 还包括在发生 `Edit` 错误后重新显示该页时设置选定项的代码：</span><span class="sxs-lookup"><span data-stu-id="92f28-127">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="92f28-128">此代码可确保在重新显示页面以显示错误消息时，选择的任何部门始终处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="92f28-128">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="92f28-129">在 *Views\Course\Create.cshtml* 中，添加突出显示的代码，以在 " **标题** " 字段之前创建新的课程编号字段。</span><span class="sxs-lookup"><span data-stu-id="92f28-129">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="92f28-130">如前面的教程中所述，默认情况下主键字段不基架，但此主键是有意义的，因此你希望用户能够输入密钥值。</span><span class="sxs-lookup"><span data-stu-id="92f28-130">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="92f28-131">在 *Views\Course\Edit.cshtml*、 *Views\Course\Delete.cshtml* 和 *Views\Course\Details.cshtml* 中，在 " **标题** " 字段之前添加课程编号字段。</span><span class="sxs-lookup"><span data-stu-id="92f28-131">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="92f28-132">由于它是主键，因此将显示，但不能更改它。</span><span class="sxs-lookup"><span data-stu-id="92f28-132">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="92f28-133">运行 " **创建** " 页 (显示 "课程索引" 页，然后单击 **"新建)** 并为新课程输入数据：</span><span class="sxs-lookup"><span data-stu-id="92f28-133">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="92f28-135">单击“创建”。</span><span class="sxs-lookup"><span data-stu-id="92f28-135">Click **Create**.</span></span> <span data-ttu-id="92f28-136">将显示 "课程索引" 页，新课程将添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="92f28-136">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="92f28-137">索引页列表中的院系名称来自导航属性，表明已正确建立关系。</span><span class="sxs-lookup"><span data-stu-id="92f28-137">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="92f28-139">运行 " **编辑** " 页 (显示 "课程索引" 页，然后单击课程) 上的 " **编辑** "。</span><span class="sxs-lookup"><span data-stu-id="92f28-139">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="92f28-141">更改页面上的数据，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="92f28-141">Change data on the page and click **Save**.</span></span> <span data-ttu-id="92f28-142">将显示 "课程索引" 页和更新的课程数据。</span><span class="sxs-lookup"><span data-stu-id="92f28-142">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="92f28-143">为讲师添加编辑页面</span><span class="sxs-lookup"><span data-stu-id="92f28-143">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="92f28-144">编辑讲师记录时，有时希望能更新讲师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="92f28-144">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="92f28-145">`Instructor`实体与实体之间存在一对零或一的关系 `OfficeAssignment` ，这意味着你必须处理以下情况：</span><span class="sxs-lookup"><span data-stu-id="92f28-145">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="92f28-146">如果用户清除 office 分配，并且它最初具有值，则必须删除并删除该 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="92f28-146">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="92f28-147">如果用户输入 office 分配值并且它最初为空，则必须创建新 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="92f28-147">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="92f28-148">如果用户更改了 office 分配的值，则必须更改现有实体中的值 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-148">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="92f28-149">打开 *InstructorController.cs* 并查看 `HttpGet` `Edit` 方法：</span><span class="sxs-lookup"><span data-stu-id="92f28-149">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="92f28-150">此处的基架代码不是你所需的代码。</span><span class="sxs-lookup"><span data-stu-id="92f28-150">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="92f28-151">它为下拉列表设置数据，但您需要的是文本框。</span><span class="sxs-lookup"><span data-stu-id="92f28-151">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="92f28-152">将此方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="92f28-152">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="92f28-153">此代码删除 `ViewBag` 语句，并为关联实体添加预先加载 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-153">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="92f28-154">不能使用方法执行预先加载 `Find` ，因此， `Where` 使用和 `Single` 方法来选择讲师。</span><span class="sxs-lookup"><span data-stu-id="92f28-154">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="92f28-155">将 `HttpPost` `Edit` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="92f28-155">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="92f28-156">处理 office 分配更新的：</span><span class="sxs-lookup"><span data-stu-id="92f28-156">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="92f28-157">该代码执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="92f28-157">The code does the following:</span></span>

- <span data-ttu-id="92f28-158">使用 `OfficeAssignment` 导航属性的预先加载从数据库获取当前的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="92f28-158">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="92f28-159">这与你在方法中执行的操作相同 `HttpGet` `Edit` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-159">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="92f28-160">用模型绑定器中的值更新检索到的 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="92f28-160">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="92f28-161">使用的 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 重载使你能够将你要包括的属性 *列入* 允许列表。</span><span class="sxs-lookup"><span data-stu-id="92f28-161">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="92f28-162">这可以防止过度发布，如 [第二个教程中所](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)述。</span><span class="sxs-lookup"><span data-stu-id="92f28-162">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="92f28-163">如果办公室位置为空，则将 `Instructor.OfficeAssignment` 属性设置为 null，以便删除表中的相关行 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-163">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="92f28-164">将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="92f28-164">Saves the changes to the database.</span></span>

<span data-ttu-id="92f28-165">在 *Views\Instructor\Edit.cshtml* 中，在 `div` " **雇佣日期** " 字段的元素之后，添加一个用于编辑办公室位置的新字段：</span><span class="sxs-lookup"><span data-stu-id="92f28-165">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="92f28-166">运行页面 (选择 " **讲师** " 选项卡，然后单击讲师) 上的 " **编辑** "。</span><span class="sxs-lookup"><span data-stu-id="92f28-166">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="92f28-167">更改“办公室位置”，然后单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="92f28-167">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="92f28-169">向 "讲师编辑" 页添加课程分配</span><span class="sxs-lookup"><span data-stu-id="92f28-169">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="92f28-170">讲师可能教授任意数量的课程。</span><span class="sxs-lookup"><span data-stu-id="92f28-170">Instructors may teach any number of courses.</span></span> <span data-ttu-id="92f28-171">现在可以通过使用一组复选框来更改课程分配，从而增强讲师编辑页面的性能，如以下屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="92f28-171">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="92f28-173">和实体之间的 `Course` 关系 `Instructor` 是多对多，这意味着您不能直接访问联接表。</span><span class="sxs-lookup"><span data-stu-id="92f28-173">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="92f28-174">相反，您将在导航属性中添加和移除实体 `Instructor.Courses` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-174">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="92f28-175">用于更改讲师所对应的课程的 UI 是一组复选框。</span><span class="sxs-lookup"><span data-stu-id="92f28-175">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="92f28-176">该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。</span><span class="sxs-lookup"><span data-stu-id="92f28-176">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="92f28-177">用户可以通过选择或清除复选框来更改课程分配。</span><span class="sxs-lookup"><span data-stu-id="92f28-177">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="92f28-178">如果课程数量很大，您可能想要使用不同的方法来显示视图中的数据，但您可以使用相同的方法来处理导航属性，以便创建或删除关系。</span><span class="sxs-lookup"><span data-stu-id="92f28-178">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="92f28-179">若要为复选框列表的视图提供数据，将使用视图模型类。</span><span class="sxs-lookup"><span data-stu-id="92f28-179">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="92f28-180">在 *viewmodel* 文件夹中创建 *AssignedCourseData.cs* ，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="92f28-180">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="92f28-181">在 *InstructorController.cs* 中，将 `HttpGet` `Edit` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="92f28-181">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="92f28-182">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="92f28-182">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="92f28-183">该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。</span><span class="sxs-lookup"><span data-stu-id="92f28-183">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="92f28-184">方法中的代码 `PopulateAssignedCourseData` 读取所有 `Course` 实体，以便使用视图模型类加载课程列表。</span><span class="sxs-lookup"><span data-stu-id="92f28-184">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="92f28-185">对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。</span><span class="sxs-lookup"><span data-stu-id="92f28-185">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="92f28-186">若要在检查是否将课程分配给讲师时创建高效的查找，则分配给讲师的课程将被放入 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 集合。</span><span class="sxs-lookup"><span data-stu-id="92f28-186">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="92f28-187">`Assigned`对于指定讲师的课程，将属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-187">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="92f28-188">视图将使用此属性来确定应将哪些复选框显示为选中状态。</span><span class="sxs-lookup"><span data-stu-id="92f28-188">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="92f28-189">最后，将列表传递给属性中的视图 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-189">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="92f28-190">接下来，添加用户单击“保存”时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="92f28-190">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="92f28-191">将 `HttpPost` `Edit` 方法替换为以下代码，该代码调用更新实体的导航属性的新方法 `Courses` `Instructor` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-191">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="92f28-192">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="92f28-192">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="92f28-193">由于视图不具有实体集合，因此 `Course` 模型绑定器无法自动更新 `Courses` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="92f28-193">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="92f28-194">你将在新的方法中执行此操作，而不是使用模型联编程序更新课程导航属性 `UpdateInstructorCourses` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-194">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="92f28-195">为此，需要从模型绑定中排除 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="92f28-195">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="92f28-196">这不需要对调用 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 的代码进行任何更改，因为你使用的是 *允许列表* 重载，而 `Courses` 不是包含列表。</span><span class="sxs-lookup"><span data-stu-id="92f28-196">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="92f28-197">如果未选择任何复选框，则中的代码将 `UpdateInstructorCourses` `Courses` 使用空集合初始化导航属性：</span><span class="sxs-lookup"><span data-stu-id="92f28-197">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="92f28-198">之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。</span><span class="sxs-lookup"><span data-stu-id="92f28-198">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="92f28-199">为便于高效查找，后两个集合存储在 `HashSet` 对象中。</span><span class="sxs-lookup"><span data-stu-id="92f28-199">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="92f28-200">如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。</span><span class="sxs-lookup"><span data-stu-id="92f28-200">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="92f28-201">如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。</span><span class="sxs-lookup"><span data-stu-id="92f28-201">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="92f28-202">在 *Views\Instructor\Edit.cshtml* 中，通过在字段的元素后添加以下突出显示的代码，添加一个包含复选框数组的 " **课程** " 字段 `div` `OfficeAssignment` ：</span><span class="sxs-lookup"><span data-stu-id="92f28-202">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="92f28-203">此代码将创建一个具有三列的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="92f28-203">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="92f28-204">每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。</span><span class="sxs-lookup"><span data-stu-id="92f28-204">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="92f28-205">所有复选框都具有相同的名称 ( "selectedCourses" ) ，这会通知模型绑定器将这些复选框视为组。</span><span class="sxs-lookup"><span data-stu-id="92f28-205">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="92f28-206">`value`每个复选框的属性都设置为 `CourseID.` 页面发布后的值，模型联编程序将一个数组传递到控制器，该控制器 `CourseID` 仅包含所选复选框的值。</span><span class="sxs-lookup"><span data-stu-id="92f28-206">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="92f28-207">最初呈现复选框时，分配给讲师的课程的 `checked` 属性具有属性，这些属性将选择它们 (显示选中) 。</span><span class="sxs-lookup"><span data-stu-id="92f28-207">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="92f28-208">更改课程分配后，你将希望能够在站点返回到页面时验证所做的更改 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="92f28-208">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="92f28-209">因此，您需要在该页面的表中添加一列。</span><span class="sxs-lookup"><span data-stu-id="92f28-209">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="92f28-210">在这种情况下，不需要使用 `ViewBag` 对象，因为您要显示的信息已位于 `Courses` `Instructor` 作为模型传递到页面的实体的导航属性中。</span><span class="sxs-lookup"><span data-stu-id="92f28-210">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="92f28-211">在 *Views\Instructor\Index.cshtml* 中，在 " **Office** " 标题后面添加一个 **课程** 标题，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="92f28-211">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="92f28-212">然后，在 "办公室位置详细信息" 单元之后立即添加一个新的详细信息单元：</span><span class="sxs-lookup"><span data-stu-id="92f28-212">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="92f28-213">运行 " **讲师索引** " 页，查看分配给每位讲师的课程：</span><span class="sxs-lookup"><span data-stu-id="92f28-213">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="92f28-215">单击指导员上的 " **编辑** " 以查看 "编辑" 页。</span><span class="sxs-lookup"><span data-stu-id="92f28-215">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="92f28-217">更改某些课程分配，并单击 " **保存**"。</span><span class="sxs-lookup"><span data-stu-id="92f28-217">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="92f28-218">所作更改将反映在索引页上。</span><span class="sxs-lookup"><span data-stu-id="92f28-218">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="92f28-219">注意：在有有限数量的课程时，用于编辑讲师课程数据的方法很有用。</span><span class="sxs-lookup"><span data-stu-id="92f28-219">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="92f28-220">若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="92f28-220">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  

## <a name="update-the-delete-method"></a><span data-ttu-id="92f28-221">更新 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="92f28-221">Update the Delete Method</span></span>

<span data-ttu-id="92f28-222">更改 HttpPost Delete 方法中的代码，以便在删除指导员时删除任何)  (office 分配记录：</span><span class="sxs-lookup"><span data-stu-id="92f28-222">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

<span data-ttu-id="92f28-223">如果尝试删除以管理员身份分配到部门的指导员，将会出现引用完整性错误。</span><span class="sxs-lookup"><span data-stu-id="92f28-223">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="92f28-224">请参阅 [本教程的当前版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) ，以获取其他代码，此代码将自动从指定为管理员的任何部门删除教师。</span><span class="sxs-lookup"><span data-stu-id="92f28-224">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="92f28-225">总结</span><span class="sxs-lookup"><span data-stu-id="92f28-225">Summary</span></span>

<span data-ttu-id="92f28-226">你现在已经完成了使用相关数据的这一简介。</span><span class="sxs-lookup"><span data-stu-id="92f28-226">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="92f28-227">到目前为止，在这些教程中，您已完成了一系列完整的 CRUD 操作，但您并未处理并发问题。</span><span class="sxs-lookup"><span data-stu-id="92f28-227">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="92f28-228">下一教程将介绍并发性的主题、说明如何处理它，以及如何将并发处理添加到已为一种实体类型编写的代码段。</span><span class="sxs-lookup"><span data-stu-id="92f28-228">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="92f28-229">可以在 [本系列最后一个教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)结尾处找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="92f28-229">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="92f28-230">[上一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="92f28-230">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>

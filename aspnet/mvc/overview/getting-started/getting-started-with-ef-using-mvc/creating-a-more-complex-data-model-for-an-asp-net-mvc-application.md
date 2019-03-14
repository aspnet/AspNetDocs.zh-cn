---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 教程：创建 ASP.NET MVC 应用的更复杂数据模型
author: tdykstra
description: 在本教程将添加更多实体和关系并将通过指定格式设置、 验证和数据库映射规则来自定义数据模型。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5deab7da776c3c43e3e2cdf42b04922678f956c7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041854"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a><span data-ttu-id="2a990-103">教程：创建 ASP.NET MVC 应用的更复杂数据模型</span><span class="sxs-lookup"><span data-stu-id="2a990-103">Tutorial: Create a more complex data model for an ASP.NET MVC app</span></span>

<span data-ttu-id="2a990-104">在前面的教程中，您过了由三个实体组成的简单数据模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-104">In the previous tutorials you worked with a simple data model that was composed of three entities.</span></span> <span data-ttu-id="2a990-105">在本教程中添加更多实体和关系，并通过指定格式设置、 验证和数据库映射规则来自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-105">In this tutorial you add more entities and relationships and you customize the data model by specifying formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="2a990-106">本文演示两种方式自定义数据模型： 通过将属性添加到实体类并通过将代码添加到数据库上下文类。</span><span class="sxs-lookup"><span data-stu-id="2a990-106">This article shows two ways to customize the data model: by adding attributes to entity classes and by adding code to the database context class.</span></span>

<span data-ttu-id="2a990-107">完成本教程后，实体类将构成下图所示的完整数据模型：</span><span class="sxs-lookup"><span data-stu-id="2a990-107">When you're finished, the entity classes will make up the completed data model that's shown in the following illustration:</span></span>

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="2a990-109">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="2a990-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a990-110">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="2a990-110">Customize the data model</span></span>
> * <span data-ttu-id="2a990-111">更新 Student 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-111">Update Student entity</span></span>
> * <span data-ttu-id="2a990-112">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-112">Create Instructor entity</span></span>
> * <span data-ttu-id="2a990-113">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-113">Create OfficeAssignment entity</span></span>
> * <span data-ttu-id="2a990-114">修改 Course 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-114">Modify the Course entity</span></span>
> * <span data-ttu-id="2a990-115">创建 Department 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-115">Create the Department entity</span></span>
> * <span data-ttu-id="2a990-116">修改 Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-116">Modify the Enrollment entity</span></span>
> * <span data-ttu-id="2a990-117">将代码添加到数据库上下文</span><span class="sxs-lookup"><span data-stu-id="2a990-117">Add code to database context</span></span>
> * <span data-ttu-id="2a990-118">使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="2a990-118">Seed database with test data</span></span>
> * <span data-ttu-id="2a990-119">添加迁移</span><span class="sxs-lookup"><span data-stu-id="2a990-119">Add a migration</span></span>
> * <span data-ttu-id="2a990-120">更新数据库</span><span class="sxs-lookup"><span data-stu-id="2a990-120">Update the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a990-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="2a990-121">Prerequisites</span></span>

* [<span data-ttu-id="2a990-122">第一个迁移和部署代码</span><span class="sxs-lookup"><span data-stu-id="2a990-122">Code First migrations and deployment</span></span>](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a><span data-ttu-id="2a990-123">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="2a990-123">Customize the data model</span></span>

<span data-ttu-id="2a990-124">本节介绍如何使用指定格式化、验证和数据库映射规则的特性来自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-124">In this section you'll see how to customize the data model by using attributes that specify formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="2a990-125">然后在多个以下各节，你将创建一种完整`School`通过添加数据模型属性对类已在模型中剩余的实体类型的创建和创建新类。</span><span class="sxs-lookup"><span data-stu-id="2a990-125">Then in several of the following sections you'll create the complete `School` data model by adding attributes to the classes you already created and creating new classes for the remaining entity types in the model.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="2a990-126">DataType 特性</span><span class="sxs-lookup"><span data-stu-id="2a990-126">The DataType Attribute</span></span>

<span data-ttu-id="2a990-127">对于学生注册日期，目前所有网页都显示有时间和日期，尽管对此字段而言重要的只是日期。</span><span class="sxs-lookup"><span data-stu-id="2a990-127">For student enrollment dates, all of the web pages currently display the time along with the date, although all you care about for this field is the date.</span></span> <span data-ttu-id="2a990-128">使用数据注释特性，可更改一次代码，修复每个视图中数据的显示格式。</span><span class="sxs-lookup"><span data-stu-id="2a990-128">By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.</span></span> <span data-ttu-id="2a990-129">若要查看如何执行此操作，请向 `Student` 类的 `EnrollmentDate` 属性添加一个特性。</span><span class="sxs-lookup"><span data-stu-id="2a990-129">To see an example of how to do that, you'll add an attribute to the `EnrollmentDate` property in the `Student` class.</span></span>

<span data-ttu-id="2a990-130">在*Models\Student.cs*，添加`using`语句`System.ComponentModel.DataAnnotations`命名空间，并添加`DataType`并`DisplayFormat`属性到`EnrollmentDate`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="2a990-130">In *Models\Student.cs*, add a `using` statement for the `System.ComponentModel.DataAnnotations` namespace and add `DataType` and `DisplayFormat` attributes to the `EnrollmentDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

<span data-ttu-id="2a990-131">[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性用于指定比数据库内部类型更具体的数据类型。</span><span class="sxs-lookup"><span data-stu-id="2a990-131">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="2a990-132">在此示例中，我们只想跟踪日期，而不是日期和时间。</span><span class="sxs-lookup"><span data-stu-id="2a990-132">In this case we only want to keep track of the date, not the date and time.</span></span> <span data-ttu-id="2a990-133">[DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供了多种数据类型，如*日期、 时间、 电话号码、 货币、 电子邮件地址*和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a990-133">The [DataType Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) provides for many data types, such as *Date, Time, PhoneNumber, Currency, EmailAddress* and more.</span></span> <span data-ttu-id="2a990-134">应用程序还可通过 `DataType` 特性自动提供类型特定的功能。</span><span class="sxs-lookup"><span data-stu-id="2a990-134">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="2a990-135">例如，`mailto:`可以为创建链接[DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)，和日期选择器可提供用于[DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)中支持的浏览器[HTML5](http://html5.org/).</span><span class="sxs-lookup"><span data-stu-id="2a990-135">For example, a `mailto:` link can be created for [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), and a date selector can be provided for [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in browsers that support [HTML5](http://html5.org/).</span></span> <span data-ttu-id="2a990-136">[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性发出 HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (读作*数据 dash*) 特性供 HTML 5 浏览器理解。</span><span class="sxs-lookup"><span data-stu-id="2a990-136">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes emits HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (pronounced *data dash*) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="2a990-137">[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性不提供任何验证。</span><span class="sxs-lookup"><span data-stu-id="2a990-137">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes do not provide any validation.</span></span>

<span data-ttu-id="2a990-138">`DataType.Date` 不指定显示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="2a990-138">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="2a990-139">默认情况下，显示该数据字段根据基于服务器的默认格式[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a990-139">By default, the data field is displayed according to the default formats based on the server's [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).</span></span>

<span data-ttu-id="2a990-140">`DisplayFormat` 特性用于显式指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="2a990-140">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


<span data-ttu-id="2a990-141">`ApplyFormatInEditMode`设置指定，指定的格式设置也应该应用时的值显示在文本框中以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="2a990-141">The `ApplyFormatInEditMode` setting specifies that the specified formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="2a990-142">(您可能不想为某些字段 — 例如，对于货币值，您可能不希望在文本框中的货币符号以进行编辑。)</span><span class="sxs-lookup"><span data-stu-id="2a990-142">(You might not want that for some fields — for example, for currency values, you might not want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="2a990-143">可以使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性本身，但它通常是使用一个好办法[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性。</span><span class="sxs-lookup"><span data-stu-id="2a990-143">You can use the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute by itself, but it's generally a good idea to use the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute also.</span></span> <span data-ttu-id="2a990-144">`DataType`特性传达*语义*的数据作为相对于屏幕上的呈现方式，提供了以下具有前所未有的优势`DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="2a990-144">The `DataType` attribute conveys the *semantics* of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with `DisplayFormat`:</span></span>

- <span data-ttu-id="2a990-145">浏览器可启用 HTML5 功能（例如，显示日历控件、区域设置适用的货币符号、电子邮件链接、某种客户端输入验证等）。</span><span class="sxs-lookup"><span data-stu-id="2a990-145">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, some client-side input validation, etc.).</span></span>
- <span data-ttu-id="2a990-146">默认情况下，在浏览器将呈现数据采用正确的格式基于你[区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a990-146">By default, the browser will render data using the correct format based on your [locale](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).</span></span>
- <span data-ttu-id="2a990-147">[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性使 MVC 能够选择正确的字段模板来呈现数据 ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)使用字符串模板)。</span><span class="sxs-lookup"><span data-stu-id="2a990-147">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute can enable MVC to choose the right field template to render the data (the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) uses the string template).</span></span> <span data-ttu-id="2a990-148">有关详细信息，请参阅 Brad Wilson [ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="2a990-148">For more information, see Brad Wilson's [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="2a990-149">（为 MVC 2 编写的但本文仍适用于 ASP.NET MVC 的当前版本。）</span><span class="sxs-lookup"><span data-stu-id="2a990-149">(Though written for MVC 2, this article still applies to the current version of ASP.NET MVC.)</span></span>

<span data-ttu-id="2a990-150">如果您使用`DataType`属性与日期字段，则必须指定`DisplayFormat`还以确保字段正确呈现在 Chrome 浏览器中的属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-150">If you use the `DataType` attribute with a date field, you have to specify the `DisplayFormat` attribute also in order to ensure that the field renders correctly in Chrome browsers.</span></span> <span data-ttu-id="2a990-151">有关详细信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。</span><span class="sxs-lookup"><span data-stu-id="2a990-151">For more information, see [this StackOverflow thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).</span></span>

<span data-ttu-id="2a990-152">有关如何处理在 MVC 中的其他日期格式的详细信息，请转到[MVC 5 简介：检查编辑方法和编辑视图](../introduction/examining-the-edit-methods-and-edit-view.md)中的页和搜索&quot;国际化&quot;。</span><span class="sxs-lookup"><span data-stu-id="2a990-152">For more information about how to handle other date formats in MVC, go to [MVC 5 Introduction: Examining the Edit Methods and Edit View](../introduction/examining-the-edit-methods-and-edit-view.md) and search in the page for &quot;internationalization&quot;.</span></span>

<span data-ttu-id="2a990-153">再次运行学生索引页，请注意注册日期不再显示时间。</span><span class="sxs-lookup"><span data-stu-id="2a990-153">Run the Student Index page again and notice that times are no longer displayed for the enrollment dates.</span></span> <span data-ttu-id="2a990-154">相同，则为 true 的任何视图，它使用`Student`模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-154">The same will be true for any view that uses the `Student` model.</span></span>

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a><span data-ttu-id="2a990-156">StringLengthAttribute</span><span class="sxs-lookup"><span data-stu-id="2a990-156">The StringLengthAttribute</span></span>

<span data-ttu-id="2a990-157">还可使用特性指定数据验证规则和验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="2a990-157">You can also specify data validation rules and validation error messages using attributes.</span></span> <span data-ttu-id="2a990-158">[StringLength 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)设置数据库中的最大长度，并提供客户端和服务器端的 ASP.NET MVC 验证。</span><span class="sxs-lookup"><span data-stu-id="2a990-158">The [StringLength attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) sets the maximum length in the database and provides client side and server side validation for ASP.NET MVC.</span></span> <span data-ttu-id="2a990-159">还可在此属性中指定最小字符串长度，但最小值对数据库架构没有影响。</span><span class="sxs-lookup"><span data-stu-id="2a990-159">You can also specify the minimum string length in this attribute, but the minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="2a990-160">假设要确保用户输入的名称不超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="2a990-160">Suppose you want to ensure that users don't enter more than 50 characters for a name.</span></span> <span data-ttu-id="2a990-161">若要添加此限制，添加[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)向属性`LastName`和`FirstMidName`属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="2a990-161">To add this limitation, add [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attributes to the `LastName` and `FirstMidName` properties, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

<span data-ttu-id="2a990-162">[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性不会阻止用户输入一个名称的空格。</span><span class="sxs-lookup"><span data-stu-id="2a990-162">The [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute won't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="2a990-163">可以使用[正则表达式](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性来限制应用于输入。</span><span class="sxs-lookup"><span data-stu-id="2a990-163">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to apply restrictions to the input.</span></span> <span data-ttu-id="2a990-164">例如，下面的代码要求第一个字符为大写，其余字符按字母顺序排列：</span><span class="sxs-lookup"><span data-stu-id="2a990-164">For example the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

<span data-ttu-id="2a990-165">[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)属性提供了与类似的功能[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性但不提供客户端验证。</span><span class="sxs-lookup"><span data-stu-id="2a990-165">The [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) attribute provides similar functionality to the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute but doesn't provide client side validation.</span></span>

<span data-ttu-id="2a990-166">运行应用程序，然后单击**学生**选项卡。你收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="2a990-166">Run the application and click the **Students** tab. You get the following error:</span></span>

<span data-ttu-id="2a990-167">*创建数据库后，支持 SchoolContext 上下文的模型已更改。请考虑使用 Code First 迁移来更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。*</span><span class="sxs-lookup"><span data-stu-id="2a990-167">*The model backing the 'SchoolContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*</span></span>

<span data-ttu-id="2a990-168">数据库模型已更改需要在数据库架构中，更改的方式，实体框架检测到的。</span><span class="sxs-lookup"><span data-stu-id="2a990-168">The database model has changed in a way that requires a change in the database schema, and Entity Framework detected that.</span></span> <span data-ttu-id="2a990-169">将使用迁移来更新架构，而不会丢失任何数据，使用 UI 添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="2a990-169">You'll use migrations to update the schema without losing any data that you added to the database by using the UI.</span></span> <span data-ttu-id="2a990-170">如果更改由创建的数据`Seed`方法，将更改回其原始状态由于[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法中使用`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="2a990-170">If you changed data that was created by the `Seed` method, that will be changed back to its original state because of the [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) method that you're using in the `Seed` method.</span></span> <span data-ttu-id="2a990-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)等效于"upsert"操作从数据库术语中。)</span><span class="sxs-lookup"><span data-stu-id="2a990-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) is equivalent to an "upsert" operation from database terminology.)</span></span>

<span data-ttu-id="2a990-172">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2a990-172">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

<span data-ttu-id="2a990-173">`add-migration`命令创建名为的文件*&lt;时间戳&gt;\_MaxLengthOnNames.cs*。</span><span class="sxs-lookup"><span data-stu-id="2a990-173">The `add-migration` command creates a file named *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*.</span></span> <span data-ttu-id="2a990-174">此文件包含 `Up` 方法中的代码，该代码将更新数据库以匹配当前数据模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-174">This file contains code in the `Up` method that will update the database to match the current data model.</span></span> <span data-ttu-id="2a990-175">`update-database` 命令运行该代码。</span><span class="sxs-lookup"><span data-stu-id="2a990-175">The `update-database` command ran that code.</span></span>

<span data-ttu-id="2a990-176">Entity Framework 使用迁移文件名前面预置的时间戳进行排序的迁移。</span><span class="sxs-lookup"><span data-stu-id="2a990-176">The timestamp prepended to the migrations file name is used by Entity Framework to order the migrations.</span></span> <span data-ttu-id="2a990-177">您可以创建多个迁移，然后再运行`update-database`命令和所有迁移都应用中已创建的顺序。</span><span class="sxs-lookup"><span data-stu-id="2a990-177">You can create multiple migrations before running the `update-database` command, and then all of the migrations are applied in the order in which they were created.</span></span>

<span data-ttu-id="2a990-178">运行**创建**页上，然后输入名称超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="2a990-178">Run the **Create** page, and enter either name longer than 50 characters.</span></span> <span data-ttu-id="2a990-179">当您单击**创建**，客户端端验证会显示一条错误消息：*姓氏字段必须是具有最大长度为 50 的字符串。*</span><span class="sxs-lookup"><span data-stu-id="2a990-179">When you click **Create**, client side validation shows an error message: *The field LastName must be a string with a maximum length of 50.*</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="2a990-180">列属性</span><span class="sxs-lookup"><span data-stu-id="2a990-180">The Column Attribute</span></span>

<span data-ttu-id="2a990-181">还可使用特性来控制类和属性映射到数据库的方式。</span><span class="sxs-lookup"><span data-stu-id="2a990-181">You can also use attributes to control how your classes and properties are mapped to the database.</span></span> <span data-ttu-id="2a990-182">假设在名字字段使用了 `FirstMidName`，这是因为该字段也可能包含中间名。</span><span class="sxs-lookup"><span data-stu-id="2a990-182">Suppose you had used the name `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span> <span data-ttu-id="2a990-183">但却希望将数据库列命名为 `FirstName`，因为要针对数据库编写即席查询的用户习惯使用该姓名。</span><span class="sxs-lookup"><span data-stu-id="2a990-183">But you want the database column to be named `FirstName`, because users who will be writing ad-hoc queries against the database are accustomed to that name.</span></span> <span data-ttu-id="2a990-184">若要进行此映射，可使用 `Column` 特性。</span><span class="sxs-lookup"><span data-stu-id="2a990-184">To make this mapping, you can use the `Column` attribute.</span></span>

<span data-ttu-id="2a990-185">`Column` 特性指定，创建数据库时，映射到 `FirstMidName` 属性的 `Student` 表的列将被命名为 `FirstName`。</span><span class="sxs-lookup"><span data-stu-id="2a990-185">The `Column` attribute specifies that when the database is created, the column of the `Student` table that maps to the `FirstMidName` property will be named `FirstName`.</span></span> <span data-ttu-id="2a990-186">换言之，在代码引用 `Student.FirstMidName` 时，数据来源将是 `Student` 表的 `FirstName` 列或在其中进行更新。</span><span class="sxs-lookup"><span data-stu-id="2a990-186">In other words, when your code refers to `Student.FirstMidName`, the data will come from or be updated in the `FirstName` column of the `Student` table.</span></span> <span data-ttu-id="2a990-187">如果未指定列名称，系统会提供名称与属性名称相同。</span><span class="sxs-lookup"><span data-stu-id="2a990-187">If you don't specify column names, they are given the same name as the property name.</span></span>

<span data-ttu-id="2a990-188">在中*Student.cs*文件中，添加`using`语句[System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) ，并添加到列名称特性`FirstMidName`属性，如中所示以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-188">In the *Student.cs* file, add a `using` statement for [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) and add the column name attribute to the `FirstMidName` property, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

<span data-ttu-id="2a990-189">添加了[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)更改备份 SchoolContext，因此它不会与数据库匹配的模型。</span><span class="sxs-lookup"><span data-stu-id="2a990-189">The addition of the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) changes the model backing the SchoolContext, so it won't match the database.</span></span> <span data-ttu-id="2a990-190">在 PMC 创建另一个迁移中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2a990-190">Enter the following commands in the PMC to create another migration:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

<span data-ttu-id="2a990-191">在中**服务器资源管理器**，打开*学生*表设计器通过双击*学生*表。</span><span class="sxs-lookup"><span data-stu-id="2a990-191">In **Server Explorer**, open the *Student* table designer by double-clicking the *Student* table.</span></span>

<span data-ttu-id="2a990-192">下图显示的原始列名称之前应用的前两个迁移。</span><span class="sxs-lookup"><span data-stu-id="2a990-192">The following image shows the original column name as it was before you applied the first two migrations.</span></span> <span data-ttu-id="2a990-193">除了从更改的列名称`FirstMidName`到`FirstName`，从已更改的两个名称列`MAX`长度为 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="2a990-193">In addition to the column name changing from `FirstMidName` to `FirstName`, the two name columns have changed from `MAX` length to 50 characters.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="2a990-194">您还可以进行数据库映射更改使用[Fluent API](https://msdn.microsoft.com/data/jj591617)，正如您将看到在本教程的后面。</span><span class="sxs-lookup"><span data-stu-id="2a990-194">You can also make database mapping changes using the [Fluent API](https://msdn.microsoft.com/data/jj591617), as you'll see later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="2a990-195">如果尚未按以下各节所述创建所有实体类就尝试进行编译，则可能会出现编译器错误。</span><span class="sxs-lookup"><span data-stu-id="2a990-195">If you try to compile before you finish creating all of the entity classes in the following sections, you might get compiler errors.</span></span>

## <a name="update-student-entity"></a><span data-ttu-id="2a990-196">更新 Student 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-196">Update Student entity</span></span>

<span data-ttu-id="2a990-197">在中*Models\Student.cs*，添加的代码之前替换以下代码。</span><span class="sxs-lookup"><span data-stu-id="2a990-197">In *Models\Student.cs*, replace the code you added earlier with the following code.</span></span> <span data-ttu-id="2a990-198">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="2a990-198">The changes are highlighted.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a><span data-ttu-id="2a990-199">所需的属性</span><span class="sxs-lookup"><span data-stu-id="2a990-199">The Required Attribute</span></span>

<span data-ttu-id="2a990-200">[所需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)使名称属性必填的字段。</span><span class="sxs-lookup"><span data-stu-id="2a990-200">The [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) makes the name properties required fields.</span></span> <span data-ttu-id="2a990-201">`Required attribute`不需要值类型，如 DateTime、 int、 double、 和 float。</span><span class="sxs-lookup"><span data-stu-id="2a990-201">The `Required attribute` is not needed for value types such as DateTime, int, double, and float.</span></span> <span data-ttu-id="2a990-202">值类型无法将分配一个 null 值，因此它们本质上是被视为必填字段。</span><span class="sxs-lookup"><span data-stu-id="2a990-202">Value types cannot be assigned a null value, so they are inherently treated as required fields.</span></span> <span data-ttu-id="2a990-203">无法删除[所需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)并将其替换的最小长度参数为`StringLength`属性：</span><span class="sxs-lookup"><span data-stu-id="2a990-203">You could remove the [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) and replace it with a minimum length parameter for the `StringLength` attribute:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

### <a name="the-display-attribute"></a><span data-ttu-id="2a990-204">Display 特性</span><span class="sxs-lookup"><span data-stu-id="2a990-204">The Display Attribute</span></span>

<span data-ttu-id="2a990-205">`Display` 特性指定文本框的标题应是“名”、“姓”、“全名”和“注册日期”，而不是每个实例中的属性名称（其中没有分隔单词的空格）。</span><span class="sxs-lookup"><span data-stu-id="2a990-205">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date" instead of the property name in each instance (which has no space dividing the words).</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="2a990-206">FullName 计算属性</span><span class="sxs-lookup"><span data-stu-id="2a990-206">The FullName Calculated Property</span></span>

<span data-ttu-id="2a990-207">`FullName` 是计算属性，可返回通过串联两个其他属性创建的值。</span><span class="sxs-lookup"><span data-stu-id="2a990-207">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="2a990-208">因此只有`get`访问器，但没有`FullName`将在数据库中生成列。</span><span class="sxs-lookup"><span data-stu-id="2a990-208">Therefore it has only a `get` accessor, and no `FullName` column will be generated in the database.</span></span>

## <a name="create-instructor-entity"></a><span data-ttu-id="2a990-209">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-209">Create Instructor entity</span></span>

<span data-ttu-id="2a990-210">创建*Models\Instructor.cs*，模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-210">Create *Models\Instructor.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="2a990-211">请注意，`Student` 和 `Instructor` 实体中具有几个相同属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-211">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="2a990-212">本系列后面的[实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程将重构此代码以消除冗余。</span><span class="sxs-lookup"><span data-stu-id="2a990-212">In the [Implementing Inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series, you'll refactor this code to eliminate the redundancy.</span></span>

<span data-ttu-id="2a990-213">因此您也可以编写 instructor 类，如下所示，可以在同一行，将多个属性：</span><span class="sxs-lookup"><span data-stu-id="2a990-213">You can put multiple attributes on one line, so you could also write the instructor class as follows:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a><span data-ttu-id="2a990-214">课程和 OfficeAssignment 导航属性</span><span class="sxs-lookup"><span data-stu-id="2a990-214">The Courses and OfficeAssignment Navigation Properties</span></span>

<span data-ttu-id="2a990-215">`Courses` 和 `OfficeAssignment` 是导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-215">The `Courses` and `OfficeAssignment` properties are navigation properties.</span></span> <span data-ttu-id="2a990-216">如前所述，它们通常定义为[虚拟](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，以便他们可以利用名为实体框架功能[延迟加载](https://msdn.microsoft.com/magazine/hh205756.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a990-216">As was explained earlier, they are typically defined as [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) so that they can take advantage of an Entity Framework feature called [lazy loading](https://msdn.microsoft.com/magazine/hh205756.aspx).</span></span> <span data-ttu-id="2a990-217">此外，如果导航属性可以包含多个实体，其类型必须实现[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="2a990-217">In addition, if a navigation property can hold multiple entities, its type must implement the [ICollection&lt;T&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface.</span></span> <span data-ttu-id="2a990-218">例如[IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)但不是限定[IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx)因为`IEnumerable<T>`不会实现[添加](https://msdn.microsoft.com/library/63ywd54z.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a990-218">For example [IList&lt;T&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifies but not [IEnumerable&lt;T&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) because `IEnumerable<T>` doesn't implement [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).</span></span>

<span data-ttu-id="2a990-219">一名讲师可以教授任意数量的课程，因此`Courses`定义为一系列`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-219">An instructor can teach any number of courses, so `Courses` is defined as a collection of `Course` entities.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="2a990-220">我们的业务规则规定一名讲师只能具有最多一个办公室，因此`OfficeAssignment`定义为单个`OfficeAssignment`实体 (这可能会`null`如果没有 office 分配)。</span><span class="sxs-lookup"><span data-stu-id="2a990-220">Our business rules state an instructor can only have at most one office, so `OfficeAssignment` is defined as a single `OfficeAssignment` entity (which may be `null` if no office is assigned).</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a><span data-ttu-id="2a990-221">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-221">Create OfficeAssignment entity</span></span>

<span data-ttu-id="2a990-222">创建*Models\OfficeAssignment.cs*使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-222">Create *Models\OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="2a990-223">生成项目时，该操作将保存所做的更改并确认没有进行任何复制并粘贴编译器可以捕获的错误。</span><span class="sxs-lookup"><span data-stu-id="2a990-223">Build the project, which saves your changes and verifies you haven't made any copy and paste errors the compiler can catch.</span></span>

### <a name="the-key-attribute"></a><span data-ttu-id="2a990-224">键属性</span><span class="sxs-lookup"><span data-stu-id="2a990-224">The Key Attribute</span></span>

<span data-ttu-id="2a990-225">对零或一一之间没有关系`Instructor`和`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-225">There's a one-to-zero-or-one relationship between the `Instructor` and the `OfficeAssignment` entities.</span></span> <span data-ttu-id="2a990-226">分配到办公室的讲师相关才存在办公室分配，因此其主键也是其外的键`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-226">An office assignment only exists in relation to the instructor it's assigned to, and therefore its primary key is also its foreign key to the `Instructor` entity.</span></span> <span data-ttu-id="2a990-227">但 Entity Framework 无法自动识别`InstructorID`作为主要因为其名称不符合此实体的键`ID`或*classname* `ID`命名约定。</span><span class="sxs-lookup"><span data-stu-id="2a990-227">But the Entity Framework can't automatically recognize `InstructorID` as the primary key of this entity because its name doesn't follow the `ID` or *classname* `ID` naming convention.</span></span> <span data-ttu-id="2a990-228">因此，`Key` 特性用于将其识别为主键：</span><span class="sxs-lookup"><span data-stu-id="2a990-228">Therefore, the `Key` attribute is used to identify it as the key:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="2a990-229">此外可以使用`Key`属性如果实体具有其自己的主键，但你想要属性名称不同于`classnameID`或`ID`。</span><span class="sxs-lookup"><span data-stu-id="2a990-229">You can also use the `Key` attribute if the entity does have its own primary key but you want to name the property something different than `classnameID` or `ID`.</span></span> <span data-ttu-id="2a990-230">默认情况下 EF 将键视为非数据库生成因为该列面向的是识别关系。</span><span class="sxs-lookup"><span data-stu-id="2a990-230">By default EF treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-foreignkey-attribute"></a><span data-ttu-id="2a990-231">ForeignKey 属性</span><span class="sxs-lookup"><span data-stu-id="2a990-231">The ForeignKey Attribute</span></span>

<span data-ttu-id="2a990-232">当两个实体之间的一对一关系或一对零或一一种关系 (如`OfficeAssignment`和`Instructor`)，EF 不能计算出的关系的哪一端是主体，依赖哪一端。</span><span class="sxs-lookup"><span data-stu-id="2a990-232">When there is a one-to-zero-or-one relationship or a one-to-one relationship between two entities (such as between `OfficeAssignment` and `Instructor`), EF can't work out which end of the relationship is the principal and which end is dependent.</span></span> <span data-ttu-id="2a990-233">一对一关系中与其他类的每个类具有引用导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-233">One-to-one relationships have a reference navigation property in each class to the other class.</span></span> <span data-ttu-id="2a990-234">[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以应用于相关的类来建立此关系。</span><span class="sxs-lookup"><span data-stu-id="2a990-234">The [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) can be applied to the dependent class to establish the relationship.</span></span> <span data-ttu-id="2a990-235">如果省略[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，当你尝试创建迁移时出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="2a990-235">If you omit the [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), you get the following error when you try to create the migration:</span></span>

<span data-ttu-id="2a990-236">*无法确定类型 ContosoUniversity.Models.OfficeAssignment 和 ContosoUniversity.Models.Instructor 之间的关联的主体端。此关联的主体端必须使用的关系 fluent API 或数据批注进行显式配置。*</span><span class="sxs-lookup"><span data-stu-id="2a990-236">*Unable to determine the principal end of an association between the types 'ContosoUniversity.Models.OfficeAssignment' and 'ContosoUniversity.Models.Instructor'. The principal end of this association must be explicitly configured using either the relationship fluent API or data annotations.*</span></span>

<span data-ttu-id="2a990-237">在本教程后面你将了解如何使用 fluent API 配置此关系。</span><span class="sxs-lookup"><span data-stu-id="2a990-237">Later in the tutorial you'll see how to configure this relationship with the fluent API.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="2a990-238">Instructor 导航属性</span><span class="sxs-lookup"><span data-stu-id="2a990-238">The Instructor Navigation Property</span></span>

<span data-ttu-id="2a990-239">`Instructor`实体具有一个可以为 null`OfficeAssignment`导航属性 （因为一名讲师可能没有办公室分配），并`OfficeAssignment`实体具有不可为 null`Instructor`导航属性 （因为办公室分配不能没有讲师-`InstructorID`不可为 null)。</span><span class="sxs-lookup"><span data-stu-id="2a990-239">The `Instructor` entity has a nullable `OfficeAssignment` navigation property (because an instructor might not have an office assignment), and the `OfficeAssignment` entity has a non-nullable `Instructor` navigation property (because an office assignment can't exist without an instructor -- `InstructorID` is non-nullable).</span></span> <span data-ttu-id="2a990-240">当`Instructor`实体具有相关`OfficeAssignment`实体，每个实体都有对另一个在其导航属性的引用。</span><span class="sxs-lookup"><span data-stu-id="2a990-240">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity will have a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="2a990-241">您可以将`[Required]`Instructor 导航属性来指定必须有相关的讲师，但无需这样做是因为 InstructorID 外键 （这也是此表的关键） 是不可以为 null 的属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-241">You could put a `[Required]` attribute on the Instructor navigation property to specify that there must be a related instructor, but you don't have to do that because the InstructorID foreign key (which is also the key to this table) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="2a990-242">修改 Course 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-242">Modify the Course entity</span></span>

<span data-ttu-id="2a990-243">在中*Models\Course.cs*，添加的代码之前替换以下代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-243">In *Models\Course.cs*, replace the code you added earlier with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="2a990-244">Course 实体具有外键属性`DepartmentID`它指向相关`Department`实体，同时它具有`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-244">The course entity has a foreign key property `DepartmentID` which points to the related `Department` entity and it has a `Department` navigation property.</span></span> <span data-ttu-id="2a990-245">如果拥有相关实体的导航属性，则 Entity Framework 不会要求为数据模型添加外键属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-245">The Entity Framework doesn't require you to add a foreign key property to your data model when you have a navigation property for a related entity.</span></span> <span data-ttu-id="2a990-246">EF 会自动在数据库中创建外键在需要的位置。</span><span class="sxs-lookup"><span data-stu-id="2a990-246">EF automatically creates foreign keys in the database wherever they are needed.</span></span> <span data-ttu-id="2a990-247">但如果数据模型包含外键，则更新会变得更简单、更高效。</span><span class="sxs-lookup"><span data-stu-id="2a990-247">But having the foreign key in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="2a990-248">例如，当提取 course 实体进行编辑，请`Department`实体为 null 如果未加载它，因此当更新 course 实体，必须先提取`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-248">For example, when you fetch a course entity to edit, the `Department` entity is null if you don't load it, so when you update the course entity, you would have to first fetch the `Department` entity.</span></span> <span data-ttu-id="2a990-249">当外键属性`DepartmentID`包含在数据模型中，您无需提取`Department`实体，然后才能更新。</span><span class="sxs-lookup"><span data-stu-id="2a990-249">When the foreign key property `DepartmentID` is included in the data model, you don't need to fetch the `Department` entity before you update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="2a990-250">DatabaseGenerated 特性</span><span class="sxs-lookup"><span data-stu-id="2a990-250">The DatabaseGenerated Attribute</span></span>

<span data-ttu-id="2a990-251">[DatabaseGenerated 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)与[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)参数`CourseID`属性指定主键值是由用户提供而不是由数据库生成。</span><span class="sxs-lookup"><span data-stu-id="2a990-251">The [DatabaseGenerated attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) with the [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parameter on the `CourseID` property specifies that primary key values are provided by the user rather than generated by the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="2a990-252">默认情况下，Entity Framework 假定主键值由数据库生成。</span><span class="sxs-lookup"><span data-stu-id="2a990-252">By default, the Entity Framework assumes that primary key values are generated by the database.</span></span> <span data-ttu-id="2a990-253">大多数情况下，这是理想情况。</span><span class="sxs-lookup"><span data-stu-id="2a990-253">That's what you want in most scenarios.</span></span> <span data-ttu-id="2a990-254">但是，对于`Course`实体，您将使用用户指定的课程编号，例如 1000年系列的一个部门，另一个系为 2000年系列等。</span><span class="sxs-lookup"><span data-stu-id="2a990-254">However, for `Course` entities, you'll use a user-specified course number such as a 1000 series for one department, a 2000 series for another department, and so on.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="2a990-255">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="2a990-255">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="2a990-256">外键属性和导航属性中的`Course`实体可反映以下关系：</span><span class="sxs-lookup"><span data-stu-id="2a990-256">The foreign key properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

- <span data-ttu-id="2a990-257">向一个系分配课程后，出于上述原因，会出现 `DepartmentID` 外键和 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-257">A course is assigned to one department, so there's a `DepartmentID` foreign key and a `Department` navigation property for the reasons mentioned above.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- <span data-ttu-id="2a990-258">参与一门课程的学生数量不定，因此 `Enrollments` 导航属性是一个集合：</span><span class="sxs-lookup"><span data-stu-id="2a990-258">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- <span data-ttu-id="2a990-259">一门课程可能由多位讲师讲授，因此 `Instructors` 导航属性是一个集合：</span><span class="sxs-lookup"><span data-stu-id="2a990-259">A course may be taught by multiple instructors, so the `Instructors` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a><span data-ttu-id="2a990-260">创建 Department 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-260">Create the Department entity</span></span>

<span data-ttu-id="2a990-261">创建*Models\Department.cs*使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-261">Create *Models\Department.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a><span data-ttu-id="2a990-262">列属性</span><span class="sxs-lookup"><span data-stu-id="2a990-262">The Column Attribute</span></span>

<span data-ttu-id="2a990-263">之前用于[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)若要更改列名称映射。</span><span class="sxs-lookup"><span data-stu-id="2a990-263">Earlier you used the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) to change column name mapping.</span></span> <span data-ttu-id="2a990-264">中的代码`Department`实体，`Column`特性用于更改 SQL 数据类型映射，以便将使用 SQL Server 定义该列[资金](https://msdn.microsoft.com/library/ms179882.aspx)数据库中的类型：</span><span class="sxs-lookup"><span data-stu-id="2a990-264">In the code for the `Department` entity, the `Column` attribute is being used to change SQL data type mapping so that the column will be defined using the SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) type in the database:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="2a990-265">列映射通常不是必需的因为实体框架通常选择适当 SQL Server 数据类型为属性定义的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="2a990-265">Column mapping is generally not required, because the Entity Framework usually chooses the appropriate SQL Server data type based on the CLR type that you define for the property.</span></span> <span data-ttu-id="2a990-266">CLR `decimal` 类型会映射到 SQL Server `decimal` 类型。</span><span class="sxs-lookup"><span data-stu-id="2a990-266">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="2a990-267">但在这种情况下您知道列将包含货币金额，并[资金](https://msdn.microsoft.com/library/ms179882.aspx)数据类型是更适合。</span><span class="sxs-lookup"><span data-stu-id="2a990-267">But in this case you know that the column will be holding currency amounts, and the [money](https://msdn.microsoft.com/library/ms179882.aspx) data type is more appropriate for that.</span></span> <span data-ttu-id="2a990-268">有关 CLR 数据类型和如何与 SQL Server 数据类型的匹配的详细信息，请参阅[SqlClient 实体 FrameworkTypes](https://msdn.microsoft.com/library/bb896344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2a990-268">For more information about CLR data types and how they match to SQL Server data types, see [SqlClient for Entity FrameworkTypes](https://msdn.microsoft.com/library/bb896344.aspx).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="2a990-269">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="2a990-269">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="2a990-270">外键和导航属性可反映以下关系：</span><span class="sxs-lookup"><span data-stu-id="2a990-270">The foreign key and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="2a990-271">一个系可能有也可能没有管理员，而管理员始终是讲师。</span><span class="sxs-lookup"><span data-stu-id="2a990-271">A department may or may not have an administrator, and an administrator is always an instructor.</span></span> <span data-ttu-id="2a990-272">因此`InstructorID`属性是作为外键到包含`Instructor`实体，并将问号后添加`int`类型指派将标记为可为 null 的属性。导航属性名为`Administrator`但其中包含`Instructor`实体：</span><span class="sxs-lookup"><span data-stu-id="2a990-272">Therefore the `InstructorID` property is included as the foreign key to the `Instructor` entity, and a question mark is added after the `int` type designation to mark the property as nullable.The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- <span data-ttu-id="2a990-273">一个系可以有多门课程，因此没有`Courses`导航属性：</span><span class="sxs-lookup"><span data-stu-id="2a990-273">A department may have many courses, so there's a `Courses` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > <span data-ttu-id="2a990-274">按照约定，Entity Framework 能针对不可为 null 的外键和多对多关系启用级联删除。</span><span class="sxs-lookup"><span data-stu-id="2a990-274">By convention, the Entity Framework enables cascade delete for non-nullable foreign keys and for many-to-many relationships.</span></span> <span data-ttu-id="2a990-275">这可能导致循环级联删除规则，尝试添加迁移时该规则会造成异常。</span><span class="sxs-lookup"><span data-stu-id="2a990-275">This can result in circular cascade delete rules, which will cause an exception when you try to add a migration.</span></span> <span data-ttu-id="2a990-276">例如，如果你未定义`Department.InstructorID`为可以为 null 的属性，你会收到以下异常消息："引用关系会导致不允许的循环引用。"</span><span class="sxs-lookup"><span data-stu-id="2a990-276">For example, if you didn't define the `Department.InstructorID` property as nullable, you'd get the following exception message: "The referential relationship will result in a cyclical reference that's not allowed."</span></span> <span data-ttu-id="2a990-277">如果您的业务规则需要`InstructorID`属性设置为不可为 null，必须使用以下 fluent API 语句禁用关系的级联删除：</span><span class="sxs-lookup"><span data-stu-id="2a990-277">If your business rules required `InstructorID` property to be non-nullable, you would have to use the following fluent API statement to disable cascade delete on the relationship:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a><span data-ttu-id="2a990-278">修改 Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-278">Modify the Enrollment entity</span></span>

 <span data-ttu-id="2a990-279">在中*Models\Enrollment.cs*，添加的代码之前替换以下代码</span><span class="sxs-lookup"><span data-stu-id="2a990-279">In *Models\Enrollment.cs*, replace the code you added earlier with the following code</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="2a990-280">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="2a990-280">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="2a990-281">外键属性和导航属性可反映以下关系：</span><span class="sxs-lookup"><span data-stu-id="2a990-281">The foreign key properties and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="2a990-282">注册记录面向一门课程，因此存在 `CourseID` 外键属性和 `Course` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="2a990-282">An enrollment record is for a single course, so there's a `CourseID` foreign key property and a `Course` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- <span data-ttu-id="2a990-283">注册记录面向一名学生，因此存在 `StudentID` 外键属性和 `Student` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="2a990-283">An enrollment record is for a single student, so there's a `StudentID` foreign key property and a `Student` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a><span data-ttu-id="2a990-284">多对多关系</span><span class="sxs-lookup"><span data-stu-id="2a990-284">Many-to-Many Relationships</span></span>

<span data-ttu-id="2a990-285">没有之间的多对多关系`Student`和`Course`实体，并`Enrollment`实体用作多对多联接表*有效负载为*数据库中。</span><span class="sxs-lookup"><span data-stu-id="2a990-285">There's a many-to-many relationship between the `Student` and `Course` entities, and the `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="2a990-286">这意味着`Enrollment`表包含除联接表的外键的其他数据 (在这种情况下，主键和`Grade`属性)。</span><span class="sxs-lookup"><span data-stu-id="2a990-286">This means that the `Enrollment` table contains additional data besides foreign keys for the joined tables (in this case, a primary key and a `Grade` property).</span></span>

<span data-ttu-id="2a990-287">下图显示这些关系在实体关系图中的外观。</span><span class="sxs-lookup"><span data-stu-id="2a990-287">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="2a990-288">(使用生成此关系图[Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); 创建此关系图不是本教程的一部分，只需使用此处为举例说明。)</span><span class="sxs-lookup"><span data-stu-id="2a990-288">(This diagram was generated using the [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); creating the diagram isn't part of the tutorial, it's just being used here as an illustration.)</span></span>

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="2a990-290">每条关系线都为 1，另一端星号 (\*) 在另一个，指示一个对多关系。</span><span class="sxs-lookup"><span data-stu-id="2a990-290">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="2a990-291">如果`Enrollment`表不包含年级信息，它只需包含两个外键`CourseID`和`StudentID`。</span><span class="sxs-lookup"><span data-stu-id="2a990-291">If the `Enrollment` table didn't include grade information, it would only need to contain the two foreign keys `CourseID` and `StudentID`.</span></span> <span data-ttu-id="2a990-292">在这种情况下，它将对应的多对多联接表*不带有效负载*(或*纯联接表*) 在数据库中，并且不会有根本为它创建的模型类。</span><span class="sxs-lookup"><span data-stu-id="2a990-292">In that case, it would correspond to a many-to-many join table *without payload* (or a *pure join table*) in the database, and you wouldn't have to create a model class for it at all.</span></span> <span data-ttu-id="2a990-293">`Instructor`和`Course`实体都有这种多对多关系，并且正如您所看到的它们之间没有实体类：</span><span class="sxs-lookup"><span data-stu-id="2a990-293">The `Instructor` and `Course` entities have that kind of many-to-many relationship, and as you can see, there is no entity class between them:</span></span>

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="2a990-295">但是在数据库中，需要联接表，如以下数据库关系图中所示：</span><span class="sxs-lookup"><span data-stu-id="2a990-295">A join table is required in the database, however, as shown in the following database diagram:</span></span>

![Instructor-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="2a990-297">实体框架会自动创建`CourseInstructor`表，并且您读取和更新到通过读取和更新的间接`Instructor.Courses`和`Course.Instructors`导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-297">The Entity Framework automatically creates the `CourseInstructor` table, and you read and update it indirectly by reading and updating the `Instructor.Courses` and `Course.Instructors` navigation properties.</span></span>

## <a name="entity-relationship-diagram"></a><span data-ttu-id="2a990-298">实体关系图</span><span class="sxs-lookup"><span data-stu-id="2a990-298">Entity relationship diagram</span></span>

<span data-ttu-id="2a990-299">下图显示 Entity Framework Power Tools 针对已完成的学校模型创建的关系图。</span><span class="sxs-lookup"><span data-stu-id="2a990-299">The following illustration shows the diagram that the Entity Framework Power Tools create for the completed School model.</span></span>

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="2a990-301">除了多对多关系线 (\*到\*) 和一个对多关系线 (1 到\*)，您可以看到对零或一一的关系线 (1 到 0..1) 之间`Instructor`和`OfficeAssignment`实体和 0-或--一对多关系线 (0..1 到\*) 之间的 Instructor 和 Department 实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-301">Besides the many-to-many relationship lines (\* to \*) and the one-to-many relationship lines (1 to \*), you can see here the one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities and the zero-or-one-to-many relationship line (0..1 to \*) between the Instructor and Department entities.</span></span>

## <a name="add-code-to-database-context"></a><span data-ttu-id="2a990-302">将代码添加到数据库上下文</span><span class="sxs-lookup"><span data-stu-id="2a990-302">Add code to database context</span></span>

<span data-ttu-id="2a990-303">接下来将添加到新的实体`SchoolContext`类，并自定义映射使用的某些[fluent API](https://msdn.microsoft.com/data/jj591617)调用。</span><span class="sxs-lookup"><span data-stu-id="2a990-303">Next you'll add the new entities to the `SchoolContext` class and customize some of the mapping using [fluent API](https://msdn.microsoft.com/data/jj591617) calls.</span></span> <span data-ttu-id="2a990-304">API 是"fluent"，因为它通常用于按顺序排列的一系列方法调用连接成单个语句，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="2a990-304">The API is "fluent" because it's often used by stringing a series of method calls together into a single statement, as in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

<span data-ttu-id="2a990-305">在本教程将使用 fluent API，仅对数据库不能使用特性实现的映射。</span><span class="sxs-lookup"><span data-stu-id="2a990-305">In this tutorial you'll use the fluent API only for database mapping that you can't do with attributes.</span></span> <span data-ttu-id="2a990-306">但 Fluent API 还可用于指定大多数格式化、验证和映射规则，这可通过特性完成。</span><span class="sxs-lookup"><span data-stu-id="2a990-306">However, you can also use the fluent API to specify most of the formatting, validation, and mapping rules that you can do by using attributes.</span></span> <span data-ttu-id="2a990-307">`MinimumLength` 等特性不能通过 Fluent API 应用。</span><span class="sxs-lookup"><span data-stu-id="2a990-307">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="2a990-308">如前所述，`MinimumLength`不会更改架构，它仅应用客户端和服务器端验证规则</span><span class="sxs-lookup"><span data-stu-id="2a990-308">As mentioned previously, `MinimumLength` doesn't change the schema, it only applies a client and server side validation rule</span></span>

<span data-ttu-id="2a990-309">某些开发者倾向于仅使用 Fluent API 以保持实体类的“纯净”。</span><span class="sxs-lookup"><span data-stu-id="2a990-309">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="2a990-310">如有需要，可混合使用特性和 Fluent API，且有些自定义只能通过 Fluent API 实现，但通常建议选择一种方法并尽可能坚持使用这一种。</span><span class="sxs-lookup"><span data-stu-id="2a990-310">You can mix attributes and fluent API if you want, and there are a few customizations that can only be done by using fluent API, but in general the recommended practice is to choose one of these two approaches and use that consistently as much as possible.</span></span>

<span data-ttu-id="2a990-311">若要添加的新实体的数据建模和执行数据库没有做通过使用特性的映射中的代码替换*DAL\SchoolContext.cs*使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="2a990-311">To add the new entities to the data model and perform database mapping that you didn't do by using attributes, replace the code in *DAL\SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="2a990-312">中的新语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法配置多对多联接表：</span><span class="sxs-lookup"><span data-stu-id="2a990-312">The new statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method configures the many-to-many join table:</span></span>

- <span data-ttu-id="2a990-313">之间的多对多关系`Instructor`和`Course`实体，该代码指定联接表的表和列名称。</span><span class="sxs-lookup"><span data-stu-id="2a990-313">For the many-to-many relationship between the `Instructor` and `Course` entities, the code specifies the table and column names for the join table.</span></span> <span data-ttu-id="2a990-314">代码首先可以配置多对多关系，而无需此代码，但如果不调用它，则会默认名称如`InstructorInstructorID`为`InstructorID`列。</span><span class="sxs-lookup"><span data-stu-id="2a990-314">Code First can configure the many-to-many relationship for you without this code, but if you don't call it, you will get default names such as `InstructorInstructorID` for the `InstructorID` column.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="2a990-315">以下代码举例说明如何您可以使用 fluent API 而不是属性来指定之间的关系`Instructor`和`OfficeAssignment`实体：</span><span class="sxs-lookup"><span data-stu-id="2a990-315">The following code provides an example of how you could have used fluent API instead of attributes to specify the relationship between the `Instructor` and `OfficeAssignment` entities:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

<span data-ttu-id="2a990-316">有关"fluent API"语句会在后台执行的操作的信息，请参阅[Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx)博客文章。</span><span class="sxs-lookup"><span data-stu-id="2a990-316">For information about what "fluent API" statements are doing behind the scenes, see the [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog post.</span></span>

## <a name="seed-database-with-test-data"></a><span data-ttu-id="2a990-317">使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="2a990-317">Seed database with test data</span></span>

<span data-ttu-id="2a990-318">中的代码替换*migrations\ configuration.cs*文件与以下代码，以便为已创建的新实体提供种子数据。</span><span class="sxs-lookup"><span data-stu-id="2a990-318">Replace the code in the *Migrations\Configuration.cs* file with the following code in order to provide seed data for the new entities you've created.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

<span data-ttu-id="2a990-319">如您所看到的第一个教程中，此代码的大部分只需更新或创建新实体对象并将示例数据加载到所需的测试的属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-319">As you saw in the first tutorial, most of this code simply updates or creates new entity objects and loads sample data into properties as required for testing.</span></span> <span data-ttu-id="2a990-320">但请注意如何`Course`具有多对多关系的实体与`Instructor`实体，进行处理：</span><span class="sxs-lookup"><span data-stu-id="2a990-320">However, notice how the `Course` entity, which has a many-to-many relationship with the `Instructor` entity, is handled:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

<span data-ttu-id="2a990-321">当您创建`Course`对象，初始化`Instructors`导航属性为空集合使用的代码`Instructors = new List<Instructor>()`。</span><span class="sxs-lookup"><span data-stu-id="2a990-321">When you create a `Course` object, you initialize the `Instructors` navigation property as an empty collection using the code `Instructors = new List<Instructor>()`.</span></span> <span data-ttu-id="2a990-322">这样就可以添加`Instructor`与此相关的实体`Course`通过使用`Instructors.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="2a990-322">This makes it possible to add `Instructor` entities that are related to this `Course` by using the `Instructors.Add` method.</span></span> <span data-ttu-id="2a990-323">如果未创建一个空列表，您将无法添加这些关系，因为`Instructors`属性将为 null，并且不会有`Add`方法。</span><span class="sxs-lookup"><span data-stu-id="2a990-323">If you didn't create an empty list, you wouldn't be able to add these relationships, because the `Instructors` property would be null and wouldn't have an `Add` method.</span></span> <span data-ttu-id="2a990-324">您也可以添加到构造函数的列表初始化。</span><span class="sxs-lookup"><span data-stu-id="2a990-324">You could also add the list initialization to the constructor.</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="2a990-325">添加迁移</span><span class="sxs-lookup"><span data-stu-id="2a990-325">Add a migration</span></span>

<span data-ttu-id="2a990-326">在 PMC 中，输入`add-migration`命令 (不执行操作`update-database`命令):</span><span class="sxs-lookup"><span data-stu-id="2a990-326">From the PMC, enter the `add-migration` command (don't do the `update-database` command yet):</span></span>

`add-Migration ComplexDataModel`

<span data-ttu-id="2a990-327">如果此时尝试运行 `update-database` 命令（先不要执行此操作），则会出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="2a990-327">If you tried to run the `update-database` command at this point (don't do it yet), you would get the following error:</span></span>

<span data-ttu-id="2a990-328">*ALTER TABLE 语句与 FOREIGN KEY 约束冲突"FK\_dbo。课程\_dbo。部门\_DepartmentID"。冲突发生于数据库"ContosoUniversity"表"dbo。部门"，列 DepartmentID。*</span><span class="sxs-lookup"><span data-stu-id="2a990-328">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Course\_dbo.Department\_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.*</span></span>

<span data-ttu-id="2a990-329">有时在执行迁移的现有数据时，需将存根 （stub） 数据插入到数据库，满足外键约束，这也必须立即执行操作。</span><span class="sxs-lookup"><span data-stu-id="2a990-329">Sometimes when you execute migrations with existing data, you need to insert stub data into the database to satisfy foreign key constraints, and that's what you have to do now.</span></span> <span data-ttu-id="2a990-330">生成的代码中 ComplexDataModel`Up`方法将添加不可为 null`DepartmentID`外键的`Course`表。</span><span class="sxs-lookup"><span data-stu-id="2a990-330">The generated code in the ComplexDataModel `Up` method adds a non-nullable `DepartmentID` foreign key to the `Course` table.</span></span> <span data-ttu-id="2a990-331">因为已经有了中的行`Course`表的代码运行时，`AddColumn`操作将失败，因为 SQL Server 不知道要放入不能为 null 的列的值。</span><span class="sxs-lookup"><span data-stu-id="2a990-331">Because there are already rows in the `Course` table when the code runs, the `AddColumn` operation will fail because SQL Server doesn't know what value to put in the column that can't be null.</span></span> <span data-ttu-id="2a990-332">因此需要更改代码来为新列默认值，并创建名为"Temp"作为默认系的存根 （stub） 部门。</span><span class="sxs-lookup"><span data-stu-id="2a990-332">Therefore have to change the code to give the new column a default value, and create a stub department named "Temp" to act as the default department.</span></span> <span data-ttu-id="2a990-333">因此，现有`Course`行将所有与"Temp"系建立联系后`Up`方法运行。</span><span class="sxs-lookup"><span data-stu-id="2a990-333">As a result, existing `Course` rows will all be related to the "Temp" department after the `Up` method runs.</span></span> <span data-ttu-id="2a990-334">可以与中的正确部门`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="2a990-334">You can relate them to the correct departments in the `Seed` method.</span></span>

<span data-ttu-id="2a990-335">编辑&lt;*时间戳&gt;\_ComplexDataModel.cs*文件，注释掉的代码将 DepartmentID 列添加到 Course 表行，并添加以下突出显示的代码 （在注释行也会突出显示）：</span><span class="sxs-lookup"><span data-stu-id="2a990-335">Edit the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, comment out the line of code that adds the DepartmentID column to the Course table, and add the following highlighted code (the commented line is also highlighted):</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

<span data-ttu-id="2a990-336">当`Seed`方法运行时，它将插入中的行`Department`表和它将与现有`Course`到这些新行`Department`行。</span><span class="sxs-lookup"><span data-stu-id="2a990-336">When the `Seed` method runs, it will insert rows in the `Department` table and it will relate existing `Course` rows to those new `Department` rows.</span></span> <span data-ttu-id="2a990-337">如果尚未在 UI 中添加任何课程，然后不再需要"Temp"系或默认值上`Course.DepartmentID`列。</span><span class="sxs-lookup"><span data-stu-id="2a990-337">If you haven't added any courses in the UI, you would then no longer need the "Temp" department or the default value on the `Course.DepartmentID` column.</span></span> <span data-ttu-id="2a990-338">若要允许，有人可能已添加课程使用应用程序的可能性，您还想要更新`Seed`方法代码，以确保所有`Course`行 (而不仅仅是由早期运行的插入`Seed`方法) 具有有效`DepartmentID`值之前删除默认列中的值并删除"Temp"系。</span><span class="sxs-lookup"><span data-stu-id="2a990-338">To allow for the possibility that someone might have added courses by using the application, you'd also want to update the `Seed` method code to ensure that all `Course` rows (not just the ones inserted by earlier runs of the `Seed` method) have valid `DepartmentID` values before you remove the default value from the column and delete the "Temp" department.</span></span>

## <a name="update-the-database"></a><span data-ttu-id="2a990-339">更新数据库</span><span class="sxs-lookup"><span data-stu-id="2a990-339">Update the database</span></span>

<span data-ttu-id="2a990-340">完成编辑后&lt;*时间戳&gt;\_ComplexDataModel.cs*文件中，输入`update-database`PMC 执行迁移命令。</span><span class="sxs-lookup"><span data-stu-id="2a990-340">After you have finished editing the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, enter the `update-database` command in the PMC to execute the migration.</span></span>

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> <span data-ttu-id="2a990-341">就可以将迁移数据，也使架构更改时遇到其他错误。</span><span class="sxs-lookup"><span data-stu-id="2a990-341">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="2a990-342">如果遇到无法解决的迁移错误，你可以更改连接字符串中的数据库名称，或删除数据库。</span><span class="sxs-lookup"><span data-stu-id="2a990-342">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="2a990-343">最简单方法是在数据库重命名*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="2a990-343">The simplest approach is to rename the database in *Web.config* file.</span></span> <span data-ttu-id="2a990-344">下面的示例演示名称更改为 CU\_测试：</span><span class="sxs-lookup"><span data-stu-id="2a990-344">The following example shows the name changed to CU\_Test:</span></span>
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> <span data-ttu-id="2a990-345">使用新数据库没有数据迁移，和`update-database`命令是更有望完成且未出错。</span><span class="sxs-lookup"><span data-stu-id="2a990-345">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="2a990-346">有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="2a990-346">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span>
>
> <span data-ttu-id="2a990-347">如果失败，你可以尝试另一件事是通过在 PMC 中输入以下命令会重新初始化数据库：</span><span class="sxs-lookup"><span data-stu-id="2a990-347">If that fails, another thing you can try is re-initialize the database by entering the following command in the PMC:</span></span>
>
> `update-database -TargetMigration:0`

<span data-ttu-id="2a990-348">打开中的数据库**服务器资源管理器**像前面，并展开**表**节点以查看是否已创建的所有表。</span><span class="sxs-lookup"><span data-stu-id="2a990-348">Open the database in **Server Explorer** as you did earlier, and expand the **Tables** node to see that all of the tables have been created.</span></span> <span data-ttu-id="2a990-349">(如果仍有**服务器资源管理器**从较早的时间打开，请单击**刷新**按钮。)</span><span class="sxs-lookup"><span data-stu-id="2a990-349">(If you still have **Server Explorer** open from the earlier time, click the **Refresh** button.)</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

<span data-ttu-id="2a990-350">未创建的模型类`CourseInstructor`表。</span><span class="sxs-lookup"><span data-stu-id="2a990-350">You didn't create a model class for the `CourseInstructor` table.</span></span> <span data-ttu-id="2a990-351">如前面所述，这是一个联接表之间的多对多关系`Instructor`和`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="2a990-351">As explained earlier, this is a join table for the many-to-many relationship between the `Instructor` and `Course` entities.</span></span>

<span data-ttu-id="2a990-352">右键单击`CourseInstructor`表，然后选择**显示表数据**以确认它在其中为具有数据`Instructor`添加到实体`Course.Instructors`导航属性。</span><span class="sxs-lookup"><span data-stu-id="2a990-352">Right-click the `CourseInstructor` table and select **Show Table Data** to verify that it has data in it as a result of the `Instructor` entities you added to the `Course.Instructors` navigation property.</span></span>

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a><span data-ttu-id="2a990-354">获取代码</span><span class="sxs-lookup"><span data-stu-id="2a990-354">Get the code</span></span>

[<span data-ttu-id="2a990-355">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="2a990-355">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="2a990-356">其他资源</span><span class="sxs-lookup"><span data-stu-id="2a990-356">Additional resources</span></span>

<span data-ttu-id="2a990-357">其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="2a990-357">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a990-358">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2a990-358">Next steps</span></span>

<span data-ttu-id="2a990-359">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="2a990-359">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a990-360">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="2a990-360">Customized the data model</span></span>
> * <span data-ttu-id="2a990-361">已更新的 Student 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-361">Updated Student entity</span></span>
> * <span data-ttu-id="2a990-362">已创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-362">Created Instructor entity</span></span>
> * <span data-ttu-id="2a990-363">已创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-363">Created OfficeAssignment entity</span></span>
> * <span data-ttu-id="2a990-364">修改 Course 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-364">Modified the Course entity</span></span>
> * <span data-ttu-id="2a990-365">创建 Department 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-365">Created the Department entity</span></span>
> * <span data-ttu-id="2a990-366">修改 Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="2a990-366">Modified the Enrollment entity</span></span>
> * <span data-ttu-id="2a990-367">为数据库上下文添加的代码</span><span class="sxs-lookup"><span data-stu-id="2a990-367">Added code to database context</span></span>
> * <span data-ttu-id="2a990-368">已使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="2a990-368">Seeded database with test data</span></span>
> * <span data-ttu-id="2a990-369">已添加迁移</span><span class="sxs-lookup"><span data-stu-id="2a990-369">Added a migration</span></span>
> * <span data-ttu-id="2a990-370">已更新数据库</span><span class="sxs-lookup"><span data-stu-id="2a990-370">Updated the database</span></span>

<span data-ttu-id="2a990-371">转到下一步的文章，了解如何读取和显示 Entity Framework 加载到导航属性的相关的数据。</span><span class="sxs-lookup"><span data-stu-id="2a990-371">Advance to the next article to learn how to read and display related data that the Entity Framework loads into navigation properties.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a990-372">读取相关数据</span><span class="sxs-lookup"><span data-stu-id="2a990-372">Read related data</span></span>](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

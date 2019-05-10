---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 使用数据批注验证程序 (VB) 验证 |Microsoft Docs
author: microsoft
description: 充分利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。 了解如何使用不同类型的验证程序...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117578"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="336bf-104">使用数据注释验证程序进行验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="336bf-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="336bf-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="336bf-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="336bf-106">充分利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="336bf-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="336bf-107">了解如何使用不同类型的验证程序属性和 Microsoft 实体框架中处理它们。</span><span class="sxs-lookup"><span data-stu-id="336bf-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="336bf-108">在本教程中，您将学习如何使用数据批注验证程序在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="336bf-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="336bf-109">使用数据批注验证程序的优点是它们使您能够执行验证，只需通过添加一个或多个属性 – 例如，Required 或 StringLength 属性 – 目标设定为类属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="336bf-110">可以使用数据批注验证程序之前，必须下载数据批注模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="336bf-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="336bf-111">可以通过单击从 CodePlex 网站下载数据批注模型绑定器示例[此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)。</span><span class="sxs-lookup"><span data-stu-id="336bf-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="336bf-112">请务必了解数据批注模型联编程序不是 Microsoft ASP.NET MVC 框架的正式组成部分。</span><span class="sxs-lookup"><span data-stu-id="336bf-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="336bf-113">尽管数据批注模型联编程序由 Microsoft ASP.NET MVC 团队创建的但 Microsoft 不提供对数据批注模型联编程序的官方产品支持所述和本教程中使用。</span><span class="sxs-lookup"><span data-stu-id="336bf-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="336bf-114">使用数据批注模型联编程序</span><span class="sxs-lookup"><span data-stu-id="336bf-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="336bf-115">若要在 ASP.NET MVC 应用程序中使用数据批注模型联编程序，首先需要添加对该 Microsoft.Web.Mvc.DataAnnotations.dll 程序集 System.ComponentModel.DataAnnotations.dll 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="336bf-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="336bf-116">选择菜单选项**项目中，添加引用**。</span><span class="sxs-lookup"><span data-stu-id="336bf-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="336bf-117">接下来，单击**浏览**选项卡上，浏览到下载 （并解压缩） 数据批注模型联编程序示例的位置 (请参阅**图 1**)。</span><span class="sxs-lookup"><span data-stu-id="336bf-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="336bf-118">**图 1**:添加对数据批注模型联编程序的引用 ([单击此项可查看原尺寸图像](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="336bf-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="336bf-119">选择 Microsoft.Web.Mvc.DataAnnotations.dll 程序集和 System.ComponentModel.DataAnnotations.dll 程序集，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="336bf-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="336bf-120">不能使用与数据批注模型联编程序的.NET Framework Service Pack 1 中包含的 System.ComponentModel.DataAnnotations.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="336bf-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="336bf-121">您必须使用数据批注模型绑定器示例下载中包含的 System.ComponentModel.DataAnnotations.dll 程序集的版本。</span><span class="sxs-lookup"><span data-stu-id="336bf-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="336bf-122">最后，您需要在 Global.asax 文件中注册 DataAnnotations 模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="336bf-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="336bf-123">将以下代码行添加到应用程序\_start （） 事件处理程序，以便应用程序\_start （） 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="336bf-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="336bf-124">这行代码将 DataAnnotationsModelBinder 注册为整个 ASP.NET MVC 应用程序的默认模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="336bf-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="336bf-125">使用数据注释验证程序属性</span><span class="sxs-lookup"><span data-stu-id="336bf-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="336bf-126">当您使用数据批注模型联编程序时，使用验证程序属性来执行验证。</span><span class="sxs-lookup"><span data-stu-id="336bf-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="336bf-127">System.ComponentModel.DataAnnotations 命名空间包含以下验证程序属性：</span><span class="sxs-lookup"><span data-stu-id="336bf-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="336bf-128">范围-可以验证是否属性的值介于指定的值范围之间。</span><span class="sxs-lookup"><span data-stu-id="336bf-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="336bf-129">正则表达式 – 可以验证是否属性的值与指定正则表达式模式相匹配。</span><span class="sxs-lookup"><span data-stu-id="336bf-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="336bf-130">所需 – 使你能够将标记为必需属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="336bf-131">StringLength – 可用于指定字符串属性的最大长度。</span><span class="sxs-lookup"><span data-stu-id="336bf-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="336bf-132">验证-所有验证程序属性的基类。</span><span class="sxs-lookup"><span data-stu-id="336bf-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="336bf-133">如果验证需求不满足任何标准的验证程序然后始终必须通过从基本的验证特性继承新的验证程序属性创建自定义验证程序属性的选项。</span><span class="sxs-lookup"><span data-stu-id="336bf-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="336bf-134">中的产品类**清单 1**演示了如何使用这些验证程序属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="336bf-135">名称、 说明和 UnitPrice 属性标记所需的方式。</span><span class="sxs-lookup"><span data-stu-id="336bf-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="336bf-136">名称属性必须是少于 10 个字符的字符串长度。</span><span class="sxs-lookup"><span data-stu-id="336bf-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="336bf-137">最后，UnitPrice 属性必须与表示货币金额的正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="336bf-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="336bf-138">**代码清单 1**:Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="336bf-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="336bf-139">Product 类说明了如何使用一个附加属性： DisplayName 属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="336bf-140">DisplayName 属性，可修改的属性的名称，当属性显示在一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="336bf-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="336bf-141">而不是显示错误消息"单价字段必填"可以显示错误消息"价格字段是必填"。</span><span class="sxs-lookup"><span data-stu-id="336bf-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="336bf-142">如果你想要完全自定义验证程序显示的错误消息然后可以将此类验证程序的 ErrorMessage 属性分配自定义错误消息： `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="336bf-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="336bf-143">可以使用中的产品类**清单 1** create （） 控制器操作中使用**代码清单 2**。</span><span class="sxs-lookup"><span data-stu-id="336bf-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="336bf-144">模型状态包含的任何错误时，此控制器操作重新显示创建视图。</span><span class="sxs-lookup"><span data-stu-id="336bf-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="336bf-145">**代码清单 2**:Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="336bf-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="336bf-146">最后，您可以创建中的视图**清单 3**右键单击 create （） 操作并选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="336bf-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="336bf-147">作为模型类使用 Product 类来创建强类型化视图。</span><span class="sxs-lookup"><span data-stu-id="336bf-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="336bf-148">选择**创建**视图内容的下拉列表中 (请参阅**图 2**)。</span><span class="sxs-lookup"><span data-stu-id="336bf-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="336bf-149">**图 2**:添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="336bf-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="336bf-150">**代码清单 3**:Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="336bf-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="336bf-151">从生成的创建表单中删除 Id 字段**添加视图**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="336bf-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="336bf-152">Id 字段对应于一个标识列，因为您不想允许用户输入此字段的值。</span><span class="sxs-lookup"><span data-stu-id="336bf-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="336bf-153">如果提交的窗体创建产品，并且不执行操作的必填字段，输入值则中的验证错误消息**图 3**显示。</span><span class="sxs-lookup"><span data-stu-id="336bf-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="336bf-154">**图 3**:缺少必填的字段</span><span class="sxs-lookup"><span data-stu-id="336bf-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="336bf-155">如果输入无效的货币金额，则中的错误消息**图 4**显示。</span><span class="sxs-lookup"><span data-stu-id="336bf-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="336bf-156">**图 4**:无效的货币金额</span><span class="sxs-lookup"><span data-stu-id="336bf-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="336bf-157">通过 Entity Framework 使用数据批注验证程序</span><span class="sxs-lookup"><span data-stu-id="336bf-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="336bf-158">如果使用 Microsoft 实体框架来生成模型的数据类不能将验证程序特性应用直接向您的类。</span><span class="sxs-lookup"><span data-stu-id="336bf-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="336bf-159">由于实体框架设计器生成的模型类，的下次在设计器中进行任何更改将覆盖在 model 类的任何更改。</span><span class="sxs-lookup"><span data-stu-id="336bf-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="336bf-160">如果你想要使用实体框架生成的类中使用验证程序然后您需要创建元数据类。</span><span class="sxs-lookup"><span data-stu-id="336bf-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="336bf-161">将验证程序应用于元数据类，而不是应用的实际类验证程序。</span><span class="sxs-lookup"><span data-stu-id="336bf-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="336bf-162">例如，假设您创建使用实体框架的 Movie 类 (请参阅**图 5**)。</span><span class="sxs-lookup"><span data-stu-id="336bf-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="336bf-163">此外，假设你想要使电影标题和主管属性所需的属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="336bf-164">在这种情况下，可以创建的分部类和元数据类中的**清单 4**。</span><span class="sxs-lookup"><span data-stu-id="336bf-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="336bf-165">**图 5**:实体框架所生成的 movie 类</span><span class="sxs-lookup"><span data-stu-id="336bf-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="336bf-166">**列表 4**:Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="336bf-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="336bf-167">中的文件**清单 4**包含名为电影和 MovieMetaData 的两个类。</span><span class="sxs-lookup"><span data-stu-id="336bf-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="336bf-168">Movie 类是分部类。</span><span class="sxs-lookup"><span data-stu-id="336bf-168">The Movie class is a partial class.</span></span> <span data-ttu-id="336bf-169">它对应于由 DataModel.Designer.vb 文件中包含的实体框架生成的分部类。</span><span class="sxs-lookup"><span data-stu-id="336bf-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="336bf-170">目前，.NET framework 不支持部分属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="336bf-171">因此，没有办法将验证程序特性应用于电影类 DataModel.Designer.vb 文件来将验证程序特性应用到在文件中定义的 Movie 类的属性定义的属性**清单 4**.</span><span class="sxs-lookup"><span data-stu-id="336bf-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="336bf-172">请注意，使用指向 MovieMetaData 类利用 MetadataType 特性修饰的电影分部类。</span><span class="sxs-lookup"><span data-stu-id="336bf-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="336bf-173">MovieMetaData 类包含属性的 Movie 类的代理属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="336bf-174">验证程序属性应用于 MovieMetaData 类的属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="336bf-175">所有标记为必需属性的标题、 总监和 DateReleased 属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="336bf-176">必须将总监属性分配一个字符串，包含不超过 5 个字符。</span><span class="sxs-lookup"><span data-stu-id="336bf-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="336bf-177">最后，DisplayName 特性应用于 DateReleased 属性来显示错误消息，例如"日期已发布字段是必需"。</span><span class="sxs-lookup"><span data-stu-id="336bf-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="336bf-178">而不是错误"DateReleased 字段是必需。"</span><span class="sxs-lookup"><span data-stu-id="336bf-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="336bf-179">请注意，不需要 MovieMetaData 类中的代理属性来表示相同的 Movie 类中的相应属性类型。</span><span class="sxs-lookup"><span data-stu-id="336bf-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="336bf-180">例如，主管属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="336bf-181">中的页**图 6**说明了电影属性的输入无效值时返回的错误消息。</span><span class="sxs-lookup"><span data-stu-id="336bf-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="336bf-182">**图 6**:通过 Entity Framework 使用验证程序 ([单击此项可查看原尺寸图像](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="336bf-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="336bf-183">总结</span><span class="sxs-lookup"><span data-stu-id="336bf-183">Summary</span></span>

<span data-ttu-id="336bf-184">在本教程中，您学习了如何利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="336bf-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="336bf-185">您学习了如何使用不同类型的验证程序属性，例如，Required 和 StringLength 属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="336bf-186">您还学习了如何使用 Microsoft 实体框架时使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="336bf-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="336bf-187">上一篇</span><span class="sxs-lookup"><span data-stu-id="336bf-187">Previous</span></span>](validating-with-a-service-layer-vb.md)

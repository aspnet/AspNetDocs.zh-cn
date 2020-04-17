---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 使用数据注释验证器 （VB） 进行验证 |微软文档
author: rick-anderson
description: 利用数据注释模型绑定器在 mVC 应用程序中执行验证ASP.NET。 了解如何使用不同类型的验证器...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542633"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="23fc3-104">使用数据注释验证程序进行验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="23fc3-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="23fc3-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="23fc3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="23fc3-106">利用数据注释模型绑定器在 mVC 应用程序中执行验证ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="23fc3-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="23fc3-107">了解如何使用不同类型的验证器属性，并在 Microsoft 实体框架中使用它们。</span><span class="sxs-lookup"><span data-stu-id="23fc3-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="23fc3-108">在本教程中，您将了解如何使用数据注释验证器在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="23fc3-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="23fc3-109">使用数据注释验证器的优点是，它们仅通过向类属性添加一个或多个属性（如"必需"或"字符串长度"属性）即可执行验证。</span><span class="sxs-lookup"><span data-stu-id="23fc3-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="23fc3-110">在使用数据注释验证器之前，必须下载数据注释模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="23fc3-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="23fc3-111">您可以通过[单击此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)从 CodePlex 网站下载数据注释模型粘合剂示例。</span><span class="sxs-lookup"><span data-stu-id="23fc3-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="23fc3-112">请务必了解，数据注释模型绑定器不是 Microsoft ASP.NET MVC 框架的正式部分。</span><span class="sxs-lookup"><span data-stu-id="23fc3-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="23fc3-113">尽管数据注释模型活页夹是由 Microsoft ASP.NET MVC 团队创建的，但 Microsoft 不会为本教程中介绍和使用的数据注释模型粘合剂提供官方产品支持。</span><span class="sxs-lookup"><span data-stu-id="23fc3-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="23fc3-114">使用数据注释模型绑定器</span><span class="sxs-lookup"><span data-stu-id="23fc3-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="23fc3-115">为了在ASP.NET MVC 应用程序中使用数据注释模型绑定器，首先需要添加对 Microsoft.Web.Mvc.Dataannotations.dll 程序集和 System.组件模型.Datathethe.dll 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="23fc3-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="23fc3-116">选择菜单选项 **"项目"，添加参考**。</span><span class="sxs-lookup"><span data-stu-id="23fc3-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="23fc3-117">接下来，单击 **"浏览"** 选项卡并浏览到下载（并解压缩）数据注释模型装订器示例的位置（参见**图 1）。**</span><span class="sxs-lookup"><span data-stu-id="23fc3-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="23fc3-118">**图 1**： 添加对数据注释模型装订器的引用 （[单击以查看全尺寸图像](validation-with-the-data-annotation-validators-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="23fc3-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="23fc3-119">同时选择 Microsoft.Web.Mvc.Data注释.dll 程序集和系统.组件模型.DataAnnotations.dll 程序集，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="23fc3-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="23fc3-120">不能使用系统.组件模型.Data注释.dll 程序集包含在 .NET 框架服务包 1 与数据注释模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="23fc3-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="23fc3-121">您必须使用系统版本.组件模型.Data注释.dll 程序集包含在数据注释模型装订器示例下载中。</span><span class="sxs-lookup"><span data-stu-id="23fc3-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="23fc3-122">最后，您需要在 Global.asax 文件中注册 DataAnnotations 模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="23fc3-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="23fc3-123">将以下代码行添加到应用程序\_Start（） 事件处理程序，以便应用程序\_Start（） 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="23fc3-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="23fc3-124">此代码行将 DataAnnotationsModelBinder 注册为整个ASP.NET MVC 应用程序的默认模型活页夹。</span><span class="sxs-lookup"><span data-stu-id="23fc3-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="23fc3-125">使用数据注释验证器属性</span><span class="sxs-lookup"><span data-stu-id="23fc3-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="23fc3-126">使用数据注释模型装订器时，可以使用验证器属性执行验证。</span><span class="sxs-lookup"><span data-stu-id="23fc3-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="23fc3-127">系统.组件模型.Data注释命名空间包括以下验证器属性：</span><span class="sxs-lookup"><span data-stu-id="23fc3-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="23fc3-128">范围 – 使您能够验证属性的值是否介于指定的值范围之间。</span><span class="sxs-lookup"><span data-stu-id="23fc3-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="23fc3-129">正则表达式 – 使您能够验证属性的值是否与指定的正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="23fc3-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="23fc3-130">必需 = 使您能够根据需要标记属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="23fc3-131">字符串长度 – 使您能够为字符串属性指定最大长度。</span><span class="sxs-lookup"><span data-stu-id="23fc3-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="23fc3-132">验证 = 所有验证器属性的基类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="23fc3-133">如果任何标准验证器未满足验证需求，则始终可以选择通过从基本验证属性继承新的验证器属性来创建自定义验证器属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="23fc3-134">**清单1**中的"产品"类说明了如何使用这些验证器属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="23fc3-135">名称、说明和单价属性按要求进行标记。</span><span class="sxs-lookup"><span data-stu-id="23fc3-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="23fc3-136">Name 属性的字符串长度必须小于 10 个字符。</span><span class="sxs-lookup"><span data-stu-id="23fc3-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="23fc3-137">最后，UnitPrice 属性必须匹配表示货币金额的正则表达式模式。</span><span class="sxs-lookup"><span data-stu-id="23fc3-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="23fc3-138">**清单1**：型号\Product.vb</span><span class="sxs-lookup"><span data-stu-id="23fc3-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="23fc3-139">"产品"类说明了如何使用一个附加属性：显示名称属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="23fc3-140">在错误消息中显示属性时，显示Name 属性允许您修改属性的名称。</span><span class="sxs-lookup"><span data-stu-id="23fc3-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="23fc3-141">您可以显示错误消息"需要价格"，而不是显示错误消息"需要价格"</span><span class="sxs-lookup"><span data-stu-id="23fc3-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="23fc3-142">如果要完全自定义验证器显示的错误消息，则可以将自定义错误消息分配给验证器的 ErrorMessage 属性，如下所示：`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="23fc3-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="23fc3-143">您可以将**清单 1**中的"产品"类与**清单 2**中的 Create（） 控制器操作一起使用。</span><span class="sxs-lookup"><span data-stu-id="23fc3-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="23fc3-144">当模型状态包含任何错误时，此控制器操作重新显示"创建"视图。</span><span class="sxs-lookup"><span data-stu-id="23fc3-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="23fc3-145">**清单2**：控制器\产品控制器.vb</span><span class="sxs-lookup"><span data-stu-id="23fc3-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="23fc3-146">最后，您可以通过右键单击 Create（） 操作并选择菜单选项 **"添加视图**"来在**清单 3**中创建视图。</span><span class="sxs-lookup"><span data-stu-id="23fc3-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="23fc3-147">创建以 Product 类为模型类的强类型视图。</span><span class="sxs-lookup"><span data-stu-id="23fc3-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="23fc3-148">从视图内容下拉列表中**选择"创建**"（参见**图 2**）。</span><span class="sxs-lookup"><span data-stu-id="23fc3-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="23fc3-149">**图 2**： 添加创建视图</span><span class="sxs-lookup"><span data-stu-id="23fc3-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="23fc3-150">**清单3**：视图\产品\创建.aspx</span><span class="sxs-lookup"><span data-stu-id="23fc3-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="23fc3-151">从"**添加视图"** 菜单选项生成的"创建窗体"中删除"Id"字段。</span><span class="sxs-lookup"><span data-stu-id="23fc3-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="23fc3-152">由于 Id 字段对应于标识列，因此您不希望允许用户输入此字段的值。</span><span class="sxs-lookup"><span data-stu-id="23fc3-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="23fc3-153">如果提交表单以创建产品，并且未输入所需字段的值，则将显示**图 3**中的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="23fc3-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="23fc3-154">**图 3**：缺少必填字段</span><span class="sxs-lookup"><span data-stu-id="23fc3-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="23fc3-155">如果输入无效的货币金额，则将显示**图 4**中的错误消息。</span><span class="sxs-lookup"><span data-stu-id="23fc3-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="23fc3-156">**图4**：无效货币金额</span><span class="sxs-lookup"><span data-stu-id="23fc3-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="23fc3-157">将数据注释验证器与实体框架一起使用</span><span class="sxs-lookup"><span data-stu-id="23fc3-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="23fc3-158">如果使用 Microsoft 实体框架生成数据模型类，则无法将验证器属性直接应用于类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="23fc3-159">由于实体框架设计器生成模型类，因此下次在设计器中进行任何更改时，将对模型类所做的任何更改都将被覆盖。</span><span class="sxs-lookup"><span data-stu-id="23fc3-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="23fc3-160">如果要将验证器与实体框架生成的类一起使用，则需要创建元数据类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="23fc3-161">将验证器应用于元数据类，而不是将验证器应用于实际类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="23fc3-162">例如，假设您已使用实体框架创建了 Movie 类（参见**图 5**）。</span><span class="sxs-lookup"><span data-stu-id="23fc3-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="23fc3-163">此外，假设您要使影片标题和导演属性成为所需的属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="23fc3-164">在这种情况下，您可以在**清单 4**中创建部分类和元数据类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="23fc3-165">**图 5**： 实体框架生成的影片类</span><span class="sxs-lookup"><span data-stu-id="23fc3-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="23fc3-166">**清单4**：模型_Movie.vb</span><span class="sxs-lookup"><span data-stu-id="23fc3-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="23fc3-167">**清单4**中的文件包含名为"电影"和"MovieMetaData"的两个类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="23fc3-168">"影片"类是部分类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-168">The Movie class is a partial class.</span></span> <span data-ttu-id="23fc3-169">它对应于数据模型.Designer.vb 文件中包含的实体框架生成的部分类。</span><span class="sxs-lookup"><span data-stu-id="23fc3-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="23fc3-170">目前，.NET 框架不支持部分属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="23fc3-171">因此，无法通过将验证器属性应用于**清单 4**中文件中定义的 Movie 类的属性，从而将验证器属性应用于 DataModel.designer.vb 文件中定义的 Movie 类的属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="23fc3-172">请注意，影片部分类用指向 MovieMetaData 类的元数据类型属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="23fc3-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="23fc3-173">MovieMetaData 类包含影片类属性的代理属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="23fc3-174">验证器属性应用于 MovieMetaData 类的属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="23fc3-175">标题、控制器和日期释放属性都标记为必需属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="23fc3-176">必须为 Director 属性分配包含少于 5 个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="23fc3-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="23fc3-177">最后，显示Name 属性应用于 Date 下达属性，以显示错误消息，如"需要发布日期发布"字段。</span><span class="sxs-lookup"><span data-stu-id="23fc3-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="23fc3-178">而不是错误"需要日期释放字段"。</span><span class="sxs-lookup"><span data-stu-id="23fc3-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="23fc3-179">请注意，MovieMetaData 类中的代理属性不需要表示与 Movie 类中的相应属性相同的类型。</span><span class="sxs-lookup"><span data-stu-id="23fc3-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="23fc3-180">例如，Director 属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="23fc3-181">**图 6**中的页面演示了在为 Movie 属性输入无效值时返回的错误消息。</span><span class="sxs-lookup"><span data-stu-id="23fc3-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="23fc3-182">**图 6**： 使用验证器与实体框架 （[单击以查看全尺寸图像](validation-with-the-data-annotation-validators-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="23fc3-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="23fc3-183">总结</span><span class="sxs-lookup"><span data-stu-id="23fc3-183">Summary</span></span>

<span data-ttu-id="23fc3-184">在本教程中，您学习了如何使用数据注释模型绑定器在ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="23fc3-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="23fc3-185">您学习了如何使用不同类型的验证器属性，如"必需"和"字符串长度"属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="23fc3-186">在使用 Microsoft 实体框架时，您还学习了如何使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="23fc3-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="23fc3-187">上一篇</span><span class="sxs-lookup"><span data-stu-id="23fc3-187">Previous</span></span>](validating-with-a-service-layer-vb.md)

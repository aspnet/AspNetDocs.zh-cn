---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 将验证添加到模型 (C#) |Microsoft Docs
author: Rick-Anderson
description: 创建控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: d6ad229775da61544d2d97e75b291d158e79af87
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130148"
---
# <a name="adding-validation-to-the-model-c"></a><span data-ttu-id="19e0d-103">向模型添加验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="19e0d-103">Adding Validation to the Model (C#)</span></span>

<span data-ttu-id="19e0d-104">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="19e0d-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="19e0d-105">本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="19e0d-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="19e0d-106">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="19e0d-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="19e0d-107">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="19e0d-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="19e0d-108">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="19e0d-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="19e0d-109">可以通过单击以下链接安装所有这些：[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="19e0d-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="19e0d-110">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="19e0d-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="19e0d-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="19e0d-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="19e0d-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="19e0d-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="19e0d-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="19e0d-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="19e0d-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，请通过单击以下链接安装必备组件：[Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="19e0d-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="19e0d-115">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="19e0d-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="19e0d-116">[下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="19e0d-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="19e0d-117">如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="19e0d-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="19e0d-118">在本部分中，你将添加到的验证逻辑`Movie`模型，并确保每次用户尝试创建或编辑电影使用应用程序时，强制的验证规则。</span><span class="sxs-lookup"><span data-stu-id="19e0d-118">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="19e0d-119">DRY 地保管东西</span><span class="sxs-lookup"><span data-stu-id="19e0d-119">Keeping Things DRY</span></span>

<span data-ttu-id="19e0d-120">ASP.NET MVC 的核心设计原则之一是 DRY （"不要自我重复"）。</span><span class="sxs-lookup"><span data-stu-id="19e0d-120">One of the core design tenets of ASP.NET MVC is DRY ("Don't Repeat Yourself").</span></span> <span data-ttu-id="19e0d-121">ASP.NET MVC 支持你指定的功能或行为只有一次，然后让它应用到整个应用程序中。</span><span class="sxs-lookup"><span data-stu-id="19e0d-121">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="19e0d-122">这可以减少需要编写的代码量，并使您编写的代码执行操作变得更加容易维护。</span><span class="sxs-lookup"><span data-stu-id="19e0d-122">This reduces the amount of code you need to write and makes the code you do write much easier to maintain.</span></span>

<span data-ttu-id="19e0d-123">由 ASP.NET MVC 和 Entity Framework Code First 提供的验证支持是 DRY 原则在操作中的一个极好示例。</span><span class="sxs-lookup"><span data-stu-id="19e0d-123">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="19e0d-124">在一个位置 （在模型类中） 以声明方式指定验证规则，然后这些规则是所有位置强制执行应用程序中。</span><span class="sxs-lookup"><span data-stu-id="19e0d-124">You can declaratively specify validation rules in one place (in the model class) and then those rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="19e0d-125">让我们看看电影应用程序中，您就可以充分利用此验证支持。</span><span class="sxs-lookup"><span data-stu-id="19e0d-125">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="19e0d-126">向电影模型添加验证规则</span><span class="sxs-lookup"><span data-stu-id="19e0d-126">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="19e0d-127">您将首先添加到某些验证逻辑`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="19e0d-127">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="19e0d-128">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="19e0d-128">Open the *Movie.cs* file.</span></span> <span data-ttu-id="19e0d-129">添加`using`语句引用的文件的顶部[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间：</span><span class="sxs-lookup"><span data-stu-id="19e0d-129">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="19e0d-130">命名空间是.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="19e0d-130">The namespace is part of the .NET Framework.</span></span> <span data-ttu-id="19e0d-131">它提供了一组内置验证特性，可以以声明方式应用于任何类或属性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-131">It provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="19e0d-132">现在，更新`Movie`类，以充分利用内置[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，并且[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性.</span><span class="sxs-lookup"><span data-stu-id="19e0d-132">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="19e0d-133">使用以下代码作为应用特性的位置的示例。</span><span class="sxs-lookup"><span data-stu-id="19e0d-133">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

<span data-ttu-id="19e0d-134">验证特性指定要对应用这些特性的模型属性强制执行的行为。</span><span class="sxs-lookup"><span data-stu-id="19e0d-134">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="19e0d-135">`Required`属性指示属性必须具有一个值; 在此示例中，电影已具有值`Title`， `ReleaseDate`， `Genre`，和`Price`属性才有效。</span><span class="sxs-lookup"><span data-stu-id="19e0d-135">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="19e0d-136">`Range` 特性将值限制在指定范围内。</span><span class="sxs-lookup"><span data-stu-id="19e0d-136">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="19e0d-137">`StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。</span><span class="sxs-lookup"><span data-stu-id="19e0d-137">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span>

<span data-ttu-id="19e0d-138">代码首先确保之前应用程序将更改保存在数据库中实施的 model 类指定的验证规则。</span><span class="sxs-lookup"><span data-stu-id="19e0d-138">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="19e0d-139">例如，下面的代码将引发异常时`SaveChanges`调用方法，因为所需的几个`Movie`缺少属性值，价格为零 （即不在有效范围内）。</span><span class="sxs-lookup"><span data-stu-id="19e0d-139">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

<span data-ttu-id="19e0d-140">具有自动强制执行由.NET Framework 的验证规则有助于使您的应用程序更可靠。</span><span class="sxs-lookup"><span data-stu-id="19e0d-140">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="19e0d-141">同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。</span><span class="sxs-lookup"><span data-stu-id="19e0d-141">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="19e0d-142">以下是列出了已更新的完整代码*Movie.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="19e0d-142">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="19e0d-143">验证错误在 ASP.NET MVC 中的 UI</span><span class="sxs-lookup"><span data-stu-id="19e0d-143">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="19e0d-144">重新运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="19e0d-144">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="19e0d-145">单击**创建电影**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="19e0d-145">Click the **Create Movie** link to add a new movie.</span></span> <span data-ttu-id="19e0d-146">填写表单的某些无效的值，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="19e0d-146">Fill out the form with some invalid values and then click the **Create** button.</span></span>

<span data-ttu-id="19e0d-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="19e0d-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span></span>

<span data-ttu-id="19e0d-148">请注意如何在窗体具有自动使用背景色突出显示的文本框包含无效的数据和已发出每个适当的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="19e0d-148">Notice how the form has automatically used a background color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="19e0d-149">错误消息与指定带批注时的错误字符串匹配`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="19e0d-149">The error messages match the error strings you specified when you annotated the `Movie` class.</span></span> <span data-ttu-id="19e0d-150">这些错误会强制客户端 （使用 JavaScript） 和服务器端执行，（如果用户已禁用 JavaScript）。</span><span class="sxs-lookup"><span data-stu-id="19e0d-150">The errors are enforced both client-side (using JavaScript) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="19e0d-151">一个实际优点是不需要更改任何一行中的代码`MoviesController`类中或在*Create.cshtml*来启用此验证 UI 的视图。</span><span class="sxs-lookup"><span data-stu-id="19e0d-151">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="19e0d-152">控制器和自动在本教程前面创建的视图上选择的了验证规则上使用特性指定`Movie`的模型。</span><span class="sxs-lookup"><span data-stu-id="19e0d-152">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified using attributes on the `Movie` model class.</span></span>

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="19e0d-153">如何在中进行验证创建查看和创建操作方法</span><span class="sxs-lookup"><span data-stu-id="19e0d-153">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="19e0d-154">你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。</span><span class="sxs-lookup"><span data-stu-id="19e0d-154">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="19e0d-155">下一步列表显示什么`Create`中的方法`MovieController`类看起来像。</span><span class="sxs-lookup"><span data-stu-id="19e0d-155">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="19e0d-156">它们是如何在本教程前面创建它们相比没有变化。</span><span class="sxs-lookup"><span data-stu-id="19e0d-156">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

<span data-ttu-id="19e0d-157">第一个操作方法显示初始创建窗体。</span><span class="sxs-lookup"><span data-stu-id="19e0d-157">The first action method displays the initial Create form.</span></span> <span data-ttu-id="19e0d-158">第二个处理窗体 post。</span><span class="sxs-lookup"><span data-stu-id="19e0d-158">The second handles the form post.</span></span> <span data-ttu-id="19e0d-159">第二个`Create`方法调用`ModelState.IsValid`检查电影是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="19e0d-159">The second `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="19e0d-160">调用此方法将评估已应用于对象的任何验证特性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-160">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="19e0d-161">如果对象具有验证错误，`Create`方法重新显示该窗体。</span><span class="sxs-lookup"><span data-stu-id="19e0d-161">If the object has validation errors, the `Create` method redisplays the form.</span></span> <span data-ttu-id="19e0d-162">如果没有错误，此方法则将新电影保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="19e0d-162">If there are no errors, the method saves the new movie in the database.</span></span>

<span data-ttu-id="19e0d-163">下面是*Create.cshtml*基架在本教程前面部分中的视图模板。</span><span class="sxs-lookup"><span data-stu-id="19e0d-163">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="19e0d-164">以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="19e0d-164">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="19e0d-165">请注意代码如何使用`Html.EditorFor`帮助器输出`<input>`每个元素`Movie`属性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-165">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="19e0d-166">此帮助器旁边是对的调用`Html.ValidationMessageFor`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="19e0d-166">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="19e0d-167">这两个帮助器方法使用由控制器传递给视图的模型对象 (在这种情况下，`Movie`对象)。</span><span class="sxs-lookup"><span data-stu-id="19e0d-167">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="19e0d-168">它们会自动查找适当的模型和显示错误消息中指定的验证特性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-168">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="19e0d-169">有关此方法非常令人愉快的是，在控制器和创建视图模板都不知道任何有关强制实施的实际验证规则或显示的特定错误消息。</span><span class="sxs-lookup"><span data-stu-id="19e0d-169">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="19e0d-170">仅可在 `Movie` 类中指定验证规则和错误字符串。</span><span class="sxs-lookup"><span data-stu-id="19e0d-170">The validation rules and the error strings are specified only in the `Movie` class.</span></span>

<span data-ttu-id="19e0d-171">如果你想要以后更改验证逻辑，就可以做到在同一个位置。</span><span class="sxs-lookup"><span data-stu-id="19e0d-171">If you want to change the validation logic later, you can do so in exactly one place.</span></span> <span data-ttu-id="19e0d-172">无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="19e0d-172">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="19e0d-173">这使代码非常简洁，并且更易于维护和改进。</span><span class="sxs-lookup"><span data-stu-id="19e0d-173">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="19e0d-174">这意味着对 DRY 原则的完全遵守。</span><span class="sxs-lookup"><span data-stu-id="19e0d-174">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="19e0d-175">将格式添加到电影模型</span><span class="sxs-lookup"><span data-stu-id="19e0d-175">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="19e0d-176">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="19e0d-176">Open the *Movie.cs* file.</span></span> <span data-ttu-id="19e0d-177">[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供除了一组内置验证特性的格式设置属性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-177">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="19e0d-178">将应用[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性和一个[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)发布日期和价格字段的枚举值。</span><span class="sxs-lookup"><span data-stu-id="19e0d-178">You'll apply the [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute and a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="19e0d-179">下面的代码演示`ReleaseDate`并`Price`具有适当[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="19e0d-179">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

<span data-ttu-id="19e0d-180">或者，您可以显式设置[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="19e0d-180">Alternatively, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="19e0d-181">下面的代码演示了日期格式字符串的发行日期属性 (即，"d")。</span><span class="sxs-lookup"><span data-stu-id="19e0d-181">The following code shows the release date property with a date format string (namely, "d").</span></span> <span data-ttu-id="19e0d-182">将此位置用于指定你不想为时间发布日期的一部分。</span><span class="sxs-lookup"><span data-stu-id="19e0d-182">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

<span data-ttu-id="19e0d-183">下面的代码格式`Price`属性设置为货币。</span><span class="sxs-lookup"><span data-stu-id="19e0d-183">The following code formats the `Price` property as currency.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="19e0d-184">完整`Movie`类如下所示。</span><span class="sxs-lookup"><span data-stu-id="19e0d-184">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="19e0d-185">运行应用程序，并浏览到`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="19e0d-185">Run the application and browse to the `Movies` controller.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

<span data-ttu-id="19e0d-187">在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。</span><span class="sxs-lookup"><span data-stu-id="19e0d-187">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="19e0d-188">[上一页](adding-a-new-field.md)
> [下一页](improving-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="19e0d-188">[Previous](adding-a-new-field.md)
[Next](improving-the-details-and-delete-methods.md)</span></span>

---
ms.openlocfilehash: 873e399dc7bf6bf97c0925c1bdcf21f699f0be2e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057584"
---
# <a name="add-validation-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="96b0b-101">将验证添加到 ASP.NET Core MVC 应用</span><span class="sxs-lookup"><span data-stu-id="96b0b-101">Add validation to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="96b0b-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="96b0b-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="96b0b-103">在本部分中，将向 `Movie` 模型添加验证逻辑，并确保每当用户创建或编辑电影时，都会强制执行验证规则。</span><span class="sxs-lookup"><span data-stu-id="96b0b-103">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user creates or edits a movie.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="96b0b-104">坚持 DRY 原则</span><span class="sxs-lookup"><span data-stu-id="96b0b-104">Keeping things DRY</span></span>

<span data-ttu-id="96b0b-105">MVC 的设计原则之一是 [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself)（“不要自我重复”）。</span><span class="sxs-lookup"><span data-stu-id="96b0b-105">One of the design tenets of MVC is [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) ("Don't Repeat Yourself").</span></span> <span data-ttu-id="96b0b-106">ASP.NET Core MVC 支持你仅指定一次功能或行为，然后使它应用到整个应用中。</span><span class="sxs-lookup"><span data-stu-id="96b0b-106">ASP.NET Core MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an app.</span></span> <span data-ttu-id="96b0b-107">这可以减少所需编写的代码量，并使编写的代码更少出错，更易于测试和维护。</span><span class="sxs-lookup"><span data-stu-id="96b0b-107">This reduces the amount of code you need to write and makes the code you do write less error prone, easier to test, and easier to maintain.</span></span>

<span data-ttu-id="96b0b-108">MVC 和 Entity Framework Core Code First 提供的验证支持是 DRY 原则在实际操作中的极佳示例。</span><span class="sxs-lookup"><span data-stu-id="96b0b-108">The validation support provided by MVC and Entity Framework Core Code First is a good example of the DRY principle in action.</span></span> <span data-ttu-id="96b0b-109">可以在一个位置（模型类中）以声明方式指定验证规则，并且在应用中的所有位置强制执行。</span><span class="sxs-lookup"><span data-stu-id="96b0b-109">You can declaratively specify validation rules in one place (in the model class) and the rules are enforced everywhere in the app.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="96b0b-110">将验证规则添加到电影模型</span><span class="sxs-lookup"><span data-stu-id="96b0b-110">Adding validation rules to the movie model</span></span>

<span data-ttu-id="96b0b-111">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="96b0b-111">Open the *Movie.cs* file.</span></span> <span data-ttu-id="96b0b-112">DataAnnotations 提供一组内置验证特性，可通过声明方式应用于任何类或属性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-112">DataAnnotations provides a built-in set of validation attributes that you apply declaratively to any class or property.</span></span> <span data-ttu-id="96b0b-113">（它还包含 `DataType` 等格式特性，这些特性可帮助进行格式设置，但不提供任何验证。）</span><span class="sxs-lookup"><span data-stu-id="96b0b-113">(It also contains formatting attributes like `DataType` that help with formatting and don't provide any validation.)</span></span>

<span data-ttu-id="96b0b-114">更新 `Movie` 类以使用内置的 `Required`、`StringLength`、`RegularExpression` 和 `Range` 验证特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-114">Update the `Movie` class to take advantage of the built-in `Required`, `StringLength`, `RegularExpression`, and `Range` validation attributes.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="96b0b-115">验证特性指定要对应用这些特性的模型属性强制执行的行为。</span><span class="sxs-lookup"><span data-stu-id="96b0b-115">The validation attributes specify behavior that you want to enforce on the model properties they're applied to.</span></span> <span data-ttu-id="96b0b-116">`Required` 和 `MinimumLength` 特性表示属性必须有值；但用户可输入空格来满足此验证。</span><span class="sxs-lookup"><span data-stu-id="96b0b-116">The `Required` and `MinimumLength` attributes indicates that a property must have a value; but nothing prevents a user from entering white space to satisfy this validation.</span></span> <span data-ttu-id="96b0b-117">`RegularExpression` 特性用于限制可输入的字符。</span><span class="sxs-lookup"><span data-stu-id="96b0b-117">The `RegularExpression` attribute is used to limit what characters can be input.</span></span> <span data-ttu-id="96b0b-118">在上述代码中，`Genre` 和 `Rating` 必须使用纯字母（禁用首字母大写、空格、数字和特殊字符）。</span><span class="sxs-lookup"><span data-stu-id="96b0b-118">In the code above, `Genre` and `Rating` must use only letters (First letter uppercase, white space, numbers and special characters are not allowed).</span></span> <span data-ttu-id="96b0b-119">`Range` 特性将值限制在指定范围内。</span><span class="sxs-lookup"><span data-stu-id="96b0b-119">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="96b0b-120">`StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。</span><span class="sxs-lookup"><span data-stu-id="96b0b-120">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span> <span data-ttu-id="96b0b-121">从本质上来说，需要值类型（如 `decimal`、`int`、`float`、`DateTime`），但不需要 `[Required]` 特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-121">Value types (such as `decimal`, `int`, `float`, `DateTime`) are inherently required and don't need the `[Required]` attribute.</span></span>

<span data-ttu-id="96b0b-122">让 ASP.NET Core 强制自动执行验证规则有助于提升你的应用的可靠性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-122">Having validation rules automatically enforced by ASP.NET Core helps make your app more robust.</span></span> <span data-ttu-id="96b0b-123">同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。</span><span class="sxs-lookup"><span data-stu-id="96b0b-123">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

## <a name="validation-error-ui-in-mvc"></a><span data-ttu-id="96b0b-124">MVC 中的验证错误 UI</span><span class="sxs-lookup"><span data-stu-id="96b0b-124">Validation Error UI in MVC</span></span>

<span data-ttu-id="96b0b-125">运行应用并导航到电影控制器。</span><span class="sxs-lookup"><span data-stu-id="96b0b-125">Run the app and navigate to the Movies controller.</span></span>

<span data-ttu-id="96b0b-126">点击“新建”连接添加新电影的链接。</span><span class="sxs-lookup"><span data-stu-id="96b0b-126">Tap the **Create New** link to add a new movie.</span></span> <span data-ttu-id="96b0b-127">使用无效值填写表单。</span><span class="sxs-lookup"><span data-stu-id="96b0b-127">Fill out the form with some invalid values.</span></span> <span data-ttu-id="96b0b-128">当 jQuery 客户端验证检测到错误时，会显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="96b0b-128">As soon as jQuery client side validation detects the error, it displays an error message.</span></span>

![带有多个 jQuery 客户端验证错误的电影视图表单](~/tutorials/first-mvc-app/validation/_static/val.png)

[!INCLUDE[](~/includes/currency.md)]

<span data-ttu-id="96b0b-130">请注意表单如何自动呈现每个包含无效值的字段中相应的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="96b0b-130">Notice how the form has automatically rendered an appropriate validation error message in each field containing an invalid value.</span></span> <span data-ttu-id="96b0b-131">客户端（使用 JavaScript 和 jQuery）和服务器端（若用户禁用 JavaScript）都必定会遇到这些错误。</span><span class="sxs-lookup"><span data-stu-id="96b0b-131">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="96b0b-132">明显的好处在于不需要在 `MoviesController` 类或 Create.cshtml 视图中更改单个代码行来启用此验证 UI。</span><span class="sxs-lookup"><span data-stu-id="96b0b-132">A significant benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="96b0b-133">在本教程前面创建的控制器和视图会自动选取验证规则，这些规则是通过在 `Movie` 模型类的属性上使用验证特性所指定的。</span><span class="sxs-lookup"><span data-stu-id="96b0b-133">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified by using validation attributes on the properties of the `Movie` model class.</span></span> <span data-ttu-id="96b0b-134">使用 `Edit` 操作方法测试验证后，即已应用相同的验证。</span><span class="sxs-lookup"><span data-stu-id="96b0b-134">Test validation using the `Edit` action method, and the same validation is applied.</span></span>

<span data-ttu-id="96b0b-135">存在客户端验证错误时，不会将表单数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="96b0b-135">The form data isn't sent to the server until there are no client side validation errors.</span></span> <span data-ttu-id="96b0b-136">可通过使用 [Fiddler 工具](http://www.telerik.com/fiddler)或 [F12 开发人员工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)在 `HTTP Post` 方法中设置断点来对此进行验证。</span><span class="sxs-lookup"><span data-stu-id="96b0b-136">You can verify this by putting a break point in the `HTTP Post` method, by using the [Fiddler tool](http://www.telerik.com/fiddler) , or the [F12 Developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>

## <a name="how-validation-works"></a><span data-ttu-id="96b0b-137">验证工作原理</span><span class="sxs-lookup"><span data-stu-id="96b0b-137">How validation works</span></span>

<span data-ttu-id="96b0b-138">你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。</span><span class="sxs-lookup"><span data-stu-id="96b0b-138">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="96b0b-139">下列代码显示两种 `Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="96b0b-139">The following code shows the two `Create` methods.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Controllers/MoviesController.cs?name=snippetCreate)]

<span data-ttu-id="96b0b-140">第一个 (HTTP GET) `Create` 操作方法显示初始的“创建”表单。</span><span class="sxs-lookup"><span data-stu-id="96b0b-140">The first (HTTP GET) `Create` action method displays the initial Create form.</span></span> <span data-ttu-id="96b0b-141">第二个 (`[HttpPost]`) 版本处理表单发布。</span><span class="sxs-lookup"><span data-stu-id="96b0b-141">The second (`[HttpPost]`) version handles the form post.</span></span> <span data-ttu-id="96b0b-142">第二个 `Create` 方法（`[HttpPost]` 版本）调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="96b0b-142">The second `Create` method (The `[HttpPost]` version) calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="96b0b-143">调用此方法将评估已应用于对象的任何验证特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-143">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="96b0b-144">如果对象有验证错误，则 `Create` 方法会重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="96b0b-144">If the object has validation errors, the `Create` method re-displays the form.</span></span> <span data-ttu-id="96b0b-145">如果没有错误，此方法则将新电影保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="96b0b-145">If there are no errors, the method saves the new movie in the database.</span></span> <span data-ttu-id="96b0b-146">在我们的电影示例中，在检测到客户端上存在验证错误时，表单不会发布到服务器。当存在客户端验证错误时，第二个 `Create` 方法永远不会被调用。</span><span class="sxs-lookup"><span data-stu-id="96b0b-146">In our movie example, the form isn't posted to the server when there are validation errors detected on the client side; the second `Create` method is never called when there are client side validation errors.</span></span> <span data-ttu-id="96b0b-147">如果在浏览器中禁用 JavaScript，客户端验证将被禁用，而你可以测试 HTTP POST `Create` 方法 `ModelState.IsValid` 检测任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="96b0b-147">If you disable JavaScript in your browser, client validation is disabled and you can test the HTTP POST `Create` method `ModelState.IsValid` detecting any validation errors.</span></span>

<span data-ttu-id="96b0b-148">可以在 `[HttpPost] Create` 方法中设置断点，并验证方法从未被调用，客户端验证在检测到存在验证错误时不会提交表单数据。</span><span class="sxs-lookup"><span data-stu-id="96b0b-148">You can set a break point in the `[HttpPost] Create` method and verify the method is never called, client side validation won't submit the form data when validation errors are detected.</span></span> <span data-ttu-id="96b0b-149">如果在浏览器中禁用 JavaScript，然后提交错误的表单，将触发断点。</span><span class="sxs-lookup"><span data-stu-id="96b0b-149">If you disable JavaScript in your browser, then submit the form with errors, the break point will be hit.</span></span> <span data-ttu-id="96b0b-150">在没有 JavaScript 的情况下仍然可以进行完整的验证。</span><span class="sxs-lookup"><span data-stu-id="96b0b-150">You still get full validation without JavaScript.</span></span> 

<span data-ttu-id="96b0b-151">以下图片显示如何在 FireFox 浏览器中禁用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="96b0b-151">The following image shows how to disable JavaScript in the FireFox browser.</span></span>

![Firefox：在“选项”的“内容”选项卡上，取消选中“启用 Javascript”复选框。](~/tutorials/first-mvc-app/validation/_static/ff.png)

<span data-ttu-id="96b0b-153">以下图片显示如何在 Chrome 浏览器中禁用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="96b0b-153">The following image shows how to disable JavaScript in the Chrome browser.</span></span>

![Google Chrome：在“内容”设置的 Javascript 部分中，选择“不允许任何网站运行 JavaScript”。](~/tutorials/first-mvc-app/validation/_static/chrome.png)

<span data-ttu-id="96b0b-155">禁用 JavaScript 后，发布无效数据并单步执行调试程序。</span><span class="sxs-lookup"><span data-stu-id="96b0b-155">After you disable JavaScript, post invalid data and step through the debugger.</span></span>

![在对无效数据进行调试时，ModelState.IsValid 上的 Intellisense 显示值为 false。](~/tutorials/first-mvc-app/validation/_static/ms.png)

<span data-ttu-id="96b0b-157">以下是之前在本教程中已搭建基架的 Create.cshtml 视图模板的一部分。</span><span class="sxs-lookup"><span data-stu-id="96b0b-157">Below is portion of the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="96b0b-158">以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="96b0b-158">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Views/Movies/CreateRatingBrevity.cshtml)]

<span data-ttu-id="96b0b-159">[输入标记帮助程序](xref:mvc/views/working-with-forms)使用 [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 特性，并在客户端上生成 jQuery 验证所需的 HTML 特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-159">The [Input Tag Helper](xref:mvc/views/working-with-forms) uses the [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client side.</span></span> <span data-ttu-id="96b0b-160">[验证标记帮助程序](xref:mvc/views/working-with-forms#the-validation-tag-helpers)用于显示验证错误。</span><span class="sxs-lookup"><span data-stu-id="96b0b-160">The [Validation Tag Helper](xref:mvc/views/working-with-forms#the-validation-tag-helpers) displays validation errors.</span></span> <span data-ttu-id="96b0b-161">有关详细信息，请参阅[验证](xref:mvc/models/validation)。</span><span class="sxs-lookup"><span data-stu-id="96b0b-161">See [Validation](xref:mvc/models/validation) for more information.</span></span>

<span data-ttu-id="96b0b-162">此方法真正好的一点是：无论是控制器还是 `Create` 视图模板都不知道强制实施的实际验证规则或显示的特定错误消息。</span><span class="sxs-lookup"><span data-stu-id="96b0b-162">What's really nice about this approach is that neither the controller nor the `Create` view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="96b0b-163">仅可在 `Movie` 类中指定验证规则和错误字符串。</span><span class="sxs-lookup"><span data-stu-id="96b0b-163">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="96b0b-164">这些相同的验证规则自动应用于 `Edit` 视图和可能创建用于编辑模型的任何其他视图模板。</span><span class="sxs-lookup"><span data-stu-id="96b0b-164">These same validation rules are automatically applied to the `Edit` view and any other views templates you might create that edit your model.</span></span>

<span data-ttu-id="96b0b-165">需要更改验证逻辑时，可以通过将验证特性添加到模型在同一个位置实现此操作。（在此示例中为 `Movie` 类）。</span><span class="sxs-lookup"><span data-stu-id="96b0b-165">When you need to change validation logic, you can do so in exactly one place by adding validation attributes to the model (in this example, the `Movie` class).</span></span> <span data-ttu-id="96b0b-166">无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="96b0b-166">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="96b0b-167">这使代码非常简洁，并且更易于维护和改进。</span><span class="sxs-lookup"><span data-stu-id="96b0b-167">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="96b0b-168">这意味着对 DRY 原则的完全遵守。</span><span class="sxs-lookup"><span data-stu-id="96b0b-168">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="using-datatype-attributes"></a><span data-ttu-id="96b0b-169">使用 DataType 特性</span><span class="sxs-lookup"><span data-stu-id="96b0b-169">Using DataType Attributes</span></span>

<span data-ttu-id="96b0b-170">打开 Movie.cs 文件并检查 `Movie` 类。</span><span class="sxs-lookup"><span data-stu-id="96b0b-170">Open the *Movie.cs* file and examine the `Movie` class.</span></span> <span data-ttu-id="96b0b-171">除了一组内置的验证特性，`System.ComponentModel.DataAnnotations` 命名空间还提供格式特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-171">The `System.ComponentModel.DataAnnotations` namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="96b0b-172">我们已经在发布日期和价格字段中应用了 `DataType` 枚举值。</span><span class="sxs-lookup"><span data-stu-id="96b0b-172">We've already applied a `DataType` enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="96b0b-173">以下代码显示具有适当 `DataType` 特性的 `ReleaseDate` 和 `Price` 属性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-173">The following code shows the `ReleaseDate` and `Price` properties with the appropriate `DataType` attribute.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?highlight=2,6&name=snippet2)]

<span data-ttu-id="96b0b-174">`DataType` 属性仅提供相关提示来帮助视图引擎设置数据格式（并提供元素/属性，例如向 URL 提供 `<a>` 和向电子邮件提供 `<a href="mailto:EmailAddress.com">`）。</span><span class="sxs-lookup"><span data-stu-id="96b0b-174">The `DataType` attributes only provide hints for the view engine to format the data (and supplies elements/attributes such as `<a>` for URL's and `<a href="mailto:EmailAddress.com">` for email.</span></span> <span data-ttu-id="96b0b-175">可以使用 `RegularExpression` 特性验证数据的格式。</span><span class="sxs-lookup"><span data-stu-id="96b0b-175">You can use the `RegularExpression` attribute to validate the format of the data.</span></span> <span data-ttu-id="96b0b-176">`DataType` 属性用于指定比数据库内部类型更具体的数据类型，它们不是验证属性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-176">The `DataType` attribute is used to specify a data type that's more specific than the database intrinsic type, they're not validation attributes.</span></span> <span data-ttu-id="96b0b-177">在此示例中，我们只想跟踪日期，而不是时间。</span><span class="sxs-lookup"><span data-stu-id="96b0b-177">In this case we only want to keep track of the date, not the time.</span></span> <span data-ttu-id="96b0b-178">`DataType` 枚举提供了多种数据类型，例如日期、时间、电话号码、货币、电子邮件地址等。</span><span class="sxs-lookup"><span data-stu-id="96b0b-178">The `DataType` Enumeration provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress and more.</span></span> <span data-ttu-id="96b0b-179">应用程序还可通过 `DataType` 特性自动提供类型特定的功能。</span><span class="sxs-lookup"><span data-stu-id="96b0b-179">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="96b0b-180">例如，可以为 `DataType.EmailAddress` 创建 `mailto:` 链接，并且可以在支持 HTML5 的浏览器中为 `DataType.Date` 提供日期选择器。</span><span class="sxs-lookup"><span data-stu-id="96b0b-180">For example, a `mailto:` link can be created for `DataType.EmailAddress`, and a date selector can be provided for `DataType.Date` in browsers that support HTML5.</span></span> <span data-ttu-id="96b0b-181">`DataType` 特性发出 HTML 5 `data-`（读作 data dash）特性供 HTML 5 浏览器理解。</span><span class="sxs-lookup"><span data-stu-id="96b0b-181">The `DataType` attributes emit HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="96b0b-182">`DataType` 特性不提供任何验证。</span><span class="sxs-lookup"><span data-stu-id="96b0b-182">The `DataType` attributes do **not** provide any validation.</span></span>

<span data-ttu-id="96b0b-183">`DataType.Date` 不指定显示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="96b0b-183">`DataType.Date` doesn't specify the format of the date that's displayed.</span></span> <span data-ttu-id="96b0b-184">默认情况下，数据字段根据基于服务器的 `CultureInfo` 的默认格式进行显示。</span><span class="sxs-lookup"><span data-stu-id="96b0b-184">By default, the data field is displayed according to the default formats based on the server's `CultureInfo`.</span></span>

<span data-ttu-id="96b0b-185">`DisplayFormat` 特性用于显式指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="96b0b-185">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
public DateTime ReleaseDate { get; set; }
```

<span data-ttu-id="96b0b-186">`ApplyFormatInEditMode` 设置指定在文本框中显示值以进行编辑时也应用格式。</span><span class="sxs-lookup"><span data-stu-id="96b0b-186">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="96b0b-187">（你可能不想为某些字段执行此操作 — 例如对于货币值，你可能不希望文本框中的货币符号可编辑。）</span><span class="sxs-lookup"><span data-stu-id="96b0b-187">(You might not want that for some fields — for example, for currency values, you probably don't want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="96b0b-188">可以单独使用 `DisplayFormat` 特性，但通常建议使用 `DataType` 特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-188">You can use the `DisplayFormat` attribute by itself, but it's generally a good idea to use the `DataType` attribute.</span></span> <span data-ttu-id="96b0b-189">`DataType` 特性传达数据的语义而不是传达如何在屏幕上呈现数据，并提供 DisplayFormat 不具备的以下优势：</span><span class="sxs-lookup"><span data-stu-id="96b0b-189">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with DisplayFormat:</span></span>

* <span data-ttu-id="96b0b-190">浏览器可启用 HTML5 功能（例如显示日历控件、区域设置适用的货币符号、电子邮件链接等）</span><span class="sxs-lookup"><span data-stu-id="96b0b-190">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, etc.)</span></span>

* <span data-ttu-id="96b0b-191">默认情况下，浏览器将根据区域设置采用正确的格式呈现数据。</span><span class="sxs-lookup"><span data-stu-id="96b0b-191">By default, the browser will render data using the correct format based on your locale.</span></span>

* <span data-ttu-id="96b0b-192">`DataType` 特性使 MVC 能够选择正确的字段模板来呈现数据（如果 `DisplayFormat` 由自身使用，则使用的是字符串模板）。</span><span class="sxs-lookup"><span data-stu-id="96b0b-192">The `DataType` attribute can enable MVC to choose the right field template to render the data (the `DisplayFormat` if used by itself uses the string template).</span></span>

> [!NOTE]
> <span data-ttu-id="96b0b-193">jQuery 验证不适用于 `Range` 属性和 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="96b0b-193">jQuery validation doesn't work with the `Range` attribute and `DateTime`.</span></span> <span data-ttu-id="96b0b-194">例如，以下代码将始终显示客户端验证错误，即便日期在指定的范围内：</span><span class="sxs-lookup"><span data-stu-id="96b0b-194">For example, the following code will always display a client side validation error, even when the date is in the specified range:</span></span>

```csharp
[Range(typeof(DateTime), "1/1/1966", "1/1/2020")]
   ```

<span data-ttu-id="96b0b-195">需要禁用 jQuery 日期验证才能使用具有 `DateTime` 的 `Range` 特性。</span><span class="sxs-lookup"><span data-stu-id="96b0b-195">You will need to disable jQuery date validation to use the `Range` attribute with `DateTime`.</span></span> <span data-ttu-id="96b0b-196">通常，在模型中编译固定日期是不恰当的，因此不推荐使用 `Range` 特性和 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="96b0b-196">It's generally not a good practice to compile hard dates in your models, so using the `Range` attribute and `DateTime` is discouraged.</span></span>

<span data-ttu-id="96b0b-197">以下代码显示组合在一行上的特性：</span><span class="sxs-lookup"><span data-stu-id="96b0b-197">The following code shows combining attributes on one line:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="96b0b-198">在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。</span><span class="sxs-lookup"><span data-stu-id="96b0b-198">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96b0b-199">其他资源</span><span class="sxs-lookup"><span data-stu-id="96b0b-199">Additional resources</span></span>

* [<span data-ttu-id="96b0b-200">使用表单</span><span class="sxs-lookup"><span data-stu-id="96b0b-200">Working with Forms</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="96b0b-201">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="96b0b-201">Globalization and localization</span></span>](xref:fundamentals/localization)
* [<span data-ttu-id="96b0b-202">标记帮助程序简介</span><span class="sxs-lookup"><span data-stu-id="96b0b-202">Introduction to Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="96b0b-203">创作标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="96b0b-203">Author Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)

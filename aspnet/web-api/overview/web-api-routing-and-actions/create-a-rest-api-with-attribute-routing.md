---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: 使用 ASP.NET Web API 2 中的属性路由创建 REST API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188766"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="9c6bb-102">使用 ASP.NET Web API 2 中的属性路由创建 REST API</span><span class="sxs-lookup"><span data-stu-id="9c6bb-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="9c6bb-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9c6bb-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9c6bb-104">Web API 2 支持一种新的路由类型，称为*属性路由*。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="9c6bb-105">有关属性路由的一般概述，请参阅[WEB API 2 中的属性路由](attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="9c6bb-106">在本教程中，您将使用属性路由为书籍集合创建 REST API。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="9c6bb-107">该 API 将支持以下操作：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-107">The API will support the following actions:</span></span>

| <span data-ttu-id="9c6bb-108">操作</span><span class="sxs-lookup"><span data-stu-id="9c6bb-108">Action</span></span> | <span data-ttu-id="9c6bb-109">示例 URI</span><span class="sxs-lookup"><span data-stu-id="9c6bb-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="9c6bb-110">获取所有书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-110">Get a list of all books.</span></span> | <span data-ttu-id="9c6bb-111">/api/books</span><span class="sxs-lookup"><span data-stu-id="9c6bb-111">/api/books</span></span> |
| <span data-ttu-id="9c6bb-112">按 ID 获取书籍。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-112">Get a book by ID.</span></span> | <span data-ttu-id="9c6bb-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="9c6bb-113">/api/books/1</span></span> |
| <span data-ttu-id="9c6bb-114">获取书籍的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-114">Get the details of a book.</span></span> | <span data-ttu-id="9c6bb-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="9c6bb-115">/api/books/1/details</span></span> |
| <span data-ttu-id="9c6bb-116">按流派获取书籍列表。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-116">Get a list of books by genre.</span></span> | <span data-ttu-id="9c6bb-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="9c6bb-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="9c6bb-118">按发布日期获取书籍列表。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="9c6bb-119">/api/books/date/2013-02-16/api/books/date/2013/02/16 (备用形式) </span><span class="sxs-lookup"><span data-stu-id="9c6bb-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="9c6bb-120">获取特定作者的书籍列表。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="9c6bb-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="9c6bb-121">/api/authors/1/books</span></span> |

<span data-ttu-id="9c6bb-122">所有方法都是只读的 (HTTP GET 请求) 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="9c6bb-123">对于数据层，我们将使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="9c6bb-124">图书记录将具有以下字段：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="9c6bb-125">ID</span><span class="sxs-lookup"><span data-stu-id="9c6bb-125">ID</span></span>
- <span data-ttu-id="9c6bb-126">标题</span><span class="sxs-lookup"><span data-stu-id="9c6bb-126">Title</span></span>
- <span data-ttu-id="9c6bb-127">流派</span><span class="sxs-lookup"><span data-stu-id="9c6bb-127">Genre</span></span>
- <span data-ttu-id="9c6bb-128">发布日期</span><span class="sxs-lookup"><span data-stu-id="9c6bb-128">Publication date</span></span>
- <span data-ttu-id="9c6bb-129">价格</span><span class="sxs-lookup"><span data-stu-id="9c6bb-129">Price</span></span>
- <span data-ttu-id="9c6bb-130">说明</span><span class="sxs-lookup"><span data-stu-id="9c6bb-130">Description</span></span>
- <span data-ttu-id="9c6bb-131">AuthorID (作者表的外键) </span><span class="sxs-lookup"><span data-stu-id="9c6bb-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="9c6bb-132">但对于大多数请求，API 将返回此数据的子集， (标题、作者和流派) 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="9c6bb-133">若要获取完整记录，客户端将请求 `/api/books/{id}/details` 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c6bb-134">必备知识</span><span class="sxs-lookup"><span data-stu-id="9c6bb-134">Prerequisites</span></span>

<span data-ttu-id="9c6bb-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="9c6bb-136">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="9c6bb-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="9c6bb-137">首先运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-137">Start by running Visual Studio.</span></span> <span data-ttu-id="9c6bb-138">从“文件”菜单中，选择“新建”，然后选择“项目”\*\*\*\*\*\*\*\*\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="9c6bb-139">展开 "**已安装**的  >  **Visual c #** " 类别。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="9c6bb-140">在**Visual c #** 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="9c6bb-141">在项目模板列表中，选择 " \*\*ASP.NET Web 应用程序 ( .NET Framework) \*\*"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="9c6bb-142">将项目命名为 &quot; BooksAPI &quot; 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="9c6bb-143">在 "**新建 ASP.NET Web 应用程序**" 对话框中，选择 "**空**" 模板。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="9c6bb-144">在 "添加文件夹和核心引用" 下，选择 " **WEB API** " 复选框。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="9c6bb-145">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="9c6bb-146">这会创建一个为 Web API 功能配置的主干项目。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="9c6bb-147">域模型</span><span class="sxs-lookup"><span data-stu-id="9c6bb-147">Domain Models</span></span>

<span data-ttu-id="9c6bb-148">接下来，添加域模型的类。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-148">Next, add classes for domain models.</span></span> <span data-ttu-id="9c6bb-149">在解决方案资源管理器中，右键单击“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="9c6bb-150">选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="9c6bb-151">命名类 `Author`。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="9c6bb-152">将 Author.cs 中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="9c6bb-153">现在，添加另一个名为 `Book` 的类。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="9c6bb-154">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="9c6bb-154">Add a Web API Controller</span></span>

<span data-ttu-id="9c6bb-155">在此步骤中，我们将添加一个使用实体框架作为数据层的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="9c6bb-156">按 Ctrl+Shift+B 生成项目。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="9c6bb-157">实体框架使用反射来发现模型的属性，因此它需要已编译的程序集来创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="9c6bb-158">在“解决方案资源管理器”中，右键单击“控制器”文件夹。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="9c6bb-159">选择 "**添加**"，然后选择 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="9c6bb-160">在 "**添加基架**" 对话框中，选择 **"包含操作的 Web API 2 控制器"，并使用实体框架**。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="9c6bb-161">在 "**添加控制器**" 对话框中的 "**控制器名称**" 下输入 &quot; BooksController &quot; 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="9c6bb-162">选中 " &quot; 使用异步控制器操作" &quot; 复选框。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="9c6bb-163">对于 "**模型类**"，选择 " &quot; 书籍" &quot; 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="9c6bb-164"> (如果未在 `Book` 下拉列表中看到该类，请确保生成项目。 ) 然后单击 "+" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="9c6bb-165">单击 "**新建数据上下文**" 对话框中的 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="9c6bb-166">在 "**添加控制器**" 对话框中单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="9c6bb-167">基架添加一个名为 `BooksController` 的类，该类定义 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="9c6bb-168">它还会在模型文件夹中添加一个名为的类 `BooksAPIContext` ，该类定义实体框架的数据上下文。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="9c6bb-169">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="9c6bb-169">Seed the Database</span></span>

<span data-ttu-id="9c6bb-170">从 "工具" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="9c6bb-171">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="9c6bb-172">此命令创建一个迁移文件夹并添加一个名为 Configuration.cs 的新代码文件。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="9c6bb-173">打开此文件，并将以下代码添加到 `Configuration.Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="9c6bb-174">在 "包管理器控制台" 窗口中，键入以下命令。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="9c6bb-175">这些命令将创建一个本地数据库，并调用 Seed 方法来填充该数据库。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="9c6bb-176">添加 DTO 类</span><span class="sxs-lookup"><span data-stu-id="9c6bb-176">Add DTO Classes</span></span>

<span data-ttu-id="9c6bb-177">如果现在运行应用程序并将 GET 请求发送到/api/books/1，则响应类似于以下内容。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="9c6bb-178"> (添加了缩进以提高可读性。 ) </span><span class="sxs-lookup"><span data-stu-id="9c6bb-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="9c6bb-179">而是希望此请求返回字段的子集。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="9c6bb-180">此外，我希望它返回作者姓名，而不是作者 ID。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="9c6bb-181">为实现此目的，我们将修改控制器方法，以将*数据传输对象* (DTO) （而不是 EF 模型）返回。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="9c6bb-182">DTO 是仅用于携带数据的对象。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="9c6bb-183">在解决方案资源管理器中，右键单击项目并选择 "**添加**  |  **新文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="9c6bb-184">将文件夹命名为 &quot; dto &quot; 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="9c6bb-185">`BookDto`使用以下定义，将名为的类添加到 dto 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="9c6bb-186">添加名为 `BookDetailDto` 的另一个类。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="9c6bb-187">接下来，更新 `BooksController` 类以返回 `BookDto` 实例。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="9c6bb-188">我们将使用可[查询的 Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx)方法将 `Book` 实例投影到 `BookDto` 实例。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="9c6bb-189">下面是控制器类的更新代码。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="9c6bb-190">我删除了 `PutBook` 、 `PostBook` 和 `DeleteBook` 方法，因为本教程不需要它们。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="9c6bb-191">现在，如果您运行应用程序并请求/api/books/1，则响应正文应如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="9c6bb-192">添加路由属性</span><span class="sxs-lookup"><span data-stu-id="9c6bb-192">Add Route Attributes</span></span>

<span data-ttu-id="9c6bb-193">接下来，将控制器转换为使用属性路由。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="9c6bb-194">首先，将**RoutePrefix**属性添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="9c6bb-195">此属性定义此控制器上所有方法的初始 URI 段。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="9c6bb-196">然后将 **[Route]** 特性添加到控制器操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="9c6bb-197">每个控制器方法的路由模板都是前缀加上**route**特性中指定的字符串。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="9c6bb-198">对于 `GetBook` 方法，路由模板包含参数化字符串 &quot; {id： int} &quot; ，如果 URI 段包含整数值，则匹配。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="9c6bb-199">方法</span><span class="sxs-lookup"><span data-stu-id="9c6bb-199">Method</span></span> | <span data-ttu-id="9c6bb-200">路由模板</span><span class="sxs-lookup"><span data-stu-id="9c6bb-200">Route Template</span></span> | <span data-ttu-id="9c6bb-201">示例 URI</span><span class="sxs-lookup"><span data-stu-id="9c6bb-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="9c6bb-202">"api/书籍"</span><span class="sxs-lookup"><span data-stu-id="9c6bb-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="9c6bb-203">"api/书籍/{id： int}"</span><span class="sxs-lookup"><span data-stu-id="9c6bb-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="9c6bb-204">获取书籍详细信息</span><span class="sxs-lookup"><span data-stu-id="9c6bb-204">Get Book Details</span></span>

<span data-ttu-id="9c6bb-205">若要获取书籍详细信息，客户端将向发送 GET 请求 `/api/books/{id}/details` ，其中 *{id}* 是书籍的 id。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="9c6bb-206">将以下方法添加到 `BooksController` 类。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="9c6bb-207">如果请求 `/api/books/1/details` ，响应如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="9c6bb-208">按流派获取书籍</span><span class="sxs-lookup"><span data-stu-id="9c6bb-208">Get Books By Genre</span></span>

<span data-ttu-id="9c6bb-209">若要获取特定流派的书籍列表，客户端将向发送 GET 请求 `/api/books/genre` ，其中，*流派*为流派的名称。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="9c6bb-210">（例如：`/api/books/fantasy`。）</span><span class="sxs-lookup"><span data-stu-id="9c6bb-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="9c6bb-211">将以下方法添加到 `BooksController` 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="9c6bb-212">此处定义的路由包含 URI 模板中的 {流派} 参数。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="9c6bb-213">请注意，Web API 能够区分这两个 Uri 并将它们路由到不同的方法：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="9c6bb-214">这是因为该 `GetBook` 方法包含一个约束，该约束的 "id" 段必须是整数值：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="9c6bb-215">如果请求/api/books/fantasy，响应如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="9c6bb-216">按作者获取书籍</span><span class="sxs-lookup"><span data-stu-id="9c6bb-216">Get Books By Author</span></span>

<span data-ttu-id="9c6bb-217">若要获取特定作者的书籍列表，客户端将向发送 GET 请求 `/api/authors/id/books` ，其中*id*是作者的 id。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="9c6bb-218">将以下方法添加到 `BooksController` 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="9c6bb-219">此示例很有趣，因为 &quot; 书籍 &quot; 被视为作者的子 &quot; 资源 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="9c6bb-220">此模式在 RESTful Api 中非常常见。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="9c6bb-221">路由模板中的波形符 (~) 会替代**RoutePrefix**属性中的路由前缀。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="9c6bb-222">按发布日期获取书籍</span><span class="sxs-lookup"><span data-stu-id="9c6bb-222">Get Books By Publication Date</span></span>

<span data-ttu-id="9c6bb-223">若要按发布日期获取书籍列表，客户端将向发送 GET 请求 `/api/books/date/yyyy-mm-dd` ，其中*yyyy-mm-dd*为日期。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="9c6bb-224">下面是执行此操作的一种方法：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="9c6bb-225">`{pubdate:datetime}`参数被约束为与**DateTime**值匹配。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="9c6bb-226">这种方法很有效，但实际上比我们更喜欢。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="9c6bb-227">例如，这些 Uri 还会与路由匹配：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="9c6bb-228">允许这些 Uri 没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="9c6bb-229">但是，您可以通过将正则表达式约束添加到路由模板，来限制特定格式的路由：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="9c6bb-230">现在，只有 yyyy-mm-dd 格式的日期才 &quot; &quot; 匹配。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="9c6bb-231">请注意，我们不会使用 regex 来验证我们是否获得了真实的数据。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="9c6bb-232">当 Web API 尝试将 URI 分段转换为**日期时间**实例时进行处理。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="9c6bb-233">无效日期（如 "2012-47-99"）将失败，客户端将收到404错误。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="9c6bb-234">还可以 `/api/books/date/yyyy/mm/dd` 通过使用其他 regex 添加另一个 **[Route]** 属性， () 来支持斜线分隔符。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="9c6bb-235">这里有一个微妙但重要的细节。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="9c6bb-236">第二个路由模板 \* 在 {e} 参数的开头有一个通配符 () ：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="9c6bb-237">这将告知 {e} 应与 URI 的其余部分匹配的路由引擎。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="9c6bb-238">默认情况下，模板参数匹配单个 URI 段。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="9c6bb-239">在这种情况下，我们希望 {e} 跨越几个 URI 段：</span><span class="sxs-lookup"><span data-stu-id="9c6bb-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="9c6bb-240">控制器代码</span><span class="sxs-lookup"><span data-stu-id="9c6bb-240">Controller Code</span></span>

<span data-ttu-id="9c6bb-241">下面是 BooksController 类的完整代码。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="9c6bb-242">总结</span><span class="sxs-lookup"><span data-stu-id="9c6bb-242">Summary</span></span>

<span data-ttu-id="9c6bb-243">在设计 API 的 Uri 时，属性路由可提供更多控制和更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="9c6bb-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>

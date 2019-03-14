---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 创建具有 Web API 2 OData v3 终结点 |Microsoft Docs
author: MikeWasson
description: 开放数据协议 (OData) 是一种用于 web 的数据访问协议。 OData 提供统一的方法来构造数据、 查询的数据和操作的数据...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 2e0d3b45fd51192d227d852dc2f05b45ca42944c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031194"
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="ad115-104">创建具有 Web API 2 OData v3 终结点</span><span class="sxs-lookup"><span data-stu-id="ad115-104">Creating an OData v3 Endpoint with Web API 2</span></span>
====================
<span data-ttu-id="ad115-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ad115-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ad115-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="ad115-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="ad115-107">[开放数据协议](http://www.odata.org/)(OData) 是用于 web 的数据访问协议。</span><span class="sxs-lookup"><span data-stu-id="ad115-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="ad115-108">OData 提供统一的方法来构造数据、 查询的数据和操作该数据集通过 CRUD 操作 （创建、 读取、 更新和删除）。</span><span class="sxs-lookup"><span data-stu-id="ad115-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="ad115-109">OData 支持 AtomPub (XML) 和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="ad115-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="ad115-110">OData 还定义了一种方法来公开数据的元数据。</span><span class="sxs-lookup"><span data-stu-id="ad115-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="ad115-111">客户端可以使用元数据发现的类型信息和数据集的关系。</span><span class="sxs-lookup"><span data-stu-id="ad115-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="ad115-112">ASP.NET Web API 可以轻松地创建数据集的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="ad115-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="ad115-113">您可以控制完全的 OData 操作的终结点支持。</span><span class="sxs-lookup"><span data-stu-id="ad115-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="ad115-114">你可以托管多个 OData 终结点，以及非 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="ad115-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="ad115-115">您可以完全控制数据模型、 后端业务逻辑和数据层。</span><span class="sxs-lookup"><span data-stu-id="ad115-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ad115-116">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ad115-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="ad115-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ad115-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="ad115-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="ad115-118">Web API 2</span></span>
> - <span data-ttu-id="ad115-119">OData 版本 3</span><span class="sxs-lookup"><span data-stu-id="ad115-119">OData Version 3</span></span>
> - <span data-ttu-id="ad115-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ad115-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="ad115-121">Fiddler Web 调试代理 （可选）</span><span class="sxs-lookup"><span data-stu-id="ad115-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="ad115-122">中增加了 web API OData 支持[ASP.NET 和 Web Tools 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="ad115-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="ad115-123">但是，本教程使用 Visual Studio 2013 中已添加的基架。</span><span class="sxs-lookup"><span data-stu-id="ad115-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>


<span data-ttu-id="ad115-124">在本教程中，将创建一个简单的 OData 终结点的客户端可以查询。</span><span class="sxs-lookup"><span data-stu-id="ad115-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="ad115-125">您还将创建终结点的 C# 客户端。</span><span class="sxs-lookup"><span data-stu-id="ad115-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="ad115-126">完成本教程后下, 一步的系列教程介绍如何添加更多的功能，包括实体关系操作，并展开的 $/ $选择。</span><span class="sxs-lookup"><span data-stu-id="ad115-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="ad115-127">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="ad115-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="ad115-128">添加实体模型</span><span class="sxs-lookup"><span data-stu-id="ad115-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="ad115-129">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="ad115-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="ad115-130">添加的 EDM 和路由</span><span class="sxs-lookup"><span data-stu-id="ad115-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="ad115-131">（可选） 数据库中植入</span><span class="sxs-lookup"><span data-stu-id="ad115-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="ad115-132">探索 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="ad115-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="ad115-133">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="ad115-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ad115-134">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="ad115-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="ad115-135">在本教程中，将创建支持基本的 CRUD 操作的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="ad115-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="ad115-136">终结点将公开单个资源，产品列表。</span><span class="sxs-lookup"><span data-stu-id="ad115-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="ad115-137">后续教程将添加更多的功能。</span><span class="sxs-lookup"><span data-stu-id="ad115-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="ad115-138">启动 Visual Studio 并选择**新的项目**从起始页。</span><span class="sxs-lookup"><span data-stu-id="ad115-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="ad115-139">或者，从**文件**菜单中，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="ad115-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="ad115-140">在中**模板**窗格中，选择**已安装的模板**并展开 Visual C# 节点。</span><span class="sxs-lookup"><span data-stu-id="ad115-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="ad115-141">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="ad115-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="ad115-142">选择**ASP.NET Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="ad115-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="ad115-143">在中**新建 ASP.NET 项目**对话框中，选择**空**模板。</span><span class="sxs-lookup"><span data-stu-id="ad115-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="ad115-144">下&quot;添加文件夹和核心引用...&quot;，检查**Web API**。</span><span class="sxs-lookup"><span data-stu-id="ad115-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="ad115-145">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="ad115-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="ad115-146">添加实体模型</span><span class="sxs-lookup"><span data-stu-id="ad115-146">Add an Entity Model</span></span>

<span data-ttu-id="ad115-147">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="ad115-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="ad115-148">本教程中，我们需要表示产品的模型。</span><span class="sxs-lookup"><span data-stu-id="ad115-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="ad115-149">模型对应于我们的 OData 实体类型。</span><span class="sxs-lookup"><span data-stu-id="ad115-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="ad115-150">在解决方案资源管理器，右键单击模型文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad115-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="ad115-151">从上下文菜单中，选择**外**然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="ad115-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="ad115-152">在中**新添**项对话框中，类命名&quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="ad115-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="ad115-153">按照约定，模型类位于 Models 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ad115-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="ad115-154">无需遵循此约定在您自己的项目，但我们将在本教程中使用它。</span><span class="sxs-lookup"><span data-stu-id="ad115-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>


<span data-ttu-id="ad115-155">在 Product.cs 文件中，添加以下类定义：</span><span class="sxs-lookup"><span data-stu-id="ad115-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="ad115-156">ID 属性将为实体键。</span><span class="sxs-lookup"><span data-stu-id="ad115-156">The ID property will be the entity key.</span></span> <span data-ttu-id="ad115-157">客户端可以查询产品的 id。</span><span class="sxs-lookup"><span data-stu-id="ad115-157">Clients can query products by ID.</span></span> <span data-ttu-id="ad115-158">此字段也是后端数据库中的主键。</span><span class="sxs-lookup"><span data-stu-id="ad115-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="ad115-159">现在生成项目。</span><span class="sxs-lookup"><span data-stu-id="ad115-159">Build the project now.</span></span> <span data-ttu-id="ad115-160">在下一步，我们将使用一些使用反射来查找产品类型的 Visual Studio 基架。</span><span class="sxs-lookup"><span data-stu-id="ad115-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="ad115-161">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="ad115-161">Add an OData Controller</span></span>

<span data-ttu-id="ad115-162">一个*控制器*是处理 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="ad115-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="ad115-163">定义每个实体在你的 OData 服务中设置单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="ad115-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="ad115-164">在本教程中，我们将创建一个控制器。</span><span class="sxs-lookup"><span data-stu-id="ad115-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="ad115-165">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad115-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="ad115-166">选择**外**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="ad115-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="ad115-167">在中**添加基架**对话框中，选择&quot;包含 Web API 2 OData 控制器操作，使用实体框架&quot;。</span><span class="sxs-lookup"><span data-stu-id="ad115-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="ad115-168">在中**添加控制器**对话框中，将控制器"ProductsController"。</span><span class="sxs-lookup"><span data-stu-id="ad115-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="ad115-169">选择&quot;使用异步控制器操作&quot;复选框。</span><span class="sxs-lookup"><span data-stu-id="ad115-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="ad115-170">在中**模型**下拉列表中，选择 Product 类。</span><span class="sxs-lookup"><span data-stu-id="ad115-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="ad115-171">单击**新建数据上下文...** 按钮。</span><span class="sxs-lookup"><span data-stu-id="ad115-171">Click the **New data context...** button.</span></span> <span data-ttu-id="ad115-172">保留数据上下文类型的默认名称，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="ad115-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="ad115-173">在添加控制器对话框来添加控制器，单击添加。</span><span class="sxs-lookup"><span data-stu-id="ad115-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="ad115-174">注意:如果收到错误消息，指出&quot;时出错，获取类型...&quot;，请确保添加 Product 类后生成 Visual Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="ad115-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="ad115-175">基架使用反射来查找类。</span><span class="sxs-lookup"><span data-stu-id="ad115-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="ad115-176">基架添加到项目的两个代码文件：</span><span class="sxs-lookup"><span data-stu-id="ad115-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="ad115-177">Products.cs 定义实现 OData 终结点的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="ad115-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="ad115-178">ProductServiceContext.cs 提供方法来查询基础数据库中，使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="ad115-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="ad115-179">添加的 EDM 和路由</span><span class="sxs-lookup"><span data-stu-id="ad115-179">Add the EDM and Route</span></span>

<span data-ttu-id="ad115-180">在解决方案资源管理器，展开应用\_启动文件夹并打开名为 WebApiConfig.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="ad115-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="ad115-181">此类包含对 Web API 配置代码。</span><span class="sxs-lookup"><span data-stu-id="ad115-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="ad115-182">此代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="ad115-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="ad115-183">此代码执行两项操作：</span><span class="sxs-lookup"><span data-stu-id="ad115-183">This code does two things:</span></span>

- <span data-ttu-id="ad115-184">创建 OData 终结点的实体数据模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="ad115-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="ad115-185">将添加为终结点的路由。</span><span class="sxs-lookup"><span data-stu-id="ad115-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="ad115-186">EDM 是抽象的数据模型。</span><span class="sxs-lookup"><span data-stu-id="ad115-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="ad115-187">EDM 用于创建元数据文档，并定义服务的 Uri。</span><span class="sxs-lookup"><span data-stu-id="ad115-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="ad115-188">**ODataConventionModelBuilder**创建 EDM 使用一组默认命名约定 EDM。</span><span class="sxs-lookup"><span data-stu-id="ad115-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="ad115-189">此方法要求最少的代码。</span><span class="sxs-lookup"><span data-stu-id="ad115-189">This approach requires the least code.</span></span> <span data-ttu-id="ad115-190">如果你想更好地控制 EDM，则可以使用**ODataModelBuilder**类，以通过添加属性、 键和导航属性显式创建 EDM。</span><span class="sxs-lookup"><span data-stu-id="ad115-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="ad115-191">**EntitySet**方法将添加一个实体集到 EDM:</span><span class="sxs-lookup"><span data-stu-id="ad115-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="ad115-192">"产品"的字符串定义的实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="ad115-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="ad115-193">控制器的名称必须与实体集的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="ad115-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="ad115-194">在本教程中，实体集被命名为"产品"和控制器被命名为`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="ad115-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="ad115-195">如果在名为的实体集"ProductSet"，则将命名为控制器`ProductSetController`。</span><span class="sxs-lookup"><span data-stu-id="ad115-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="ad115-196">请注意，终结点可以具有多个实体集。</span><span class="sxs-lookup"><span data-stu-id="ad115-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="ad115-197">调用**EntitySet&lt;T&gt;** 为每个实体集，，然后定义相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="ad115-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="ad115-198">**MapODataRoute**方法将添加为 OData 终结点的路由。</span><span class="sxs-lookup"><span data-stu-id="ad115-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="ad115-199">第一个参数是路由的友好名称。</span><span class="sxs-lookup"><span data-stu-id="ad115-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="ad115-200">你的服务的客户端不会看到此名称。</span><span class="sxs-lookup"><span data-stu-id="ad115-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="ad115-201">第二个参数是终结点的 URI 前缀。</span><span class="sxs-lookup"><span data-stu-id="ad115-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="ad115-202">给定此代码，Products 实体集的 URI 为 http://<em>主机名</em>  /odata/产品。</span><span class="sxs-lookup"><span data-stu-id="ad115-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="ad115-203">应用程序可以具有多个 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="ad115-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="ad115-204">对于每个终结点，调用<strong>MapODataRoute</strong>提供唯一的路由名称和唯一的 URI 前缀。</span><span class="sxs-lookup"><span data-stu-id="ad115-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="ad115-205">（可选） 数据库中植入</span><span class="sxs-lookup"><span data-stu-id="ad115-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="ad115-206">在此步骤中，将使用 Entity Framework 以设置一些测试数据与数据库的种子。</span><span class="sxs-lookup"><span data-stu-id="ad115-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="ad115-207">此步骤是可选的但它可以立即测试 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="ad115-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="ad115-208">从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="ad115-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ad115-209">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ad115-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="ad115-210">这将添加名为迁移和名为 Configuration.cs 代码文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad115-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="ad115-211">打开此文件，并将以下代码添加到`Configuration.Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="ad115-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="ad115-212">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="ad115-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="ad115-213">这些命令将生成创建数据库，然后执行该代码的代码。</span><span class="sxs-lookup"><span data-stu-id="ad115-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="ad115-214">探索 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="ad115-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="ad115-215">在本部分中，我们将使用[Fiddler Web 调试代理](http://www.fiddler2.com)将请求发送到终结点并检查响应消息。</span><span class="sxs-lookup"><span data-stu-id="ad115-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="ad115-216">这将帮助您了解 OData 终结点的功能。</span><span class="sxs-lookup"><span data-stu-id="ad115-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="ad115-217">在 Visual Studio 中，按 F5 启动调试。</span><span class="sxs-lookup"><span data-stu-id="ad115-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="ad115-218">默认情况下，Visual Studio 将打开你的浏览器`http://localhost:*port*`，其中*端口*是在项目设置中配置的端口号。</span><span class="sxs-lookup"><span data-stu-id="ad115-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="ad115-219">你可以在项目设置中的端口号。</span><span class="sxs-lookup"><span data-stu-id="ad115-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="ad115-220">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="ad115-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="ad115-221">在属性窗口中，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="ad115-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="ad115-222">输入下的端口号**项目 Url**。</span><span class="sxs-lookup"><span data-stu-id="ad115-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="ad115-223">服务文档</span><span class="sxs-lookup"><span data-stu-id="ad115-223">Service Document</span></span>

<span data-ttu-id="ad115-224">*服务文档*包含 OData 终结点的实体集的列表。</span><span class="sxs-lookup"><span data-stu-id="ad115-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="ad115-225">若要获取服务文档，请对根服务的 URI 发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="ad115-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="ad115-226">使用 Fiddler，输入中的以下 URI **Composer**选项卡： `http://localhost:port/odata/`，其中*端口*是端口号。</span><span class="sxs-lookup"><span data-stu-id="ad115-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="ad115-227">单击**Execute**按钮。</span><span class="sxs-lookup"><span data-stu-id="ad115-227">Click the **Execute** button.</span></span> <span data-ttu-id="ad115-228">Fiddler 将 HTTP GET 请求发送到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad115-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="ad115-229">应看到 Web 会话列表中的响应。</span><span class="sxs-lookup"><span data-stu-id="ad115-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="ad115-230">如果一切正常，则状态代码将为 200。</span><span class="sxs-lookup"><span data-stu-id="ad115-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="ad115-231">双击要查看检查器选项卡中的响应消息的详细信息的 Web 会话列表中的响应。</span><span class="sxs-lookup"><span data-stu-id="ad115-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="ad115-232">原始 HTTP 响应消息应类似于下面所示：</span><span class="sxs-lookup"><span data-stu-id="ad115-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="ad115-233">默认情况下，Web API 返回 AtomPub 格式的服务文档。</span><span class="sxs-lookup"><span data-stu-id="ad115-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="ad115-234">若要请求 JSON，将 HTTP 请求中添加以下标头：</span><span class="sxs-lookup"><span data-stu-id="ad115-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="ad115-235">现在的 HTTP 响应包含 JSON 有效负载：</span><span class="sxs-lookup"><span data-stu-id="ad115-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="ad115-236">服务元数据文档</span><span class="sxs-lookup"><span data-stu-id="ad115-236">Service Metadata Document</span></span>

<span data-ttu-id="ad115-237">*服务元数据文档*介绍了使用一种称为概念架构定义语言 (CSDL) 的 XML 语言的服务数据模型。</span><span class="sxs-lookup"><span data-stu-id="ad115-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="ad115-238">元数据文档在服务中，显示的数据结构，并可用于生成客户端代码。</span><span class="sxs-lookup"><span data-stu-id="ad115-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="ad115-239">若要获取的元数据文档，请将发送 GET 请求到`http://localhost:port/odata/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="ad115-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="ad115-240">下面是本教程中所示的终结点的元数据。</span><span class="sxs-lookup"><span data-stu-id="ad115-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="ad115-241">实体集</span><span class="sxs-lookup"><span data-stu-id="ad115-241">Entity Set</span></span>

<span data-ttu-id="ad115-242">若要获取的产品实体集，将发送 GET 请求到`http://localhost:port/odata/Products`。</span><span class="sxs-lookup"><span data-stu-id="ad115-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="ad115-243">实体</span><span class="sxs-lookup"><span data-stu-id="ad115-243">Entity</span></span>

<span data-ttu-id="ad115-244">若要获取的各个产品，发送 GET 请求到`http://localhost:port/odata/Products(1)`，其中"1"是产品 id。</span><span class="sxs-lookup"><span data-stu-id="ad115-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="ad115-245">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="ad115-245">OData Serialization Formats</span></span>

<span data-ttu-id="ad115-246">OData 支持多种序列化格式：</span><span class="sxs-lookup"><span data-stu-id="ad115-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="ad115-247">Atom Pub (XML)</span><span class="sxs-lookup"><span data-stu-id="ad115-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="ad115-248">JSON"light"（在 OData v3 中引入）</span><span class="sxs-lookup"><span data-stu-id="ad115-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="ad115-249">JSON"详细"(OData v2)</span><span class="sxs-lookup"><span data-stu-id="ad115-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="ad115-250">默认情况下，Web API 使用 AtomPubJSON"light"格式。</span><span class="sxs-lookup"><span data-stu-id="ad115-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="ad115-251">若要获取 AtomPub 格式，请设置为"application/atom + xml"Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="ad115-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="ad115-252">下面是响应正文示例：</span><span class="sxs-lookup"><span data-stu-id="ad115-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="ad115-253">您所见 Atom 格式的一个明显的缺点：它是 JSON 精简模式的更详细。</span><span class="sxs-lookup"><span data-stu-id="ad115-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="ad115-254">但是，如果必须理解 AtomPub 的客户端，客户端可能更倾向于该格式通过 JSON。</span><span class="sxs-lookup"><span data-stu-id="ad115-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="ad115-255">下面是实体的相同的 JSON 轻型版本：</span><span class="sxs-lookup"><span data-stu-id="ad115-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="ad115-256">OData 协议版本 3 中引入了 JSON 轻型格式。</span><span class="sxs-lookup"><span data-stu-id="ad115-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="ad115-257">为了向后兼容性，客户端可以请求的较旧的"详细"JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="ad115-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="ad115-258">若要请求详细 JSON，请将 Accept 标头设置为`application/json;odata=verbose`。</span><span class="sxs-lookup"><span data-stu-id="ad115-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="ad115-259">下面是详细的版本：</span><span class="sxs-lookup"><span data-stu-id="ad115-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="ad115-260">此格式会告知在响应正文中，可以极大地增加开销通过整个会话的多个元数据。</span><span class="sxs-lookup"><span data-stu-id="ad115-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="ad115-261">此外，它会通过包装在名为"d"的属性的对象添加一定程度的间接性。</span><span class="sxs-lookup"><span data-stu-id="ad115-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad115-262">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ad115-262">Next Steps</span></span>

- [<span data-ttu-id="ad115-263">添加实体关系</span><span class="sxs-lookup"><span data-stu-id="ad115-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="ad115-264">添加 OData 操作</span><span class="sxs-lookup"><span data-stu-id="ad115-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="ad115-265">从.NET 客户端调用 OData 服务</span><span class="sxs-lookup"><span data-stu-id="ad115-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)

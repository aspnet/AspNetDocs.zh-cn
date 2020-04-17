---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证构建模型 |微软文档
author: rick-anderson
description: 步骤 3 演示如何创建模型，可用于查询和更新 NerdDinner 应用程序的数据库。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541632"
---
# <a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="30e28-103">生成具有业务规则验证功能的模型</span><span class="sxs-lookup"><span data-stu-id="30e28-103">Build a Model with Business Rule Validations</span></span>

<span data-ttu-id="30e28-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="30e28-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="30e28-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="30e28-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="30e28-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第3步，该教程演示如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="30e28-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="30e28-107">步骤 3 演示如何创建模型，可用于查询和更新 NerdDinner 应用程序的数据库。</span><span class="sxs-lookup"><span data-stu-id="30e28-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="30e28-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="30e28-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="30e28-109">神经晚餐步骤 3： 构建模型</span><span class="sxs-lookup"><span data-stu-id="30e28-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="30e28-110">在模型视图控制器框架中，术语"模型"是指表示应用程序数据的对象，以及与其集成验证和业务规则的相应域逻辑。</span><span class="sxs-lookup"><span data-stu-id="30e28-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="30e28-111">该模型在许多方面是基于 MVC 的应用程序的"心脏"，稍后我们将看到从根本上推动它的行为。</span><span class="sxs-lookup"><span data-stu-id="30e28-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="30e28-112">ASP.NET MVC 框架支持使用任何数据访问技术，开发人员可以从各种丰富的 .NET 数据选项中进行选择以实施其模型，包括：LINQ 到实体、LINQ 到 SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM，或者只是原始ADO.NET数据阅读器或数据集集。</span><span class="sxs-lookup"><span data-stu-id="30e28-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="30e28-113">对于我们的NerdDinner应用程序，我们将使用LINQ到SQL来创建一个与数据库设计相当一致的简单模型，并添加一些自定义验证逻辑和业务规则。</span><span class="sxs-lookup"><span data-stu-id="30e28-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="30e28-114">然后，我们将实现一个存储库类，该类可帮助从应用程序的其余部分提取数据持久性实现，并使我们能够轻松地对其进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="30e28-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="30e28-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="30e28-115">LINQ to SQL</span></span>

<span data-ttu-id="30e28-116">LINQ 到 SQL 是作为 .NET 3.5 的一部分而附带的 ORM（对象关系映射器）。</span><span class="sxs-lookup"><span data-stu-id="30e28-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="30e28-117">LINQ 到 SQL 提供了一种将数据库表映射到 .NET 类的简单方法，我们可以针对它编写代码。</span><span class="sxs-lookup"><span data-stu-id="30e28-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="30e28-118">对于我们的NerdDinner应用程序，我们将用它来将数据库中的晚餐和RSVP表映射到晚餐和RSVP类。</span><span class="sxs-lookup"><span data-stu-id="30e28-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="30e28-119">晚餐和 RSVP 表的列将对应于"晚餐"和"RSVP"类的属性。</span><span class="sxs-lookup"><span data-stu-id="30e28-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="30e28-120">每个 Dinner 和 RSVP 对象将表示数据库中的 Dinner 或 RSVP 表中的单独行。</span><span class="sxs-lookup"><span data-stu-id="30e28-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="30e28-121">LINQ 到 SQL 允许我们避免手动构造 SQL 语句来检索和更新具有数据库数据的 Dinner 和 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="30e28-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="30e28-122">相反，我们将定义 Dinner 和 RSVP 类、它们如何映射到/从数据库映射以及它们之间的关系。</span><span class="sxs-lookup"><span data-stu-id="30e28-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="30e28-123">然后，LINQ 到 SQL 将负责生成适当的 SQL 执行逻辑，以便在运行时交互使用它们时使用。</span><span class="sxs-lookup"><span data-stu-id="30e28-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="30e28-124">我们可以在 VB 和 C# 中使用 LINQ 语言支持来编写表达性查询，从数据库中检索 Dinner 和 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="30e28-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="30e28-125">这最大限度地减少了我们需要编写的数据代码量，并允许我们构建真正干净的应用程序。</span><span class="sxs-lookup"><span data-stu-id="30e28-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="30e28-126">将 LINQ 添加到 SQL 类到我们的项目</span><span class="sxs-lookup"><span data-stu-id="30e28-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="30e28-127">我们将从右键单击项目中的"模型"文件夹开始，然后选择 **"添加新&gt;项目**"菜单命令：</span><span class="sxs-lookup"><span data-stu-id="30e28-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="30e28-128">这将弹出"添加新项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="30e28-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="30e28-129">我们将按"数据"类别进行筛选，并在其中选择"LINQ 到 SQL 类"模板：</span><span class="sxs-lookup"><span data-stu-id="30e28-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="30e28-130">我们将为项目命名为"NerdDinner"，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="30e28-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="30e28-131">Visual Studio 将在我们的 #Model 目录下添加 NerdDinner.dbml 文件，然后打开 LINQ 到 SQL 对象关系设计器：</span><span class="sxs-lookup"><span data-stu-id="30e28-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="30e28-132">使用 LINQ 创建到 SQL 的数据模型类</span><span class="sxs-lookup"><span data-stu-id="30e28-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="30e28-133">LINQ 到 SQL 使我们能够从现有数据库架构快速创建数据模型类。</span><span class="sxs-lookup"><span data-stu-id="30e28-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="30e28-134">为此，我们将在服务器资源管理器中打开 NerdDinner 数据库，并选择要在其中建模的表：</span><span class="sxs-lookup"><span data-stu-id="30e28-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="30e28-135">然后，我们可以将表拖到 LINQ 到 SQL 设计器表面。</span><span class="sxs-lookup"><span data-stu-id="30e28-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="30e28-136">当我们执行此操作 LINQ 到 SQL 时，将使用表的架构（具有映射到数据库表列的类属性）自动创建 Dinner 和 RSVP 类：</span><span class="sxs-lookup"><span data-stu-id="30e28-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="30e28-137">默认情况下，LINQ 到 SQL 设计器在基于数据库架构创建类时自动"复数"表和列名称。</span><span class="sxs-lookup"><span data-stu-id="30e28-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="30e28-138">例如：我们上面示例中的"Dinners"表产生了一个"Dinner"类。</span><span class="sxs-lookup"><span data-stu-id="30e28-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="30e28-139">此类命名有助于使我们的模型与 .NET 命名约定保持一致，我通常发现让设计器修复这一点很方便（尤其是在添加大量表时）。</span><span class="sxs-lookup"><span data-stu-id="30e28-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="30e28-140">但是，如果您不喜欢设计器生成的类或属性的名称，则始终可以重写它并将其更改为所需的任何名称。</span><span class="sxs-lookup"><span data-stu-id="30e28-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="30e28-141">可以通过在设计器内编辑实体/属性名称，或通过属性网格对其进行修改来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="30e28-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="30e28-142">默认情况下，LINQ 到 SQL 设计器还会检查表的主键/外键关系，并基于这些关系自动在它创建的不同模型类之间创建默认的"关系关联"。</span><span class="sxs-lookup"><span data-stu-id="30e28-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="30e28-143">例如，当我们将 Dinner 和 RSVP 表拖到 LINQ 到 SQL 设计器时，根据 RSVP 表对 Dinners 表具有外键（由设计器中的箭头指示）推断两者之间存在一对多关系关联：</span><span class="sxs-lookup"><span data-stu-id="30e28-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="30e28-144">上述关联将导致 LINQ 到 SQL 向 RSVP 类添加强类型"Dinner"属性，开发人员可以使用该属性访问与给定 RSVP 关联的 Dinner。</span><span class="sxs-lookup"><span data-stu-id="30e28-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="30e28-145">它还会导致 Dinner 类具有"RSVP"集合属性，使开发人员能够检索和更新与特定 Dinner 关联的 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="30e28-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="30e28-146">下面您可以看到 Visual Studio 中一个智能感知示例，当我们创建新的 RSVP 对象并将其添加到 Dinner 的 RSVP 集合中时。</span><span class="sxs-lookup"><span data-stu-id="30e28-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="30e28-147">请注意 LINQ 到 SQL 如何在 Dinner 对象上自动添加"RSV"集合：</span><span class="sxs-lookup"><span data-stu-id="30e28-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="30e28-148">通过将 RSVP 对象添加到 Dinner 的 RSVP 集合中，我们告诉 LINQ 到 SQL 来关联数据库中的 Dinner 和 RSVP 行之间的外键关系：</span><span class="sxs-lookup"><span data-stu-id="30e28-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="30e28-149">如果您不喜欢设计器建模或命名表关联的方式，则可以重写它。</span><span class="sxs-lookup"><span data-stu-id="30e28-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="30e28-150">只需单击设计器中的关联箭头，并通过属性网格访问其属性以重命名、删除或修改它。</span><span class="sxs-lookup"><span data-stu-id="30e28-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="30e28-151">但是，对于我们的 NerdDinner 应用程序，默认关联规则非常适合我们构建的数据模型类，我们可以只使用默认行为。</span><span class="sxs-lookup"><span data-stu-id="30e28-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="30e28-152">内德晚餐数据上下文类</span><span class="sxs-lookup"><span data-stu-id="30e28-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="30e28-153">Visual Studio 将自动创建 .NET 类，这些类表示使用 LINQ 到 SQL 设计器定义的模型和数据库关系。</span><span class="sxs-lookup"><span data-stu-id="30e28-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="30e28-154">还将为添加到解决方案的每个 LINQ 到 SQL 设计器文件生成 LINQ 到 SQL DataContext 类。</span><span class="sxs-lookup"><span data-stu-id="30e28-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="30e28-155">由于我们将 LINQ 命名为 SQL 类项"NerdDinner"，因此创建的数据上下文类将称为"NerdDinnerDataContext"。</span><span class="sxs-lookup"><span data-stu-id="30e28-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="30e28-156">此 NerdDinnerDataContext 类是我们与数据库交互的主要方式。</span><span class="sxs-lookup"><span data-stu-id="30e28-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="30e28-157">我们的 NerdDinnerDataContext 类公开了两个属性 - "Dinners" 和"RSVPs" - 它们表示我们在数据库中建模的两个表。</span><span class="sxs-lookup"><span data-stu-id="30e28-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="30e28-158">我们可以使用 C# 针对这些属性编写 LINQ 查询，以便从数据库中查询和检索 Dinner 和 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="30e28-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="30e28-159">以下代码演示如何实例化 NerdDinnerDataContext 对象，并针对该对象执行 LINQ 查询，以获取将来发生的一系列 Dinner。</span><span class="sxs-lookup"><span data-stu-id="30e28-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="30e28-160">Visual Studio 在编写 LINQ 查询时提供完整的无意义，从它返回的对象是强类型，并且还支持智能感知：</span><span class="sxs-lookup"><span data-stu-id="30e28-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="30e28-161">除了允许我们查询晚餐和RSVP对象外，NerdDinnerDataContext 还会自动跟踪我们随后对我们通过它检索的晚餐和 RSVP 对象所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="30e28-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="30e28-162">我们可以使用此功能轻松地将更改保存回数据库 - 而无需编写任何显式 SQL 更新代码。</span><span class="sxs-lookup"><span data-stu-id="30e28-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="30e28-163">例如，下面的代码演示如何使用 LINQ 查询从数据库中检索单个 Dinner 对象，更新两个 Dinner 属性，然后将更改保存回数据库：</span><span class="sxs-lookup"><span data-stu-id="30e28-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="30e28-164">上面代码中的 NerdDinnerDataContext 对象自动跟踪我们对从该对象检索到的 Dinner 对象所做的属性更改。</span><span class="sxs-lookup"><span data-stu-id="30e28-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="30e28-165">当我们调用"提交更改（）"方法时，它将对数据库执行适当的 SQL"UPDATE"语句，以保留更新的值。</span><span class="sxs-lookup"><span data-stu-id="30e28-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="30e28-166">创建晚餐存储库类</span><span class="sxs-lookup"><span data-stu-id="30e28-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="30e28-167">对于小型应用程序，有时让控制器直接针对 LINQ 到 SQL DataContext 类工作，并将 LINQ 查询嵌入到控制器中，这有时很好。</span><span class="sxs-lookup"><span data-stu-id="30e28-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="30e28-168">但是，随着应用程序变得越来越大，此方法在维护和测试方面变得繁琐起来。</span><span class="sxs-lookup"><span data-stu-id="30e28-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="30e28-169">它还可能导致我们在多个位置复制相同的 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="30e28-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="30e28-170">使应用程序更易于维护和测试的一种方法是使用"存储库"模式。</span><span class="sxs-lookup"><span data-stu-id="30e28-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="30e28-171">存储库类有助于封装数据查询和持久性逻辑，并从应用程序抽象数据持久性的实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="30e28-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="30e28-172">除了使应用程序代码更简洁之外，使用存储库模式还可以使将来更轻松地更改数据存储实现，并且它可以帮助简化应用程序单元测试，而无需真正的数据库。</span><span class="sxs-lookup"><span data-stu-id="30e28-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="30e28-173">对于我们的NerdDinner应用程序，我们将定义一个带有以下签名的 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="30e28-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="30e28-174">*注意：在本章的后面部分，我们将从此类中提取 IDinnerRepository 接口，并在我们的控制器上启用依赖项注入。不过，首先，我们将开始简单，只是直接与 DinnerRepository 类一起工作。*</span><span class="sxs-lookup"><span data-stu-id="30e28-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="30e28-175">要实现此类，我们将右键单击我们的"模型"文件夹，然后选择 **"添加新&gt;项目**"菜单命令。</span><span class="sxs-lookup"><span data-stu-id="30e28-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="30e28-176">在"添加新项目"对话框中，我们将选择"类"模板并将文件命名为"DinnerRepository.cs"：</span><span class="sxs-lookup"><span data-stu-id="30e28-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="30e28-177">然后，我们可以使用以下代码实现我们的 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="30e28-177">We can then implement our DinnerRepository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="30e28-178">使用 DinnerRepository 类检索、更新、插入和删除</span><span class="sxs-lookup"><span data-stu-id="30e28-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="30e28-179">现在，我们已经创建了 DinnerRepository 类，让我们看一些代码示例，这些示例演示了我们可以执行的常见任务：</span><span class="sxs-lookup"><span data-stu-id="30e28-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="30e28-180">查询示例</span><span class="sxs-lookup"><span data-stu-id="30e28-180">Querying Examples</span></span>

<span data-ttu-id="30e28-181">以下代码使用 DinnerID 值检索单个晚餐：</span><span class="sxs-lookup"><span data-stu-id="30e28-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="30e28-182">下面的代码检索所有即将举办的晚餐，并在它们上循环：</span><span class="sxs-lookup"><span data-stu-id="30e28-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="30e28-183">插入和更新示例</span><span class="sxs-lookup"><span data-stu-id="30e28-183">Insert and Update Examples</span></span>

<span data-ttu-id="30e28-184">下面的代码演示了添加两个新晚餐。</span><span class="sxs-lookup"><span data-stu-id="30e28-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="30e28-185">在调用"Save（）"方法之前，不会将存储库的添加/修改提交到数据库。</span><span class="sxs-lookup"><span data-stu-id="30e28-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="30e28-186">LINQ 到 SQL 会自动包装数据库事务中的所有更改 ， 因此，当我们的存储库保存时，要么发生所有更改，要么这些更改都不会发生：</span><span class="sxs-lookup"><span data-stu-id="30e28-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="30e28-187">下面的代码检索现有的 Dinner 对象，并修改其上的两个属性。</span><span class="sxs-lookup"><span data-stu-id="30e28-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="30e28-188">当我们的存储库上调用"Save（））"方法时，更改将提交回数据库：</span><span class="sxs-lookup"><span data-stu-id="30e28-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="30e28-189">下面的代码检索晚餐，然后向其中添加 RSVP。</span><span class="sxs-lookup"><span data-stu-id="30e28-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="30e28-190">它使用 LINQ 到 SQL 为我们创建的 Dinner 对象上的 RSVP 集合来这样做（因为数据库中两者之间存在主键/外键关系）。</span><span class="sxs-lookup"><span data-stu-id="30e28-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="30e28-191">当在存储库上调用"Save（））"方法时，此更改将作为新的 RSVP 表行保留回数据库：</span><span class="sxs-lookup"><span data-stu-id="30e28-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="30e28-192">删除示例</span><span class="sxs-lookup"><span data-stu-id="30e28-192">Delete Example</span></span>

<span data-ttu-id="30e28-193">下面的代码检索现有的 Dinner 对象，然后将其标记为要删除。</span><span class="sxs-lookup"><span data-stu-id="30e28-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="30e28-194">在存储库上调用"Save（））"方法时，它将将删除提交回数据库：</span><span class="sxs-lookup"><span data-stu-id="30e28-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="30e28-195">将验证和业务规则逻辑与模型类集成</span><span class="sxs-lookup"><span data-stu-id="30e28-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="30e28-196">集成验证和业务规则逻辑是任何处理数据的应用程序的关键部分。</span><span class="sxs-lookup"><span data-stu-id="30e28-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="30e28-197">架构验证</span><span class="sxs-lookup"><span data-stu-id="30e28-197">Schema Validation</span></span>

<span data-ttu-id="30e28-198">使用 LINQ 到 SQL 设计器定义模型类时，数据模型类中属性的数据类型对应于数据库表的数据类型。</span><span class="sxs-lookup"><span data-stu-id="30e28-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="30e28-199">例如：如果 Dinners 表中的"EventDate"列是"日期时间"，则 LINQ 创建的 SQL 数据模型类的类型为"DateTime"（这是内置的 .NET 数据类型）。</span><span class="sxs-lookup"><span data-stu-id="30e28-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="30e28-200">这意味着，如果您尝试从代码为其分配整数或布尔，则收到编译错误，如果尝试在运行时隐式将无效字符串类型转换为该字符串类型，则会自动引发错误。</span><span class="sxs-lookup"><span data-stu-id="30e28-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="30e28-201">LINQ 到 SQL 还会在使用字符串时自动处理转义 SQL 值，这有助于在使用字符串时防止 SQL 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="30e28-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="30e28-202">验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="30e28-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="30e28-203">架构验证作为第一步非常有用，但很少足够。</span><span class="sxs-lookup"><span data-stu-id="30e28-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="30e28-204">大多数实际方案都需要能够指定更丰富的验证逻辑，该验证逻辑可以跨越多个属性，执行代码，并且通常了解模型的状态（例如：它是在创建/更新/删除，还是处于特定于域的状态（如"存档"）。</span><span class="sxs-lookup"><span data-stu-id="30e28-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="30e28-205">有多种不同的模式和框架可用于定义验证规则并将其应用于模型类，并且有几个基于 .NET 的框架可用于帮助实现此。</span><span class="sxs-lookup"><span data-stu-id="30e28-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="30e28-206">您可以在mVC应用程序中使用几乎任何ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="30e28-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="30e28-207">为了我们的 NerdDinner 应用程序，我们将使用相对简单和直接的模式，在其中我们公开 IsValid 属性和 GetRule侵犯（） 方法在我们的 Dinner 模型对象上。</span><span class="sxs-lookup"><span data-stu-id="30e28-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="30e28-208">IsValid 属性将返回真或假，具体取决于验证和业务规则是否都有效。</span><span class="sxs-lookup"><span data-stu-id="30e28-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="30e28-209">GetRule违反（） 方法将返回任何规则错误的列表。</span><span class="sxs-lookup"><span data-stu-id="30e28-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="30e28-210">我们将通过在我们的项目中添加"部分类"来实现"有效"和 GetRule违反（）） 我们的晚餐模型。</span><span class="sxs-lookup"><span data-stu-id="30e28-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="30e28-211">部分类可用于向 VS 设计器维护的类（如 LINQ 生成的到 SQL 设计器生成的 Dinner 类）添加方法/属性/事件，并帮助避免工具混乱我们的代码。</span><span class="sxs-lookup"><span data-stu-id="30e28-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="30e28-212">我们可以通过右键单击 #Model 文件夹，将新的部分类添加到项目中，然后选择"添加新项目"菜单命令。</span><span class="sxs-lookup"><span data-stu-id="30e28-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="30e28-213">然后，我们可以在"添加新项目"对话框中选择"类"模板，并将其命名为Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="30e28-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="30e28-214">单击"添加"按钮会将Dinner.cs文件添加到我们的项目中，并在 IDE 中打开该文件。</span><span class="sxs-lookup"><span data-stu-id="30e28-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="30e28-215">然后，我们可以使用以下代码实现基本的规则/验证实施框架：</span><span class="sxs-lookup"><span data-stu-id="30e28-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="30e28-216">有关上述代码的一些说明：</span><span class="sxs-lookup"><span data-stu-id="30e28-216">A few notes about the above code:</span></span>

- <span data-ttu-id="30e28-217">Dinner 类以"部分"关键字为开头 - 这意味着其中包含的代码将与 LINQ 生成/维护的类组合到 SQL 设计器并编译为单个类。</span><span class="sxs-lookup"><span data-stu-id="30e28-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="30e28-218">RuleRuleRule 类是一个帮助类，我们将添加到项目中，允许我们提供有关规则违反的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="30e28-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="30e28-219">晚餐.GetRule违反（）方法会导致评估我们的验证和业务规则（我们将很快实施它们）。</span><span class="sxs-lookup"><span data-stu-id="30e28-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="30e28-220">然后，它返回一系列规则冲突对象，这些对象提供有关任何规则错误的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="30e28-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="30e28-221">Dinner.IsValid 属性提供了一个方便的帮助程序属性，用于指示 Dinner 对象是否具有任何活动的规则冲突。</span><span class="sxs-lookup"><span data-stu-id="30e28-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="30e28-222">开发人员可以随时使用 Dinner 对象主动检查它（并且不会引发异常）。</span><span class="sxs-lookup"><span data-stu-id="30e28-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="30e28-223">Dinner.OnValidate（） 部分方法是 LINQ 到 SQL 提供的一个挂钩，它允许我们在即将在数据库中持久化 Dinner 对象的任何时间收到通知。</span><span class="sxs-lookup"><span data-stu-id="30e28-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="30e28-224">上述 OnValidate（） 实现可确保在保存之前没有规则违反规则。</span><span class="sxs-lookup"><span data-stu-id="30e28-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="30e28-225">如果处于无效状态，它将引发异常，这将导致 LINQ 到 SQL 中止事务。</span><span class="sxs-lookup"><span data-stu-id="30e28-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="30e28-226">此方法提供了一个简单的框架，我们可以将验证和业务规则集成到其中。</span><span class="sxs-lookup"><span data-stu-id="30e28-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="30e28-227">现在，让我们将以下规则添加到我们的 GetRule 违反（） 方法：</span><span class="sxs-lookup"><span data-stu-id="30e28-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="30e28-228">我们使用 C# 的"收益回报"功能来返回任何规则违反规则的序列。</span><span class="sxs-lookup"><span data-stu-id="30e28-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="30e28-229">上面的前六个规则检查只是强制说，我们 Dinner 上的字符串属性不能为空或为空。</span><span class="sxs-lookup"><span data-stu-id="30e28-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="30e28-230">最后一条规则更有趣一点，并调用 PhoneValidator.IsValidNumber（） 帮助器方法，我们可以添加到我们的项目中，以验证 ContactPhone 号码格式是否与 Dinner 的国家/地区匹配。</span><span class="sxs-lookup"><span data-stu-id="30e28-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="30e28-231">我们可以使用 。NET 的正则表达式支持实现此电话验证支持。</span><span class="sxs-lookup"><span data-stu-id="30e28-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="30e28-232">下面是一个简单的电话验证器实现，我们可以添加到我们的项目，使我们能够添加特定于国家/地区的 Regex 模式检查：</span><span class="sxs-lookup"><span data-stu-id="30e28-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="30e28-233">处理验证和业务逻辑冲突</span><span class="sxs-lookup"><span data-stu-id="30e28-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="30e28-234">现在，我们已经添加了上述验证和业务规则代码，每当我们尝试创建或更新 Dinner 时，都将评估和强制执行验证逻辑规则。</span><span class="sxs-lookup"><span data-stu-id="30e28-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="30e28-235">开发人员可以编写如下代码，以主动确定 Dinner 对象是否有效，并检索其中所有冲突的列表，而不会引发任何异常：</span><span class="sxs-lookup"><span data-stu-id="30e28-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="30e28-236">如果我们尝试将 Dinner 保存为无效状态，则当我们在 Dinner 存储库上调用 Save（） 方法时，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="30e28-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="30e28-237">这是因为 LINQ 到 SQL 在保存晚餐更改之前自动调用我们的 Dinner.OnValidate（） 部分方法，并且我们在晚餐中添加了代码。OnValidate（） 如果晚餐中存在任何违反规则的行为，则引发异常。</span><span class="sxs-lookup"><span data-stu-id="30e28-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="30e28-238">我们可以捕获此异常并被动检索要修复的违规列表：</span><span class="sxs-lookup"><span data-stu-id="30e28-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="30e28-239">由于验证和业务规则在我们的模型层中实现，而不是 UI 层内，因此它们将在应用程序中的所有方案中应用和使用。</span><span class="sxs-lookup"><span data-stu-id="30e28-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="30e28-240">我们以后可以更改或添加业务规则，并让所有与我们的 Dinner 对象一起使用的代码都遵守它们。</span><span class="sxs-lookup"><span data-stu-id="30e28-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="30e28-241">在一个位置灵活地更改业务规则，而不使这些更改波及整个应用程序和 UI 逻辑，是编写良好的应用程序的标志，也是 MVC 框架有助于鼓励的好处。</span><span class="sxs-lookup"><span data-stu-id="30e28-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="30e28-242">下一步</span><span class="sxs-lookup"><span data-stu-id="30e28-242">Next Step</span></span>

<span data-ttu-id="30e28-243">现在，我们有一个模型，我们可以用于查询和更新我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="30e28-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="30e28-244">现在，让我们向项目添加一些控制器和视图，可用于构建围绕它的 HTML UI 体验。</span><span class="sxs-lookup"><span data-stu-id="30e28-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30e28-245">[上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="30e28-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>

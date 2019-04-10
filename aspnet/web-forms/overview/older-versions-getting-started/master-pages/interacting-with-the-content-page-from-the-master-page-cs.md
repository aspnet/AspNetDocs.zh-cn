---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
title: 与母版页 (C#) 从内容页交互 |Microsoft Docs
author: rick-anderson
description: 探讨如何调用方法，从母版页中的代码中设置属性等的内容页。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 3282df5e-516c-4972-8666-313828b90fb5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a2b6d3a5ceb66c14a78b02182f49d76c72becbd4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59413641"
---
# <a name="interacting-with-the-content-page-from-the-master-page-c"></a><span data-ttu-id="22ed6-103">从母版页与内容页交互 (C#)</span><span class="sxs-lookup"><span data-stu-id="22ed6-103">Interacting with the Content Page from the Master Page (C#)</span></span>

<span data-ttu-id="22ed6-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="22ed6-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="22ed6-105">[下载代码](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_CS.zip)或[下载 PDF](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="22ed6-105">[Download Code](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_CS.zip) or [Download PDF](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_CS.pdf)</span></span>

> <span data-ttu-id="22ed6-106">探讨如何调用方法，从母版页中的代码中设置属性等的内容页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-106">Examines how to call methods, set properties, etc. of the Content Page from code in the Master Page.</span></span>


## <a name="introduction"></a><span data-ttu-id="22ed6-107">介绍</span><span class="sxs-lookup"><span data-stu-id="22ed6-107">Introduction</span></span>

<span data-ttu-id="22ed6-108">前面的教程介绍了如何有内容页以编程方式与其主页面进行交互。</span><span class="sxs-lookup"><span data-stu-id="22ed6-108">The preceding tutorial examined how to have the content page programmatically interact with its master page.</span></span> <span data-ttu-id="22ed6-109">回想一下，我们更新母版页包含列出五个最近的 GridView 控件添加产品。</span><span class="sxs-lookup"><span data-stu-id="22ed6-109">Recall that we updated the master page to include a GridView control that listed the five most recently added products.</span></span> <span data-ttu-id="22ed6-110">然后，我们创建的内容页面，用户可以从中添加一个新的产品。</span><span class="sxs-lookup"><span data-stu-id="22ed6-110">We then created a content page from which the user could add a new product.</span></span> <span data-ttu-id="22ed6-111">后添加一个新的产品，需要指示主页面刷新其 GridView，以便它包含刚添加产品内容页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-111">Upon adding a new product, the content page needed to instruct the master page to refresh its GridView so that it would include the just-added product.</span></span> <span data-ttu-id="22ed6-112">此功能已通过将一个公共方法添加到母版页，刷新数据绑定到 GridView，然后再调用该方法从内容页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-112">This functionality was accomplished by adding a public method to the master page that refreshed the data bound to the GridView, and then invoking that method from the content page.</span></span>

<span data-ttu-id="22ed6-113">最常见的内容和母版页交互形式源自内容页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-113">The most common form of content and master page interaction originates from the content page.</span></span> <span data-ttu-id="22ed6-114">但是，很可能要实现价值，rouse 维护当前内容页面的母版页并且可能需要此类功能，如果主页面包含用户界面元素，使用户能够修改数据也会显示在内容页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-114">However, it is possible for the master page to rouse the current content page into action, and such functionality may be needed if the master page contains user interface elements that enable users to modify data that is also displayed on the content page.</span></span> <span data-ttu-id="22ed6-115">请考虑内容页显示 GridView 中的产品信息控件和母版页包含一个按钮控件，单击时，所有产品将价格乘 2。</span><span class="sxs-lookup"><span data-stu-id="22ed6-115">Consider a content page that displays the products information in a GridView control and a master page that includes a Button control that, when clicked, doubles the prices of all products.</span></span> <span data-ttu-id="22ed6-116">类似于前面的教程中的示例，GridView 需要刷新，以便它将显示新的价格中，单击按钮的双精度价格后但在此方案需要为操作 rouse 维护内容页面的母版页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-116">Much like the example in the preceding tutorial, the GridView needs to be refreshed after the double price Button is clicked so that it displays the new prices, but in this scenario it's the master page that needs to rouse the content page into action.</span></span>

<span data-ttu-id="22ed6-117">本教程探讨了如何通过母版页调用内容页中定义的功能。</span><span class="sxs-lookup"><span data-stu-id="22ed6-117">This tutorial explores how to have the master page invoke functionality defined in the content page.</span></span>

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a><span data-ttu-id="22ed6-118">决定通过事件和事件处理程序的编程交互</span><span class="sxs-lookup"><span data-stu-id="22ed6-118">Instigating Programmatic Interaction via an Event and Event Handlers</span></span>

<span data-ttu-id="22ed6-119">调用从母版页的内容页面功能是比前者更具挑战性。</span><span class="sxs-lookup"><span data-stu-id="22ed6-119">Invoking content page functionality from a master page is more challenging than the other way around.</span></span> <span data-ttu-id="22ed6-120">内容页时决定以编程方式从内容页交互具有单一的主页面，因为我们知道什么公共方法和属性可供我们使用。</span><span class="sxs-lookup"><span data-stu-id="22ed6-120">Because a content page has a single master page, when instigating the programmatic interaction from the content page we know what public methods and properties are at our disposal.</span></span> <span data-ttu-id="22ed6-121">但是，主页面，可以具有不同内容页的数量，每个都有自己的属性和方法集。</span><span class="sxs-lookup"><span data-stu-id="22ed6-121">A master page, however, can have many different content pages, each with its own set of properties and methods.</span></span> <span data-ttu-id="22ed6-122">如何，然后，编写代码时我们不知道哪些内容页将调用直到运行时在其内容页面中执行某些操作的母版页中？</span><span class="sxs-lookup"><span data-stu-id="22ed6-122">How, then, can we write code in the master page to perform some action in its content page when we don't know what content page will be invoked until runtime?</span></span>

<span data-ttu-id="22ed6-123">请考虑一个 ASP.NET Web 控件，例如按钮控件。</span><span class="sxs-lookup"><span data-stu-id="22ed6-123">Consider an ASP.NET Web control, such as the Button control.</span></span> <span data-ttu-id="22ed6-124">按钮控件可以显示在任意数量的 ASP.NET 页面上，并需要依据它会发出警告页已被单击的机制。</span><span class="sxs-lookup"><span data-stu-id="22ed6-124">A Button control can appear on any number of ASP.NET pages and needs a mechanism by which it can alert the page that it has been clicked.</span></span> <span data-ttu-id="22ed6-125">这通过*事件*。</span><span class="sxs-lookup"><span data-stu-id="22ed6-125">This is accomplished using *events*.</span></span> <span data-ttu-id="22ed6-126">具体而言，按钮控件引发其`Click`事件时单击; 包含按钮的 ASP.NET 页面 （可选） 可以响应通过该通知*事件处理程序*。</span><span class="sxs-lookup"><span data-stu-id="22ed6-126">In particular, the Button control raises its `Click` event when it is clicked; the ASP.NET page that contains the Button can optionally respond to that notification via an *event handler*.</span></span>

<span data-ttu-id="22ed6-127">此相同的模式可用于在其内容页面中有母版页触发器功能：</span><span class="sxs-lookup"><span data-stu-id="22ed6-127">This same pattern can be used to have a master page trigger functionality in its content pages:</span></span>

1. <span data-ttu-id="22ed6-128">将事件添加到母版页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-128">Add an event to the master page.</span></span>
2. <span data-ttu-id="22ed6-129">引发事件时主页面需要其内容页与进行通信。</span><span class="sxs-lookup"><span data-stu-id="22ed6-129">Raise the event whenever the master page needs to communicate with its content page.</span></span> <span data-ttu-id="22ed6-130">例如，如果主页面需要提醒用户加倍价格其内容页面，其事件将后立即引发价格已增加一倍。</span><span class="sxs-lookup"><span data-stu-id="22ed6-130">For example, if the master page needs to alert its content page that the user has doubled the prices, its event would be raised immediately after the prices have been doubled.</span></span>
3. <span data-ttu-id="22ed6-131">在需要执行一些操作这些内容页面中创建一个事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="22ed6-131">Create an event handler in those content pages that need to take some action.</span></span>

<span data-ttu-id="22ed6-132">本教程的余下内容实现引入; 中所述的示例也就是说，列出数据库中的产品的内容页和母版页包含一个按钮控制翻倍，价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-132">This remainder of this tutorial implements the example outlined in the Introduction; namely, a content page that lists the products in the database and a master page that includes a Button control to double the prices.</span></span>

## <a name="step-1-displaying-products-in-a-content-page"></a><span data-ttu-id="22ed6-133">步骤 1：在内容页面中显示的产品</span><span class="sxs-lookup"><span data-stu-id="22ed6-133">Step 1: Displaying Products in a Content Page</span></span>

<span data-ttu-id="22ed6-134">我们首要任务是创建内容页，其中列出了 Northwind 数据库中的产品。</span><span class="sxs-lookup"><span data-stu-id="22ed6-134">Our first order of business is to create a content page that lists the products from the Northwind database.</span></span> <span data-ttu-id="22ed6-135">(我们 Northwind 数据库到项目中添加前面的教程[*与母版页从内容页交互*](interacting-with-the-master-page-from-the-content-page-cs.md)。)首先，通过添加新的 ASP.NET 页面到`~/Admin`名为的文件夹`Products.aspx`，确保将将其绑定到`Site.master`母版页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-135">(We added the Northwind database to the project in the preceding tutorial, [*Interacting with the Master Page from the Content Page*](interacting-with-the-master-page-from-the-content-page-cs.md).) Start by adding a new ASP.NET page to the `~/Admin` folder named `Products.aspx`, making sure to bind it to the `Site.master` master page.</span></span> <span data-ttu-id="22ed6-136">图 1 显示此页添加到网站后的解决方案资源管理器。</span><span class="sxs-lookup"><span data-stu-id="22ed6-136">Figure 1 shows the Solution Explorer after this page has been added to the website.</span></span>


[![A<span data-ttu-id="22ed6-137">dd Admin 文件夹到一个新的 ASP.NET 页]</span><span class="sxs-lookup"><span data-stu-id="22ed6-137">dd a New ASP.NET Page to the Admin Folder]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image1.png)

<span data-ttu-id="22ed6-138">**图 01**:添加到新的 ASP.NET 页`Admin`文件夹 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-138">**Figure 01**: Add a New ASP.NET Page to the `Admin` Folder ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image3.png))</span></span>


<span data-ttu-id="22ed6-139">回想一下，在[*母版页中指定的标题、 元标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)教程中，我们创建一个名为的自定义基本页类`BasePage`，如果它不生成页面的标题显式设置。</span><span class="sxs-lookup"><span data-stu-id="22ed6-139">Recall that in the [*Specifying the Title, Meta Tags, and Other HTML Headers in the Master Page*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) tutorial we created a custom base page class named `BasePage` that generates the page's title if it is not explicitly set.</span></span> <span data-ttu-id="22ed6-140">转到`Products.aspx`页面的代码隐藏类，并将其派生`BasePage`(而不是从`System.Web.UI.Page`)。</span><span class="sxs-lookup"><span data-stu-id="22ed6-140">Go to the `Products.aspx` page's code-behind class and have it derive from `BasePage` (instead of from `System.Web.UI.Page`).</span></span>

<span data-ttu-id="22ed6-141">最后，更新`Web.sitemap`文件以便包括本课程中的一个条目。</span><span class="sxs-lookup"><span data-stu-id="22ed6-141">Finally, update the `Web.sitemap` file to include an entry for this lesson.</span></span> <span data-ttu-id="22ed6-142">添加以下标记下方`<siteMapNode>`Master 页交互的课程内容：</span><span class="sxs-lookup"><span data-stu-id="22ed6-142">Add the following markup beneath the `<siteMapNode>` for the Content to Master Page Interaction lesson:</span></span>


[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample1.xml)]

<span data-ttu-id="22ed6-143">此加法`<siteMapNode>`元素反映在课程列表 （请参阅图 5）。</span><span class="sxs-lookup"><span data-stu-id="22ed6-143">The addition of this `<siteMapNode>` element is reflected in the Lessons list (see Figure 5).</span></span>

<span data-ttu-id="22ed6-144">返回到`Products.aspx`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-144">Return to `Products.aspx`.</span></span> <span data-ttu-id="22ed6-145">中的内容控件`MainContent`中，添加 GridView 控件并将其命名`ProductsGrid`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-145">In the Content control for `MainContent`, add a GridView control and name it `ProductsGrid`.</span></span> <span data-ttu-id="22ed6-146">将 GridView 绑定到名为的新 SqlDataSource 控件`ProductsDataSource`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-146">Bind the GridView to a new SqlDataSource control named `ProductsDataSource`.</span></span>


[![B<span data-ttu-id="22ed6-147">ind 新 SqlDataSource 控件为 GridView]</span><span class="sxs-lookup"><span data-stu-id="22ed6-147">ind the GridView to a New SqlDataSource Control]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image4.png)

<span data-ttu-id="22ed6-148">**图 02**:将 GridView 绑定到新的 SqlDataSource 控件 ([单击此项可查看原尺寸图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-148">**Figure 02**: Bind the GridView to a New SqlDataSource Control  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image6.png))</span></span>


<span data-ttu-id="22ed6-149">将向导配置，使其使用 Northwind 数据库。</span><span class="sxs-lookup"><span data-stu-id="22ed6-149">Configure the wizard so that it uses the Northwind database.</span></span> <span data-ttu-id="22ed6-150">如果您已完成上一教程中，则应该已拥有一个名为的连接字符串`NorthwindConnectionString`在`Web.config`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-150">If you worked through the previous tutorial then you should already have a connection string named `NorthwindConnectionString` in `Web.config`.</span></span> <span data-ttu-id="22ed6-151">从下拉列表中，选择此连接字符串，如图 3 中所示。</span><span class="sxs-lookup"><span data-stu-id="22ed6-151">Choose this connection string from the drop-down list, as shown in Figure 3.</span></span>


[![C<span data-ttu-id="22ed6-152">配置 SqlDataSource 使用 Northwind 数据库]</span><span class="sxs-lookup"><span data-stu-id="22ed6-152">onfigure the SqlDataSource to Use the Northwind Database]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image7.png)

<span data-ttu-id="22ed6-153">**图 03**:配置 SqlDataSource 使用 Northwind 数据库 ([单击此项可查看原尺寸图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-153">**Figure 03**: Configure the SqlDataSource to Use the Northwind Database  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image9.png))</span></span>


<span data-ttu-id="22ed6-154">接下来，指定数据源控件`SELECT`通过从下拉列表中选择产品表并返回语句`ProductName`和`UnitPrice`（请参阅图 4） 的列。</span><span class="sxs-lookup"><span data-stu-id="22ed6-154">Next, specify the data source control's `SELECT` statement by choosing the Products table from the drop-down list and returning the `ProductName` and `UnitPrice` columns (see Figure 4).</span></span> <span data-ttu-id="22ed6-155">单击下一步并在完成以完成配置数据源向导。</span><span class="sxs-lookup"><span data-stu-id="22ed6-155">Click Next and then Finish to complete the Configure Data Source wizard.</span></span>


[![R<span data-ttu-id="22ed6-156">eturn 产品名称和产品表中的单价字段]</span><span class="sxs-lookup"><span data-stu-id="22ed6-156">eturn the ProductName and UnitPrice Fields from the Products Table]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image10.png)

<span data-ttu-id="22ed6-157">**图 04**:返回`ProductName`并`UnitPrice`字段从`Products`表 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-157">**Figure 04**: Return the `ProductName` and `UnitPrice` Fields from the `Products` Table  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image12.png))</span></span>


<span data-ttu-id="22ed6-158">就这么简单！</span><span class="sxs-lookup"><span data-stu-id="22ed6-158">That's all there is to it!</span></span> <span data-ttu-id="22ed6-159">完成向导后 Visual Studio 将两个 BoundFields 添加到 GridView 镜像 SqlDataSource 控件返回的两个字段。</span><span class="sxs-lookup"><span data-stu-id="22ed6-159">After completing the wizard Visual Studio adds two BoundFields to the GridView to mirror the two fields returned by the SqlDataSource control.</span></span> <span data-ttu-id="22ed6-160">遵循 GridView 和 SqlDataSource 控件的标记。</span><span class="sxs-lookup"><span data-stu-id="22ed6-160">The GridView and SqlDataSource controls' markup follows.</span></span> <span data-ttu-id="22ed6-161">图 5 显示了通过浏览器查看时的结果。</span><span class="sxs-lookup"><span data-stu-id="22ed6-161">Figure 5 shows the results when viewed through a browser.</span></span>


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample2.aspx)]


[![E<span data-ttu-id="22ed6-162">支票产品和它的价格是 GridView 中列出的]</span><span class="sxs-lookup"><span data-stu-id="22ed6-162">ach Product and its Price is Listed in the GridView]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image13.png)

<span data-ttu-id="22ed6-163">**图 05**:GridView 中列出每个产品和它的价格 ([单击此项可查看原尺寸图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-163">**Figure 05**: Each Product and its Price is Listed in the GridView  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image15.png))</span></span>


> [!NOTE]
> <span data-ttu-id="22ed6-164">随意清理的 GridView 的外观。</span><span class="sxs-lookup"><span data-stu-id="22ed6-164">Feel free to clean up the appearance of the GridView.</span></span> <span data-ttu-id="22ed6-165">某些建议包括格式化为货币的显示的单价值以及如何使用背景颜色和字体以改善该网格的外观。</span><span class="sxs-lookup"><span data-stu-id="22ed6-165">Some suggestions include formatting the displayed UnitPrice value as a currency and using background colors and fonts to improve the grid's appearance.</span></span> <span data-ttu-id="22ed6-166">有关显示和格式设置在 ASP.NET 中的数据的详细信息，请参阅我[使用数据的系列教程](../../data-access/index.md)。</span><span class="sxs-lookup"><span data-stu-id="22ed6-166">For more information on displaying and formatting data in ASP.NET, refer to my [Working with Data tutorial series](../../data-access/index.md).</span></span>


## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a><span data-ttu-id="22ed6-167">步骤 2：将双精度价格按钮添加到母版页</span><span class="sxs-lookup"><span data-stu-id="22ed6-167">Step 2: Adding a Double Prices Button to the Master Page</span></span>

<span data-ttu-id="22ed6-168">我们的下一个任务是要添加到主按钮 Web 控件页上，单击时，将双精度的数据库中的所有产品的价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-168">Our next task is to add a Button Web control to the master page that, when clicked, will double the price of all products in the database.</span></span> <span data-ttu-id="22ed6-169">打开`Site.master`母版页和将一个按钮从工具箱拖到设计器中，将其下放置`RecentProductsDataSource`SqlDataSource 控件，我们添加了在上一教程。</span><span class="sxs-lookup"><span data-stu-id="22ed6-169">Open the `Site.master` master page and drag a Button from the Toolbox onto the Designer, placing it beneath the `RecentProductsDataSource` SqlDataSource control we added in the previous tutorial.</span></span> <span data-ttu-id="22ed6-170">设置按钮的`ID`属性设置为`DoublePrice`并将其`Text`属性设置为"双产品价格"。</span><span class="sxs-lookup"><span data-stu-id="22ed6-170">Set the Button's `ID` property to `DoublePrice` and its `Text` property to "Double Product Prices".</span></span>

<span data-ttu-id="22ed6-171">接下来，将使用 SqlDataSource 控件添加到主页上，其命名为`DoublePricesDataSource`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-171">Next, add a SqlDataSource control to the master page, naming it `DoublePricesDataSource`.</span></span> <span data-ttu-id="22ed6-172">此 SqlDataSource 将用于执行`UPDATE`语句翻倍，所有价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-172">This SqlDataSource will be used to execute the `UPDATE` statement to double all prices.</span></span> <span data-ttu-id="22ed6-173">具体而言，我们需要设置其`ConnectionString`并`UpdateCommand`属性设置为适当的连接字符串和`UPDATE`语句。</span><span class="sxs-lookup"><span data-stu-id="22ed6-173">Specifically, we need to set its `ConnectionString` and `UpdateCommand` properties to the appropriate connection string and `UPDATE` statement.</span></span> <span data-ttu-id="22ed6-174">然后我们需要调用此 SqlDataSource 控件`Update`方法时`DoublePrice`单击按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-174">Then we need to call this SqlDataSource control's `Update` method when the `DoublePrice` Button is clicked.</span></span> <span data-ttu-id="22ed6-175">若要设置`ConnectionString`和`UpdateCommand`属性中，选择 SqlDataSource 控件，然后转到属性窗口。</span><span class="sxs-lookup"><span data-stu-id="22ed6-175">To set the `ConnectionString` and `UpdateCommand` properties, select the SqlDataSource control and then go to the Properties window.</span></span> <span data-ttu-id="22ed6-176">`ConnectionString`属性列出了已存储在这些连接字符串`Web.config`在下拉列表中; 选择`NorthwindConnectionString`选项如图 6 中所示。</span><span class="sxs-lookup"><span data-stu-id="22ed6-176">The `ConnectionString` property lists those connection strings already stored in `Web.config` in a drop-down list; choose the `NorthwindConnectionString` option as shown in Figure 6.</span></span>


[![C<span data-ttu-id="22ed6-177">配置 SqlDataSource 使用 NorthwindConnectionString]</span><span class="sxs-lookup"><span data-stu-id="22ed6-177">onfigure the SqlDataSource to Use the NorthwindConnectionString]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image16.png)

<span data-ttu-id="22ed6-178">**图 06**:配置为使用 SqlDataSource `NorthwindConnectionString` ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-178">**Figure 06**: Configure the SqlDataSource to Use the `NorthwindConnectionString` ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image18.png))</span></span>


<span data-ttu-id="22ed6-179">若要设置`UpdateCommand`属性，在属性窗口中找到 UpdateQuery 选项。</span><span class="sxs-lookup"><span data-stu-id="22ed6-179">To set the `UpdateCommand` property, locate the UpdateQuery option in the Properties window.</span></span> <span data-ttu-id="22ed6-180">此属性，请选中时，显示一个具有省略号; 的按钮单击此按钮将显示在图 7 所示的命令和参数编辑器对话框。</span><span class="sxs-lookup"><span data-stu-id="22ed6-180">This property, when selected, displays a button with ellipses; click this button to display the Command and Parameter Editor dialog box shown in Figure 7.</span></span> <span data-ttu-id="22ed6-181">键入以下内容`UPDATE`到对话框的文本框中的语句：</span><span class="sxs-lookup"><span data-stu-id="22ed6-181">Type the following `UPDATE` statement into the dialog box's textbox:</span></span>


[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample3.sql)]

<span data-ttu-id="22ed6-182">此语句中，执行时，将会翻倍`UnitPrice`值中的每条`Products`表。</span><span class="sxs-lookup"><span data-stu-id="22ed6-182">This statement, when executed, will double the `UnitPrice` value for each record in the `Products` table.</span></span>


[![S<span data-ttu-id="22ed6-183">et SqlDataSource 的 UpdateCommand 属性]</span><span class="sxs-lookup"><span data-stu-id="22ed6-183">et SqlDataSource's UpdateCommand Property]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image19.png)

<span data-ttu-id="22ed6-184">**图 07**:设置的 SqlDataSource`UpdateCommand`属性 ([单击以查看实际尺寸的图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-184">**Figure 07**: Set SqlDataSource's `UpdateCommand` Property  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image21.png))</span></span>


<span data-ttu-id="22ed6-185">以后设置这些属性，这些按钮和 SqlDataSource 控件的声明性标记看起来应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="22ed6-185">After setting these properties, your Button and SqlDataSource controls' declarative markup should look similar to the following:</span></span>


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample4.aspx)]

<span data-ttu-id="22ed6-186">剩下的就是调用其`Update`方法时`DoublePrice`单击按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-186">All that remains is to call its `Update` method when the `DoublePrice` Button is clicked.</span></span> <span data-ttu-id="22ed6-187">创建`Click`事件处理程序`DoublePrice`按钮并添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="22ed6-187">Create a `Click` event handler for the `DoublePrice` Button and add the following code:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample5.cs)]

<span data-ttu-id="22ed6-188">若要测试此功能，请访问`~/Admin/Products.aspx`页面，我们在步骤 1 中创建，并单击"双产品价格"按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-188">To test this functionality, visit the `~/Admin/Products.aspx` page we created in Step 1 and click the "Double Product Prices" button.</span></span> <span data-ttu-id="22ed6-189">单击按钮会导致回发，并执行`DoublePrice`按钮的`Click`事件处理程序，使所有产品的价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-189">Clicking the button causes a postback and executes the `DoublePrice` Button's `Click` event handler, doubling the prices of all products.</span></span> <span data-ttu-id="22ed6-190">然后重新呈现页面标记则返回并重新显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="22ed6-190">The page is then re-rendered and the markup is returned and re-displayed in the browser.</span></span> <span data-ttu-id="22ed6-191">GridView 中内容页上，但是，列出了相同的价格"双产品价格"按钮被单击。</span><span class="sxs-lookup"><span data-stu-id="22ed6-191">The GridView in the content page, however, lists the same prices as before the "Double Product Prices" button was clicked.</span></span> <span data-ttu-id="22ed6-192">这是因为最初加载在 GridView 中的数据必须存储在视图状态，因此它不重新加载在回发除非规定，否则其状态。</span><span class="sxs-lookup"><span data-stu-id="22ed6-192">This is because the data initially loaded in the GridView had its state stored in view state, so it's not reloaded on postbacks unless instructed otherwise.</span></span> <span data-ttu-id="22ed6-193">如果访问不同的页面，然后返回到`~/Admin/Products.aspx`页上，将看到更新后的价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-193">If you visit a different page and then return to the `~/Admin/Products.aspx` page you'll see the updated prices.</span></span>

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a><span data-ttu-id="22ed6-194">步骤 3：引发事件时的价格将增加一倍</span><span class="sxs-lookup"><span data-stu-id="22ed6-194">Step 3: Raising an Event When the Prices are Doubled</span></span>

<span data-ttu-id="22ed6-195">因为在 GridView`~/Admin/Products.aspx`页不会立即反映价格加倍，用户可以理解的是可能会认为它们未单击"双产品价格"按钮，否则它不起作用。</span><span class="sxs-lookup"><span data-stu-id="22ed6-195">Because the GridView in the `~/Admin/Products.aspx` page does not immediately reflect the price doubling, a user may understandably think that they did not click the "Double Product Prices" button, or that it didn't work.</span></span> <span data-ttu-id="22ed6-196">它们可以尝试单击按钮更多时间，反复地价格乘 2。</span><span class="sxs-lookup"><span data-stu-id="22ed6-196">They may try clicking the button a few more times, doubling the prices again and again.</span></span> <span data-ttu-id="22ed6-197">若要修复此，我们需要的内容中有在网格页的新价格后立即显示它们增加一倍。</span><span class="sxs-lookup"><span data-stu-id="22ed6-197">To fix this we need to have the grid in the content page display the new prices immediately after they are doubled.</span></span>

<span data-ttu-id="22ed6-198">在本教程前面所述，我们需要引发母版页中的事件，每当用户单击`DoublePrice`按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-198">As discussed earlier in this tutorial, we need to raise an event in the master page whenever the user clicks the `DoublePrice` Button.</span></span> <span data-ttu-id="22ed6-199">事件是一个类 （事件发布者） 的方式通知另一组的一些有趣的事情发生了其他类 （事件订阅服务器）。</span><span class="sxs-lookup"><span data-stu-id="22ed6-199">An event is a way for one class (an event publisher) to notify another a set of other classes (the event subscribers) that something interesting has occurred.</span></span> <span data-ttu-id="22ed6-200">在此示例中，主页面是事件发布服务器。这些内容时要注意的页`DoublePrice`单击按钮是订阅服务器。</span><span class="sxs-lookup"><span data-stu-id="22ed6-200">In this example, the master page is the event publisher; those content pages that care about when the `DoublePrice` Button is clicked are the subscribers.</span></span>

<span data-ttu-id="22ed6-201">一个类，通过创建订阅的事件*事件处理程序*，这是在响应所引发的事件中执行的方法。</span><span class="sxs-lookup"><span data-stu-id="22ed6-201">A class subscribes to an event by creating an *event handler*, which is a method that is executed in response to the event being raised.</span></span> <span data-ttu-id="22ed6-202">发布服务器上定义他通过定义引发的事件*事件委托*。</span><span class="sxs-lookup"><span data-stu-id="22ed6-202">The publisher defines the events he raises by defining an *event delegate*.</span></span> <span data-ttu-id="22ed6-203">事件委托指定的事件处理程序必须接受的输入的参数。</span><span class="sxs-lookup"><span data-stu-id="22ed6-203">The event delegate specifies what input parameters the event handler must accept.</span></span> <span data-ttu-id="22ed6-204">在.NET Framework 中，事件委托执行不返回任何值，并接受两个输入的参数：</span><span class="sxs-lookup"><span data-stu-id="22ed6-204">In the .NET Framework, event delegates do not return any value and accept two input parameters:</span></span>

- <span data-ttu-id="22ed6-205">`Object`，用于标识事件源和</span><span class="sxs-lookup"><span data-stu-id="22ed6-205">An `Object`, which identifies the event source, and</span></span>
- <span data-ttu-id="22ed6-206">派生自的类</span><span class="sxs-lookup"><span data-stu-id="22ed6-206">A class derived from</span></span> `System.EventArgs`

<span data-ttu-id="22ed6-207">第二个参数传递给事件处理程序可以包括有关事件的其他信息。</span><span class="sxs-lookup"><span data-stu-id="22ed6-207">The second parameter passed to an event handler can include additional information about the event.</span></span> <span data-ttu-id="22ed6-208">虽然基`EventArgs`类不传递任何信息、.NET Framework 包括大量的扩展的类`EventArgs`和包含其他属性。</span><span class="sxs-lookup"><span data-stu-id="22ed6-208">While the base `EventArgs` class does not pass along any information, the .NET Framework includes a number of classes that extend `EventArgs` and encompass additional properties.</span></span> <span data-ttu-id="22ed6-209">例如，`CommandEventArgs`实例传递给事件处理程序响应`Command`事件，并包括两个信息性的属性：`CommandArgument`和`CommandName`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-209">For example, a `CommandEventArgs` instance is passed to event handlers that respond to the `Command` event, and includes two informational properties: `CommandArgument` and `CommandName`.</span></span>

> [!NOTE]
> <span data-ttu-id="22ed6-210">有关创建的详细信息，提高，和处理事件，请参阅[事件和委托](https://msdn.microsoft.com/library/17sde2xt.aspx)并[简单英语中的事件委托](http://www.codeproject.com/KB/cs/eventdelegates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="22ed6-210">For more information on creating, raising, and handling events, see [Events and Delegates](https://msdn.microsoft.com/library/17sde2xt.aspx) and [Event Delegates in Simple English](http://www.codeproject.com/KB/cs/eventdelegates.aspx).</span></span>


<span data-ttu-id="22ed6-211">若要定义一个事件，请使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="22ed6-211">To define an event use the following syntax:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample6.cs)]

<span data-ttu-id="22ed6-212">因为我们只需要用户单击时发出警报内容页`DoublePrice`按钮并不需要传递任何其他附加信息，我们可以使用事件委托`EventHandler`，用于定义的事件处理程序接受作为第二个操作数参数类型的对象`System.EventArgs`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-212">Because we only need to alert the content page when the user has clicked the `DoublePrice` Button and do not need to pass along any other additional information, we can use the event delegate `EventHandler`, which defines an event handler that accepts as its second parameter an object of type `System.EventArgs`.</span></span> <span data-ttu-id="22ed6-213">若要创建主页面中的事件，请到母版页的代码隐藏类添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="22ed6-213">To create the event in the master page, add the following line of code to the master page's code-behind class:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample7.cs)]

<span data-ttu-id="22ed6-214">上面的代码将公共事件添加到名为母版页`PricesDoubled`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-214">The above code adds a public event to the master page named `PricesDoubled`.</span></span> <span data-ttu-id="22ed6-215">现在，我们需要引发此事件后的价格已增加一倍。</span><span class="sxs-lookup"><span data-stu-id="22ed6-215">We now need to raise this event after the prices have been doubled.</span></span> <span data-ttu-id="22ed6-216">若要引发事件，请使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="22ed6-216">To raise an event use the following syntax:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample8.cs)]

<span data-ttu-id="22ed6-217">其中*发件人*并*eventArgs*是你想要传递到订阅服务器的事件处理程序的值。</span><span class="sxs-lookup"><span data-stu-id="22ed6-217">Where *sender* and *eventArgs* are the values you want to pass to the subscriber's event handler.</span></span>

<span data-ttu-id="22ed6-218">更新`DoublePrice``Click`事件处理程序使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="22ed6-218">Update the `DoublePrice` `Click` event handler with the following code:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample9.cs)]

<span data-ttu-id="22ed6-219">与前面一样，`Click`事件处理程序通过调用来启动`DoublePricesDataSource`SqlDataSource 控件`Update`方法翻倍的所有产品的价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-219">As before, the `Click` event handler starts by calling the `DoublePricesDataSource` SqlDataSource control's `Update` method to double the prices of all products.</span></span> <span data-ttu-id="22ed6-220">以下有两个添加到事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="22ed6-220">Following that there are two additions to the event handler.</span></span> <span data-ttu-id="22ed6-221">首先， `RecentProducts` GridView 的数据刷新。</span><span class="sxs-lookup"><span data-stu-id="22ed6-221">First, the `RecentProducts` GridView's data is refreshed.</span></span> <span data-ttu-id="22ed6-222">此 GridView 已添加到母版页中前面的教程，并显示最近添加的五种产品。</span><span class="sxs-lookup"><span data-stu-id="22ed6-222">This GridView was added to the master page in the preceding tutorial and displays the five most recently-added products.</span></span> <span data-ttu-id="22ed6-223">我们需要刷新该网格，使之显示这些五种产品的只是双写价格。</span><span class="sxs-lookup"><span data-stu-id="22ed6-223">We need to refresh this grid so that it shows the just-doubled prices for these five products.</span></span> <span data-ttu-id="22ed6-224">之后，`PricesDoubled`引发事件。</span><span class="sxs-lookup"><span data-stu-id="22ed6-224">Following that, the `PricesDoubled` event is raised.</span></span> <span data-ttu-id="22ed6-225">对主页面本身的引用 (`this`) 作为事件源和一个空发送到事件处理程序`EventArgs`作为事件参数发送对象。</span><span class="sxs-lookup"><span data-stu-id="22ed6-225">A reference to the master page itself (`this`) is sent to the event handler as the event source and an empty `EventArgs` object is sent as the event arguments.</span></span>

## <a name="step-4-handling-the-event-in-the-content-page"></a><span data-ttu-id="22ed6-226">步骤 4：处理内容页中的事件</span><span class="sxs-lookup"><span data-stu-id="22ed6-226">Step 4: Handling the Event in the Content Page</span></span>

<span data-ttu-id="22ed6-227">主页面现在引发其`PricesDoubled`事件时`DoublePrice`单击按钮控件。</span><span class="sxs-lookup"><span data-stu-id="22ed6-227">At this point the master page raises its `PricesDoubled` event whenever the `DoublePrice` Button control is clicked.</span></span> <span data-ttu-id="22ed6-228">但是，这是只完成了一半任务-我们仍需处理订阅服务器中的事件。</span><span class="sxs-lookup"><span data-stu-id="22ed6-228">However, this is only half the battle - we still need to handle the event in the subscriber.</span></span> <span data-ttu-id="22ed6-229">这涉及到两个步骤： 创建事件处理程序并添加事件绑定代码，以便当引发事件时执行的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="22ed6-229">This involves two steps: creating the event handler and adding event wiring code so that when the event is raised the event handler is executed.</span></span>

<span data-ttu-id="22ed6-230">首先，创建名为一个事件处理程序`Master_PricesDoubled`。</span><span class="sxs-lookup"><span data-stu-id="22ed6-230">Start by creating an event handler named `Master_PricesDoubled`.</span></span> <span data-ttu-id="22ed6-231">由于我们是如何定义`PricesDoubled`母版页中的事件的事件处理程序的两个输入的参数必须是类型`Object`和`EventArgs`分别。</span><span class="sxs-lookup"><span data-stu-id="22ed6-231">Because of how we defined the `PricesDoubled` event in the master page the event handler's two input parameters must be of types `Object` and `EventArgs`, respectively.</span></span> <span data-ttu-id="22ed6-232">在事件处理程序调用`ProductsGrid`GridView 的`DataBind`方法重新绑定到网格的数据。</span><span class="sxs-lookup"><span data-stu-id="22ed6-232">In the event handler call the `ProductsGrid` GridView's `DataBind` method to rebind the data to the grid.</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample10.cs)]

<span data-ttu-id="22ed6-233">事件处理程序的代码已完成，但我们尚未为关联母版页的`PricesDoubled`到此事件处理程序的事件。</span><span class="sxs-lookup"><span data-stu-id="22ed6-233">The code for the event handler is complete but we've yet to wire the master page's `PricesDoubled` event to this event handler.</span></span> <span data-ttu-id="22ed6-234">订阅服务器上将事件与事件处理程序通过以下语法：</span><span class="sxs-lookup"><span data-stu-id="22ed6-234">The subscriber wires an event to an event handler via the following syntax:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample11.cs)]

<span data-ttu-id="22ed6-235">*发布服务器*是对提供事件的对象的引用*eventName*，和*methodName*是在订阅服务器具有与对应的签名中定义的事件处理程序的名称*eventDelegate*。</span><span class="sxs-lookup"><span data-stu-id="22ed6-235">*publisher* is a reference to the object that offers the event *eventName*, and *methodName* is the name of the event handler defined in the subscriber that has a signature corresponding to the *eventDelegate*.</span></span> <span data-ttu-id="22ed6-236">换而言之，如果事件委托是`EventHandler`，然后*methodName*必须是不会返回一个值，并接受两个输入参数的类型的订阅服务器中的方法的名称`Object`和`EventArgs`，分别。</span><span class="sxs-lookup"><span data-stu-id="22ed6-236">In other words, if the event delegate is `EventHandler`, then *methodName* must be the name of a method in the subscriber that does not return a value and accepts two input parameters of types `Object` and `EventArgs`, respectively.</span></span>

<span data-ttu-id="22ed6-237">此事件绑定代码必须执行的第一次页面访问和后续回发，而应出现在之前可能会引发该事件时的页面生命周期中的点。</span><span class="sxs-lookup"><span data-stu-id="22ed6-237">This event wiring code must be executed on the first page visit and subsequent postbacks and should occur at a point in the page lifecycle that precedes when the event may be raised.</span></span> <span data-ttu-id="22ed6-238">添加事件绑定代码的好时机是在 PreInit 阶段中，很早在页面生命周期中出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="22ed6-238">A good time to add event wiring code is in the PreInit stage, which occurs very early in the page lifecycle.</span></span>

<span data-ttu-id="22ed6-239">打开`~/Admin/Products.aspx`并创建`Page_PreInit`事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="22ed6-239">Open `~/Admin/Products.aspx` and create a `Page_PreInit` event handler:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample12.cs)]

<span data-ttu-id="22ed6-240">若要完成此绑定代码，我们需要对主页面从内容页的以编程方式引用。</span><span class="sxs-lookup"><span data-stu-id="22ed6-240">In order to complete this wiring code we need a programmatic reference to the master page from the content page.</span></span> <span data-ttu-id="22ed6-241">上一教程中所述，有两种方法来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="22ed6-241">As noted in the previous tutorial, there are two ways to do this:</span></span>

- <span data-ttu-id="22ed6-242">通过强制转换松散类型`Page.Master`属性设置为适当的母版页类型，或</span><span class="sxs-lookup"><span data-stu-id="22ed6-242">By casting the loosely-typed `Page.Master` property to the appropriate master page type, or</span></span>
- <span data-ttu-id="22ed6-243">通过添加`@MasterType`指令`.aspx`页，然后使用强类型`Master`属性。</span><span class="sxs-lookup"><span data-stu-id="22ed6-243">By adding a `@MasterType` directive in the `.aspx` page and then using the strongly-typed `Master` property.</span></span>

<span data-ttu-id="22ed6-244">让我们使用后一种方法。</span><span class="sxs-lookup"><span data-stu-id="22ed6-244">Let's use the latter approach.</span></span> <span data-ttu-id="22ed6-245">以下代码添加到`@MasterType`指令的声明性标记中页面的顶部：</span><span class="sxs-lookup"><span data-stu-id="22ed6-245">Add the following `@MasterType` directive to the top of the page's declarative markup:</span></span>


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample13.aspx)]

<span data-ttu-id="22ed6-246">然后添加以下事件绑定代码在`Page_PreInit`事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="22ed6-246">Then add the following event wiring code in the `Page_PreInit` event handler:</span></span>


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample14.cs)]

<span data-ttu-id="22ed6-247">在内容页中的 GridView 刷新使用此代码，只要`DoublePrice`单击按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-247">With this code in place, the GridView in the content page is refreshed whenever the `DoublePrice` Button is clicked.</span></span>

<span data-ttu-id="22ed6-248">图 8 和 9 说明了此行为。</span><span class="sxs-lookup"><span data-stu-id="22ed6-248">Figures 8 and 9 illustrate this behavior.</span></span> <span data-ttu-id="22ed6-249">图 8 显示了页面在首次访问时。</span><span class="sxs-lookup"><span data-stu-id="22ed6-249">Figure 8 shows the page when first visited.</span></span> <span data-ttu-id="22ed6-250">请注意，在这种价格值`RecentProducts`（在主页面的左侧列） 的 GridView 和`ProductsGrid`GridView （在内容页）。</span><span class="sxs-lookup"><span data-stu-id="22ed6-250">Note that price values in both the `RecentProducts` GridView (in the left column of the master page) and the `ProductsGrid` GridView (in the content page).</span></span> <span data-ttu-id="22ed6-251">图 9 显示了相同屏幕后立即`DoublePrice`单击按钮。</span><span class="sxs-lookup"><span data-stu-id="22ed6-251">Figure 9 shows the same screen immediately after the `DoublePrice` Button has been clicked.</span></span> <span data-ttu-id="22ed6-252">正如您所看到的新价格会立即反映在这两个 Gridview。</span><span class="sxs-lookup"><span data-stu-id="22ed6-252">As you can see, the new prices are instantaneously reflected in both GridViews.</span></span>


[![T<span data-ttu-id="22ed6-253">他初始价格值]</span><span class="sxs-lookup"><span data-stu-id="22ed6-253">he Initial Price Values]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image22.png)

<span data-ttu-id="22ed6-254">**图 08**:初始的价格值 ([单击此项可查看原尺寸图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-254">**Figure 08**: The Initial Price Values  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image24.png))</span></span>


[![T<span data-ttu-id="22ed6-255">在 Gridview 中显示他 Just-Doubled 价格]</span><span class="sxs-lookup"><span data-stu-id="22ed6-255">he Just-Doubled Prices are Displayed in the GridViews]</span></span>(interacting-with-the-content-page-from-the-master-page-cs/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image25.png)

<span data-ttu-id="22ed6-256">**图 09**:在 Gridview 中显示 Just-Doubled 价格 ([单击此项可查看原尺寸图像](interacting-with-the-content-page-from-the-master-page-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="22ed6-256">**Figure 09**: The Just-Doubled Prices are Displayed in the GridViews  ([Click to view full-size image](interacting-with-the-content-page-from-the-master-page-cs/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="22ed6-257">总结</span><span class="sxs-lookup"><span data-stu-id="22ed6-257">Summary</span></span>

<span data-ttu-id="22ed6-258">理想情况下，主页面和其内容的页面是从另一个完全独立，不需要交互的任何级别。</span><span class="sxs-lookup"><span data-stu-id="22ed6-258">Ideally, a master page and its content pages are completely separate from one another and require no level of interaction.</span></span> <span data-ttu-id="22ed6-259">但是，如果你有主页面或内容页面，其中显示可以从主页或内容页面修改的数据，然后您可能需要具有母版页内容页 （或进行相反的转换） 发出警报，以便可以更新显示的数据修改时。</span><span class="sxs-lookup"><span data-stu-id="22ed6-259">However, if you have a master page or content page that displays data that can be modified from the master page or content page, then you may need to have the master page alert the content page (or vice-a-versa) when data is modified so that the display can be updated.</span></span> <span data-ttu-id="22ed6-260">在前面的教程中我们已了解如何以编程方式与其主页面; 进行交互的内容页面在本教程中我们介绍了如何通过母版页启动交互。</span><span class="sxs-lookup"><span data-stu-id="22ed6-260">In the preceding tutorial we saw how to have a content page programmatically interact with its master page; in this tutorial we looked at how to have a master page initiate the interaction.</span></span>

<span data-ttu-id="22ed6-261">虽然编程交互内容和母版页之间可以源自的内容或母版页，所使用的交互模式取决于资助创始费。</span><span class="sxs-lookup"><span data-stu-id="22ed6-261">While programmatic interaction between a content and master page can originate from either the content or master page, the interaction pattern used depends on the origination.</span></span> <span data-ttu-id="22ed6-262">差异是由于访问的内容页面含有单个主页面，但主页面可能有许多不同的内容页面。</span><span class="sxs-lookup"><span data-stu-id="22ed6-262">The differences are due to the fact that a content page has a single master page, but a master page can have many different content pages.</span></span> <span data-ttu-id="22ed6-263">而不是让母版页与内容页直接交互，更好的方法将引发一个事件来指示某项操作已发生的母版页。</span><span class="sxs-lookup"><span data-stu-id="22ed6-263">Rather than having a master page directly interact with a content page, a better approach is to have the master page raise an event to signal that some action has taken place.</span></span> <span data-ttu-id="22ed6-264">有关操作处理这些内容页可以创建事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="22ed6-264">Those content pages that care about the action can create event handlers.</span></span>

<span data-ttu-id="22ed6-265">快乐编程 ！</span><span class="sxs-lookup"><span data-stu-id="22ed6-265">Happy Programming!</span></span>

### <a name="further-reading"></a><span data-ttu-id="22ed6-266">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="22ed6-266">Further Reading</span></span>

<span data-ttu-id="22ed6-267">在本教程中讨论的主题的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="22ed6-267">For more information on the topics discussed in this tutorial, refer to the following resources:</span></span>

- [<span data-ttu-id="22ed6-268">访问和更新在 ASP.NET 中的数据</span><span class="sxs-lookup"><span data-stu-id="22ed6-268">Accessing and Updating Data in ASP.NET</span></span>](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [<span data-ttu-id="22ed6-269">事件和委托</span><span class="sxs-lookup"><span data-stu-id="22ed6-269">Events and Delegates</span></span>](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [<span data-ttu-id="22ed6-270">内容和母版页之间传递信息</span><span class="sxs-lookup"><span data-stu-id="22ed6-270">Passing Information Between Content and Master Pages</span></span>](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [<span data-ttu-id="22ed6-271">在 ASP.NET 教程中使用的数据</span><span class="sxs-lookup"><span data-stu-id="22ed6-271">Working with Data in ASP.NET Tutorials</span></span>](../../data-access/index.md)

### <a name="about-the-author"></a><span data-ttu-id="22ed6-272">关于作者</span><span class="sxs-lookup"><span data-stu-id="22ed6-272">About the Author</span></span>

<span data-ttu-id="22ed6-273">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。</span><span class="sxs-lookup"><span data-stu-id="22ed6-273">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of multiple ASP/ASP.NET books and founder of 4GuysFromRolla.com, has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="22ed6-274">Scott 是独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="22ed6-274">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="22ed6-275">他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="22ed6-275">His latest book is [*Sams Teach Yourself ASP.NET 3.5 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco).</span></span> <span data-ttu-id="22ed6-276">可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。</span><span class="sxs-lookup"><span data-stu-id="22ed6-276">Scott can be reached at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) or via his blog at [http://ScottOnWriting.NET](http://scottonwriting.net/).</span></span>

### <a name="special-thanks-to"></a><span data-ttu-id="22ed6-277">特别感谢</span><span class="sxs-lookup"><span data-stu-id="22ed6-277">Special Thanks To</span></span>

<span data-ttu-id="22ed6-278">很多有用的审阅者已评审本系列教程。</span><span class="sxs-lookup"><span data-stu-id="22ed6-278">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="22ed6-279">本教程中的潜在顾客审阅者已 Suchi Banerjee。</span><span class="sxs-lookup"><span data-stu-id="22ed6-279">Lead reviewer for this tutorial was Suchi Banerjee.</span></span> <span data-ttu-id="22ed6-280">是否有兴趣查看我即将推出的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="22ed6-280">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="22ed6-281">如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="22ed6-281">If so, drop me a line at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22ed6-282">[上一页](interacting-with-the-master-page-from-the-content-page-cs.md)
> [下一页](master-pages-and-asp-net-ajax-cs.md)</span><span class="sxs-lookup"><span data-stu-id="22ed6-282">[Previous](interacting-with-the-master-page-from-the-content-page-cs.md)
[Next](master-pages-and-asp-net-ajax-cs.md)</span></span>

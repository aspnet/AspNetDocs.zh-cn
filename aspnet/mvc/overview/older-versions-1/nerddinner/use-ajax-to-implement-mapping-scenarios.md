---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 实现映射方案 |Microsoft Docs
author: rick-anderson
description: 步骤11显示了如何将 AJAX 映射支持集成到 NerdDinner 应用程序中，从而允许正在创建、编辑或查看就的用户查看 .。。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 03b3a27d4b761d0417160b95cc6f39a345385065
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044319"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="a83bf-103">使用 AJAX 实现映射方案</span><span class="sxs-lookup"><span data-stu-id="a83bf-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="a83bf-104">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a83bf-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="a83bf-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a83bf-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a83bf-106">这是免费的 ["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md) 的第11步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a83bf-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a83bf-107">步骤11显示了如何将 AJAX 映射支持集成到 NerdDinner 应用程序中，使创建、编辑或查看就的用户能够以图形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="a83bf-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="a83bf-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 或 [Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="a83bf-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="a83bf-109">NerdDinner 步骤11：集成 AJAX 地图</span><span class="sxs-lookup"><span data-stu-id="a83bf-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="a83bf-110">接下来，我们将使应用程序更引人注目，因为集成了 AJAX 映射支持。</span><span class="sxs-lookup"><span data-stu-id="a83bf-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="a83bf-111">这将允许创建、编辑或查看就的用户以图形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="a83bf-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="a83bf-112">创建地图分部视图</span><span class="sxs-lookup"><span data-stu-id="a83bf-112">Creating a Map Partial View</span></span>

<span data-ttu-id="a83bf-113">我们将在应用程序中的多个位置使用映射功能。</span><span class="sxs-lookup"><span data-stu-id="a83bf-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="a83bf-114">为了使我们的代码保持干燥，我们将在单个部分模板中封装常见地图功能，可跨多个控制器操作和视图重复使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="a83bf-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="a83bf-115">我们会将此分部视图命名为 "map .ascx"，并在 \Views\Dinners 目录中创建它。</span><span class="sxs-lookup"><span data-stu-id="a83bf-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="a83bf-116">可以通过右键单击 \Views\Dinners 目录，然后选择 "添加 &gt; 视图" 菜单命令来创建映射 .ascx 部分。</span><span class="sxs-lookup"><span data-stu-id="a83bf-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="a83bf-117">我们会将视图命名为 ".Map"，将其作为分部视图进行检查，并指示我们将向其传递强类型 "晚餐" 模型类：</span><span class="sxs-lookup"><span data-stu-id="a83bf-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="a83bf-118">单击 "添加" 按钮时，将会创建部分模板。</span><span class="sxs-lookup"><span data-stu-id="a83bf-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="a83bf-119">然后，我们将更新映射 .ascx 文件，使其包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="a83bf-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="a83bf-120">第一个 &lt; 脚本 &gt; 引用指向 Microsoft Virtual 地球6.2 映射库。</span><span class="sxs-lookup"><span data-stu-id="a83bf-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="a83bf-121">第二个 &lt; 脚本 &gt; 引用指向稍后将创建的 map.js 文件，这将封装常见的 Javascript 映射逻辑。</span><span class="sxs-lookup"><span data-stu-id="a83bf-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="a83bf-122">&lt;Div id = "theMap" &gt; 元素是 Virtual 地球用来托管地图的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="a83bf-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="a83bf-123">然后，将包含一个 &lt; 嵌入 &gt; 的脚本块，其中包含特定于此视图的两个 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="a83bf-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="a83bf-124">第一个函数使用 jQuery 来连接一个函数，该函数在页面准备好运行客户端脚本时执行。</span><span class="sxs-lookup"><span data-stu-id="a83bf-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="a83bf-125">它会调用 LoadMap ( # A1 helper 函数，我们将在 Map.js 脚本文件中定义该函数以加载虚拟的地图控件。</span><span class="sxs-lookup"><span data-stu-id="a83bf-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="a83bf-126">第二个函数是回调事件处理程序，它将 pin 添加到标识位置的映射。</span><span class="sxs-lookup"><span data-stu-id="a83bf-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="a83bf-127">请注意，我们如何使用 &lt; 客户端脚本块中的服务器端% =% &gt; 块嵌入要映射到 JavaScript 中的晚餐的纬度和经度。</span><span class="sxs-lookup"><span data-stu-id="a83bf-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="a83bf-128">这是一项有用的技术，用于输出可由客户端脚本 (使用的动态值，而无需单独的 AJAX 回调服务器来检索值，从而使其更快) 。</span><span class="sxs-lookup"><span data-stu-id="a83bf-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="a83bf-129">&lt; &gt; 当在服务器上呈现视图时，% =% 块将会执行–因此，HTML 的输出将以嵌入的 JavaScript 值结束， (例如： var 纬度 = 47.64312; ) 。</span><span class="sxs-lookup"><span data-stu-id="a83bf-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="a83bf-130">创建 Map.js 实用工具库</span><span class="sxs-lookup"><span data-stu-id="a83bf-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="a83bf-131">现在，让我们创建一个 Map.js 文件，该文件可用于封装用于映射的 JavaScript 功能 (并实现上述) 上的 LoadMap 和 LoadPin 方法。</span><span class="sxs-lookup"><span data-stu-id="a83bf-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="a83bf-132">为此，我们可以右键单击项目中的 \Scripts 目录，然后选择 "添加- &gt; 新建项" 菜单命令，选择 JScript 项，并将其命名为 "Map.js"。</span><span class="sxs-lookup"><span data-stu-id="a83bf-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="a83bf-133">下面是要添加到 Map.js 文件中的 JavaScript 代码，该文件将与 Virtual 地球交互，以便为就显示地图并为其添加位置 pin：</span><span class="sxs-lookup"><span data-stu-id="a83bf-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="a83bf-134">将地图与创建和编辑表单集成</span><span class="sxs-lookup"><span data-stu-id="a83bf-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="a83bf-135">现在，我们会将地图支持与现有的创建和编辑方案相集成。</span><span class="sxs-lookup"><span data-stu-id="a83bf-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="a83bf-136">好消息是，这是非常简单的操作，不需要我们更改任何控制器代码。</span><span class="sxs-lookup"><span data-stu-id="a83bf-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="a83bf-137">由于我们的 "创建" 和 "编辑" 视图共享公共的 "DinnerForm" 分部视图来实现晚餐窗体 UI，因此可以在一个位置添加地图，同时让创建和编辑方案使用该地图。</span><span class="sxs-lookup"><span data-stu-id="a83bf-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="a83bf-138">我们需要做的就是打开 \Views\Dinners\DinnerForm.ascx 分部视图，并将其更新为包含新的映射部分。</span><span class="sxs-lookup"><span data-stu-id="a83bf-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="a83bf-139">下面是已更新的 DinnerForm 在添加地图后的外观 (注意：下面的代码片段中省略了 HTML 窗体元素以便于简洁) ：</span><span class="sxs-lookup"><span data-stu-id="a83bf-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="a83bf-140">上面的 DinnerForm 部分采用类型为 "DinnerFormViewModel" 的对象作为其模型类型 (因为它需要晚餐对象，以及用于填充) 国家/地区的 dropdownlist 的 SelectList。</span><span class="sxs-lookup"><span data-stu-id="a83bf-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="a83bf-141">我们的地图部分只需要一个 "晚餐" 类型的对象作为其模型类型，因此，当我们呈现地图部分时，我们只会将 DinnerFormViewModel 的晚餐子属性传递给它：</span><span class="sxs-lookup"><span data-stu-id="a83bf-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="a83bf-142">我们添加到部分的 JavaScript 函数使用 jQuery 将 "模糊" 事件附加到 "地址" HTML 文本框。</span><span class="sxs-lookup"><span data-stu-id="a83bf-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="a83bf-143">你可能听说过当用户在文本框中单击或选项卡时激发的 "焦点" 事件。</span><span class="sxs-lookup"><span data-stu-id="a83bf-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="a83bf-144">相反，就是用户退出文本框时激发的 "模糊" 事件。</span><span class="sxs-lookup"><span data-stu-id="a83bf-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="a83bf-145">上述事件处理程序会在发生这种情况时清除纬度和经度文本框的值，然后在地图上绘制新地址位置。</span><span class="sxs-lookup"><span data-stu-id="a83bf-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="a83bf-146">然后，在 map.js 文件中定义的回调事件处理程序将使用虚拟地球基于我们提供的地址的值来更新窗体上的经度和纬度文本框。</span><span class="sxs-lookup"><span data-stu-id="a83bf-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="a83bf-147">现在，当我们再次运行应用程序，然后单击 "主机晚餐" 选项卡时，将看到与标准晚餐窗体元素一起显示的默认地图：</span><span class="sxs-lookup"><span data-stu-id="a83bf-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="a83bf-148">当我们键入地址，然后按 tab 键时，地图会动态更新以显示位置，并且我们的事件处理程序将使用 location 值填充纬度/经度文本框：</span><span class="sxs-lookup"><span data-stu-id="a83bf-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="a83bf-149">如果我们保存新晚餐，然后再次将其打开进行编辑，则会发现当页面加载时，会显示地图位置：</span><span class="sxs-lookup"><span data-stu-id="a83bf-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="a83bf-150">每次更改地址字段时，地图和纬度/经度坐标都将更新。</span><span class="sxs-lookup"><span data-stu-id="a83bf-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="a83bf-151">现在，地图显示晚餐位置，还可以将 "纬度" 和 "经度" 窗体字段从 "可见" 文本框改为隐藏元素，因为在每次) 输入地址时，地图会自动更新 (。</span><span class="sxs-lookup"><span data-stu-id="a83bf-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="a83bf-152">要执行此操作，我们将使用 Html. TextBox ( # A1 HTML helper 来使用 Html. Hidden ( # A3 帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="a83bf-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="a83bf-153">现在，我们的窗体更易于用户理解，并避免 (显示原始纬度/经度，同时还会将它们存储在数据库中的每个晚餐中) ：</span><span class="sxs-lookup"><span data-stu-id="a83bf-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="a83bf-154">将映射与详细信息视图集成</span><span class="sxs-lookup"><span data-stu-id="a83bf-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="a83bf-155">现在，我们已将地图与我们的创建和编辑方案集成，接下来让我们将其与我们的详细方案相集成。</span><span class="sxs-lookup"><span data-stu-id="a83bf-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="a83bf-156">我们需要做的就是在 &lt; &gt; 详细信息视图中调用% RenderPartial ( "map" ) ;%。</span><span class="sxs-lookup"><span data-stu-id="a83bf-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="a83bf-157">下面是 (与地图集成) 的 "完整详细信息" 视图的源代码：</span><span class="sxs-lookup"><span data-stu-id="a83bf-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="a83bf-158">现在，当用户导航到/Dinners/Details/[id] URL 时，他们将看到晚餐的详细信息，地图上晚餐的位置 (使用图钉完成后，当悬停在上方时，将显示晚餐的标题和其地址) ，并为其提供一个指向 RSVP 的 AJAX 链接：</span><span class="sxs-lookup"><span data-stu-id="a83bf-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="a83bf-159">在数据库和存储库中实现位置搜索</span><span class="sxs-lookup"><span data-stu-id="a83bf-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="a83bf-160">若要完成 AJAX 实现，请向应用程序主页添加一个映射，使用户能够以图形方式搜索附近的就。</span><span class="sxs-lookup"><span data-stu-id="a83bf-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="a83bf-161">首先，我们将在数据库和数据存储库层中实现支持，以便有效地执行基于位置的 radius 搜索就。</span><span class="sxs-lookup"><span data-stu-id="a83bf-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="a83bf-162">我们可以使用 SQL 2008 的新的 [地理空间功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 实现此功能，也可以使用以下文章中所述的用于 DRYDEN 的 sql 函数方法： [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 和 "Conery LINQ to SQL 针对发表"。 [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="a83bf-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="a83bf-163">若要实现此方法，我们将在 Visual Studio 中打开 "服务器资源管理器"，选择 NerdDinner 数据库，然后右键单击其下的 "函数" 子节点，然后选择创建新的 "标量值函数"：</span><span class="sxs-lookup"><span data-stu-id="a83bf-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="a83bf-164">然后，将粘贴到以下 DistanceBetween 函数：</span><span class="sxs-lookup"><span data-stu-id="a83bf-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="a83bf-165">然后，将在 SQL Server 中创建一个新的表值函数，我们将调用 "NearestDinners"：</span><span class="sxs-lookup"><span data-stu-id="a83bf-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="a83bf-166">此 "NearestDinners" 表函数使用 DistanceBetween helper 函数来返回所提供的纬度和经度100英里以内的所有就：</span><span class="sxs-lookup"><span data-stu-id="a83bf-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="a83bf-167">若要调用此函数，我们首先要打开 LINQ to SQL 设计器，方法是双击 \Models 目录中的 NerdDinner 文件：</span><span class="sxs-lookup"><span data-stu-id="a83bf-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="a83bf-168">然后，将 NearestDinners 和 DistanceBetween 函数拖到 LINQ to SQL 设计器，这将导致这些函数作为 LINQ to SQL NerdDinnerDataContext 类的方法添加：</span><span class="sxs-lookup"><span data-stu-id="a83bf-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="a83bf-169">然后，可以在 DinnerRepository 类上公开 "FindByLocation" 查询方法，该方法使用 NearestDinner 函数返回指定位置100英里以内的即将到来的就：</span><span class="sxs-lookup"><span data-stu-id="a83bf-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="a83bf-170">实现基于 JSON 的 AJAX 搜索操作方法</span><span class="sxs-lookup"><span data-stu-id="a83bf-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="a83bf-171">现在，我们将实现一种控制器操作方法，该方法利用新的 FindByLocation ( # A1 存储库方法返回可用于填充地图的晚餐数据列表。</span><span class="sxs-lookup"><span data-stu-id="a83bf-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="a83bf-172">此操作方法会以 JSON (JavaScript 对象表示法) 格式返回晚餐数据，以便在客户端上使用 JavaScript 轻松地对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="a83bf-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="a83bf-173">为实现此方法，我们将创建一个新的 "SearchController" 类，方法是右键单击 "\Controllers" 目录，然后选择 "添加 &gt; 控制器" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="a83bf-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="a83bf-174">然后，在新的 SearchController 类中实现 "SearchByLocation" 操作方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a83bf-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="a83bf-175">SearchController 的 SearchByLocation 操作方法在内部调用 DinnerRepository 上的 FindByLocation 方法，以获取附近就的列表。</span><span class="sxs-lookup"><span data-stu-id="a83bf-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="a83bf-176">但不是将晚餐对象直接返回给客户端，而是返回 JsonDinner 对象。</span><span class="sxs-lookup"><span data-stu-id="a83bf-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="a83bf-177">JsonDinner 类公开了晚餐属性的子集 (例如：出于安全原因，它不会透露有 RSVP) 的人员的姓名。</span><span class="sxs-lookup"><span data-stu-id="a83bf-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="a83bf-178">它还包含 RSVPCount 属性，该属性不存在于晚宴上–并且通过对与特定晚餐关联的 RSVP 对象的数量进行动态计算。</span><span class="sxs-lookup"><span data-stu-id="a83bf-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="a83bf-179">然后，使用 Json ( # A1 helper 方法在控制器基类上使用基于 JSON 的线路格式返回就序列。</span><span class="sxs-lookup"><span data-stu-id="a83bf-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="a83bf-180">JSON 是一种用于表示简单数据结构的标准文本格式。</span><span class="sxs-lookup"><span data-stu-id="a83bf-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="a83bf-181">下面是一个示例，其中包含以下两个 JsonDinner 对象的 JSON 格式列表：</span><span class="sxs-lookup"><span data-stu-id="a83bf-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.txt)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="a83bf-182">使用 jQuery 调用基于 JSON 的 AJAX 方法</span><span class="sxs-lookup"><span data-stu-id="a83bf-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="a83bf-183">现在，我们已准备好更新 NerdDinner 应用程序的主页，以使用 SearchController 的 SearchByLocation 操作方法。</span><span class="sxs-lookup"><span data-stu-id="a83bf-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="a83bf-184">为此，我们将打开 "/Views/Home/Index.aspx" 视图模板并将其更新为包含 "文本框"、"搜索" 按钮、映射和 &lt; 一个 &gt; 名为 "dinnerList" 的 div 元素：</span><span class="sxs-lookup"><span data-stu-id="a83bf-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="a83bf-185">然后，可以将两个 JavaScript 函数添加到页面：</span><span class="sxs-lookup"><span data-stu-id="a83bf-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="a83bf-186">第一次加载页面时，第一个 JavaScript 函数会加载该映射。</span><span class="sxs-lookup"><span data-stu-id="a83bf-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="a83bf-187">第二个 JavaScript 函数在 "搜索" 按钮上向 JavaScript 单击事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="a83bf-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="a83bf-188">按下该按钮时，它会调用 FindDinnersGivenLocation ( # A1 JavaScript 函数，我们会将其添加到 Map.js 文件：</span><span class="sxs-lookup"><span data-stu-id="a83bf-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="a83bf-189">此 FindDinnersGivenLocation ( # A1 函数调用 map。在虚拟地球控件上查找 ( # A3，使其在输入位置上居中。</span><span class="sxs-lookup"><span data-stu-id="a83bf-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="a83bf-190">当虚拟的地球地图服务返回时，映射。Find ( # A1 方法会调用 callbackUpdateMapDinners 回调方法，并将其作为最后一个参数传递。</span><span class="sxs-lookup"><span data-stu-id="a83bf-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="a83bf-191">CallbackUpdateMapDinners ( # A1 方法是实际工作的位置。</span><span class="sxs-lookup"><span data-stu-id="a83bf-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="a83bf-192">它使用 jQuery 的 $. post ( # A1 helper 方法，以对我们的 SearchController 的 SearchByLocation 执行 AJAX 调用。 ( # A3 操作方法–向其传递新居中地图的纬度和经度。</span><span class="sxs-lookup"><span data-stu-id="a83bf-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="a83bf-193">它定义了一个内联函数，当 $ post ( # A1 helper 方法完成时，将调用该函数，并将使用一个名为 "就" 的变量向 ( SearchByLocation 中返回的 JSON 格式的晚餐结果传递该函数。</span><span class="sxs-lookup"><span data-stu-id="a83bf-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="a83bf-194">然后，它对每个返回的晚餐执行 foreach，并使用晚餐的纬度和经度以及其他属性在地图上添加新的 pin。</span><span class="sxs-lookup"><span data-stu-id="a83bf-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="a83bf-195">它还会将晚餐条目添加到地图右侧就的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="a83bf-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="a83bf-196">然后，它将图钉和 HTML 列表的悬停事件上滑，以便在用户将其悬停在其上方时显示晚餐的详细信息：</span><span class="sxs-lookup"><span data-stu-id="a83bf-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="a83bf-197">现在，当我们运行应用程序并访问主页时，我们会看到一个地图。</span><span class="sxs-lookup"><span data-stu-id="a83bf-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="a83bf-198">输入城市名称后，地图会在其附近显示即将到来的就：</span><span class="sxs-lookup"><span data-stu-id="a83bf-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="a83bf-199">将鼠标悬停在晚宴上方会显示有关它的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a83bf-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="a83bf-200">单击 "冒泡" 或 "HTML" 列表右侧的晚餐标题即可导航到晚餐，然后可以选择 RSVP：</span><span class="sxs-lookup"><span data-stu-id="a83bf-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="a83bf-201">下一步</span><span class="sxs-lookup"><span data-stu-id="a83bf-201">Next Step</span></span>

<span data-ttu-id="a83bf-202">现在，我们实现了 NerdDinner 应用程序的所有应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="a83bf-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="a83bf-203">现在我们来看看如何启用它的自动单元测试。</span><span class="sxs-lookup"><span data-stu-id="a83bf-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a83bf-204">[上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="a83bf-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>

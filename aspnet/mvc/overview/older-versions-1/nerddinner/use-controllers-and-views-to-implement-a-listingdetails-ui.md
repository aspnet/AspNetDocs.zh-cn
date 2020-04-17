---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |微软文档
author: rick-anderson
description: 步骤 4 演示如何向应用程序添加控制器，该应用程序利用我们的模型为用户提供数据列表/详细信息导航体验...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541307"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="e396c-103">使用控制器和视图实现列表/详细信息 UI</span><span class="sxs-lookup"><span data-stu-id="e396c-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="e396c-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e396c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e396c-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e396c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e396c-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第4步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="e396c-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e396c-107">步骤 4 演示如何向应用程序添加控制器，该应用程序利用我们的模型为用户提供在 NerdDinner 网站上晚餐的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="e396c-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="e396c-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="e396c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="e396c-109">神经晚餐步骤 4：控制器和视图</span><span class="sxs-lookup"><span data-stu-id="e396c-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="e396c-110">对于传统的 Web 框架（经典 ASP、PHP、ASP.NET Web 窗体等），传入 URL 通常映射到磁盘上的文件。</span><span class="sxs-lookup"><span data-stu-id="e396c-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="e396c-111">例如：诸如"/Products.aspx"或"/Products.php"这样的 URL 请求可能由"Products.aspx"或"Products.php"文件处理。</span><span class="sxs-lookup"><span data-stu-id="e396c-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="e396c-112">基于 Web 的 MVC 框架以略有不同的方式将 URL 映射到服务器代码。</span><span class="sxs-lookup"><span data-stu-id="e396c-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="e396c-113">它们不是将传入 URL 映射到文件，而是将 URL 映射到类上的方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="e396c-114">这些类称为"控制器"，它们负责处理传入的 HTTP 请求、处理用户输入、检索和保存数据以及确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他 URL 等）。</span><span class="sxs-lookup"><span data-stu-id="e396c-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="e396c-115">现在，我们已经为我们的NerdDinner应用程序建立了基本模型，我们的下一步将是向应用程序添加一个控制器，利用它为用户提供我们网站上的 Dinner 的数据列表/详细信息导航体验。</span><span class="sxs-lookup"><span data-stu-id="e396c-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="e396c-116">添加晚餐控制器控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="e396c-117">我们将从右键单击 Web 项目中的"控制器"文件夹开始，然后选择 **"添加-&gt;控制器"** 菜单命令（您也可以通过键入 Ctrl-M、Ctrl-C 来执行此命令）：</span><span class="sxs-lookup"><span data-stu-id="e396c-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="e396c-118">这将弹出"添加控制器"对话框：</span><span class="sxs-lookup"><span data-stu-id="e396c-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="e396c-119">我们将命名新的控制器"DinnersController"，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="e396c-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="e396c-120">然后，Visual Studio 将在我们的 @控制器目录下添加DinnersController.cs文件：</span><span class="sxs-lookup"><span data-stu-id="e396c-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="e396c-121">它还将在代码编辑器中打开新的 DinnersController 类。</span><span class="sxs-lookup"><span data-stu-id="e396c-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="e396c-122">向晚餐控制器类添加索引（） 和详细信息（） 操作方法</span><span class="sxs-lookup"><span data-stu-id="e396c-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="e396c-123">我们希望让使用我们的应用程序的访问者浏览即将举办的晚宴列表，并允许他们点击列表中的任何晚餐以查看有关此晚餐的具体细节。</span><span class="sxs-lookup"><span data-stu-id="e396c-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="e396c-124">我们将通过发布应用程序的以下 URL 来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="e396c-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="e396c-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="e396c-125">**URL**</span></span> | <span data-ttu-id="e396c-126">**目标**</span><span class="sxs-lookup"><span data-stu-id="e396c-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="e396c-127">*/晚餐/*</span><span class="sxs-lookup"><span data-stu-id="e396c-127">*/Dinners/*</span></span> | <span data-ttu-id="e396c-128">显示即将来临的晚宴的 HTML 列表</span><span class="sxs-lookup"><span data-stu-id="e396c-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="e396c-129">*/晚餐/详情/[id]*</span><span class="sxs-lookup"><span data-stu-id="e396c-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="e396c-130">显示 URL 中嵌入的"id"参数指示的特定晚餐的详细信息 ， 这将与数据库中的晚餐 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="e396c-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="e396c-131">例如：/Dinners/详细信息/2 将显示一个 HTML 页面，其中详细介绍了晚餐 ID 值为 2 的晚餐。</span><span class="sxs-lookup"><span data-stu-id="e396c-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="e396c-132">我们将通过向 DinnersController 类中添加两种公共"操作方法"来发布这些 URL 的初始实现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="e396c-133">然后，我们将运行 NerdDinner 应用程序，并使用我们的浏览器来调用它们。</span><span class="sxs-lookup"><span data-stu-id="e396c-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="e396c-134">键入 *"/Dinners/"URL*将导致我们的*Index（）* 方法运行，并且它将发送回以下响应：</span><span class="sxs-lookup"><span data-stu-id="e396c-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="e396c-135">键入 *"/晚餐/详细信息/2"URL*将导致运行*我们的详细信息（）* 方法，并发送回以下响应：</span><span class="sxs-lookup"><span data-stu-id="e396c-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="e396c-136">您可能想知道 - ASP.NET MVC 如何知道创建我们的 DinnersController 类并调用这些方法？</span><span class="sxs-lookup"><span data-stu-id="e396c-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="e396c-137">为了理解这一点，让我们快速了解路由的工作原理。</span><span class="sxs-lookup"><span data-stu-id="e396c-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="e396c-138">了解ASP.NET MVC 路由</span><span class="sxs-lookup"><span data-stu-id="e396c-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="e396c-139">ASP.NET MVC 包含强大的 URL 路由引擎，在控制 URL 如何映射到控制器类方面提供了很大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="e396c-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="e396c-140">它允许我们完全自定义ASP.NET MVC 如何选择要创建的控制器类、调用哪种方法，以及配置不同的方式，以便变量可以从 URL/Querystring 自动解析并传递给方法作为参数参数。</span><span class="sxs-lookup"><span data-stu-id="e396c-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="e396c-141">它提供了灵活性，完全优化了SEO网站（搜索引擎优化），以及发布任何我们想要从应用程序。</span><span class="sxs-lookup"><span data-stu-id="e396c-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="e396c-142">默认情况下，新的ASP.NET MVC 项目附带一组已注册的 URL 路由规则。</span><span class="sxs-lookup"><span data-stu-id="e396c-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="e396c-143">这使我们能够轻松启动应用程序，而无需显式配置任何内容。</span><span class="sxs-lookup"><span data-stu-id="e396c-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="e396c-144">默认路由规则注册可以在项目的"应用程序"类中找到 ， 我们可以通过双击项目根目录中的"Global.asax"文件来打开：</span><span class="sxs-lookup"><span data-stu-id="e396c-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="e396c-145">默认ASP.NET MVC 路由规则在此类的"注册路由"方法中注册：</span><span class="sxs-lookup"><span data-stu-id="e396c-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="e396c-146">"路线。上面的 MapRoute（）方法调用注册了一个默认路由规则，该规则使用 URL 格式将传入 URL 映射到控制器类："//{控制器}/{{{操作}/{id}" - 其中"控制器"是要实例化的控制器类的名称，"操作"是要调用它的公共方法的名称，"id"是嵌入在 URL 中的可选参数，可以作为参数传递给该方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="e396c-147">传递给"MapRoute（）"方法调用的第三个参数是一组默认值，用于在 URL 中不存在的控制器/操作/id 值（控制器 = "Home"，操作 ="索引"，Id="）。</span><span class="sxs-lookup"><span data-stu-id="e396c-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="e396c-148">下面是一个表，演示如何使用默认的<em>"//控制器\/{操作}/{id}"</em>路由规则映射各种 URL：</span><span class="sxs-lookup"><span data-stu-id="e396c-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="e396c-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="e396c-149">**URL**</span></span> | <span data-ttu-id="e396c-150">**控制器类**</span><span class="sxs-lookup"><span data-stu-id="e396c-150">**Controller Class**</span></span> | <span data-ttu-id="e396c-151">**操作方法**</span><span class="sxs-lookup"><span data-stu-id="e396c-151">**Action Method**</span></span> | <span data-ttu-id="e396c-152">**传递的参数**</span><span class="sxs-lookup"><span data-stu-id="e396c-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e396c-153">*/晚餐/细节/2*</span><span class="sxs-lookup"><span data-stu-id="e396c-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="e396c-154">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-154">DinnersController</span></span> | <span data-ttu-id="e396c-155">详细信息（ID）</span><span class="sxs-lookup"><span data-stu-id="e396c-155">Details(id)</span></span> | <span data-ttu-id="e396c-156">id=2</span><span class="sxs-lookup"><span data-stu-id="e396c-156">id=2</span></span> |
| <span data-ttu-id="e396c-157">*/晚餐/编辑/5*</span><span class="sxs-lookup"><span data-stu-id="e396c-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="e396c-158">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-158">DinnersController</span></span> | <span data-ttu-id="e396c-159">编辑（ID）</span><span class="sxs-lookup"><span data-stu-id="e396c-159">Edit(id)</span></span> | <span data-ttu-id="e396c-160">id=5</span><span class="sxs-lookup"><span data-stu-id="e396c-160">id=5</span></span> |
| <span data-ttu-id="e396c-161">*/晚餐/创建*</span><span class="sxs-lookup"><span data-stu-id="e396c-161">*/Dinners/Create*</span></span> | <span data-ttu-id="e396c-162">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-162">DinnersController</span></span> | <span data-ttu-id="e396c-163">Create()</span><span class="sxs-lookup"><span data-stu-id="e396c-163">Create()</span></span> | <span data-ttu-id="e396c-164">空值</span><span class="sxs-lookup"><span data-stu-id="e396c-164">N/A</span></span> |
| <span data-ttu-id="e396c-165">*/晚餐*</span><span class="sxs-lookup"><span data-stu-id="e396c-165">*/Dinners*</span></span> | <span data-ttu-id="e396c-166">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-166">DinnersController</span></span> | <span data-ttu-id="e396c-167">索引（）</span><span class="sxs-lookup"><span data-stu-id="e396c-167">Index()</span></span> | <span data-ttu-id="e396c-168">空值</span><span class="sxs-lookup"><span data-stu-id="e396c-168">N/A</span></span> |
| <span data-ttu-id="e396c-169">*/首页*</span><span class="sxs-lookup"><span data-stu-id="e396c-169">*/Home*</span></span> | <span data-ttu-id="e396c-170">家庭控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-170">HomeController</span></span> | <span data-ttu-id="e396c-171">索引（）</span><span class="sxs-lookup"><span data-stu-id="e396c-171">Index()</span></span> | <span data-ttu-id="e396c-172">空值</span><span class="sxs-lookup"><span data-stu-id="e396c-172">N/A</span></span> |
| */* | <span data-ttu-id="e396c-173">家庭控制器</span><span class="sxs-lookup"><span data-stu-id="e396c-173">HomeController</span></span> | <span data-ttu-id="e396c-174">索引（）</span><span class="sxs-lookup"><span data-stu-id="e396c-174">Index()</span></span> | <span data-ttu-id="e396c-175">空值</span><span class="sxs-lookup"><span data-stu-id="e396c-175">N/A</span></span> |

<span data-ttu-id="e396c-176">最后三行显示正在使用的默认值（控制器 = 主页、操作 + 索引、ID =""）。</span><span class="sxs-lookup"><span data-stu-id="e396c-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="e396c-177">由于"Index"方法注册为默认操作名称（如果未指定），因此"/Dinners"和"/home"URL 会导致在其控制器类上调用 Index（） 操作方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="e396c-178">由于"Home"控制器在未指定时注册为默认控制器，因此"/" URL 会导致创建 HomeController，并调用其上的索引（） 操作方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="e396c-179">如果您不喜欢这些默认 URL 路由规则，好消息是它们很容易更改 - 只需在上面的注册路由方法中编辑它们即可。</span><span class="sxs-lookup"><span data-stu-id="e396c-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="e396c-180">但是，对于我们的 NerdDinner 应用程序，我们不会更改任何默认 URL 路由规则，而只是将它们作为本操作使用。</span><span class="sxs-lookup"><span data-stu-id="e396c-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="e396c-181">使用我们的晚餐控制器的晚餐存储库</span><span class="sxs-lookup"><span data-stu-id="e396c-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="e396c-182">现在，让我们用使用我们的模型的实现替换当前对 DinnersController Index（） 和详细信息（）操作方法的实现。</span><span class="sxs-lookup"><span data-stu-id="e396c-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="e396c-183">我们将使用之前构建的 DinnerRepository 类来实现该行为。</span><span class="sxs-lookup"><span data-stu-id="e396c-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="e396c-184">我们将首先添加一个"使用"语句，该语句引用"NerdDinner.Model"命名空间，然后声明我们的 DinnerRepository 的实例作为 DinnerController 类上的字段。</span><span class="sxs-lookup"><span data-stu-id="e396c-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="e396c-185">在本章的后面部分，我们将介绍"依赖注入"的概念，并展示我们的控制器获取对 DinnerRepository 的引用的另一种方法，该存储库可实现更好的单元测试 -但现在，我们将创建一个类似于下面的 DinnerRepository 内联实例。</span><span class="sxs-lookup"><span data-stu-id="e396c-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="e396c-186">现在，我们准备使用检索到的数据模型对象生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="e396c-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="e396c-187">将视图与我们的控制器一起使用</span><span class="sxs-lookup"><span data-stu-id="e396c-187">Using Views with our Controller</span></span>

<span data-ttu-id="e396c-188">虽然可以在我们的操作方法中编写代码来组装 HTML，然后使用*Response.Write（）* 帮助器方法将其发送回客户端，但这种方法很快就会变得相当笨拙。</span><span class="sxs-lookup"><span data-stu-id="e396c-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="e396c-189">更好的方法是，我们只能在 DinnersController 操作方法中执行应用程序和数据逻辑，然后将呈现 HTML 响应所需的数据传递给负责提供其 HTML 表示的单独"视图"模板。</span><span class="sxs-lookup"><span data-stu-id="e396c-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="e396c-190">正如我们在一瞬间看到的，"视图"模板是一个文本文件，通常包含 HTML 标记和嵌入呈现代码的组合。</span><span class="sxs-lookup"><span data-stu-id="e396c-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="e396c-191">将控制器逻辑与视图渲染分离带来了几个大好处。</span><span class="sxs-lookup"><span data-stu-id="e396c-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="e396c-192">特别是，它有助于在应用程序代码和 UI 格式/呈现代码之间强制实施明确的"关注点分离"。</span><span class="sxs-lookup"><span data-stu-id="e396c-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="e396c-193">这使得与 UI 呈现逻辑隔离的单元测试应用程序逻辑变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="e396c-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="e396c-194">它便于以后修改 UI 呈现模板，而无需更改应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="e396c-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="e396c-195">而且，它可以使开发人员和设计人员更轻松地在项目上协作。</span><span class="sxs-lookup"><span data-stu-id="e396c-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="e396c-196">我们可以更新 DinnersController 类，以指示我们希望使用视图模板发送回 HTML UI 响应，方法是将两种操作方法的方法签名从返回类型的"void"改为"ActionResult"。"</span><span class="sxs-lookup"><span data-stu-id="e396c-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="e396c-197">然后，我们可以调用控制器基类上的*View（）* 帮助器方法返回如下所示的"ViewResult"对象：</span><span class="sxs-lookup"><span data-stu-id="e396c-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="e396c-198">我们在上面使用的*View（）* 帮助器方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="e396c-199">*View（）* 帮助程序方法的第一个参数是我们要用于呈现 HTML 响应的视图模板文件的名称。</span><span class="sxs-lookup"><span data-stu-id="e396c-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="e396c-200">第二个参数是一个模型对象，其中包含视图模板为呈现 HTML 响应所需的数据。</span><span class="sxs-lookup"><span data-stu-id="e396c-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="e396c-201">在我们的 Index（） 操作方法中，我们调用*View（）* 帮助器方法，并指示我们希望使用"Index"视图模板呈现晚餐的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="e396c-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="e396c-202">我们正在传递视图模板一系列 Dinner 对象，以便从以下角度生成列表：</span><span class="sxs-lookup"><span data-stu-id="e396c-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="e396c-203">在我们的"详细信息"操作方法中，我们尝试使用 URL 中提供的 ID 检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="e396c-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="e396c-204">如果找到有效的"晚餐"，我们调用*View（）* 帮助器方法，指示我们要使用"详细信息"视图模板来呈现检索到的 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="e396c-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="e396c-205">如果请求无效的晚餐，我们会呈现一条有用的错误消息，指示使用"NotFound"视图模板（以及仅采用模板名称的*View（）* 帮助器方法的重载版本不存在 Dinner：</span><span class="sxs-lookup"><span data-stu-id="e396c-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="e396c-206">现在，让我们实现"未找到"、"详细信息"和"索引"视图模板。</span><span class="sxs-lookup"><span data-stu-id="e396c-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="e396c-207">实现"未找到"视图模板</span><span class="sxs-lookup"><span data-stu-id="e396c-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="e396c-208">我们将首先实现"NotFound"视图模板 -它显示一条友好的错误消息，指示找不到请求的晚餐。</span><span class="sxs-lookup"><span data-stu-id="e396c-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="e396c-209">我们将通过在控制器操作方法中定位文本光标来创建新的视图模板，然后右键单击并选择"添加视图"菜单命令（我们还可以通过键入 Ctrl-M、Ctrl-V 来执行此命令）：</span><span class="sxs-lookup"><span data-stu-id="e396c-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="e396c-210">这将弹出一个"添加视图"对话框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e396c-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="e396c-211">默认情况下，对话框将预填充创建视图的名称，以匹配启动对话框时光标所采用的操作方法的名称（在本例中为"详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="e396c-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="e396c-212">由于我们想要首先实现"未找到"模板，我们将重写此视图名称并将其设置为"未找到"：</span><span class="sxs-lookup"><span data-stu-id="e396c-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="e396c-213">单击"添加"按钮时，Visual Studio 将在"_Views_Dinners"目录中为我们创建新的"NotFound.aspx"视图模板（如果目录不存在，它还会创建该模板）：</span><span class="sxs-lookup"><span data-stu-id="e396c-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="e396c-214">它还将在代码编辑器中打开我们新的"NotFound.aspx"视图模板：</span><span class="sxs-lookup"><span data-stu-id="e396c-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="e396c-215">默认情况下，查看模板有两个"内容区域"，我们可以在其中添加内容和代码。</span><span class="sxs-lookup"><span data-stu-id="e396c-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="e396c-216">第一个允许我们自定义发回的 HTML 页面的"标题"。</span><span class="sxs-lookup"><span data-stu-id="e396c-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="e396c-217">第二个允许我们自定义发回的 HTML 页面的"主要内容"。</span><span class="sxs-lookup"><span data-stu-id="e396c-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="e396c-218">要实现我们的"未找到"视图模板，我们将添加一些基本内容：</span><span class="sxs-lookup"><span data-stu-id="e396c-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="e396c-219">然后，我们可以在浏览器中试用。</span><span class="sxs-lookup"><span data-stu-id="e396c-219">We can then try it out within the browser.</span></span> <span data-ttu-id="e396c-220">为此，让我们请求 *"/晚餐/详细信息/9999"URL。*</span><span class="sxs-lookup"><span data-stu-id="e396c-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="e396c-221">这将引用数据库中当前不存在的晚餐，并导致我们的 DinnersController.详细信息（） 操作方法呈现我们的"未找到"视图模板：</span><span class="sxs-lookup"><span data-stu-id="e396c-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="e396c-222">在上面的屏幕截图中，您会注意到一件事，那就是我们的基本视图模板继承了一堆环绕屏幕上主要内容的 HTML。</span><span class="sxs-lookup"><span data-stu-id="e396c-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="e396c-223">这是因为我们的视图模板使用"母版页"模板，使我们能够在网站上的所有视图上应用一致的布局。</span><span class="sxs-lookup"><span data-stu-id="e396c-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="e396c-224">我们将在本教程的后续部分讨论母版页如何工作。</span><span class="sxs-lookup"><span data-stu-id="e396c-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="e396c-225">实现"详细信息"视图模板</span><span class="sxs-lookup"><span data-stu-id="e396c-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="e396c-226">现在，让我们实现"详细信息"视图模板 ， 它将为单个晚餐模型生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="e396c-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="e396c-227">我们将通过将文本光标定位到"详细信息"操作方法中，然后右键单击并选择"添加视图"菜单命令（或按 Ctrl-M，Ctrl-V） 来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="e396c-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="e396c-228">这将弹出"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="e396c-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="e396c-229">我们将保留默认视图名称（"详细信息"）。</span><span class="sxs-lookup"><span data-stu-id="e396c-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="e396c-230">我们还在对话框中选择"创建强类型视图"复选框，并选择（使用组合框下拉下）我们从控制器传递到视图的模型类型的名称。</span><span class="sxs-lookup"><span data-stu-id="e396c-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="e396c-231">对于此视图，我们传递一个 Dinner 对象（此类型的完全限定名称为："NerdDinner.Model.Dinner"）：</span><span class="sxs-lookup"><span data-stu-id="e396c-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="e396c-232">与之前选择创建"空视图"的模板不同，这次我们将选择使用"详细信息"模板自动"基架"视图。</span><span class="sxs-lookup"><span data-stu-id="e396c-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="e396c-233">我们可以通过更改上面对话框中的"查看内容"下拉列表来指示这一点。</span><span class="sxs-lookup"><span data-stu-id="e396c-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="e396c-234">"Scaffold"将根据我们传递给它的 Dinner 对象生成我们详细信息视图模板的初始实现。</span><span class="sxs-lookup"><span data-stu-id="e396c-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="e396c-235">这为我们提供了一种快速开始视图模板实现的简单方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="e396c-236">当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"详细信息.aspx"视图模板文件：</span><span class="sxs-lookup"><span data-stu-id="e396c-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="e396c-237">它还将在代码编辑器中打开我们新的"Details.aspx"视图模板。</span><span class="sxs-lookup"><span data-stu-id="e396c-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="e396c-238">它将包含基于 Dinner 模型的详细信息视图的初始基架实现。</span><span class="sxs-lookup"><span data-stu-id="e396c-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="e396c-239">基架引擎使用 .NET 反射来查看通过该数据库的类上公开的公共属性，并将根据找到的每个类型添加适当的内容：</span><span class="sxs-lookup"><span data-stu-id="e396c-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="e396c-240">我们可以请求 *"/晚餐/详细信息/1"URL*以查看浏览器中此"详细信息"基架实现的外观。</span><span class="sxs-lookup"><span data-stu-id="e396c-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="e396c-241">使用此 URL 将显示我们首次创建数据库时手动添加到数据库的晚餐之一：</span><span class="sxs-lookup"><span data-stu-id="e396c-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="e396c-242">这让我们快速启动和运行，并为我们提供了详细信息.aspx 视图的初始实现。</span><span class="sxs-lookup"><span data-stu-id="e396c-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="e396c-243">然后，我们可以去调整它，以自定义 UI，以让我们满意。</span><span class="sxs-lookup"><span data-stu-id="e396c-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="e396c-244">当我们更仔细地查看 Details.aspx 模板时，我们会发现它包含静态 HTML 以及嵌入式呈现代码。</span><span class="sxs-lookup"><span data-stu-id="e396c-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="e396c-245">&lt;%&gt; % 代码块在视图模板呈现时执行代码&lt;，%= %&gt;代码块执行其中包含的代码，然后将结果呈现给模板的输出流。</span><span class="sxs-lookup"><span data-stu-id="e396c-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="e396c-246">我们可以在 View 中编写代码，该代码访问使用强类型"Model"属性从控制器传递的"Dinner"模型对象。</span><span class="sxs-lookup"><span data-stu-id="e396c-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="e396c-247">Visual Studio 在编辑器中访问此"模型"属性时，为我们提供了完整的代码无意义：</span><span class="sxs-lookup"><span data-stu-id="e396c-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="e396c-248">让我们做一些调整，以便我们最终的详细信息视图模板的源如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="e396c-249">当我们再次访问 *"/晚餐/细节/1"URL*时，它现在将呈现如下：</span><span class="sxs-lookup"><span data-stu-id="e396c-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="e396c-250">实现"索引"视图模板</span><span class="sxs-lookup"><span data-stu-id="e396c-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="e396c-251">现在，让我们实现"索引"视图模板 - 这将生成即将推出的晚餐的列表。</span><span class="sxs-lookup"><span data-stu-id="e396c-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="e396c-252">为此，我们将将文本光标定位在 Index 操作方法中，然后右键单击并选择"添加视图"菜单命令（或按 Ctrl-M、Ctrl-V）。</span><span class="sxs-lookup"><span data-stu-id="e396c-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="e396c-253">在"添加视图"对话框中，我们将保留名为"索引"的视图模板，并选择"创建强类型视图"复选框。</span><span class="sxs-lookup"><span data-stu-id="e396c-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="e396c-254">这一次，我们将选择自动生成"列表"视图模板，并选择"NerdDinner.Model.Dinner"作为传递给视图的模型类型（由于我们已指示我们正在创建"列表"基架将导致添加视图对话框假定我们将一系列 Dinner 对象从控制器传递到视图）：</span><span class="sxs-lookup"><span data-stu-id="e396c-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="e396c-255">当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"Index.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="e396c-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="e396c-256">它将"支架"在其中的初始实现，提供我们传递给视图的 Dinner 的 HTML 表列表。</span><span class="sxs-lookup"><span data-stu-id="e396c-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="e396c-257">当我们运行应用程序并访问 *"/Dinners/"URL*时，它将呈现我们的晚餐列表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="e396c-258">上面的表格解决方案为我们提供了一个网格般的布局，我们的晚餐数据 - 这不是我们想要为我们的消费者面对晚餐上市。</span><span class="sxs-lookup"><span data-stu-id="e396c-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="e396c-259">我们可以更新 Index.aspx 视图模板并对其进行修改以列出较少的数据列，并使用&lt;ul&gt;元素呈现它们，而不是使用以下代码呈现表：</span><span class="sxs-lookup"><span data-stu-id="e396c-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="e396c-260">当我们循环展示模型中的每个晚餐时，我们使用上述"var"关键字。</span><span class="sxs-lookup"><span data-stu-id="e396c-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="e396c-261">不熟悉 C# 3.0 的人可能会认为使用"var"意味着晚餐对象是后期绑定的。</span><span class="sxs-lookup"><span data-stu-id="e396c-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="e396c-262">相反，这意味着编译器使用针对强类型"模型"属性的类型推理（类型为&lt;&gt;"IE500Dinner"），并将本地"Dinner"变量编译为 Dinner 类型 - 这意味着我们在代码块中获取完全的无意义和编译时间检查：</span><span class="sxs-lookup"><span data-stu-id="e396c-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="e396c-263">当我们在浏览器中的 */Dinners* URL 上刷新时，我们更新的视图现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="e396c-264">看起来更好，但还没有完全存在。</span><span class="sxs-lookup"><span data-stu-id="e396c-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="e396c-265">我们的最后一步是使最终用户能够点击列表中的单个晚餐并查看有关它们的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e396c-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="e396c-266">我们将通过呈现链接到晚餐控制器上"详细信息"操作方法的 HTML 超链接元素来实现此内容。</span><span class="sxs-lookup"><span data-stu-id="e396c-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="e396c-267">我们可以在 Index 视图中以两种方式之一生成这些超链接。</span><span class="sxs-lookup"><span data-stu-id="e396c-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="e396c-268">第一种是手动创建 HTML &lt;&gt;元素，如下所示，其中我们在&lt;&gt;HTML&gt;元素中&lt;嵌入 % 块：</span><span class="sxs-lookup"><span data-stu-id="e396c-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="e396c-269">我们可以使用的替代方法是利用 MVC 中ASP.NET内置的"Html.ActionLink（））"帮助器方法，该方法支持以编程方式创建 HTML 元素，&lt;该&gt;元素链接到控制器上的另一个操作方法：</span><span class="sxs-lookup"><span data-stu-id="e396c-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="e396c-270">Html.ActionLink（） 帮助器方法的第一个参数是要显示的链接文本（在本例中为 Dinner 的标题），第二个参数是我们想要将链接生成的控制器操作名称（在本例中为详细信息方法），第三个参数是一组要发送到操作的参数（作为具有属性名称/值的匿名类型实现）。</span><span class="sxs-lookup"><span data-stu-id="e396c-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="e396c-271">在这种情况下，我们指定我们要链接到的晚餐的"id"参数，并且由于 ASP.NET MVC 中的默认 URL 路由规则为 Html.ActionLink（） 帮助器方法的"{控制器}/{操作}/{id}"，因此 Html.ActionLink（） 帮助程序方法将生成以下输出：</span><span class="sxs-lookup"><span data-stu-id="e396c-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="e396c-272">对于我们的 Index.aspx 视图，我们将使用 Html.ActionLink（） 帮助器方法方法，并将每个晚餐都包含到相应详细信息 URL 的链接中：</span><span class="sxs-lookup"><span data-stu-id="e396c-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="e396c-273">现在，当我们点击 */Dinners* URL 时，我们的晚餐列表如下所示：</span><span class="sxs-lookup"><span data-stu-id="e396c-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="e396c-274">当我们单击列表中的任何晚餐时，我们将导航以查看有关它的详细信息：</span><span class="sxs-lookup"><span data-stu-id="e396c-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="e396c-275">基于约定的命名和 _Views 目录结构</span><span class="sxs-lookup"><span data-stu-id="e396c-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="e396c-276">默认情况下ASP.NET MVC 应用程序在解决视图模板时使用基于约定的目录命名结构。</span><span class="sxs-lookup"><span data-stu-id="e396c-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="e396c-277">这允许开发人员在从 Controller 类中引用视图时避免对位置路径进行完全限定。</span><span class="sxs-lookup"><span data-stu-id="e396c-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="e396c-278">默认情况下ASP.NET MVC 将在应用程序下方的 [视图\[控制器名称]\*目录中查找视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="e396c-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="e396c-279">例如，我们一直在研究 DinnersController 类，该类显式引用三个视图模板："索引"、"详细信息"和"未找到"。</span><span class="sxs-lookup"><span data-stu-id="e396c-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="e396c-280">默认情况下，ASP.NET MVC 将在应用程序根目录下的 *[Views_Dinners]* 目录中查找这些视图：</span><span class="sxs-lookup"><span data-stu-id="e396c-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="e396c-281">请注意，项目中当前存在三个控制器类（DinnersController、HomeController 和 AccountController - 在创建项目时默认添加了后两个控制器类），并且 _Views 目录中有三个子目录（每个控制器一个）。</span><span class="sxs-lookup"><span data-stu-id="e396c-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="e396c-282">从"主页"和"帐户"控制器引用的视图将自动解析其视图模板，这些模板来自相应的 *[视图]主页*和 *[视图]帐户*目录。</span><span class="sxs-lookup"><span data-stu-id="e396c-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="e396c-283">*[Views]共享*子目录提供了一种存储在应用程序中多个控制器中重复使用的视图模板的方法。</span><span class="sxs-lookup"><span data-stu-id="e396c-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="e396c-284">当 ASP.NET MVC 尝试解析视图模板时，它将首先在 *[视图\[控制器]* 特定目录中进行检查，如果无法找到视图模板，它将在 *[Views_Shared]* 目录中查找。</span><span class="sxs-lookup"><span data-stu-id="e396c-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="e396c-285">在命名单个视图模板时，建议的指导是让视图模板共享与导致其呈现的操作方法相同的名称。</span><span class="sxs-lookup"><span data-stu-id="e396c-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="e396c-286">例如，上面的"Index"操作方法是使用"索引"视图来呈现视图结果，而"详细信息"操作方法使用"详细信息"视图来呈现其结果。</span><span class="sxs-lookup"><span data-stu-id="e396c-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="e396c-287">这样，就可以轻松快速查看与每个操作关联的模板。</span><span class="sxs-lookup"><span data-stu-id="e396c-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="e396c-288">当视图模板与在控制器上调用的操作方法具有相同的名称时，开发人员不需要显式指定视图模板名称。</span><span class="sxs-lookup"><span data-stu-id="e396c-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="e396c-289">相反，我们可以将模型对象传递给"View（）"帮助器方法（不指定视图名称），并且ASP.NET MVC 将自动推断我们希望在磁盘上使用 *[视图\[控制器名称]\[操作名称]* 视图模板来呈现它。</span><span class="sxs-lookup"><span data-stu-id="e396c-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="e396c-290">这使我们能够稍微清理一下控制器代码，并避免在代码中重复两次名称：</span><span class="sxs-lookup"><span data-stu-id="e396c-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="e396c-291">上述代码是实现一个不错的晚餐列表/细节体验的网站所需要的一切。</span><span class="sxs-lookup"><span data-stu-id="e396c-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="e396c-292">下一步</span><span class="sxs-lookup"><span data-stu-id="e396c-292">Next Step</span></span>

<span data-ttu-id="e396c-293">我们现在有一个不错的晚餐浏览体验建立。</span><span class="sxs-lookup"><span data-stu-id="e396c-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="e396c-294">现在，让我们启用 CRUD（创建、读取、更新、删除）数据表单编辑支持。</span><span class="sxs-lookup"><span data-stu-id="e396c-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e396c-295">[上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="e396c-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>

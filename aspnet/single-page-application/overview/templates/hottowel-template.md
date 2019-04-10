---
uid: single-page-application/overview/templates/hottowel-template
title: 热 Towel 模板 |Microsoft Docs
author: madskristensen
description: HotTowel 模板
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: 017f550e2caffe1b20823e9b1880cbb4e968005a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379932"
---
# <a name="hot-towel-template"></a><span data-ttu-id="09c2b-103">Hot Towel 模板</span><span class="sxs-lookup"><span data-stu-id="09c2b-103">Hot Towel template</span></span>

<span data-ttu-id="09c2b-104">通过[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="09c2b-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="09c2b-105">John papa 编写热总是随身携带毛巾 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="09c2b-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="09c2b-106">选择要下载哪个版本：</span><span class="sxs-lookup"><span data-stu-id="09c2b-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="09c2b-107">适用于 Visual Studio 2012 的热总是随身携带毛巾 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="09c2b-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="09c2b-108">Visual Studio 2013 的热总是随身携带毛巾 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="09c2b-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="09c2b-109">热总是随身携带毛巾：因为您不希望转到没有 SPA ！</span><span class="sxs-lookup"><span data-stu-id="09c2b-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>


<span data-ttu-id="09c2b-110">想要生成 SPA，但不能确定从何处着手？</span><span class="sxs-lookup"><span data-stu-id="09c2b-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="09c2b-111">使用热总是随身携带毛巾，以秒为单位，您将得到一个 SPA 和其上构建所需的所有工具 ！</span><span class="sxs-lookup"><span data-stu-id="09c2b-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="09c2b-112">热总是随身携带毛巾创建用于构建单页应用程序 (SPA) 使用 ASP.NET 的良好起点。</span><span class="sxs-lookup"><span data-stu-id="09c2b-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="09c2b-113">现成的它提供模块化结构为代码、 查看导航、 数据绑定、 丰富的数据管理和简单但简洁的样式设置。</span><span class="sxs-lookup"><span data-stu-id="09c2b-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="09c2b-114">热总是随身携带毛巾提供构建 SPA，因此你可以专注于应用，不的基本功能所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="09c2b-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="09c2b-115">深入了解如何构建从 SPA [John Papa 视频、 教程和 Pluralsight 课程](http://johnpapa.net/spa?vsix)。</span><span class="sxs-lookup"><span data-stu-id="09c2b-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>


## <a name="application-structure"></a><span data-ttu-id="09c2b-116">应用程序结构</span><span class="sxs-lookup"><span data-stu-id="09c2b-116">Application Structure</span></span>

<span data-ttu-id="09c2b-117">热总是随身携带毛巾 SPA 提供应用程序文件夹，其中包含定义你的应用程序的 JavaScript 和 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="09c2b-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="09c2b-118">在应用程序文件夹的内容：</span><span class="sxs-lookup"><span data-stu-id="09c2b-118">Inside the App folder:</span></span>

- <span data-ttu-id="09c2b-119">Durandal</span><span class="sxs-lookup"><span data-stu-id="09c2b-119">durandal</span></span>
- <span data-ttu-id="09c2b-120">服务</span><span class="sxs-lookup"><span data-stu-id="09c2b-120">services</span></span>
- <span data-ttu-id="09c2b-121">viewmodels</span><span class="sxs-lookup"><span data-stu-id="09c2b-121">viewmodels</span></span>
- <span data-ttu-id="09c2b-122">视图</span><span class="sxs-lookup"><span data-stu-id="09c2b-122">views</span></span>

<span data-ttu-id="09c2b-123">应用程序文件夹中包含模块的集合。</span><span class="sxs-lookup"><span data-stu-id="09c2b-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="09c2b-124">这些模块封装功能，并在其他模块中声明的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="09c2b-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="09c2b-125">视图文件夹包含你的应用程序的 HTML，viewmodels 文件夹包含视图 （常用的 MVVM 模式） 的表示逻辑。</span><span class="sxs-lookup"><span data-stu-id="09c2b-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="09c2b-126">服务文件夹非常适合用于容纳任何公用服务，这些应用程序可能需要等 HTTP 数据检索或本地存储的交互。</span><span class="sxs-lookup"><span data-stu-id="09c2b-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="09c2b-127">它是常见的多个 viewmodel 重新使用服务模块中的代码。</span><span class="sxs-lookup"><span data-stu-id="09c2b-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="09c2b-128">ASP.NET MVC 服务器端应用程序结构</span><span class="sxs-lookup"><span data-stu-id="09c2b-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="09c2b-129">热总是随身携带毛巾基于熟悉且功能强大的 ASP.NET MVC 结构。</span><span class="sxs-lookup"><span data-stu-id="09c2b-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="09c2b-130">应用\_开始</span><span class="sxs-lookup"><span data-stu-id="09c2b-130">App\_Start</span></span>
- <span data-ttu-id="09c2b-131">内容</span><span class="sxs-lookup"><span data-stu-id="09c2b-131">Content</span></span>
- <span data-ttu-id="09c2b-132">Controllers</span><span class="sxs-lookup"><span data-stu-id="09c2b-132">Controllers</span></span>
- <span data-ttu-id="09c2b-133">Models</span><span class="sxs-lookup"><span data-stu-id="09c2b-133">Models</span></span>
- <span data-ttu-id="09c2b-134">脚本</span><span class="sxs-lookup"><span data-stu-id="09c2b-134">Scripts</span></span>
- <span data-ttu-id="09c2b-135">Views</span><span class="sxs-lookup"><span data-stu-id="09c2b-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="09c2b-136">特色的库</span><span class="sxs-lookup"><span data-stu-id="09c2b-136">Featured Libraries</span></span>

- <span data-ttu-id="09c2b-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="09c2b-137">ASP.NET MVC</span></span>
- <span data-ttu-id="09c2b-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="09c2b-138">ASP.NET Web API</span></span>
- <span data-ttu-id="09c2b-139">ASP.NET Web 优化的绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="09c2b-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="09c2b-140">[Breeze.js](http://Breezejs.com) -丰富的数据管理</span><span class="sxs-lookup"><span data-stu-id="09c2b-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="09c2b-141">[Durandal.js](http://Durandaljs.com) -导航和视图构成</span><span class="sxs-lookup"><span data-stu-id="09c2b-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="09c2b-142">[Knockout.js](http://Knockoutjs.com) -数据绑定</span><span class="sxs-lookup"><span data-stu-id="09c2b-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="09c2b-143">[Require.js](http://requirejs.org) -模块使用 AMD 和优化</span><span class="sxs-lookup"><span data-stu-id="09c2b-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="09c2b-144">[Toastr.js](http://jpapa.me/c7toastr)的弹出消息</span><span class="sxs-lookup"><span data-stu-id="09c2b-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="09c2b-145">[Twitter Bootstrap](http://twitter.github.com/bootstrap/) -功能强大的 CSS 样式</span><span class="sxs-lookup"><span data-stu-id="09c2b-145">[Twitter Bootstrap](http://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="09c2b-146">通过 Visual Studio 2012 热总是随身携带毛巾 SPA 模板安装</span><span class="sxs-lookup"><span data-stu-id="09c2b-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="09c2b-147">热总是随身携带毛巾可以安装为 Visual Studio 2012 模板。</span><span class="sxs-lookup"><span data-stu-id="09c2b-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="09c2b-148">只需单击`File`  |  `New Project` ，然后选择`ASP.NET MVC 4 Web Application`。</span><span class="sxs-lookup"><span data-stu-id="09c2b-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="09c2b-149">然后选择热总是随身携带毛巾单页面应用程序"模板并运行 ！</span><span class="sxs-lookup"><span data-stu-id="09c2b-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="09c2b-150">通过 NuGet 包安装</span><span class="sxs-lookup"><span data-stu-id="09c2b-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="09c2b-151">热总是随身携带毛巾也是一个 NuGet 包，增加现有空 ASP.NET MVC 项目的内容。</span><span class="sxs-lookup"><span data-stu-id="09c2b-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="09c2b-152">只需使用 Nuget 安装并运行 ！</span><span class="sxs-lookup"><span data-stu-id="09c2b-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="09c2b-153">如何生成热总是随身携带毛巾？</span><span class="sxs-lookup"><span data-stu-id="09c2b-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="09c2b-154">只需启动添加代码 ！</span><span class="sxs-lookup"><span data-stu-id="09c2b-154">Simply start adding code!</span></span>

1. <span data-ttu-id="09c2b-155">添加你自己的服务器端代码，最好是实体框架和 WebAPI （其中的亮点在于与 Breeze.js）</span><span class="sxs-lookup"><span data-stu-id="09c2b-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="09c2b-156">添加到视图`App/views`文件夹</span><span class="sxs-lookup"><span data-stu-id="09c2b-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="09c2b-157">添加到 viewmodel`App/viewmodels`文件夹</span><span class="sxs-lookup"><span data-stu-id="09c2b-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="09c2b-158">将 HTML 和 Knockout 数据绑定添加到你的新视图</span><span class="sxs-lookup"><span data-stu-id="09c2b-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="09c2b-159">更新中的导航路由</span><span class="sxs-lookup"><span data-stu-id="09c2b-159">Update the navigation routes in</span></span> `shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="09c2b-160">HTML/JavaScript 的演练</span><span class="sxs-lookup"><span data-stu-id="09c2b-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="09c2b-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="09c2b-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="09c2b-162">index.cshtml 是起始路由和视图的 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="09c2b-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="09c2b-163">它包含所有标准 meta 标记、 css 链接和你所期望的 JavaScript 引用。</span><span class="sxs-lookup"><span data-stu-id="09c2b-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="09c2b-164">正文包含一个`<div>`即全部内容 （视图） 将在要求时放置。</span><span class="sxs-lookup"><span data-stu-id="09c2b-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="09c2b-165">`@Scripts.Render` Require.js 用于运行中包含的应用程序的代码的入口点`main.js`文件。</span><span class="sxs-lookup"><span data-stu-id="09c2b-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="09c2b-166">提供初始屏幕是为了演示如何创建初始屏幕，您的应用程序加载时。</span><span class="sxs-lookup"><span data-stu-id="09c2b-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="09c2b-167">App/main.js</span><span class="sxs-lookup"><span data-stu-id="09c2b-167">App/main.js</span></span>

<span data-ttu-id="09c2b-168">`main.js`文件包含将运行您的应用程序加载的代码。</span><span class="sxs-lookup"><span data-stu-id="09c2b-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="09c2b-169">这是你想要定义导航路由、 设置视图，你启动和执行任何安装程序/启动如填充应用程序的数据。</span><span class="sxs-lookup"><span data-stu-id="09c2b-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="09c2b-170">`main.js`文件定义了多个 durandal 的模块，以帮助启动应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="09c2b-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="09c2b-171">定义语句可帮助解决模块依赖项，以便它们可为函数。</span><span class="sxs-lookup"><span data-stu-id="09c2b-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="09c2b-172">首次启用调试消息，该发送哪些事件的消息应用程序执行到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="09c2b-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="09c2b-173">在 app.start 代码指示 durandal 框架在启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="09c2b-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="09c2b-174">以便 durandal 知道所有视图和 viewmodel 分别包含在同一个命名的文件夹中，设置约定。</span><span class="sxs-lookup"><span data-stu-id="09c2b-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="09c2b-175">最后，`app.setRoot`介入负载`shell`使用一个预定义`entrance`动画。</span><span class="sxs-lookup"><span data-stu-id="09c2b-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="09c2b-176">Views</span><span class="sxs-lookup"><span data-stu-id="09c2b-176">Views</span></span>

<span data-ttu-id="09c2b-177">视图中找到`App/views`文件夹。</span><span class="sxs-lookup"><span data-stu-id="09c2b-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="09c2b-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="09c2b-178">shell.html</span></span>

<span data-ttu-id="09c2b-179">`shell.html`包含在 HTML 母版布局。</span><span class="sxs-lookup"><span data-stu-id="09c2b-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="09c2b-180">将角的某个位置构成所有其他视图在`shell`视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="09c2b-181">提供了热总是随身携带毛巾`shell`具有三个这样的区域： 标头、 内容区域和页脚。</span><span class="sxs-lookup"><span data-stu-id="09c2b-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="09c2b-182">每个区域将以加载内容构成请求时的其他视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="09c2b-183">`compose`页眉和页脚的绑定是硬编码在热总是随身携带毛巾以指向`nav`和`footer`视图，分别。</span><span class="sxs-lookup"><span data-stu-id="09c2b-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="09c2b-184">部分中的 compose 绑定`#content`绑定到`router`模块的活动项。</span><span class="sxs-lookup"><span data-stu-id="09c2b-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="09c2b-185">换而言之，当您单击时它是对应的视图的导航链接加载在此区域中。</span><span class="sxs-lookup"><span data-stu-id="09c2b-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="09c2b-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="09c2b-186">nav.html</span></span>

<span data-ttu-id="09c2b-187">`nav.html` Spa 包含导航链接。</span><span class="sxs-lookup"><span data-stu-id="09c2b-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="09c2b-188">这是菜单结构可以放置的位置，例如。</span><span class="sxs-lookup"><span data-stu-id="09c2b-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="09c2b-189">通常是数据绑定 （使用 Knockout） 到`router`模块来显示中定义的导航`shell.js`。</span><span class="sxs-lookup"><span data-stu-id="09c2b-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="09c2b-190">Knockout 将会查找数据绑定属性，并将绑定到`shell`viewmodel 来显示导航路线并显示进度栏 （使用 Twitter Bootstrap） 如果`router`模块正在进行从一个视图导航到另一个 （请参阅`router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="09c2b-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="09c2b-191">home.html 和 details.html</span><span class="sxs-lookup"><span data-stu-id="09c2b-191">home.html and details.html</span></span>

<span data-ttu-id="09c2b-192">对于自定义视图，这些视图包含 HTML。</span><span class="sxs-lookup"><span data-stu-id="09c2b-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="09c2b-193">当`home`中的链接`nav`单击视图的菜单时，`home`视图将位于的内容区域`shell`视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="09c2b-194">这些视图可以增强或替换为你自己的自定义视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="09c2b-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="09c2b-195">footer.html</span></span>

<span data-ttu-id="09c2b-196">`footer.html`包含在页脚中，在底部显示的 HTML`shell`视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="09c2b-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="09c2b-197">ViewModels</span></span>

<span data-ttu-id="09c2b-198">Viewmodel 中找到`App/viewmodels`文件夹。</span><span class="sxs-lookup"><span data-stu-id="09c2b-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="09c2b-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="09c2b-199">shell.js</span></span>

<span data-ttu-id="09c2b-200">`shell` Viewmodel 包含属性和绑定到的函数`shell`视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="09c2b-201">通常这是在其中找到菜单导航绑定 (请参阅`router.mapNav`逻辑)。</span><span class="sxs-lookup"><span data-stu-id="09c2b-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="09c2b-202">home.js 和 details.js</span><span class="sxs-lookup"><span data-stu-id="09c2b-202">home.js and details.js</span></span>

<span data-ttu-id="09c2b-203">这些 viewmodel 包含的属性和绑定到的函数`home`视图。</span><span class="sxs-lookup"><span data-stu-id="09c2b-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="09c2b-204">它还包含表示逻辑视图，并且数据与视图之间的胶水。</span><span class="sxs-lookup"><span data-stu-id="09c2b-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="09c2b-205">Services</span><span class="sxs-lookup"><span data-stu-id="09c2b-205">Services</span></span>

<span data-ttu-id="09c2b-206">在应用/服务文件夹中找到服务。</span><span class="sxs-lookup"><span data-stu-id="09c2b-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="09c2b-207">理想情况下无法放置如 dataservice 模块，负责获取和发送远程数据，您将来的服务。</span><span class="sxs-lookup"><span data-stu-id="09c2b-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="09c2b-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="09c2b-208">logger.js</span></span>

<span data-ttu-id="09c2b-209">提供了热总是随身携带毛巾`logger`服务文件夹中的模块。</span><span class="sxs-lookup"><span data-stu-id="09c2b-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="09c2b-210">`logger`模块非常适合于日志记录消息到控制台和弹出 toast 中的用户。</span><span class="sxs-lookup"><span data-stu-id="09c2b-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>

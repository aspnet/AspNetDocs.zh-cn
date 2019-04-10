---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: 了解模型、 视图和控制器 (C#) |Microsoft Docs
author: StephenWalther
description: 有关模型、 视图和控制器感到迷惑吗？ 在本教程中，Stephen Walther 向您介绍到的 ASP.NET MVC 应用程序的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c57345c510ad0afccaabf377fda35afbfc05e17
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59383403"
---
# <a name="understanding-models-views-and-controllers-c"></a><span data-ttu-id="39676-104">了解模型、视图和控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="39676-104">Understanding Models, Views, and Controllers (C#)</span></span>

<span data-ttu-id="39676-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="39676-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="39676-106">有关模型、 视图和控制器感到迷惑吗？</span><span class="sxs-lookup"><span data-stu-id="39676-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="39676-107">在本教程中，Stephen Walther 向您介绍到的 ASP.NET MVC 应用程序的不同部分。</span><span class="sxs-lookup"><span data-stu-id="39676-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="39676-108">本教程提供简要介绍 ASP.NET MVC 的模型、 视图和控制器也是如此。</span><span class="sxs-lookup"><span data-stu-id="39676-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="39676-109">换而言之，它说明了 M，V，和 C 在 ASP.NET MVC 中。</span><span class="sxs-lookup"><span data-stu-id="39676-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="39676-110">阅读本教程之后，您应该了解 ASP.NET MVC 应用程序的不同部分是如何协同工作。</span><span class="sxs-lookup"><span data-stu-id="39676-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="39676-111">您还应了解与 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序的 ASP.NET MVC 应用程序的体系结构的区别。</span><span class="sxs-lookup"><span data-stu-id="39676-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="39676-112">示例 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="39676-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="39676-113">用于创建 ASP.NET MVC Web 应用程序的默认 Visual Studio 模板包括可用于了解 ASP.NET MVC 应用程序的不同部分的极其简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="39676-114">我们利用在本教程中此简单应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="39676-115">使用 MVC 模板中启动 Visual Studio 2008 创建新的 ASP.NET MVC 应用程序并选择文件菜单选项，新建项目 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="39676-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="39676-116">在新建项目对话框中，选择你喜欢的编程语言下项目类型 （Visual Basic 或 C#），然后选择**ASP.NET MVC Web 应用程序**下模板。</span><span class="sxs-lookup"><span data-stu-id="39676-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="39676-117">单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="39676-117">Click the OK button.</span></span>


[![N<span data-ttu-id="39676-118">项目对话框中的新增功能]</span><span class="sxs-lookup"><span data-stu-id="39676-118">ew Project Dialog]</span></span>(understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

<span data-ttu-id="39676-119">**图 01**:新建项目对话框 ([单击此项可查看原尺寸图像](understanding-models-views-and-controllers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="39676-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image2.png))</span></span>


<span data-ttu-id="39676-120">创建新的 ASP.NET MVC 应用程序时**创建单元测试项目**对话框 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="39676-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="39676-121">此对话框，可用于测试你的 ASP.NET MVC 应用程序在解决方案中创建一个单独的项目。</span><span class="sxs-lookup"><span data-stu-id="39676-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="39676-122">选择的选项**否，不创建单元测试项目**然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="39676-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


[![C<span data-ttu-id="39676-123">创建单元测试对话框]</span><span class="sxs-lookup"><span data-stu-id="39676-123">reate Unit Test Dialog]</span></span>(understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

<span data-ttu-id="39676-124">**图 02**:创建单元测试对话框 ([单击此项可查看原尺寸图像](understanding-models-views-and-controllers-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="39676-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image4.png))</span></span>


<span data-ttu-id="39676-125">创建后新的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="39676-126">你将看到多个文件夹和解决方案资源管理器窗口中的文件。</span><span class="sxs-lookup"><span data-stu-id="39676-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="39676-127">具体而言，你将看到名为模型、 视图和控制器的三个文件夹。</span><span class="sxs-lookup"><span data-stu-id="39676-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="39676-128">您可能已经猜到的文件夹名称，这些文件夹包含用于实现模型、 视图和控制器的文件。</span><span class="sxs-lookup"><span data-stu-id="39676-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="39676-129">如果展开 Controllers 文件夹，你应看到一个名为 AccountController.cs 文件和一个名为 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="39676-129">If you expand the Controllers folder, you should see a file named AccountController.cs and a file named HomeController.cs.</span></span> <span data-ttu-id="39676-130">如果展开 Views 文件夹，应看到名为帐户，主页和共享的三个子文件夹。</span><span class="sxs-lookup"><span data-stu-id="39676-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="39676-131">如果展开主文件夹，您将看到两个名为 About.aspx 和 Index.aspx （请参见图 3） 的其他文件。</span><span class="sxs-lookup"><span data-stu-id="39676-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="39676-132">这些文件构成了默认的 ASP.NET MVC 模板中包含的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


[![T<span data-ttu-id="39676-133">他的解决方案资源管理器窗口]</span><span class="sxs-lookup"><span data-stu-id="39676-133">he Solution Explorer Window]</span></span>(understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

<span data-ttu-id="39676-134">**图 03**:解决方案资源管理器窗口 ([单击此项可查看原尺寸图像](understanding-models-views-and-controllers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="39676-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image6.png))</span></span>


<span data-ttu-id="39676-135">可以通过选择菜单选项来运行示例应用程序**调试、 启动调试**。</span><span class="sxs-lookup"><span data-stu-id="39676-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="39676-136">此外，您可以按 F5 键。</span><span class="sxs-lookup"><span data-stu-id="39676-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="39676-137">首次运行的 ASP.NET 应用程序时，会出现图 4 中的对话框，建议启用调试模式。</span><span class="sxs-lookup"><span data-stu-id="39676-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="39676-138">单击确定按钮，将运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-138">Click the OK button and the application will run.</span></span>


[![D<span data-ttu-id="39676-139">ebugging 未启用对话框]</span><span class="sxs-lookup"><span data-stu-id="39676-139">ebugging Not Enabled dialog]</span></span>(understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

<span data-ttu-id="39676-140">**图 04**:调试未启用对话框 ([单击此项可查看原尺寸图像](understanding-models-views-and-controllers-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="39676-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image8.png))</span></span>


<span data-ttu-id="39676-141">当您运行的 ASP.NET MVC 应用程序时，Visual Studio 将启动 web 浏览器中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="39676-142">示例应用程序只有两个页组成: 索引页和关于页面。</span><span class="sxs-lookup"><span data-stu-id="39676-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="39676-143">第一次启动应用程序，将显示索引页 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="39676-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="39676-144">可以通过单击顶部的菜单链接导航到关于页面右侧的应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


[![T<span data-ttu-id="39676-145">他索引页]</span><span class="sxs-lookup"><span data-stu-id="39676-145">he Index Page]</span></span>(understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

<span data-ttu-id="39676-146">**图 05**:索引页 ([单击此项可查看原尺寸图像](understanding-models-views-and-controllers-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="39676-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image11.png))</span></span>


<span data-ttu-id="39676-147">请注意，在浏览器地址栏中的 Url。</span><span class="sxs-lookup"><span data-stu-id="39676-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="39676-148">例如，当你单击关于菜单链接时，浏览器地址栏中的 URL 将变为 **/Home/有关**。</span><span class="sxs-lookup"><span data-stu-id="39676-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="39676-149">如果关闭浏览器窗口并返回到 Visual Studio，你将无法使用路径主页/关于查找的文件。</span><span class="sxs-lookup"><span data-stu-id="39676-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="39676-150">文件不存在。</span><span class="sxs-lookup"><span data-stu-id="39676-150">The files don't exist.</span></span> <span data-ttu-id="39676-151">这是如何实现？</span><span class="sxs-lookup"><span data-stu-id="39676-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="39676-152">URL 不等于页面</span><span class="sxs-lookup"><span data-stu-id="39676-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="39676-153">传统的 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序生成时，没有一个 URL，另一个页面之间的一一对应关系。</span><span class="sxs-lookup"><span data-stu-id="39676-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="39676-154">如果请求名 SomePage.aspx 为从服务器的页，则有更好地有一个页面上名为 SomePage.aspx 磁盘。</span><span class="sxs-lookup"><span data-stu-id="39676-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="39676-155">如果 SomePage.aspx 文件不存在，则获取费解之处**404-找不到页面**错误。</span><span class="sxs-lookup"><span data-stu-id="39676-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="39676-156">当构建 ASP.NET MVC 应用程序，与此相反，没有任何浏览器的地址栏中键入的 URL 和应用程序中查找的文件之间的对应关系。</span><span class="sxs-lookup"><span data-stu-id="39676-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="39676-157">在 ASP.NET MVC 应用程序 URL 对应于而不是磁盘上页面的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="39676-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="39676-158">在传统 ASP.NET 或 ASP 应用程序中，浏览器请求映射到页中。</span><span class="sxs-lookup"><span data-stu-id="39676-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="39676-159">ASP.NET MVC 应用程序中与此相反，浏览器请求映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="39676-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="39676-160">ASP.NET Web 窗体应用程序是以内容为中心。</span><span class="sxs-lookup"><span data-stu-id="39676-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="39676-161">ASP.NET MVC 应用程序中，与此相反，是为中心的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="39676-162">了解 ASP.NET 路由</span><span class="sxs-lookup"><span data-stu-id="39676-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="39676-163">将浏览器请求映射到通过一项功能的名为 ASP.NET 框架的控制器操作*ASP.NET 路由*。</span><span class="sxs-lookup"><span data-stu-id="39676-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="39676-164">ASP.NET MVC 框架使用 ASP.NET 路由*路由*传入到控制器操作的请求。</span><span class="sxs-lookup"><span data-stu-id="39676-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="39676-165">ASP.NET 路由使用路由表来处理传入的请求。</span><span class="sxs-lookup"><span data-stu-id="39676-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="39676-166">Web 应用程序首次启动时创建此路由表。</span><span class="sxs-lookup"><span data-stu-id="39676-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="39676-167">路由表是在 Global.asax 文件中的设置。</span><span class="sxs-lookup"><span data-stu-id="39676-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="39676-168">默认 MVC Global.asax 文件包含在列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="39676-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

**<span data-ttu-id="39676-169">Listing 1 - Global.asax</span><span class="sxs-lookup"><span data-stu-id="39676-169">Listing 1 - Global.asax</span></span>**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

<span data-ttu-id="39676-170">当 ASP.NET 应用程序首次启动时，应用程序\_调用 start （） 方法。</span><span class="sxs-lookup"><span data-stu-id="39676-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="39676-171">在列表 1 中，此方法调用 RegisterRoutes() 方法和 RegisterRoutes() 方法创建默认路由表。</span><span class="sxs-lookup"><span data-stu-id="39676-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="39676-172">默认路由表包含一个路由。</span><span class="sxs-lookup"><span data-stu-id="39676-172">The default route table consists of one route.</span></span> <span data-ttu-id="39676-173">此默认路由将分成三个段 （URL 段是正斜杠之间的任何内容） 的所有传入请求。</span><span class="sxs-lookup"><span data-stu-id="39676-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="39676-174">第一个段映射到的控制器的名称、 第二段映射到的操作名称和最后一段映射到参数传递给操作名为 id。</span><span class="sxs-lookup"><span data-stu-id="39676-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="39676-175">以下列 URL 为例：</span><span class="sxs-lookup"><span data-stu-id="39676-175">For example, consider the following URL:</span></span>

<span data-ttu-id="39676-176">/ 产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="39676-176">/Product/Details/3</span></span>

<span data-ttu-id="39676-177">此 URL 解析为如下三个参数：</span><span class="sxs-lookup"><span data-stu-id="39676-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="39676-178">控制器 = 产品</span><span class="sxs-lookup"><span data-stu-id="39676-178">Controller = Product</span></span>

<span data-ttu-id="39676-179">操作 = 详细信息</span><span class="sxs-lookup"><span data-stu-id="39676-179">Action = Details</span></span>

<span data-ttu-id="39676-180">id = 3</span><span class="sxs-lookup"><span data-stu-id="39676-180">Id = 3</span></span>

<span data-ttu-id="39676-181">Global.asax 文件中定义的默认路由包括所有三个参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="39676-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="39676-182">默认控制器是主页，默认操作是索引，默认 Id 是空字符串。</span><span class="sxs-lookup"><span data-stu-id="39676-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="39676-183">记住这些默认值，请看以下 URL 的分析方式：</span><span class="sxs-lookup"><span data-stu-id="39676-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="39676-184">/ 雇员</span><span class="sxs-lookup"><span data-stu-id="39676-184">/Employee</span></span>

<span data-ttu-id="39676-185">此 URL 解析为如下三个参数：</span><span class="sxs-lookup"><span data-stu-id="39676-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="39676-186">控制器 = 员工</span><span class="sxs-lookup"><span data-stu-id="39676-186">Controller = Employee</span></span>

<span data-ttu-id="39676-187">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="39676-187">Action = Index</span></span>

<span data-ttu-id="39676-188">Id =</span><span class="sxs-lookup"><span data-stu-id="39676-188">Id = ��</span></span>

<span data-ttu-id="39676-189">最后，如果您打开 ASP.NET MVC 应用程序无需提供任何 URL (例如， `http://localhost`)，则将 URL 解析如下：</span><span class="sxs-lookup"><span data-stu-id="39676-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="39676-190">控制器 = 主页</span><span class="sxs-lookup"><span data-stu-id="39676-190">Controller = Home</span></span>

<span data-ttu-id="39676-191">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="39676-191">Action = Index</span></span>

<span data-ttu-id="39676-192">Id =</span><span class="sxs-lookup"><span data-stu-id="39676-192">Id = ��</span></span>

<span data-ttu-id="39676-193">请求路由到 HomeController 类上的 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="39676-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="39676-194">了解控制器</span><span class="sxs-lookup"><span data-stu-id="39676-194">Understanding Controllers</span></span>

<span data-ttu-id="39676-195">控制器负责控制用户与 MVC 应用程序交互的方式。</span><span class="sxs-lookup"><span data-stu-id="39676-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="39676-196">控制器包含一个 ASP.NET MVC 应用程序的流控制逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="39676-197">控制器确定要发送回的用户，当用户浏览器请求的响应。</span><span class="sxs-lookup"><span data-stu-id="39676-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="39676-198">控制器是只是一个类 （例如，Visual Basic 或 C# 类）。</span><span class="sxs-lookup"><span data-stu-id="39676-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="39676-199">示例 ASP.NET MVC 应用程序包含名为 HomeController.cs 控制器文件夹中的控制器。</span><span class="sxs-lookup"><span data-stu-id="39676-199">The sample ASP.NET MVC application includes a controller named HomeController.cs located in the Controllers folder.</span></span> <span data-ttu-id="39676-200">列表 2 中重现的 HomeController.cs 文件的内容。</span><span class="sxs-lookup"><span data-stu-id="39676-200">The content of the HomeController.cs file is reproduced in Listing 2.</span></span>

**<span data-ttu-id="39676-201">代码清单 2-HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="39676-201">Listing 2 - HomeController.cs</span></span>**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

<span data-ttu-id="39676-202">请注意 HomeController 有两个名为 index （） 和将 about （） 的方法。</span><span class="sxs-lookup"><span data-stu-id="39676-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="39676-203">这两种方法与在控制器公开的两个操作相对应。</span><span class="sxs-lookup"><span data-stu-id="39676-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="39676-204">URL /Home/索引调用 HomeController.Index() 方法和 URL /Home/有关调用 HomeController.About() 方法。</span><span class="sxs-lookup"><span data-stu-id="39676-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="39676-205">在控制器中的任何公共方法公开为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="39676-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="39676-206">您需要注意相关信息。</span><span class="sxs-lookup"><span data-stu-id="39676-206">You need to be careful about this.</span></span> <span data-ttu-id="39676-207">这意味着在控制器中包含任何公共方法可由有权访问 Internet 的任何人都调用浏览器中输入正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="39676-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="39676-208">了解视图</span><span class="sxs-lookup"><span data-stu-id="39676-208">Understanding Views</span></span>

<span data-ttu-id="39676-209">公开 HomeController 类，index （） 和将 about （），这两个控制器操作都返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="39676-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="39676-210">视图包含 HTML 标记和发送到浏览器的内容。</span><span class="sxs-lookup"><span data-stu-id="39676-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="39676-211">使用 ASP.NET MVC 应用程序时，视图是一个页面的等效项。</span><span class="sxs-lookup"><span data-stu-id="39676-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="39676-212">必须在正确的位置中创建你的视图。</span><span class="sxs-lookup"><span data-stu-id="39676-212">You must create your views in the right location.</span></span> <span data-ttu-id="39676-213">HomeController.Index() 操作将返回一个视图，在位于以下路径：</span><span class="sxs-lookup"><span data-stu-id="39676-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="39676-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="39676-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="39676-215">HomeController.About() 操作将返回一个视图，在位于以下路径：</span><span class="sxs-lookup"><span data-stu-id="39676-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="39676-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="39676-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="39676-217">一般情况下，如果你想要返回的控制器操作的视图，然后需要使用与你的控制器相同的名称在 Views 文件夹中创建一个子文件夹。</span><span class="sxs-lookup"><span data-stu-id="39676-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="39676-218">在子文件夹，必须与同名的控制器操作来创建一个.aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="39676-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="39676-219">列表 3 中的文件包含 About.aspx 视图。</span><span class="sxs-lookup"><span data-stu-id="39676-219">The file in Listing 3 contains the About.aspx view.</span></span>

**<span data-ttu-id="39676-220">代码清单 3-About.aspx</span><span class="sxs-lookup"><span data-stu-id="39676-220">Listing 3 - About.aspx</span></span>**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

<span data-ttu-id="39676-221">如果忽略清单 3 中的第一行，视图的其他部分包含的标准 HTML。</span><span class="sxs-lookup"><span data-stu-id="39676-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="39676-222">您可以通过输入您所需要的任何 HTML 来修改视图的内容。</span><span class="sxs-lookup"><span data-stu-id="39676-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="39676-223">视图是非常类似于 Active Server Pages 或 ASP.NET Web 窗体中的页。</span><span class="sxs-lookup"><span data-stu-id="39676-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="39676-224">视图可以包含 HTML 内容和脚本。</span><span class="sxs-lookup"><span data-stu-id="39676-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="39676-225">您可以编写脚本中最喜欢的.NET 编程语言 （例如，C# 或 Visual Basic.NET）。</span><span class="sxs-lookup"><span data-stu-id="39676-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="39676-226">使用脚本来显示动态内容，例如数据库数据。</span><span class="sxs-lookup"><span data-stu-id="39676-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="39676-227">了解模型</span><span class="sxs-lookup"><span data-stu-id="39676-227">Understanding Models</span></span>

<span data-ttu-id="39676-228">我们已讨论了控制器，我们已讨论了视图。</span><span class="sxs-lookup"><span data-stu-id="39676-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="39676-229">我们需要介绍的最后一个主题是模型。</span><span class="sxs-lookup"><span data-stu-id="39676-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="39676-230">MVC 模型是什么？</span><span class="sxs-lookup"><span data-stu-id="39676-230">What is an MVC model?</span></span>

<span data-ttu-id="39676-231">MVC 模型包含所有未包含在视图或控制器应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="39676-232">该模型应包含的所有应用程序业务逻辑、 验证逻辑和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="39676-233">例如，如果使用 Microsoft 实体框架来访问你的数据库，然后你将创建您的 Entity Framework 类 （在.edmx 文件） Models 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="39676-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="39676-234">视图应包含仅与生成用户界面相关的逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="39676-235">控制器应只包含逻辑返回右视图或将用户重定向到另一个动作 （流控制） 所需的最低要求。</span><span class="sxs-lookup"><span data-stu-id="39676-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="39676-236">其他所有内容应包含在模型中。</span><span class="sxs-lookup"><span data-stu-id="39676-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="39676-237">一般情况下，您应尽量 fat 模型和瘦控制器。</span><span class="sxs-lookup"><span data-stu-id="39676-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="39676-238">控制器方法应包含只有少量的代码行。</span><span class="sxs-lookup"><span data-stu-id="39676-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="39676-239">如果控制器操作获取太 fat，则应考虑将逻辑移到模型文件夹中的新类。</span><span class="sxs-lookup"><span data-stu-id="39676-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="39676-240">总结</span><span class="sxs-lookup"><span data-stu-id="39676-240">Summary</span></span>

<span data-ttu-id="39676-241">本教程向你提供全面概述了 ASP.NET MVC 的不同部分的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="39676-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="39676-242">您学习了如何 ASP.NET 路由传入浏览器将请求映射到特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="39676-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="39676-243">您学习了如何控制器协调视图如何返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="39676-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="39676-244">最后，您学习了如何模型包含应用程序业务、 验证和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="39676-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>

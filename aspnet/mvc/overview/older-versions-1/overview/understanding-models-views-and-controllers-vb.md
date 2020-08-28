---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: 了解 (VB) 的模型、视图和控制器 |Microsoft Docs
author: StephenWalther
description: 对模型、视图和控制器的困惑？ 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 应用程序的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: e11487cbb863bae230ccb9dfdaf7172c65ec4d43
ms.sourcegitcommit: ffd0f59ef9b7d221a5b2010c32aa61c89c14f406
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042087"
---
# <a name="understanding-models-views-and-controllers-vb"></a><span data-ttu-id="75584-104">了解模型、视图和控制器 (VB)</span><span class="sxs-lookup"><span data-stu-id="75584-104">Understanding Models, Views, and Controllers (VB)</span></span>

<span data-ttu-id="75584-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="75584-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="75584-106">对模型、视图和控制器的困惑？</span><span class="sxs-lookup"><span data-stu-id="75584-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="75584-107">在本教程中，Stephen Walther 介绍了 ASP.NET MVC 应用程序的不同部分。</span><span class="sxs-lookup"><span data-stu-id="75584-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>

<span data-ttu-id="75584-108">本教程提供了 ASP.NET MVC 模型、视图和控制器的高级概述。</span><span class="sxs-lookup"><span data-stu-id="75584-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="75584-109">换句话说，它解释了 ASP.NET MVC 中的 M "，V" 和 C。</span><span class="sxs-lookup"><span data-stu-id="75584-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="75584-110">阅读本教程后，应了解 ASP.NET MVC 应用程序的不同部分如何协同工作。</span><span class="sxs-lookup"><span data-stu-id="75584-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="75584-111">还应了解 ASP.NET MVC 应用程序的体系结构如何与 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序不同。</span><span class="sxs-lookup"><span data-stu-id="75584-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="75584-112">示例 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="75584-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="75584-113">用于创建 ASP.NET MVC Web 应用程序的默认 Visual Studio 模板包含一个非常简单的示例应用程序，可用于了解 ASP.NET MVC 应用程序的不同部分。</span><span class="sxs-lookup"><span data-stu-id="75584-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="75584-114">在本教程中，我们将利用这个简单的应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="75584-115">通过启动 Visual Studio 2008 并选择菜单选项文件，然后选择 "新建项目" (请参阅图 1) ，通过 MVC 模板创建新的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="75584-116">在 "新建项目" 对话框中，选择 "项目类型 (Visual Basic 或 c ) #" 下喜欢的编程语言，然后在 "模板" 下选择 " **ASP.NET MVC Web 应用程序** "。</span><span class="sxs-lookup"><span data-stu-id="75584-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="75584-117">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="75584-117">Click the OK button.</span></span>

<span data-ttu-id="75584-118">[!["新建项目" 对话框](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="75584-118">[![New Project Dialog](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span></span>

<span data-ttu-id="75584-119">**图 01**： "新建项目" 对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-vb/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="75584-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image2.png))</span></span>

<span data-ttu-id="75584-120">创建新的 ASP.NET MVC 应用程序时，将显示 " **创建单元测试项目** " 对话框 (参见图 2) 。</span><span class="sxs-lookup"><span data-stu-id="75584-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="75584-121">此对话框可用于在解决方案中创建单独的项目，用于测试 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="75584-122">选择 " **否，不创建单元测试项目** "，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="75584-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>

<span data-ttu-id="75584-123">[!["创建单元测试" 对话框](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="75584-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span></span>

<span data-ttu-id="75584-124">**图 02**：创建单元测试对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-vb/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="75584-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image4.png))</span></span>

<span data-ttu-id="75584-125">创建新的 ASP.NET MVC 应用程序后。</span><span class="sxs-lookup"><span data-stu-id="75584-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="75584-126">"解决方案资源管理器" 窗口中会显示多个文件夹和文件。</span><span class="sxs-lookup"><span data-stu-id="75584-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="75584-127">特别是，您将看到三个名为 "模型"、"视图" 和 "控制器" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="75584-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="75584-128">正如您可能从文件夹名称中猜到的那样，这些文件夹包含用于实现模型、视图和控制器的文件。</span><span class="sxs-lookup"><span data-stu-id="75584-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="75584-129">如果展开 "控制器" 文件夹，应会看到名为 "AccountController" 的文件和一个名为 "HomeController" 的文件。</span><span class="sxs-lookup"><span data-stu-id="75584-129">If you expand the Controllers folder, you should see a file named AccountController.vb and a file named HomeController.vb.</span></span> <span data-ttu-id="75584-130">如果展开 "Views" 文件夹，应会看到名为 "帐户"、"家庭" 和 "共享" 的三个子文件夹。</span><span class="sxs-lookup"><span data-stu-id="75584-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="75584-131">如果你展开主文件夹，你将看到名为 "有关 .aspx 和 (的其他文件"。有关详细信息，请参阅图 3) 。</span><span class="sxs-lookup"><span data-stu-id="75584-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="75584-132">这些文件构成了默认 ASP.NET MVC 模板附带的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>

<span data-ttu-id="75584-133">[!["解决方案资源管理器" 窗口](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="75584-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span></span>

<span data-ttu-id="75584-134">**图 03**： "解决方案资源管理器" 窗口 ([单击以查看完全大小的图像](understanding-models-views-and-controllers-vb/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="75584-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image6.png))</span></span>

<span data-ttu-id="75584-135">可以通过选择菜单选项 " **调试"、"启动调试**" 来运行示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="75584-136">也可以按 F5 键。</span><span class="sxs-lookup"><span data-stu-id="75584-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="75584-137">首次运行 ASP.NET 应用程序时，会出现图4中的对话框，建议你启用调试模式。</span><span class="sxs-lookup"><span data-stu-id="75584-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="75584-138">单击 "确定" 按钮，应用程序将运行。</span><span class="sxs-lookup"><span data-stu-id="75584-138">Click the OK button and the application will run.</span></span>

<span data-ttu-id="75584-139">[!["未启用调试" 对话框](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="75584-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span></span>

<span data-ttu-id="75584-140">**图 04**： "未启用调试" 对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-vb/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="75584-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image8.png))</span></span>

<span data-ttu-id="75584-141">运行 ASP.NET MVC 应用程序时，Visual Studio 会在 web 浏览器中启动该应用程序。</span><span class="sxs-lookup"><span data-stu-id="75584-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="75584-142">该示例应用程序仅包含两个页面： "索引" 页和 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="75584-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="75584-143">首次启动应用程序时，将显示 "索引" 页 (参见图 5) 。</span><span class="sxs-lookup"><span data-stu-id="75584-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="75584-144">通过单击应用程序右上角的菜单链接，可以导航到 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="75584-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>

<span data-ttu-id="75584-145">[!["索引" 页](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="75584-145">[![The Index Page](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span></span>

<span data-ttu-id="75584-146">**图 05**：索引页 ([单击查看全尺寸图像](understanding-models-views-and-controllers-vb/_static/image10.png)) </span><span class="sxs-lookup"><span data-stu-id="75584-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image10.png))</span></span>

<span data-ttu-id="75584-147">请注意浏览器地址栏中的 Url。</span><span class="sxs-lookup"><span data-stu-id="75584-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="75584-148">例如，单击 "关于" 菜单链接后，浏览器地址栏中的 URL 将更改为 **/Home/About**。</span><span class="sxs-lookup"><span data-stu-id="75584-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="75584-149">如果关闭浏览器窗口并返回到 Visual Studio，则将无法查找路径为 Home/About 的文件。</span><span class="sxs-lookup"><span data-stu-id="75584-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="75584-150">这些文件不存在。</span><span class="sxs-lookup"><span data-stu-id="75584-150">The files don't exist.</span></span> <span data-ttu-id="75584-151">这是如何实现的？</span><span class="sxs-lookup"><span data-stu-id="75584-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="75584-152">URL 不等于页面</span><span class="sxs-lookup"><span data-stu-id="75584-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="75584-153">当您生成传统的 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序时，URL 和页面之间存在一对一的对应关系。</span><span class="sxs-lookup"><span data-stu-id="75584-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="75584-154">如果从服务器请求名为 SomePage 的页，则更好的做法是在磁盘上有一个名为 SomePage 的页面。</span><span class="sxs-lookup"><span data-stu-id="75584-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="75584-155">如果 SomePage 文件不存在，则会收到 "错误 **的 404-未找到页** " 错误。</span><span class="sxs-lookup"><span data-stu-id="75584-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="75584-156">相反，当你在浏览器的地址栏中键入的 URL 与在应用程序中找到的文件之间不存在任何关系。</span><span class="sxs-lookup"><span data-stu-id="75584-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="75584-157">在 ASP.NET MVC 应用程序中，URL 对应于控制器操作，而不是磁盘上的页面。</span><span class="sxs-lookup"><span data-stu-id="75584-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="75584-158">在传统的 ASP.NET 或 ASP 应用程序中，浏览器请求会映射到页面。</span><span class="sxs-lookup"><span data-stu-id="75584-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="75584-159">与此相反，在 ASP.NET MVC 应用程序中，浏览器请求映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="75584-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="75584-160">ASP.NET Web 窗体应用程序以内容为中心。</span><span class="sxs-lookup"><span data-stu-id="75584-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="75584-161">相反，ASP.NET MVC 应用程序是以应用程序为中心的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="75584-162">了解 ASP.NET 路由</span><span class="sxs-lookup"><span data-stu-id="75584-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="75584-163">浏览器请求通过名为 *ASP.NET 路由*的 ASP.NET 框架的功能映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="75584-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="75584-164">ASP.NET MVC 框架使用 ASP.NET 路由将传入的请求 *路由* 到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="75584-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="75584-165">ASP.NET 路由使用路由表来处理传入的请求。</span><span class="sxs-lookup"><span data-stu-id="75584-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="75584-166">当你的 web 应用程序首次启动时，将创建此路由表。</span><span class="sxs-lookup"><span data-stu-id="75584-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="75584-167">在 global.asax 文件中设置路由表。</span><span class="sxs-lookup"><span data-stu-id="75584-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="75584-168">默认 MVC global.asax 文件包含在列表1中。</span><span class="sxs-lookup"><span data-stu-id="75584-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="75584-169">**列表 1-global.asax**</span><span class="sxs-lookup"><span data-stu-id="75584-169">**Listing 1 - Global.asax**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

<span data-ttu-id="75584-170">ASP.NET 应用程序首次启动时，将 \_ 调用应用程序 ( # A1 方法。</span><span class="sxs-lookup"><span data-stu-id="75584-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="75584-171">在列表1中，此方法会调用 RegisterRoutes ( # A1 方法，RegisterRoutes ( # A3 方法会创建默认的路由表。</span><span class="sxs-lookup"><span data-stu-id="75584-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="75584-172">默认路由表包含一个路由。</span><span class="sxs-lookup"><span data-stu-id="75584-172">The default route table consists of one route.</span></span> <span data-ttu-id="75584-173">此默认路由会将所有传入请求拆分为三个段 (URL 段是正斜杠) 之间的任何内容。</span><span class="sxs-lookup"><span data-stu-id="75584-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="75584-174">第一段映射到控制器名称，第二段映射到操作名称，最后一段映射到传递给名为 Id 的操作的参数。</span><span class="sxs-lookup"><span data-stu-id="75584-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="75584-175">以下列 URL 为例：</span><span class="sxs-lookup"><span data-stu-id="75584-175">For example, consider the following URL:</span></span>

<span data-ttu-id="75584-176">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="75584-176">/Product/Details/3</span></span>

<span data-ttu-id="75584-177">此 URL 将分析为三个参数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75584-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="75584-178">控制器 = 产品</span><span class="sxs-lookup"><span data-stu-id="75584-178">Controller = Product</span></span>

<span data-ttu-id="75584-179">操作 = 详细信息</span><span class="sxs-lookup"><span data-stu-id="75584-179">Action = Details</span></span>

<span data-ttu-id="75584-180">Id = 3</span><span class="sxs-lookup"><span data-stu-id="75584-180">Id = 3</span></span>

<span data-ttu-id="75584-181">Global.asax 文件中定义的默认路由包含所有三个参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="75584-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="75584-182">默认控制器为 Home，默认操作为 Index，默认 Id 为空字符串。</span><span class="sxs-lookup"><span data-stu-id="75584-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="75584-183">考虑到这些默认设置，请考虑如何分析以下 URL：</span><span class="sxs-lookup"><span data-stu-id="75584-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="75584-184">/Employee</span><span class="sxs-lookup"><span data-stu-id="75584-184">/Employee</span></span>

<span data-ttu-id="75584-185">此 URL 将分析为三个参数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75584-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="75584-186">控制器 = 员工</span><span class="sxs-lookup"><span data-stu-id="75584-186">Controller = Employee</span></span>

<span data-ttu-id="75584-187">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="75584-187">Action = Index</span></span>

<span data-ttu-id="75584-188">Id =？</span><span class="sxs-lookup"><span data-stu-id="75584-188">Id = ?</span></span>

<span data-ttu-id="75584-189">最后，如果在不提供任何 URL 的情况下打开 ASP.NET MVC 应用程序 (例如， `http://localhost`) 则会分析 URL，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75584-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="75584-190">控制器 = Home</span><span class="sxs-lookup"><span data-stu-id="75584-190">Controller = Home</span></span>

<span data-ttu-id="75584-191">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="75584-191">Action = Index</span></span>

<span data-ttu-id="75584-192">Id =？</span><span class="sxs-lookup"><span data-stu-id="75584-192">Id = ?</span></span>

<span data-ttu-id="75584-193">请求路由到 HomeController 类上 ( # A1 操作的索引。</span><span class="sxs-lookup"><span data-stu-id="75584-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="75584-194">了解控制器</span><span class="sxs-lookup"><span data-stu-id="75584-194">Understanding Controllers</span></span>

<span data-ttu-id="75584-195">控制器负责控制用户与 MVC 应用程序交互的方式。</span><span class="sxs-lookup"><span data-stu-id="75584-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="75584-196">控制器包含 ASP.NET MVC 应用程序的流控制逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="75584-197">控制器确定当用户发出浏览器请求时要向用户发送的响应。</span><span class="sxs-lookup"><span data-stu-id="75584-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="75584-198">控制器只是类 (例如，Visual Basic 或 c # 类) 。</span><span class="sxs-lookup"><span data-stu-id="75584-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="75584-199">示例 ASP.NET MVC 应用程序在控制器文件夹中包括一个名为 HomeController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="75584-199">The sample ASP.NET MVC application includes a controller named HomeController.vb located in the Controllers folder.</span></span> <span data-ttu-id="75584-200">HomeController 文件的内容在清单2中重现。</span><span class="sxs-lookup"><span data-stu-id="75584-200">The content of the HomeController.vb file is reproduced in Listing 2.</span></span>

<span data-ttu-id="75584-201">**列表 2-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="75584-201">**Listing 2 - HomeController.cs**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

<span data-ttu-id="75584-202">请注意，HomeController 有两个名为 Index ( 方法： # A1 和 ( # A3。</span><span class="sxs-lookup"><span data-stu-id="75584-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="75584-203">这两个方法对应于控制器公开的两个操作。</span><span class="sxs-lookup"><span data-stu-id="75584-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="75584-204">URL/Home/Index 调用 HomeController ( # A1 方法，URL/Home/About 调用 HomeController。关于 ( # A3 方法。</span><span class="sxs-lookup"><span data-stu-id="75584-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="75584-205">控制器中的任何公共方法都作为控制器操作公开。</span><span class="sxs-lookup"><span data-stu-id="75584-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="75584-206">需要小心。</span><span class="sxs-lookup"><span data-stu-id="75584-206">You need to be careful about this.</span></span> <span data-ttu-id="75584-207">这意味着，可以通过在浏览器中输入正确的 URL 来调用控制器中包含的任何公共方法。</span><span class="sxs-lookup"><span data-stu-id="75584-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="75584-208">了解视图</span><span class="sxs-lookup"><span data-stu-id="75584-208">Understanding Views</span></span>

<span data-ttu-id="75584-209">HomeController 类、索引 ( # A1 和 ( # A3 公开的两个控制器操作都返回视图。</span><span class="sxs-lookup"><span data-stu-id="75584-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="75584-210">视图包含 HTML 标记和发送到浏览器的内容。</span><span class="sxs-lookup"><span data-stu-id="75584-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="75584-211">当使用 ASP.NET MVC 应用程序时，视图等效于页面。</span><span class="sxs-lookup"><span data-stu-id="75584-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="75584-212">你必须在正确的位置创建视图。</span><span class="sxs-lookup"><span data-stu-id="75584-212">You must create your views in the right location.</span></span> <span data-ttu-id="75584-213">HomeController ( # A1 操作返回位于以下路径的视图：</span><span class="sxs-lookup"><span data-stu-id="75584-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="75584-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="75584-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="75584-215">HomeController ( # A1 操作返回位于以下路径的视图：</span><span class="sxs-lookup"><span data-stu-id="75584-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="75584-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="75584-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="75584-217">通常，如果要为控制器操作返回视图，则需要在 Views 文件夹中创建与控制器名称相同的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="75584-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="75584-218">在子文件夹中，你必须创建一个与控制器操作同名的 .aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="75584-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="75584-219">列表3中的文件包含有关 .aspx 视图的信息。</span><span class="sxs-lookup"><span data-stu-id="75584-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="75584-220">**列表 3-关于 .aspx**</span><span class="sxs-lookup"><span data-stu-id="75584-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

<span data-ttu-id="75584-221">如果您忽略了列表3中的第一行，则视图的大多数其余部分都包含标准 HTML。</span><span class="sxs-lookup"><span data-stu-id="75584-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="75584-222">可以通过在此处输入所需的任何 HTML 来修改视图的内容。</span><span class="sxs-lookup"><span data-stu-id="75584-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="75584-223">视图非常类似于 Active Server Pages 或 ASP.NET Web Forms 中的页面。</span><span class="sxs-lookup"><span data-stu-id="75584-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="75584-224">视图可以包含 HTML 内容和脚本。</span><span class="sxs-lookup"><span data-stu-id="75584-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="75584-225">你可以采用最喜欢的 .NET 编程语言 (（例如，c # 或 Visual Basic .NET) 编写脚本。</span><span class="sxs-lookup"><span data-stu-id="75584-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="75584-226">使用脚本来显示动态内容（如数据库数据）。</span><span class="sxs-lookup"><span data-stu-id="75584-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="75584-227">了解模型</span><span class="sxs-lookup"><span data-stu-id="75584-227">Understanding Models</span></span>

<span data-ttu-id="75584-228">我们讨论了控制器，并讨论了视图。</span><span class="sxs-lookup"><span data-stu-id="75584-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="75584-229">我们需要讨论的最后一个主题是模型。</span><span class="sxs-lookup"><span data-stu-id="75584-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="75584-230">什么是 MVC 模型？</span><span class="sxs-lookup"><span data-stu-id="75584-230">What is an MVC model?</span></span>

<span data-ttu-id="75584-231">MVC 模型包含视图或控制器中未包含的所有应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="75584-232">模型应包含所有应用程序业务逻辑、验证逻辑和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="75584-233">例如，如果使用 Microsoft 实体框架来访问数据库，则需要在 "模型" 文件夹中创建实体框架类 (.edmx 文件) 。</span><span class="sxs-lookup"><span data-stu-id="75584-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="75584-234">视图应只包含与生成用户界面相关的逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="75584-235">控制器只应包含返回正确视图所需的最少逻辑，或将用户重定向到另一个操作 (流控制) 。</span><span class="sxs-lookup"><span data-stu-id="75584-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="75584-236">模型中应包含其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="75584-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="75584-237">通常情况下，应尽量应对 fat 模型和瘦控制器。</span><span class="sxs-lookup"><span data-stu-id="75584-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="75584-238">控制器方法应只包含几行代码。</span><span class="sxs-lookup"><span data-stu-id="75584-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="75584-239">如果控制器操作太大，则应该考虑将逻辑移出到模型文件夹中的新类。</span><span class="sxs-lookup"><span data-stu-id="75584-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="75584-240">摘要</span><span class="sxs-lookup"><span data-stu-id="75584-240">Summary</span></span>

<span data-ttu-id="75584-241">本教程提供了 ASP.NET MVC web 应用程序的不同部分的简要概述。</span><span class="sxs-lookup"><span data-stu-id="75584-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="75584-242">你了解了 ASP.NET 路由如何将传入浏览器请求映射到特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="75584-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="75584-243">已了解控制器如何协调如何将视图返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="75584-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="75584-244">最后，您了解了模型如何包含应用程序业务、验证和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="75584-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>

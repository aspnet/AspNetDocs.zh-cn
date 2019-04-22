---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: 帮助页面创建 ASP.NET web API-ASP.NET 4.x
author: MikeWasson
description: 本教程中的，代码显示了如何创建在 ASP.NET 中的 ASP.NET Web API 帮助页 4.x。
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: e3f6a9b8a6835b034a075d580cd9a33136969990
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59395006"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="0597e-103">创建 ASP.NET web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="0597e-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="0597e-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0597e-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0597e-105">本教程中的，代码显示了如何创建在 ASP.NET 中的 ASP.NET Web API 帮助页 4.x。</span><span class="sxs-lookup"><span data-stu-id="0597e-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="0597e-106">在创建 web API 时，很有用来创建一个帮助页面中，以便其他开发人员知道如何调用你的 API。</span><span class="sxs-lookup"><span data-stu-id="0597e-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="0597e-107">可以手动创建所有文档，但最好是自动生成尽可能多地。</span><span class="sxs-lookup"><span data-stu-id="0597e-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="0597e-108">若要简化此任务，ASP.NET Web API 提供一个库用于自动生成帮助页在运行时。</span><span class="sxs-lookup"><span data-stu-id="0597e-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="0597e-109">创建 API 帮助页</span><span class="sxs-lookup"><span data-stu-id="0597e-109">Creating API Help Pages</span></span>

<span data-ttu-id="0597e-110">安装[ASP.NET 和 Web 工具 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="0597e-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="0597e-111">此更新集成到 Web API 项目模板帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="0597e-112">接下来，创建一个新的 ASP.NET MVC 4 项目并选择 Web API 项目模板。</span><span class="sxs-lookup"><span data-stu-id="0597e-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="0597e-113">项目模板将创建名为示例 API 控制器`ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="0597e-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="0597e-114">此模板还创建 API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-114">The template also creates the API help pages.</span></span> <span data-ttu-id="0597e-115">所有的帮助页的代码文件位于项目的区域文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0597e-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="0597e-116">运行应用程序时，主页页面包含指向 API 帮助页的链接。</span><span class="sxs-lookup"><span data-stu-id="0597e-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="0597e-117">从主页页面的相对路径是 /Help。</span><span class="sxs-lookup"><span data-stu-id="0597e-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="0597e-118">此链接转到 API 摘要页。</span><span class="sxs-lookup"><span data-stu-id="0597e-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="0597e-119">此页的 MVC 视图 Areas/HelpPage/Views/Help/Index.cshtml 中定义。</span><span class="sxs-lookup"><span data-stu-id="0597e-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="0597e-120">您可以编辑此页可以修改布局、 简介、 标题、 样式等。</span><span class="sxs-lookup"><span data-stu-id="0597e-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="0597e-121">页面的主要部分是 Api，由控制器进行分组的表。</span><span class="sxs-lookup"><span data-stu-id="0597e-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="0597e-122">表项动态生成的使用**IApiExplorer**接口。</span><span class="sxs-lookup"><span data-stu-id="0597e-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="0597e-123">（我将详细讨论有关此接口更高版本。）如果添加新的 API 控制器，请在运行时自动更新表。</span><span class="sxs-lookup"><span data-stu-id="0597e-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="0597e-124">"API"列列出了 HTTP 方法和相对 URI。</span><span class="sxs-lookup"><span data-stu-id="0597e-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="0597e-125">"说明"列包含每个 API 的文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="0597e-126">最初，文档并不仅仅是占位符文本。</span><span class="sxs-lookup"><span data-stu-id="0597e-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="0597e-127">在下一步部分中，我将介绍您如何从 XML 注释中添加文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="0597e-128">每个 API 具有到包含更多详细信息，包括示例请求和响应正文的页面的链接。</span><span class="sxs-lookup"><span data-stu-id="0597e-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="0597e-129">将帮助页面添加到现有项目</span><span class="sxs-lookup"><span data-stu-id="0597e-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="0597e-130">可以使用 NuGet 包管理器将帮助页面添加到现有的 Web API 项目中。</span><span class="sxs-lookup"><span data-stu-id="0597e-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="0597e-131">此选项可从"Web API"的模板不同的项目模板开始。</span><span class="sxs-lookup"><span data-stu-id="0597e-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="0597e-132">从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="0597e-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="0597e-133">在中[程序包管理器控制台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)窗口中，键入以下命令之一：</span><span class="sxs-lookup"><span data-stu-id="0597e-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="0597e-134">有关**C#** 应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="0597e-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="0597e-135">有关**Visual Basic**应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="0597e-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="0597e-136">有两个包，适用于 C# 的一个，适用于 Visual Basic 的一个。</span><span class="sxs-lookup"><span data-stu-id="0597e-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="0597e-137">请确保使用匹配你的项目。</span><span class="sxs-lookup"><span data-stu-id="0597e-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="0597e-138">此命令将安装必需的程序集，并添加 （位于的区域/HelpPage 文件夹中） 的帮助页的 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="0597e-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="0597e-139">你将需要手动将链接添加到帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="0597e-140">该 URI 是 /Help。</span><span class="sxs-lookup"><span data-stu-id="0597e-140">The URI is /Help.</span></span> <span data-ttu-id="0597e-141">若要在 razor 视图中创建一个链接，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="0597e-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="0597e-142">此外，请确保注册的区域。</span><span class="sxs-lookup"><span data-stu-id="0597e-142">Also, make sure to register areas.</span></span> <span data-ttu-id="0597e-143">在 Global.asax 文件中，以下代码添加到**应用程序\_启动**方法，如果它尚不存在：</span><span class="sxs-lookup"><span data-stu-id="0597e-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="0597e-144">添加 API 文档</span><span class="sxs-lookup"><span data-stu-id="0597e-144">Adding API Documentation</span></span>

<span data-ttu-id="0597e-145">默认情况下，帮助页具有占位符字符串的文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="0597e-146">可以使用[XML 文档注释](https://msdn.microsoft.com/library/b2s063f7.aspx)若要创建文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="0597e-147">若要启用此功能，请打开文件应用程序的区域/HelpPage\_Start/HelpPageConfig.cs 并取消注释以下行：</span><span class="sxs-lookup"><span data-stu-id="0597e-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="0597e-148">现在启用 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-148">Now enable XML documentation.</span></span> <span data-ttu-id="0597e-149">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="0597e-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="0597e-150">选择**生成**页。</span><span class="sxs-lookup"><span data-stu-id="0597e-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="0597e-151">下**输出**，检查**XML 文档文件**。</span><span class="sxs-lookup"><span data-stu-id="0597e-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="0597e-152">在编辑框中，键入"应用\_Data/XmlDocument.xml"。</span><span class="sxs-lookup"><span data-stu-id="0597e-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="0597e-153">接下来，打开的代码`ValuesController`/Controllers/ValuesController.cs 中定义的 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="0597e-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="0597e-154">将一些文档注释添加到控制器方法。</span><span class="sxs-lookup"><span data-stu-id="0597e-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="0597e-155">例如：</span><span class="sxs-lookup"><span data-stu-id="0597e-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="0597e-156">提示:如果您的方法上方的行上放置插入点，并键入三个正斜杠，Visual Studio 将自动插入的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="0597e-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="0597e-157">然后你可以填写空值。</span><span class="sxs-lookup"><span data-stu-id="0597e-157">Then you can fill in the blanks.</span></span>


<span data-ttu-id="0597e-158">现在生成并再次运行应用程序，并导航到帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="0597e-159">文档字符串应显示在 API 表。</span><span class="sxs-lookup"><span data-stu-id="0597e-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="0597e-160">帮助页读取 XML 文件在运行时字符串。</span><span class="sxs-lookup"><span data-stu-id="0597e-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="0597e-161">（在部署应用程序时，请确保部署的 XML 文件。）</span><span class="sxs-lookup"><span data-stu-id="0597e-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="0597e-162">揭秘</span><span class="sxs-lookup"><span data-stu-id="0597e-162">Under the Hood</span></span>

<span data-ttu-id="0597e-163">帮助页的顶部构建**apiexplorer 记录**类，该类是 Web API 框架的一部分。</span><span class="sxs-lookup"><span data-stu-id="0597e-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="0597e-164">**Apiexplorer 记录**类用于创建帮助页提供原始材料。</span><span class="sxs-lookup"><span data-stu-id="0597e-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="0597e-165">对于每个 API， **apiexplorer 记录**包含**ApiDescription**描述 API。</span><span class="sxs-lookup"><span data-stu-id="0597e-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="0597e-166">出于此目的，"API"被指 HTTP 方法和相对 URI 的组合。</span><span class="sxs-lookup"><span data-stu-id="0597e-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="0597e-167">例如，下面是一些不同的 Api:</span><span class="sxs-lookup"><span data-stu-id="0597e-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="0597e-168">GET /api/Products</span><span class="sxs-lookup"><span data-stu-id="0597e-168">GET /api/Products</span></span>
- <span data-ttu-id="0597e-169">GET /api/Products/{id}</span><span class="sxs-lookup"><span data-stu-id="0597e-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="0597e-170">POST /api/Products</span><span class="sxs-lookup"><span data-stu-id="0597e-170">POST /api/Products</span></span>

<span data-ttu-id="0597e-171">如果控制器操作支持多个 HTTP 方法， **apiexplorer 记录**将视为不同的 API 的每个方法。</span><span class="sxs-lookup"><span data-stu-id="0597e-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="0597e-172">若要隐藏的 API **apiexplorer 记录**，添加**ApiExplorerSettings**属性的操作并设置为*IgnoreApi*为 true。</span><span class="sxs-lookup"><span data-stu-id="0597e-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="0597e-173">此外可以将此特性添加到控制器，以排除整个控制器。</span><span class="sxs-lookup"><span data-stu-id="0597e-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="0597e-174">Apiexplorer 记录类获取从文档字符串**IDocumentationProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="0597e-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="0597e-175">如您先前看到的帮助页面库提供了**IDocumentationProvider**从 XML 文档字符串获取文档。</span><span class="sxs-lookup"><span data-stu-id="0597e-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="0597e-176">该代码位于 /Areas/HelpPage/XmlDocumentationProvider.cs。</span><span class="sxs-lookup"><span data-stu-id="0597e-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="0597e-177">你可以获取文档从其他源通过编写您自己**IDocumentationProvider**。</span><span class="sxs-lookup"><span data-stu-id="0597e-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="0597e-178">若要连接它，请调用**SetDocumentationProvider**中定义的扩展方法**HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="0597e-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="0597e-179">**Apiexplorer 记录**自动调入**IDocumentationProvider**接口来获取每个 API 的文档字符串。</span><span class="sxs-lookup"><span data-stu-id="0597e-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="0597e-180">它将它们存储在**文档**的属性**ApiDescription**并**ApiParameterDescription**对象。</span><span class="sxs-lookup"><span data-stu-id="0597e-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0597e-181">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0597e-181">Next Steps</span></span>

<span data-ttu-id="0597e-182">您并不限于如下所示的帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="0597e-183">事实上， **apiexplorer 记录**并不局限于创建帮助页。</span><span class="sxs-lookup"><span data-stu-id="0597e-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="0597e-184">Yao Huang Lin 撰写了一些很好的博客文章以获取您考虑在初始状态：</span><span class="sxs-lookup"><span data-stu-id="0597e-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="0597e-185">将一个简单的测试客户端添加到 ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="0597e-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="0597e-186">使 ASP.NET Web API 帮助页上自承载服务工作</span><span class="sxs-lookup"><span data-stu-id="0597e-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="0597e-187">设计时生成的 ASP.NET Web API 的帮助页 （或客户端）</span><span class="sxs-lookup"><span data-stu-id="0597e-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="0597e-188">高级帮助页自定义</span><span class="sxs-lookup"><span data-stu-id="0597e-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)

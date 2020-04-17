---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 将ASP.NET MVC 与不同版本的 IIS （C#） 一起使用 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何使用ASP.NET MVC 和 URL 路由，以及不同版本的 Internet 信息服务。 你学习不同的策略...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c239c3c7cbbaae5d9c5e4dd91dc66ff4e98bcfb
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542074"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="15516-104">通过不同版本的 IIS 使用 ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="15516-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>

<span data-ttu-id="15516-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="15516-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="15516-106">在本教程中，您将了解如何使用ASP.NET MVC 和 URL 路由，以及不同版本的 Internet 信息服务。</span><span class="sxs-lookup"><span data-stu-id="15516-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="15516-107">您将学习将 ASP.NET MVC 与 IIS 7.0（经典模式）、IIS 6.0 和早期版本的 IIS 使用的不同策略。</span><span class="sxs-lookup"><span data-stu-id="15516-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="15516-108">ASP.NET MVC 框架依赖于ASP.NET路由来将浏览器请求路由到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="15516-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="15516-109">为了利用ASP.NET路由，您可能需要在 Web 服务器上执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="15516-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="15516-110">这完全取决于互联网信息服务 （IIS） 的版本和应用程序的请求处理模式。</span><span class="sxs-lookup"><span data-stu-id="15516-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="15516-111">以下是不同版本的 IIS 的摘要：</span><span class="sxs-lookup"><span data-stu-id="15516-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="15516-112">IIS 7.0（集成模式） - 无需特殊配置ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="15516-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="15516-113">IIS 7.0（经典模式） - 您需要执行特殊配置才能使用ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="15516-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="15516-114">IIS 6.0 或以下 - 您需要执行特殊配置才能使用ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="15516-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="15516-115">最新版本的 IIS 版本为 7.5 版本（在 Win7 上）。</span><span class="sxs-lookup"><span data-stu-id="15516-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="15516-116">IIS 7 的 IIS 包含在 Windows 服务器 2008 和 VISTA/SP1 及更高版本中。</span><span class="sxs-lookup"><span data-stu-id="15516-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="15516-117">您还可以在 Vista 操作系统的任何版本上安装 IIS 7.0，但家庭基本版除外[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)（参见 ）。</span><span class="sxs-lookup"><span data-stu-id="15516-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="15516-118">IIS 7.0 支持两种处理请求的模式。</span><span class="sxs-lookup"><span data-stu-id="15516-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="15516-119">您可以使用集成模式或经典模式。</span><span class="sxs-lookup"><span data-stu-id="15516-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="15516-120">在集成模式下使用 IIS 7.0 时，无需执行任何特殊配置步骤。</span><span class="sxs-lookup"><span data-stu-id="15516-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="15516-121">但是，在经典模式下使用 IIS 7.0 时，您确实需要执行其他配置。</span><span class="sxs-lookup"><span data-stu-id="15516-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="15516-122">微软 Windows 服务器 2003 包括 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="15516-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="15516-123">使用 Windows Server 2003 操作系统时，无法将 IIS 6.0 升级到 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="15516-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="15516-124">使用 IIS 6.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="15516-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="15516-125">微软视窗XP专业版包括IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="15516-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="15516-126">使用 IIS 5.1 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="15516-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="15516-127">最后，微软 Windows 2000 和微软 Windows 2000 专业版包括 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="15516-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="15516-128">使用 IIS 5.0 时，必须执行其他配置步骤。</span><span class="sxs-lookup"><span data-stu-id="15516-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="15516-129">集成模式与经典模式</span><span class="sxs-lookup"><span data-stu-id="15516-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="15516-130">IIS 7.0 可以使用两种不同的请求处理模式处理请求：集成和经典。</span><span class="sxs-lookup"><span data-stu-id="15516-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="15516-131">集成模式提供更好的性能和更多功能。</span><span class="sxs-lookup"><span data-stu-id="15516-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="15516-132">经典模式包括向后兼容早期版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="15516-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="15516-133">请求处理模式由应用程序池确定。</span><span class="sxs-lookup"><span data-stu-id="15516-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="15516-134">通过确定与应用程序关联的应用程序池，可以确定特定 Web 应用程序正在使用哪种处理模式。</span><span class="sxs-lookup"><span data-stu-id="15516-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="15516-135">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="15516-135">Follow these steps:</span></span>

1. <span data-ttu-id="15516-136">推出互联网信息服务管理器</span><span class="sxs-lookup"><span data-stu-id="15516-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="15516-137">在"连接"窗口中，选择应用程序</span><span class="sxs-lookup"><span data-stu-id="15516-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="15516-138">在"操作"窗口中，单击 **"基本设置"** 链接以打开"编辑应用程序"对话框（参见图 1）</span><span class="sxs-lookup"><span data-stu-id="15516-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="15516-139">请注意所选的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="15516-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="15516-140">默认情况下，IIS 配置为支持两个应用程序池：**默认AppPool**和**经典 .NET AppPool**。</span><span class="sxs-lookup"><span data-stu-id="15516-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="15516-141">如果选择了默认AppPool，则应用程序以集成的请求处理模式运行。</span><span class="sxs-lookup"><span data-stu-id="15516-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="15516-142">如果选择了经典 .NET AppPool，则应用程序以经典请求处理模式运行。</span><span class="sxs-lookup"><span data-stu-id="15516-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="15516-143">[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="15516-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="15516-144">**图1：** 检测请求处理模式（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="15516-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="15516-145">请注意，您可以在"编辑应用程序"对话框中修改请求处理模式。</span><span class="sxs-lookup"><span data-stu-id="15516-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="15516-146">单击"选择"按钮并更改与应用程序关联的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="15516-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="15516-147">请注意，将ASP.NET应用程序从经典模式更改为集成模式时存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="15516-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="15516-148">有关详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="15516-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="15516-149">将 ASP.NET 1.1 升级到 Windows Vista 和 Windows 服务器 2008 上的 IIS 7.0 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="15516-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="15516-150">ASP.NET与 IIS 7.0 集成 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="15516-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="15516-151">如果ASP.NET应用程序正在使用 DefaultAppPool，则无需执行任何其他步骤，就可以使ASP.NET路由（因此ASP.NET MVC）正常工作。</span><span class="sxs-lookup"><span data-stu-id="15516-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="15516-152">但是，如果ASP.NET应用程序配置为使用经典 .NET AppPool，然后继续阅读，您还有更多工作要做。</span><span class="sxs-lookup"><span data-stu-id="15516-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="15516-153">将ASP.NET MVC 与旧版本的 IIS 一起使用</span><span class="sxs-lookup"><span data-stu-id="15516-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="15516-154">如果您需要将 IIS 版本早于 IIS 7.0 的旧版本ASP.NET MVC 使用，或者需要在经典模式下使用 IIS 7.0，则有两个选项。</span><span class="sxs-lookup"><span data-stu-id="15516-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="15516-155">首先，您可以修改路由表以使用文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="15516-156">例如，您请求的 URL 不是 /Store/详细信息，而是请求 URL，如 /Store.aspx/详细信息。</span><span class="sxs-lookup"><span data-stu-id="15516-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="15516-157">第二个选项是创建称为*通配符脚本映射*的内容。</span><span class="sxs-lookup"><span data-stu-id="15516-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="15516-158">通配符脚本映射使您能够将每个请求映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="15516-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="15516-159">如果您无法访问 Web 服务器（例如，您的ASP.NET MVC 应用程序由 Internet 服务提供商托管），则需要使用第一个选项。</span><span class="sxs-lookup"><span data-stu-id="15516-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="15516-160">如果不想修改 URL 的外观，并且可以访问 Web 服务器，则可以使用第二个选项。</span><span class="sxs-lookup"><span data-stu-id="15516-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="15516-161">我们将在以下部分中详细介绍每个选项。</span><span class="sxs-lookup"><span data-stu-id="15516-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="15516-162">向路由表添加扩展</span><span class="sxs-lookup"><span data-stu-id="15516-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="15516-163">获取ASP.NET路由以使用旧版本的 IIS 的最简单方法是修改 Global.asax 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="15516-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="15516-164">清单1中的默认和未修改的 Global.asax 文件配置了一个名为"默认路由"的路由。</span><span class="sxs-lookup"><span data-stu-id="15516-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="15516-165">**清单1 - 全局.asax（未修改）**</span><span class="sxs-lookup"><span data-stu-id="15516-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="15516-166">通过清单 1 中配置的默认路由，您可以路由如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="15516-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="15516-167">/首页/索引</span><span class="sxs-lookup"><span data-stu-id="15516-167">/Home/Index</span></span>

<span data-ttu-id="15516-168">/产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="15516-168">/Product/Details/3</span></span>

<span data-ttu-id="15516-169">/Product</span><span class="sxs-lookup"><span data-stu-id="15516-169">/Product</span></span>

<span data-ttu-id="15516-170">遗憾的是，旧版本的 IIS 不会将这些请求传递给ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="15516-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="15516-171">因此，这些请求不会路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="15516-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="15516-172">例如，如果您对 URL/Home/Index 发出浏览器请求，则将在图 2 中获取错误页。</span><span class="sxs-lookup"><span data-stu-id="15516-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="15516-173">[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="15516-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="15516-174">**图2**： 收到 404 未找到错误（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="15516-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="15516-175">较旧版本的 IIS 仅将某些请求映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="15516-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="15516-176">请求必须针对具有正确文件扩展名的 URL。</span><span class="sxs-lookup"><span data-stu-id="15516-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="15516-177">例如，对 /SomePage.aspx 的请求将映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="15516-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="15516-178">但是，对 /SomePage.htm 的请求没有。</span><span class="sxs-lookup"><span data-stu-id="15516-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="15516-179">因此，要使ASP.NET路由正常工作，我们必须修改默认路由，以便它包含映射到ASP.NET框架的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="15516-180">这是使用名为 的`registermvc.wsf`脚本完成的。</span><span class="sxs-lookup"><span data-stu-id="15516-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="15516-181">它包含在 ASP.NET MVC 1 版本中`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`，但截至 ASP.NET 2，此脚本已移动到 ASP.NET 期货，可在[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)。</span><span class="sxs-lookup"><span data-stu-id="15516-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="15516-182">执行此脚本会使用 IIS 注册新的 .mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="15516-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="15516-183">注册 .mvc 扩展名后，您可以在 Global.asax 文件中修改路由，以便路由使用 .mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="15516-184">清单2中修改后的 Global.asax 文件适用于旧版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="15516-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="15516-185">**清单 2 - 全局.asax（使用扩展修改）**</span><span class="sxs-lookup"><span data-stu-id="15516-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="15516-186">**重要提示**：在更改 Global.asax 文件后，请记住再次构建ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="15516-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="15516-187">清单2中全局.asax 文件有两个重要更改。</span><span class="sxs-lookup"><span data-stu-id="15516-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="15516-188">现在，全局.asax 中定义了两个路由。</span><span class="sxs-lookup"><span data-stu-id="15516-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="15516-189">默认路由（第一个路由）的 URL 模式现在如下所示：</span><span class="sxs-lookup"><span data-stu-id="15516-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="15516-190">{控制器}.mvc/{操作}/{id}</span><span class="sxs-lookup"><span data-stu-id="15516-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="15516-191">.mvc 扩展名的添加会更改ASP.NET路由模块截获的文件类型。</span><span class="sxs-lookup"><span data-stu-id="15516-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="15516-192">通过此更改，ASP.NET MVC 应用程序现在路由如下所示的请求：</span><span class="sxs-lookup"><span data-stu-id="15516-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="15516-193">/Home.mvc/指数/</span><span class="sxs-lookup"><span data-stu-id="15516-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="15516-194">/产品.mvc/细节/3</span><span class="sxs-lookup"><span data-stu-id="15516-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="15516-195">/产品.mvc/</span><span class="sxs-lookup"><span data-stu-id="15516-195">/Product.mvc/</span></span>

<span data-ttu-id="15516-196">第二个路由，根路由，是新的。</span><span class="sxs-lookup"><span data-stu-id="15516-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="15516-197">根路由的此 URL 模式是一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="15516-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="15516-198">对于匹配针对应用程序根发出的请求，此路由是必需的。</span><span class="sxs-lookup"><span data-stu-id="15516-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="15516-199">例如，根路由将匹配如下所示的请求：</span><span class="sxs-lookup"><span data-stu-id="15516-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="15516-200">对路由表进行这些修改后，需要确保应用程序中的所有链接都与这些新 URL 模式兼容。</span><span class="sxs-lookup"><span data-stu-id="15516-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="15516-201">换句话说，请确保所有链接都包含 .mvc 扩展。</span><span class="sxs-lookup"><span data-stu-id="15516-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="15516-202">如果使用 Html.ActionLink（） 帮助器方法生成链接，则不需要进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="15516-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="15516-203">您可以手动向 iIS 添加新扩展 ASP.NET，而不是使用 registermvc.wcf 脚本。</span><span class="sxs-lookup"><span data-stu-id="15516-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="15516-204">自行添加新扩展名时，请确保未选中标记为 **"验证该文件存在"复选框**。</span><span class="sxs-lookup"><span data-stu-id="15516-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="15516-205">托管服务器</span><span class="sxs-lookup"><span data-stu-id="15516-205">Hosted Server</span></span>

<span data-ttu-id="15516-206">您并不总是有权访问 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="15516-206">You don't always have access to your web server.</span></span> <span data-ttu-id="15516-207">例如，如果您使用 Internet 托管提供商托管ASP.NET MVC 应用程序，则不一定有权访问 IIS。</span><span class="sxs-lookup"><span data-stu-id="15516-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="15516-208">在这种情况下，应使用映射到ASP.NET框架的现有文件扩展名之一。</span><span class="sxs-lookup"><span data-stu-id="15516-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="15516-209">映射到ASP.NET的文件扩展名的示例包括 .aspx、.axd 和 .ashx 扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="15516-210">例如，清单 3 中修改的 Global.asax 文件使用 .aspx 扩展名而不是 .mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="15516-211">**清单 3 - 全局.asax（使用 .aspx 扩展修改）**</span><span class="sxs-lookup"><span data-stu-id="15516-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="15516-212">清单3中的 Global.asax 文件与以前的 Global.asax 文件完全相同，只是它使用 .aspx 扩展名而不是 .mvc 扩展名。</span><span class="sxs-lookup"><span data-stu-id="15516-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="15516-213">您不必在远程 Web 服务器上执行任何设置才能使用 .aspx 扩展。</span><span class="sxs-lookup"><span data-stu-id="15516-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="15516-214">创建通配符脚本映射</span><span class="sxs-lookup"><span data-stu-id="15516-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="15516-215">如果您不想修改ASP.NET MVC 应用程序的 URL，并且可以访问 Web 服务器，则有一个其他选项。</span><span class="sxs-lookup"><span data-stu-id="15516-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="15516-216">您可以创建通配符脚本映射，将所有请求映射到 Web 服务器ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="15516-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="15516-217">这样，您可以使用默认ASP.NET MVC 路由表与 IIS 7.0（经典模式）或 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="15516-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="15516-218">请注意，此选项会导致 IIS 拦截针对 Web 服务器的每个请求。</span><span class="sxs-lookup"><span data-stu-id="15516-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="15516-219">这包括对图像、经典 ASP 页面和 HTML 页面的请求。</span><span class="sxs-lookup"><span data-stu-id="15516-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="15516-220">因此，将通配符脚本映射启用ASP.NET确实会影响性能。</span><span class="sxs-lookup"><span data-stu-id="15516-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="15516-221">以下是为 IIS 7.0 启用通配符脚本映射的方式：</span><span class="sxs-lookup"><span data-stu-id="15516-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="15516-222">在"连接"窗口中选择应用程序</span><span class="sxs-lookup"><span data-stu-id="15516-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="15516-223">确保选择了 **"功能"** 视图</span><span class="sxs-lookup"><span data-stu-id="15516-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="15516-224">双击 **"处理程序映射"** 按钮</span><span class="sxs-lookup"><span data-stu-id="15516-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="15516-225">单击 **"添加通配符脚本映射"** 链接（参见图 3）</span><span class="sxs-lookup"><span data-stu-id="15516-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="15516-226">输入 aspnet\_isapi.dll 文件的路径（可以从 PageHandlerFactory 脚本映射复制此路径）</span><span class="sxs-lookup"><span data-stu-id="15516-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="15516-227">输入名称 MVC</span><span class="sxs-lookup"><span data-stu-id="15516-227">Enter the name MVC</span></span>
7. <span data-ttu-id="15516-228">单击 **"确定"** 按钮</span><span class="sxs-lookup"><span data-stu-id="15516-228">Click the **OK** button</span></span>

<span data-ttu-id="15516-229">[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="15516-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="15516-230">**图 3**： 使用 IIS 7.0 创建通配符脚本映射（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="15516-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="15516-231">按照以下步骤创建具有 IIS 6.0 的通配符脚本映射：</span><span class="sxs-lookup"><span data-stu-id="15516-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="15516-232">右键单击网站并选择"属性"</span><span class="sxs-lookup"><span data-stu-id="15516-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="15516-233">选择**主目录**选项卡</span><span class="sxs-lookup"><span data-stu-id="15516-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="15516-234">单击 **"配置"** 按钮</span><span class="sxs-lookup"><span data-stu-id="15516-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="15516-235">选择 **"映射"** 选项卡</span><span class="sxs-lookup"><span data-stu-id="15516-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="15516-236">单击 **"插入"** 按钮（参见图 4）</span><span class="sxs-lookup"><span data-stu-id="15516-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="15516-237">将 aspnet\_isapi.dll 的路径粘贴到可执行字段（可以从 .aspx 文件的脚本映射中复制此路径）</span><span class="sxs-lookup"><span data-stu-id="15516-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="15516-238">取消选中标记为 **"验证文件存在"复选框**</span><span class="sxs-lookup"><span data-stu-id="15516-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="15516-239">单击 **"确定"** 按钮</span><span class="sxs-lookup"><span data-stu-id="15516-239">Click the **OK** button</span></span>

<span data-ttu-id="15516-240">[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="15516-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="15516-241">**图 4**： 使用 IIS 6.0 创建通配符脚本映射（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="15516-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="15516-242">启用通配符脚本映射后，需要修改 Global.asax 文件中的路由表，以便它包含根路由。</span><span class="sxs-lookup"><span data-stu-id="15516-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="15516-243">否则，当您请求应用程序的根页时，您将获得图 5 中的错误页。</span><span class="sxs-lookup"><span data-stu-id="15516-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="15516-244">您可以使用清单 4 中修改的 Global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="15516-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="15516-245">[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="15516-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="15516-246">**图 5**： 缺少根路由错误（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="15516-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="15516-247">**清单 4 - 全局.asax（使用根路由修改）**</span><span class="sxs-lookup"><span data-stu-id="15516-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="15516-248">为 IIS 7.0 或 IIS 6.0 启用通配符脚本映射后，可以发出适用于默认路由表的请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="15516-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="15516-249">/首页/索引</span><span class="sxs-lookup"><span data-stu-id="15516-249">/Home/Index</span></span>

<span data-ttu-id="15516-250">/产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="15516-250">/Product/Details/3</span></span>

<span data-ttu-id="15516-251">/Product</span><span class="sxs-lookup"><span data-stu-id="15516-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="15516-252">总结</span><span class="sxs-lookup"><span data-stu-id="15516-252">Summary</span></span>

<span data-ttu-id="15516-253">本教程的目的是解释在使用旧版本的 IIS（或经典模式下的 IIS 7.0）时如何使用ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="15516-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="15516-254">我们讨论了使ASP.NET路由与旧版本的 IIS 配合使用的方法：修改默认路由表或创建通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="15516-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="15516-255">第一个选项要求您修改ASP.NET MVC 应用程序中使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="15516-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="15516-256">第一个选项的一个显著优点是，您不需要访问 Web 服务器来修改路由表。</span><span class="sxs-lookup"><span data-stu-id="15516-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="15516-257">这意味着，即使使用 internet 托管公司托管ASP.NET MVC 应用程序，您也可以使用此选项。</span><span class="sxs-lookup"><span data-stu-id="15516-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="15516-258">第二个选项是创建通配符脚本映射。</span><span class="sxs-lookup"><span data-stu-id="15516-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="15516-259">第二个选项的优点是不需要修改 URL。</span><span class="sxs-lookup"><span data-stu-id="15516-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="15516-260">第二个选项的缺点是它会影响ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="15516-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="15516-261">下一页</span><span class="sxs-lookup"><span data-stu-id="15516-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)

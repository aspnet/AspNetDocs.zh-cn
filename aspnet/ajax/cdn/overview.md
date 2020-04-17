---
uid: ajax/cdn/overview
title: 微软Ajax内容交付网络 |微软文档
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540202"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="1811a-102">Microsoft Ajax 内容分发网络</span><span class="sxs-lookup"><span data-stu-id="1811a-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="1811a-103">生产应用程序不应对 CDN 资产产生硬性依赖。</span><span class="sxs-lookup"><span data-stu-id="1811a-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="1811a-104">应用程序应测试引用的 CDN 资产，并在 CDN 不可用时使用回退资产。</span><span class="sxs-lookup"><span data-stu-id="1811a-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="1811a-105">微软Ajax CDN除了使用 Azure CDN 之外，没有 SLA。</span><span class="sxs-lookup"><span data-stu-id="1811a-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="1811a-106">[使用此 GitHub 问题](https://github.com/dotnet/AspNetDocs/issues/116)可以报告 Microsoft Ajax CDN 的问题。</span><span class="sxs-lookup"><span data-stu-id="1811a-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="1811a-107">目录</span><span class="sxs-lookup"><span data-stu-id="1811a-107">Table of Contents</span></span>

<span data-ttu-id="1811a-108">**[ajax.microsoft.com重命名为ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="1811a-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="1811a-109">**[视觉工作室 .vsdoc 支持](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="1811a-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="1811a-110">**[使用来自 CDN 的ASP.NETAjax](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="1811a-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="1811a-111">**[使用来自 CDN 的 jQuery](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="1811a-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="1811a-112">**[使用 CDN 中的 jQuery UI](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="1811a-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="1811a-113">**[CDN 上的第三方文件](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="1811a-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="1811a-114">jQuery 在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="1811a-115">jQuery 迁移 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="1811a-116">jQuery 在 CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="1811a-117">j查询 CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="1811a-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="1811a-118">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="1811a-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="1811a-119">jQuery 模板在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="1811a-120">jQuery 周期版本在 CDN 上</span><span class="sxs-lookup"><span data-stu-id="1811a-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="1811a-121">j查询数据表在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="1811a-122">CDN 上的现代版本</span><span class="sxs-lookup"><span data-stu-id="1811a-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="1811a-123">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="1811a-124">CDN 上的挖空版本</span><span class="sxs-lookup"><span data-stu-id="1811a-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="1811a-125">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="1811a-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="1811a-126">CDN 上的响应版本</span><span class="sxs-lookup"><span data-stu-id="1811a-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="1811a-127">CDN 上的引导版本</span><span class="sxs-lookup"><span data-stu-id="1811a-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="1811a-128">CDN 上的引导触摸卡盘释放</span><span class="sxs-lookup"><span data-stu-id="1811a-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="1811a-129">Hammer.js 在 CDN 上发布</span><span class="sxs-lookup"><span data-stu-id="1811a-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="1811a-130">ASP.NET在 CDN 上的 Web 窗体和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="1811a-131">cdN 上的ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="1811a-132">ASP.NET信号R在 CDN 上的释放</span><span class="sxs-lookup"><span data-stu-id="1811a-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="1811a-133">Microsoft Ajax 内容交付网络 （CDN） 托管流行的第三方 JavaScript 库（如 jQuery），使您能够轻松地将它们添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1811a-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="1811a-134">例如，只需向指向ajax.aspnetcdn.com的页面添加&lt;指向的脚本&gt;标记，即可开始使用在此 CDN 上托管的 jQuery。</span><span class="sxs-lookup"><span data-stu-id="1811a-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="1811a-135">通过利用 CDN，您可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1811a-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="1811a-136">CDN 的内容缓存在世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="1811a-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="1811a-137">此外，CDN 使浏览器能够为位于不同域中的网站重用缓存的第三方 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="1811a-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="1811a-138">CDN 支持 SSL （HTTPS），以防您需要使用安全套接字层为网页提供服务。</span><span class="sxs-lookup"><span data-stu-id="1811a-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="1811a-139">CDN 托管以下第三方脚本库，这些库的所有者已上载并授予您许可：</span><span class="sxs-lookup"><span data-stu-id="1811a-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="1811a-140">jQuery （www.jquery.com）</span><span class="sxs-lookup"><span data-stu-id="1811a-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="1811a-141">jQuery UI（www.jqueryui.com）</span><span class="sxs-lookup"><span data-stu-id="1811a-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="1811a-142">jQuery 移动 （www.jquerymobile.com）</span><span class="sxs-lookup"><span data-stu-id="1811a-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="1811a-143">jQuery 验证 （https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="1811a-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="1811a-144">j查询周期 （www.malsup.com/jquery/cycle/）</span><span class="sxs-lookup"><span data-stu-id="1811a-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="1811a-145">j查询数据表 （http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="1811a-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="1811a-146">微软Ajax CDN还包括由微软上传的以下库：</span><span class="sxs-lookup"><span data-stu-id="1811a-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="1811a-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="1811a-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="1811a-148">ASP.NET MVC JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="1811a-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="1811a-149">ASP.NET信号R JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="1811a-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="1811a-150">Microsoft 不声明在此 CDN 上托管的任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="1811a-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="1811a-151">图书馆的版权所有者正在授权这些库给您。</span><span class="sxs-lookup"><span data-stu-id="1811a-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="1811a-152">您可能需要下载和使用此类库的任何权利仅由相应的版权所有者授予。</span><span class="sxs-lookup"><span data-stu-id="1811a-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="1811a-153">由于这些不是 Microsoft 库，因此 Microsoft 不会为此 CDN 上托管的第三方库提供担保或知识产权许可（包括无隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="1811a-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="1811a-154">如果您希望提交 JavaScript 库，并且您的库是顶级 JavaScript 库之一（如上http://trends.builtwith.com)列出的或扩展/插件到这些库，这些库是 （a） 流行;或 （b） 有助于在ASP.NET使用，则请联系AjaxCDNSubmission@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="1811a-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="1811a-155">ajax.microsoft.com重命名为ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="1811a-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="1811a-156">CDN 用于使用microsoft.com域名，并已更改为使用aspnetcdn.com域名。</span><span class="sxs-lookup"><span data-stu-id="1811a-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="1811a-157">进行此更改是为了提高性能，因为当浏览器引用microsoft.com域时，它会通过每个请求通过网络发送来自该域的任何 Cookie。</span><span class="sxs-lookup"><span data-stu-id="1811a-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="1811a-158">通过重命名为microsoft.com以外的域名，性能可以提高多达 25%。</span><span class="sxs-lookup"><span data-stu-id="1811a-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="1811a-159">注意ajax.microsoft.com将继续发挥作用，但建议ajax.aspnetcdn.com。</span><span class="sxs-lookup"><span data-stu-id="1811a-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="1811a-160">旧格式：https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="1811a-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="1811a-161">新格式：https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="1811a-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="1811a-162">视觉工作室 .vsdoc 支持</span><span class="sxs-lookup"><span data-stu-id="1811a-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="1811a-163">要正确使用 .vsdoc 文件与 Visual Studio 2008，您需要确保已安装 VS 2008 SP1 和安装 vsdoc 文件的修补程序。</span><span class="sxs-lookup"><span data-stu-id="1811a-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="1811a-164">你可以从这里得到这些：</span><span class="sxs-lookup"><span data-stu-id="1811a-164">You can get these from here:</span></span>

- [<span data-ttu-id="1811a-165">下载视觉工作室 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="1811a-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下载视觉工作室 2008 SP1")
- [<span data-ttu-id="1811a-166">下载 .vsdoc 修补程序视觉工作室 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="1811a-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "下载 .vsdoc 修补程序视觉工作室 2008 SP1")

<span data-ttu-id="1811a-167">Visual Studio 2010 支持 .vsdoc 文件，无需任何其他修补程序。</span><span class="sxs-lookup"><span data-stu-id="1811a-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="1811a-168">使用来自 CDN 的ASP.NETAjax</span><span class="sxs-lookup"><span data-stu-id="1811a-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="1811a-169">使用ASP.NET 4 时，可以将ASP.NET框架脚本的所有请求重定向到 CDN。</span><span class="sxs-lookup"><span data-stu-id="1811a-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="1811a-170">从 CDN 而不是本地 Web 服务器检索脚本可以显著提高公共ASP.NET网站的性能。</span><span class="sxs-lookup"><span data-stu-id="1811a-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="1811a-171">使用脚本管理器启用CDN属性将所有ASP.NET框架脚本请求重定向到 Microsoft Ajax CDN：</span><span class="sxs-lookup"><span data-stu-id="1811a-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="1811a-172">使用来自 CDN 的 jQuery</span><span class="sxs-lookup"><span data-stu-id="1811a-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="1811a-173">您可以通过将以下脚本元素添加到页面，使用 Web 应用程序中 CDN 上托管的 jQuery 脚本：</span><span class="sxs-lookup"><span data-stu-id="1811a-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="1811a-174">CDN 还包括 jQuery 脚本的微化版本，您可以使用以下元素获取该版本：</span><span class="sxs-lookup"><span data-stu-id="1811a-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="1811a-175">要允许页面回退到从您自己的网站上的本地路径加载 jQuery（如果 CDN 恰好不可用），请立即在引用 CDN 的元素之后添加以下元素：</span><span class="sxs-lookup"><span data-stu-id="1811a-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="1811a-176">以下示例页使用 jQuery 库的 CDN 版本（回退到本地副本）在单击按钮时显示 div 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="1811a-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="1811a-177">您可以了解有关 jQuery 的更多内容，并通过访问 jQuery 网站下载[jQuery](http://jquery.com/)的本地副本。</span><span class="sxs-lookup"><span data-stu-id="1811a-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="1811a-178">使用 CDN 中的 jQuery UI</span><span class="sxs-lookup"><span data-stu-id="1811a-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="1811a-179">CDN 还托管 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="1811a-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="1811a-180">jQuery UI 库包含一组丰富的小部件和效果，您可以在ASP.NET应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="1811a-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="1811a-181">例如，以下页面说明了如何在ASP.NET Web 窗体应用程序的上下文中使用 jQuery UI 日期选取器来显示弹出日历：</span><span class="sxs-lookup"><span data-stu-id="1811a-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="1811a-182">当您使用键盘将焦点移动到 TextBox 时，将显示日历：</span><span class="sxs-lookup"><span data-stu-id="1811a-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![使用日期选取器创建的弹出日历](overview/_static/image1.png)

<span data-ttu-id="1811a-184">请注意，您必须在上面的代码中包含来自 CDN 的三个文件：</span><span class="sxs-lookup"><span data-stu-id="1811a-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="1811a-185">jQuery 库&mdash;jQuery UI 库依赖于 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="1811a-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="1811a-186">在添加 jQuery UI 库之前，必须将 jQuery 库添加到页面。</span><span class="sxs-lookup"><span data-stu-id="1811a-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="1811a-187">jQuery UI&mdash;库 jQuery UI 库包含所有 jQuery UI 效果和小部件，如上页中使用的 Datepicker 小部件。</span><span class="sxs-lookup"><span data-stu-id="1811a-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="1811a-188">jQuery UI 主题&mdash;jQuery 支持不同的主题。</span><span class="sxs-lookup"><span data-stu-id="1811a-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="1811a-189">上面的页面包含指向 CSS 文件的链接，用于导入雷德蒙德主题。</span><span class="sxs-lookup"><span data-stu-id="1811a-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="1811a-190">所有标准 jQuery UI 主题都托管在 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="1811a-191">[访问此页面](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 的 jQuery UI 1.8.10")以查看每个主题的缩略图。</span><span class="sxs-lookup"><span data-stu-id="1811a-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="1811a-192">要了解有关 jQuery UI 库的信息，请访问[官方 jQuery UI 网站](http://jQueryUI.com "jQuery UI网站")。</span><span class="sxs-lookup"><span data-stu-id="1811a-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="1811a-193">CDN 上的第三方文件</span><span class="sxs-lookup"><span data-stu-id="1811a-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="1811a-194">CDN 托管一些最流行的第三方 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="1811a-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="1811a-195">Microsoft 不声明在此 CDN 上托管的任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="1811a-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="1811a-196">图书馆的版权所有者正在授权这些库给您。</span><span class="sxs-lookup"><span data-stu-id="1811a-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="1811a-197">您可能需要下载和使用此类库的任何权利仅由相应的版权所有者授予。</span><span class="sxs-lookup"><span data-stu-id="1811a-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="1811a-198">由于这些不是 Microsoft 库，因此 Microsoft 不会为此 CDN 上托管的第三方库提供担保或知识产权许可（包括无隐含的专利权）。</span><span class="sxs-lookup"><span data-stu-id="1811a-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="1811a-199">jQuery 在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="1811a-200">以下版本的 jQuery 托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="1811a-201">jQuery 版本 3.5.0</span><span class="sxs-lookup"><span data-stu-id="1811a-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="1811a-202">jQuery 版本 3.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="1811a-203">jQuery 版本 3.4.0</span><span class="sxs-lookup"><span data-stu-id="1811a-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="1811a-204">jQuery 版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="1811a-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="1811a-205">jQuery 版本 3.2.1</span><span class="sxs-lookup"><span data-stu-id="1811a-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="1811a-206">jQuery 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="1811a-207">jQuery 版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="1811a-208">jQuery 版本 3.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="1811a-209">jQuery 版本 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="1811a-210">jQuery 版本 2.2.4</span><span class="sxs-lookup"><span data-stu-id="1811a-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="1811a-211">jQuery 版本 2.2.3</span><span class="sxs-lookup"><span data-stu-id="1811a-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="1811a-212">jQuery 版本 2.2.2</span><span class="sxs-lookup"><span data-stu-id="1811a-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="1811a-213">jQuery 版本 2.2.1</span><span class="sxs-lookup"><span data-stu-id="1811a-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="1811a-214">jQuery 版本 2.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="1811a-215">jQuery 版本 2.1.4</span><span class="sxs-lookup"><span data-stu-id="1811a-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="1811a-216">jQuery 版本 2.1.3</span><span class="sxs-lookup"><span data-stu-id="1811a-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="1811a-217">jQuery 版本 2.1.2</span><span class="sxs-lookup"><span data-stu-id="1811a-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="1811a-218">jQuery 版本 2.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="1811a-219">jQuery 版本 2.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="1811a-220">jQuery 版本 2.0.3</span><span class="sxs-lookup"><span data-stu-id="1811a-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="1811a-221">jQuery 版本 2.0.2</span><span class="sxs-lookup"><span data-stu-id="1811a-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="1811a-222">jQuery 版本 2.0.1</span><span class="sxs-lookup"><span data-stu-id="1811a-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="1811a-223">jQuery 版本 2.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="1811a-224">jQuery 版本 1.12.4</span><span class="sxs-lookup"><span data-stu-id="1811a-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="1811a-225">jQuery 版本 1.12.3</span><span class="sxs-lookup"><span data-stu-id="1811a-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="1811a-226">jQuery 版本 1.12.2</span><span class="sxs-lookup"><span data-stu-id="1811a-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="1811a-227">jQuery 版本 1.12.1</span><span class="sxs-lookup"><span data-stu-id="1811a-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="1811a-228">jQuery 版本 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1811a-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="1811a-229">jQuery 版本 1.11.3</span><span class="sxs-lookup"><span data-stu-id="1811a-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="1811a-230">jQuery 版本 1.11.2</span><span class="sxs-lookup"><span data-stu-id="1811a-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="1811a-231">jQuery 版本 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1811a-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="1811a-232">jQuery 版本 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1811a-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="1811a-233">jQuery 版本 1.10.2</span><span class="sxs-lookup"><span data-stu-id="1811a-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="1811a-234">jQuery 版本 1.10.1</span><span class="sxs-lookup"><span data-stu-id="1811a-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="1811a-235">jQuery 版本 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1811a-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="1811a-236">jQuery 版本 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1811a-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="1811a-237">jQuery 版本 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1811a-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="1811a-238">jQuery 版本 1.8.3</span><span class="sxs-lookup"><span data-stu-id="1811a-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="1811a-239">jQuery 版本 1.8.2</span><span class="sxs-lookup"><span data-stu-id="1811a-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="1811a-240">jQuery 版本 1.8.1</span><span class="sxs-lookup"><span data-stu-id="1811a-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="1811a-241">jQuery 版本 1.8.0</span><span class="sxs-lookup"><span data-stu-id="1811a-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="1811a-242">jQuery 版本 1.7.2</span><span class="sxs-lookup"><span data-stu-id="1811a-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="1811a-243">jQuery 版本 1.7.1</span><span class="sxs-lookup"><span data-stu-id="1811a-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="1811a-244">jQuery 版本 1.7</span><span class="sxs-lookup"><span data-stu-id="1811a-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="1811a-245">jQuery 版本 1.6.4</span><span class="sxs-lookup"><span data-stu-id="1811a-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="1811a-246">jQuery 版本 1.6.3</span><span class="sxs-lookup"><span data-stu-id="1811a-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="1811a-247">jQuery 版本 1.6.2</span><span class="sxs-lookup"><span data-stu-id="1811a-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="1811a-248">jQuery 版本 1.6.1</span><span class="sxs-lookup"><span data-stu-id="1811a-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="1811a-249">jQuery 版本 1.6</span><span class="sxs-lookup"><span data-stu-id="1811a-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="1811a-250">jQuery 版本 1.5.2</span><span class="sxs-lookup"><span data-stu-id="1811a-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="1811a-251">jQuery 版本 1.5.1</span><span class="sxs-lookup"><span data-stu-id="1811a-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="1811a-252">jQuery 版本 1.5</span><span class="sxs-lookup"><span data-stu-id="1811a-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="1811a-253">jQuery 版本 1.4.4</span><span class="sxs-lookup"><span data-stu-id="1811a-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="1811a-254">jQuery 版本 1.4.3</span><span class="sxs-lookup"><span data-stu-id="1811a-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="1811a-255">jQuery 版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="1811a-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="1811a-256">jQuery 版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="1811a-257">jQuery 版本 1.4</span><span class="sxs-lookup"><span data-stu-id="1811a-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="1811a-258">jQuery 版本 1.3.2</span><span class="sxs-lookup"><span data-stu-id="1811a-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="1811a-259">jQuery 迁移 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="1811a-260">以下版本的 jQuery 迁移托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="1811a-261">jQuery 迁移版本 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="1811a-262">jQuery 迁移版本 1.2.1</span><span class="sxs-lookup"><span data-stu-id="1811a-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="1811a-263">jQuery 迁移版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="1811a-264">jQuery 迁移版本 1.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="1811a-265">jQuery 迁移版本 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="1811a-266">jQuery 迁移版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="1811a-267">jQuery 在 CDN 上的 UI 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="1811a-268">以下版本的 jQuery UI 库将托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="1811a-269">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-270">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="1811a-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN 的 jQuery UI 1.12.1")
- [<span data-ttu-id="1811a-271">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1811a-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN 的 jQuery UI 1.12.0")
- [<span data-ttu-id="1811a-272">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="1811a-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN 的 jQuery UI 1.11.4")
- [<span data-ttu-id="1811a-273">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="1811a-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN 的 jQuery UI 1.11.3")
- [<span data-ttu-id="1811a-274">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="1811a-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN 的 jQuery UI 1.11.2")
- [<span data-ttu-id="1811a-275">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1811a-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN 的 jQuery UI 1.11.1")
- [<span data-ttu-id="1811a-276">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1811a-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN 的 jQuery UI 1.11.0")
- [<span data-ttu-id="1811a-277">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="1811a-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN 的 jQuery UI 1.10.4")
- [<span data-ttu-id="1811a-278">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="1811a-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN 的 jQuery UI 1.10.3")
- [<span data-ttu-id="1811a-279">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="1811a-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN 的 jQuery UI 1.10.2")
- [<span data-ttu-id="1811a-280">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="1811a-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN 的 jQuery UI 1.10.1")
- [<span data-ttu-id="1811a-281">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1811a-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN 的 jQuery UI 1.10.0")
- [<span data-ttu-id="1811a-282">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="1811a-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN 的 jQuery UI 1.9.2")
- [<span data-ttu-id="1811a-283">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1811a-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN 的 jQuery UI 1.9.1")
- [<span data-ttu-id="1811a-284">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1811a-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN 的 jQuery UI 1.9.0")
- [<span data-ttu-id="1811a-285">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="1811a-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN 的 jQuery UI 1.8.24")
- [<span data-ttu-id="1811a-286">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="1811a-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN 的 jQuery UI 1.8.23")
- [<span data-ttu-id="1811a-287">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="1811a-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN 的 jQuery UI 1.8.22")
- [<span data-ttu-id="1811a-288">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="1811a-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN 的 jQuery UI 1.8.21")
- [<span data-ttu-id="1811a-289">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="1811a-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN 的 jQuery UI 1.8.20")
- [<span data-ttu-id="1811a-290">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="1811a-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN 的 jQuery UI 1.8.19")
- [<span data-ttu-id="1811a-291">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="1811a-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN 的 jQuery UI 1.8.18")
- [<span data-ttu-id="1811a-292">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="1811a-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN 的 jQuery UI 1.8.17")
- [<span data-ttu-id="1811a-293">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="1811a-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN 的 jQuery UI 1.8.16")
- [<span data-ttu-id="1811a-294">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="1811a-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN 的 jQuery UI 1.8.15")
- [<span data-ttu-id="1811a-295">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="1811a-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN 的 jQuery UI 1.8.14")
- [<span data-ttu-id="1811a-296">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="1811a-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN 的 jQuery UI 1.8.13")
- [<span data-ttu-id="1811a-297">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="1811a-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN 的 jQuery UI 1.8.12")
- [<span data-ttu-id="1811a-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="1811a-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN 的 jQuery UI 1.8.11")
- [<span data-ttu-id="1811a-299">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="1811a-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 的 jQuery UI 1.8.10")
- [<span data-ttu-id="1811a-300">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="1811a-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN 的 jQuery UI 1.8.9")
- [<span data-ttu-id="1811a-301">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="1811a-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN 的 jQuery UI 1.8.8")
- [<span data-ttu-id="1811a-302">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="1811a-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN 的 jQuery UI 1.8.7")
- [<span data-ttu-id="1811a-303">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="1811a-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN 的 jQuery UI 1.8.6")
- [<span data-ttu-id="1811a-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="1811a-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="1811a-305">j查询 CDN 上的验证版本</span><span class="sxs-lookup"><span data-stu-id="1811a-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="1811a-306">以下版本的[jQuery 验证](https://jqueryvalidation.org/ "jQuery验证插件")插件托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="1811a-307">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-308">jQuery 验证 1.19.1</span><span class="sxs-lookup"><span data-stu-id="1811a-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery 验证 1.19.1")
- [<span data-ttu-id="1811a-309">jQuery 验证 1.19.0</span><span class="sxs-lookup"><span data-stu-id="1811a-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery 验证 1.19.0")
- [<span data-ttu-id="1811a-310">jQuery 验证 1.17.0</span><span class="sxs-lookup"><span data-stu-id="1811a-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "j查询验证 1.17.0")
- [<span data-ttu-id="1811a-311">jQuery 验证 1.16.0</span><span class="sxs-lookup"><span data-stu-id="1811a-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 验证 1.16.0")
- [<span data-ttu-id="1811a-312">jQuery 验证 1.15.1</span><span class="sxs-lookup"><span data-stu-id="1811a-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 验证 1.15.1")
- [<span data-ttu-id="1811a-313">jQuery 验证 1.15.0</span><span class="sxs-lookup"><span data-stu-id="1811a-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 验证 1.15.0")
- [<span data-ttu-id="1811a-314">jQuery 验证 1.14.0</span><span class="sxs-lookup"><span data-stu-id="1811a-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 验证 1.14.0")
- [<span data-ttu-id="1811a-315">jQuery 验证 1.13.1</span><span class="sxs-lookup"><span data-stu-id="1811a-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 验证 1.13.1")
- [<span data-ttu-id="1811a-316">jQuery 验证 1.13.0</span><span class="sxs-lookup"><span data-stu-id="1811a-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 验证 1.13.0")
- [<span data-ttu-id="1811a-317">jQuery 验证 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1811a-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 验证 1.12.0")
- [<span data-ttu-id="1811a-318">jQuery 验证 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1811a-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 验证 1.11.1")
- [<span data-ttu-id="1811a-319">jQuery 验证 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1811a-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 验证 1.11.0")
- [<span data-ttu-id="1811a-320">jQuery 验证 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1811a-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 验证 1.10.0")
- [<span data-ttu-id="1811a-321">jQuery 验证 1.9</span><span class="sxs-lookup"><span data-stu-id="1811a-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 版本 1.9")
- [<span data-ttu-id="1811a-322">jQuery 验证 1.8.1</span><span class="sxs-lookup"><span data-stu-id="1811a-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 版本 1.8.1")
- [<span data-ttu-id="1811a-323">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="1811a-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 版本 1.8")
- [<span data-ttu-id="1811a-324">jQuery 验证 1.7</span><span class="sxs-lookup"><span data-stu-id="1811a-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 版本 1.7")
- [<span data-ttu-id="1811a-325">jQuery 验证 1.6</span><span class="sxs-lookup"><span data-stu-id="1811a-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 验证 1.6")
- [<span data-ttu-id="1811a-326">jQuery 验证 1.5.5</span><span class="sxs-lookup"><span data-stu-id="1811a-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 验证 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="1811a-327">jQuery CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="1811a-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="1811a-328">以下版本的 jQuery 移动库将托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="1811a-329">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-330">jQuery 移动 1.4.5</span><span class="sxs-lookup"><span data-stu-id="1811a-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.5")
- [<span data-ttu-id="1811a-331">jQuery 移动 1.4.2</span><span class="sxs-lookup"><span data-stu-id="1811a-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.2")
- [<span data-ttu-id="1811a-332">jQuery 移动 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.1")
- [<span data-ttu-id="1811a-333">jQuery 移动 1.4.0</span><span class="sxs-lookup"><span data-stu-id="1811a-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.0")
- [<span data-ttu-id="1811a-334">jQuery 移动 1.3.2</span><span class="sxs-lookup"><span data-stu-id="1811a-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.2")
- [<span data-ttu-id="1811a-335">jQuery 移动 1.3.1</span><span class="sxs-lookup"><span data-stu-id="1811a-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.1")
- [<span data-ttu-id="1811a-336">jQuery 移动 1.3.0</span><span class="sxs-lookup"><span data-stu-id="1811a-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.0")
- [<span data-ttu-id="1811a-337">jQuery 移动 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN 的 jQuery Mobile 1.2.0")
- [<span data-ttu-id="1811a-338">jQuery 移动 1.1.2</span><span class="sxs-lookup"><span data-stu-id="1811a-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.2")
- [<span data-ttu-id="1811a-339">jQuery 移动 1.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.1")
- [<span data-ttu-id="1811a-340">jQuery 移动 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.0")
- [<span data-ttu-id="1811a-341">jQuery 移动 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="1811a-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="1811a-342">jQuery 移动 1.0.1</span><span class="sxs-lookup"><span data-stu-id="1811a-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0.1")
- [<span data-ttu-id="1811a-343">jQuery 移动 1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0")
- [<span data-ttu-id="1811a-344">jQuery 移动 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="1811a-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="1811a-345">jQuery 移动 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="1811a-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="1811a-346">jQuery 移动 1.0 测试版 3</span><span class="sxs-lookup"><span data-stu-id="1811a-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="1811a-347">jQuery 模板在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="1811a-348">以下版本的 jQuery 模板插件托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="1811a-349">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-350">jQuery 模板 Beta 1</span><span class="sxs-lookup"><span data-stu-id="1811a-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 模板 Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="1811a-351">jQuery 周期版本在 CDN 上</span><span class="sxs-lookup"><span data-stu-id="1811a-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="1811a-352">以下版本的 jQuery 循环插件托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="1811a-353">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-354">j查询周期 2.99</span><span class="sxs-lookup"><span data-stu-id="1811a-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="1811a-355">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="1811a-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="1811a-356">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="1811a-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="1811a-357">j查询数据表在 CDN 上的发布</span><span class="sxs-lookup"><span data-stu-id="1811a-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="1811a-358">以下版本的 jQuery DataTables 插件托管在此 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="1811a-359">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="1811a-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="1811a-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="1811a-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="1811a-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="1811a-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="1811a-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="1811a-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="1811a-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="1811a-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="1811a-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1811a-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="1811a-366">j查询数据表 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1811a-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="1811a-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="1811a-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="1811a-368">CDN 上的现代版本</span><span class="sxs-lookup"><span data-stu-id="1811a-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="1811a-369">[Modernizr](http://www.modernizr.com "现代")的以下版本托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="1811a-370">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="1811a-371">以下版本的[JSHint](http://www.jshint.com "JSHint")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="1811a-372">CDN 上的挖空版本</span><span class="sxs-lookup"><span data-stu-id="1811a-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="1811a-373">以下版本的[挖空](http://www.knockoutjs.com "淘汰赛")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="1811a-374">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="1811a-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="1811a-375">[以下版本的全球化](https://github.com/jquery/globalize "全球化")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="1811a-376">全球化版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="1811a-377">全球化版本 0.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="1811a-378">所有文化</span><span class="sxs-lookup"><span data-stu-id="1811a-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="1811a-379">将"[文化代码]"替换为所需的区域性代码，例如全球化.culture.en-GB.js_ CDN 上的 Microsoft 文件\*这些库是由 Microsoft 上载的。</span><span class="sxs-lookup"><span data-stu-id="1811a-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="1811a-380">CDN 上的响应版本</span><span class="sxs-lookup"><span data-stu-id="1811a-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="1811a-381">以下版本的[响应](https://github.com/scottjehl/Respond "响应")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="1811a-382">响应版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="1811a-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="1811a-383">响应版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="1811a-384">响应版本 1.4.0</span><span class="sxs-lookup"><span data-stu-id="1811a-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="1811a-385">响应版本 1.3.0</span><span class="sxs-lookup"><span data-stu-id="1811a-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="1811a-386">响应版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="1811a-387">CDN 上的引导版本</span><span class="sxs-lookup"><span data-stu-id="1811a-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="1811a-388">CDN 上托管了以下[getbootstrap.com](http://getbootstrap.com "getbootstrap.com")引导版本：</span><span class="sxs-lookup"><span data-stu-id="1811a-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="1811a-389">引导版本 4.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-389">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="1811a-390">引导版本 4.3.1</span><span class="sxs-lookup"><span data-stu-id="1811a-390">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="1811a-391">引导版本 4.2.1</span><span class="sxs-lookup"><span data-stu-id="1811a-391">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="1811a-392">引导版本 4.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-392">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="1811a-393">引导版本 4.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-393">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="1811a-394">引导版本 3.4.1</span><span class="sxs-lookup"><span data-stu-id="1811a-394">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="1811a-395">引导版本 3.4.0</span><span class="sxs-lookup"><span data-stu-id="1811a-395">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="1811a-396">引导版本 3.3.7</span><span class="sxs-lookup"><span data-stu-id="1811a-396">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="1811a-397">引导版本 3.3.6</span><span class="sxs-lookup"><span data-stu-id="1811a-397">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="1811a-398">引导版本 3.3.5</span><span class="sxs-lookup"><span data-stu-id="1811a-398">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="1811a-399">引导版本 3.3.4</span><span class="sxs-lookup"><span data-stu-id="1811a-399">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="1811a-400">引导版本 3.3.2</span><span class="sxs-lookup"><span data-stu-id="1811a-400">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="1811a-401">引导版本 3.3.1</span><span class="sxs-lookup"><span data-stu-id="1811a-401">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="1811a-402">引导版本 3.3.0</span><span class="sxs-lookup"><span data-stu-id="1811a-402">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="1811a-403">引导版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-403">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="1811a-404">引导版本 3.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-404">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="1811a-405">引导版本 3.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-405">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="1811a-406">引导版本 3.0.3</span><span class="sxs-lookup"><span data-stu-id="1811a-406">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="1811a-407">引导版本 3.0.2</span><span class="sxs-lookup"><span data-stu-id="1811a-407">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="1811a-408">引导版本 3.0.1</span><span class="sxs-lookup"><span data-stu-id="1811a-408">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="1811a-409">引导版本 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-409">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="1811a-410">引导版本 2.3.2</span><span class="sxs-lookup"><span data-stu-id="1811a-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="1811a-411">引导版本 2.3.1</span><span class="sxs-lookup"><span data-stu-id="1811a-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="1811a-412">CDN 上的引导触摸卡盘释放</span><span class="sxs-lookup"><span data-stu-id="1811a-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="1811a-413">以下版本的[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel")引导式触摸卡马塞尔版本托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="1811a-414">靴子触摸卡马塞尔版本 0.8.0</span><span class="sxs-lookup"><span data-stu-id="1811a-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="1811a-415">Hammer.js 在 CDN 上发布</span><span class="sxs-lookup"><span data-stu-id="1811a-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="1811a-416">[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js 版本的以下版本托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="1811a-417">Hammer.js 版本 2.0.4</span><span class="sxs-lookup"><span data-stu-id="1811a-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="1811a-418">ASP.NET在 CDN 上的 Web 窗体和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="1811a-419">以下版本的ASP.NETAjax库托管在 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="1811a-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="1811a-420">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1811a-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1811a-421">ASP.NET Web 窗体和 Ajax 版本 4.5.2</span><span class="sxs-lookup"><span data-stu-id="1811a-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web 窗体和 Ajax 4.5.2")
- [<span data-ttu-id="1811a-422">ASP.NET Web 窗体和 Ajax 版本 4</span><span class="sxs-lookup"><span data-stu-id="1811a-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web 窗体和 Ajax 4")
- [<span data-ttu-id="1811a-423">ASP.NET Ajax 版本 3.5</span><span class="sxs-lookup"><span data-stu-id="1811a-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="1811a-424">cdN 上的ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="1811a-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="1811a-425">以下ASP.NET MVC JavaScript 文件托管在此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="1811a-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="1811a-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="1811a-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="1811a-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="1811a-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="1811a-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="1811a-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="1811a-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="1811a-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="1811a-430">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="1811a-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="1811a-432">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="1811a-433">ASP.NET信号R在 CDN 上的释放</span><span class="sxs-lookup"><span data-stu-id="1811a-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="1811a-434">以下ASP.NET SignalR JavaScript 文件托管在此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1811a-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="1811a-435">ASP.NET信号R 2.2.2</span><span class="sxs-lookup"><span data-stu-id="1811a-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="1811a-436">ASP.NET信号R 2.2.1</span><span class="sxs-lookup"><span data-stu-id="1811a-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="1811a-437">ASP.NET信号R 2.2.0</span><span class="sxs-lookup"><span data-stu-id="1811a-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="1811a-438">ASP.NET信号R 2.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="1811a-439">ASP.NET信号R 2.0.3</span><span class="sxs-lookup"><span data-stu-id="1811a-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="1811a-440">ASP.NET信号R 2.0.2</span><span class="sxs-lookup"><span data-stu-id="1811a-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="1811a-441">ASP.NET信号R 2.0.1</span><span class="sxs-lookup"><span data-stu-id="1811a-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="1811a-442">ASP.NET信号R 2.0.0</span><span class="sxs-lookup"><span data-stu-id="1811a-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="1811a-443">ASP.NET信号R 1.1.3</span><span class="sxs-lookup"><span data-stu-id="1811a-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="1811a-444">ASP.NET信号R 1.1.2</span><span class="sxs-lookup"><span data-stu-id="1811a-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="1811a-445">ASP.NET信号R 1.1.1</span><span class="sxs-lookup"><span data-stu-id="1811a-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="1811a-446">ASP.NET信号R 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1811a-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="1811a-447">ASP.NET信号R 1.0.1</span><span class="sxs-lookup"><span data-stu-id="1811a-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="1811a-448">有关 CDN 的使用条款的信息，请参阅 Microsoft [Ajax CDN 使用条款](https://www.asp.net/terms-of-use "微软Ajax CDN的使用条款")。</span><span class="sxs-lookup"><span data-stu-id="1811a-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>

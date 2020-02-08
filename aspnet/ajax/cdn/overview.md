---
uid: ajax/cdn/overview
title: Microsoft Ajax 内容交付网络 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 228194a7b35e116cabae6d819e7a3a8060a3ef6a
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074912"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="22aa9-102">Microsoft Ajax 内容分发网络</span><span class="sxs-lookup"><span data-stu-id="22aa9-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="22aa9-103">生产应用程序不应对 CDN 资产进行硬依赖。</span><span class="sxs-lookup"><span data-stu-id="22aa9-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="22aa9-104">应用程序应测试所引用的 CDN 资产，并在 CDN 不可用时使用后备资产。</span><span class="sxs-lookup"><span data-stu-id="22aa9-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="22aa9-105">Microsoft Ajax CDN 不会使用 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="22aa9-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="22aa9-106">使用[此 GitHub 问题](https://github.com/aspnet/AspNetDocs/issues/116)可报告 MICROSOFT Ajax CDN 的问题。</span><span class="sxs-lookup"><span data-stu-id="22aa9-106">Use [this GitHub issue](https://github.com/aspnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="22aa9-107">目录</span><span class="sxs-lookup"><span data-stu-id="22aa9-107">Table of Contents</span></span>

<span data-ttu-id="22aa9-108">**[ajax.microsoft.com 重命名为 ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="22aa9-109">**[Visual Studio. vsdoc 支持](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="22aa9-110">**[使用 CDN 中的 ASP.NET Ajax](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="22aa9-111">**[从 CDN 使用 jQuery](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="22aa9-112">**[使用 CDN 的 jQuery UI](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="22aa9-113">**[CDN 上的第三方文件](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="22aa9-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="22aa9-114">CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="22aa9-115">在 CDN 上的 jQuery 迁移版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="22aa9-116">CDN 上的 jQuery UI 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="22aa9-117">CDN 上的 jQuery 验证版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="22aa9-118">CDN 上的 jQuery Mobile 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="22aa9-119">在 CDN 上发布 jQuery 模板</span><span class="sxs-lookup"><span data-stu-id="22aa9-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="22aa9-120">CDN 上的 jQuery 循环版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="22aa9-121">CDN 上的 jQuery 数据表版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="22aa9-122">CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="22aa9-123">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="22aa9-124">CDN 上的挖空版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="22aa9-125">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="22aa9-126">在 CDN 上响应发布</span><span class="sxs-lookup"><span data-stu-id="22aa9-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="22aa9-127">CDN 上的启动版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="22aa9-128">CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="22aa9-129">CDN 上的 Hammer 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="22aa9-130">CDN 上的 ASP.NET Web 窗体和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="22aa9-131">CDN 上的 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="22aa9-132">CDN 上的 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="22aa9-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="22aa9-133">Microsoft Ajax 内容交付网络（CDN）承载流行的第三方 JavaScript 库（如 jQuery），使你能够轻松地将它们添加到你的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="22aa9-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="22aa9-134">例如，你可以开始使用在此 CDN 上托管的 jQuery，只需将 &lt;脚本&gt; 标记添加到指向 ajax.aspnetcdn.com 的页面。</span><span class="sxs-lookup"><span data-stu-id="22aa9-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="22aa9-135">利用 CDN，可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="22aa9-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="22aa9-136">CDN 的内容缓存在位于世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="22aa9-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="22aa9-137">此外，CDN 还允许浏览器对位于不同域中的网站重用缓存的第三方 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="22aa9-138">如果需要使用安全套接字层为网页提供服务，CDN 支持 SSL （HTTPS）。</span><span class="sxs-lookup"><span data-stu-id="22aa9-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="22aa9-139">CDN 承载以下第三方脚本库，这些库已上传并由这些库的所有者授权给你：</span><span class="sxs-lookup"><span data-stu-id="22aa9-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="22aa9-140">jQuery （ www.jquery.com）</span><span class="sxs-lookup"><span data-stu-id="22aa9-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="22aa9-141">jQuery UI （ www.jqueryui.com）</span><span class="sxs-lookup"><span data-stu-id="22aa9-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="22aa9-142">jQuery Mobile （ www.jquerymobile.com）</span><span class="sxs-lookup"><span data-stu-id="22aa9-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="22aa9-143">jQuery 验证（ https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="22aa9-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="22aa9-144">jQuery 循环（ www.malsup.com/jquery/cycle/）</span><span class="sxs-lookup"><span data-stu-id="22aa9-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="22aa9-145">jQuery 数据表（ http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="22aa9-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="22aa9-146">Microsoft Ajax CDN 还包括以下库，这些库已由 Microsoft 上传：</span><span class="sxs-lookup"><span data-stu-id="22aa9-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="22aa9-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="22aa9-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="22aa9-148">ASP.NET MVC JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="22aa9-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="22aa9-149">ASP.NET SignalR JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="22aa9-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="22aa9-150">Microsoft 不会宣称此 CDN 上托管的任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="22aa9-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="22aa9-151">库的版权所有者将向你授权这些库。</span><span class="sxs-lookup"><span data-stu-id="22aa9-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="22aa9-152">你可能需要下载并使用此类库的任何权限仅由各自的版权所有者授予。</span><span class="sxs-lookup"><span data-stu-id="22aa9-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="22aa9-153">由于这些不是 Microsoft 库，Microsoft 不为此 CDN 上托管的第三方库提供任何担保或知识产权许可（包括无默示专利权限）。</span><span class="sxs-lookup"><span data-stu-id="22aa9-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="22aa9-154">如果你想要提交 JavaScript 库，并且你的库是顶级 JavaScript 库之一（如 http://trends.builtwith.com) 或扩展插件上列出的那些库（），或者（b）可用于 ASP.NET，请联系 AjaxCDNSubmission@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="22aa9-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="22aa9-155">ajax.microsoft.com 重命名为 ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="22aa9-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="22aa9-156">用于使用 microsoft.com 域名并且已更改为使用 aspnetcdn.com 域名的 CDN。</span><span class="sxs-lookup"><span data-stu-id="22aa9-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="22aa9-157">进行此更改是为了提高性能，因为当浏览器引用 microsoft.com 域时，它会在每个请求的网络中从该域发送任何 cookie。</span><span class="sxs-lookup"><span data-stu-id="22aa9-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="22aa9-158">通过重命名为 microsoft.com 以外的域名，可以将最多增加25%。</span><span class="sxs-lookup"><span data-stu-id="22aa9-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="22aa9-159">请注意，ajax.microsoft.com 将继续运行，但建议使用 ajax.aspnetcdn.com。</span><span class="sxs-lookup"><span data-stu-id="22aa9-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="22aa9-160">旧格式： https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="22aa9-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="22aa9-161">新格式： https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="22aa9-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="22aa9-162">Visual Studio. vsdoc 支持</span><span class="sxs-lookup"><span data-stu-id="22aa9-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="22aa9-163">若要在 Visual Studio 2008 中正确使用 vsdoc 文件，需要确保安装了 VS 2008 SP1 并安装了 vsdoc 文件的修补程序。</span><span class="sxs-lookup"><span data-stu-id="22aa9-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="22aa9-164">可从此处获取这些内容：</span><span class="sxs-lookup"><span data-stu-id="22aa9-164">You can get these from here:</span></span>

- [<span data-ttu-id="22aa9-165">下载 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="22aa9-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下载 Visual Studio 2008 SP1")
- [<span data-ttu-id="22aa9-166">适用于 Visual Studio 2008 SP1 的 vsdoc 修补程序</span><span class="sxs-lookup"><span data-stu-id="22aa9-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "适用于 Visual Studio 2008 SP1 的 vsdoc 修补程序")

<span data-ttu-id="22aa9-167">Visual Studio 2010 支持 vsdoc 文件，无需任何其他修补程序。</span><span class="sxs-lookup"><span data-stu-id="22aa9-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="22aa9-168">使用 CDN 中的 ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="22aa9-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="22aa9-169">使用 ASP.NET 4 时，可以将 ASP.NET framework 脚本的所有请求重定向到 CDN。</span><span class="sxs-lookup"><span data-stu-id="22aa9-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="22aa9-170">从 CDN 而不是本地 web 服务器检索脚本可以显著提高公共 ASP.NET 网站的性能。</span><span class="sxs-lookup"><span data-stu-id="22aa9-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="22aa9-171">使用 ScriptManager EnableCDN 属性将所有 ASP.NET framework 脚本请求重定向到 Microsoft Ajax CDN：</span><span class="sxs-lookup"><span data-stu-id="22aa9-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="22aa9-172">从 CDN 使用 jQuery</span><span class="sxs-lookup"><span data-stu-id="22aa9-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="22aa9-173">可以通过将以下 script 元素添加到页面中，在 Web 应用程序中使用在 CDN 上托管的 jQuery 脚本：</span><span class="sxs-lookup"><span data-stu-id="22aa9-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="22aa9-174">CDN 还包括 jQuery 脚本的缩小版本，可以使用以下元素获取该脚本：</span><span class="sxs-lookup"><span data-stu-id="22aa9-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="22aa9-175">若要使页面从你自己的网站上的本地路径中回退到加载 jQuery，而 CDN 不可用，请在引用 CDN 的元素后立即添加以下元素：</span><span class="sxs-lookup"><span data-stu-id="22aa9-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="22aa9-176">下面的示例页使用 jQuery 库的 CDN 版本（回退到本地副本）在单击按钮时显示 div 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="22aa9-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="22aa9-177">可以通过访问[jquery](http://jquery.com/)网站来了解有关 jquery 的详细信息并下载 jquery 的本地副本。</span><span class="sxs-lookup"><span data-stu-id="22aa9-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="22aa9-178">使用 CDN 的 jQuery UI</span><span class="sxs-lookup"><span data-stu-id="22aa9-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="22aa9-179">CDN 还承载 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="22aa9-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="22aa9-180">JQuery UI 库包括一组丰富的小组件和效果，可在 ASP.NET 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="22aa9-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="22aa9-181">例如，以下页面说明了如何在 ASP.NET Web 窗体应用程序的上下文中使用 jQuery UI Datepicker 来显示弹出日历：</span><span class="sxs-lookup"><span data-stu-id="22aa9-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="22aa9-182">使用键盘将焦点移到文本框中时，将显示一个日历：</span><span class="sxs-lookup"><span data-stu-id="22aa9-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![用 Datepicker 创建的弹出日历](overview/_static/image1.png)

<span data-ttu-id="22aa9-184">请注意，在上面的代码中，必须包含 CDN 中的三个文件：</span><span class="sxs-lookup"><span data-stu-id="22aa9-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="22aa9-185">Jquery library &mdash; jquery UI 库依赖于 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="22aa9-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="22aa9-186">添加 jQuery UI 库之前，必须先将 jQuery library 添加到页面。</span><span class="sxs-lookup"><span data-stu-id="22aa9-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="22aa9-187">Jquery ui 库 &mdash; jQuery ui library 包含所有 jQuery UI 效果和小组件，例如上一页中使用的 Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="22aa9-188">Jquery ui 主题 &mdash; jQuery UI 支持不同的主题。</span><span class="sxs-lookup"><span data-stu-id="22aa9-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="22aa9-189">上述页面包含指向用于导入 Redmond 主题的 CSS 文件的链接。</span><span class="sxs-lookup"><span data-stu-id="22aa9-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="22aa9-190">所有标准 jQuery UI 主题都在 CDN 上托管。</span><span class="sxs-lookup"><span data-stu-id="22aa9-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="22aa9-191">[访问此页](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 的 jQuery UI 1.8.10")可查看每个主题的缩略图。</span><span class="sxs-lookup"><span data-stu-id="22aa9-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="22aa9-192">若要了解有关 jQuery UI 库的详细信息，请访问官方[JQUERY ui 网站](http://jQueryUI.com "jQuery UI 网站")。</span><span class="sxs-lookup"><span data-stu-id="22aa9-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="22aa9-193">CDN 上的第三方文件</span><span class="sxs-lookup"><span data-stu-id="22aa9-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="22aa9-194">CDN 承载一些最常用的第三方 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="22aa9-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="22aa9-195">Microsoft 不会宣称此 CDN 上托管的任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="22aa9-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="22aa9-196">库的版权所有者将向你授权这些库。</span><span class="sxs-lookup"><span data-stu-id="22aa9-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="22aa9-197">你可能需要下载并使用此类库的任何权限仅由各自的版权所有者授予。</span><span class="sxs-lookup"><span data-stu-id="22aa9-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="22aa9-198">由于这些不是 Microsoft 库，Microsoft 不为此 CDN 上托管的第三方库提供任何担保或知识产权许可（包括无默示专利权限）。</span><span class="sxs-lookup"><span data-stu-id="22aa9-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="22aa9-199">CDN 上的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="22aa9-200">以下版本的 jQuery 在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-341"></a><span data-ttu-id="22aa9-201">jQuery 版本3.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-201">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="22aa9-202">jQuery 版本3.4。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-202">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="22aa9-203">jQuery 版本3.3。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-203">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="22aa9-204">jQuery 3.2.1 版</span><span class="sxs-lookup"><span data-stu-id="22aa9-204">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="22aa9-205">jQuery 版本3.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-205">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="22aa9-206">jQuery 版本3.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-206">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="22aa9-207">jQuery 版本3.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-207">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="22aa9-208">jQuery 版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-208">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="22aa9-209">jQuery 版本2.2。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-209">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="22aa9-210">jQuery 版本2.2。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-210">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="22aa9-211">jQuery 版本2.2。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-211">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="22aa9-212">jQuery 版本2.2。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-212">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="22aa9-213">jQuery 版本2.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-213">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="22aa9-214">jQuery 版本2.1。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-214">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="22aa9-215">jQuery 版本2.1。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-215">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="22aa9-216">jQuery 版本2.1。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-216">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="22aa9-217">jQuery 版本2.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-217">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="22aa9-218">jQuery 版本2.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-218">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="22aa9-219">jQuery 版本2.0。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-219">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="22aa9-220">jQuery 版本2.0。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-220">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="22aa9-221">jQuery 版本2.0。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-221">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="22aa9-222">jQuery 版本2.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-222">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="22aa9-223">jQuery 版本1.12。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-223">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="22aa9-224">jQuery 版本1.12。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-224">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="22aa9-225">jQuery 版本1.12。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-225">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="22aa9-226">jQuery 版本1.12。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-226">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="22aa9-227">jQuery 版本1.12。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-227">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="22aa9-228">jQuery 版本1.11。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-228">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="22aa9-229">jQuery 版本1.11。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-229">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="22aa9-230">jQuery 版本1.11。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-230">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="22aa9-231">jQuery 版本1.11。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-231">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="22aa9-232">jQuery 版本1.10。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-232">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="22aa9-233">jQuery 版本1.10。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-233">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="22aa9-234">jQuery 版本1.10。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-234">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="22aa9-235">jQuery 版本1.9。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-235">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="22aa9-236">jQuery 版本1.9。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-236">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="22aa9-237">jQuery 版本1.8。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-237">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="22aa9-238">jQuery 版本1.8。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-238">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="22aa9-239">jQuery 版本1.8。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-239">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="22aa9-240">jQuery 版本1.8。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-240">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="22aa9-241">jQuery 版本1.7。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-241">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="22aa9-242">jQuery 版本1.7。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-242">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="22aa9-243">jQuery 版本1。7</span><span class="sxs-lookup"><span data-stu-id="22aa9-243">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="22aa9-244">jQuery 版本1.6。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-244">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="22aa9-245">jQuery 版本1.6。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-245">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="22aa9-246">jQuery 版本1.6。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-246">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="22aa9-247">jQuery 版本1.6。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-247">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="22aa9-248">jQuery 版本1。6</span><span class="sxs-lookup"><span data-stu-id="22aa9-248">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="22aa9-249">jQuery 版本1.5。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-249">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="22aa9-250">jQuery 版本1.5。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-250">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="22aa9-251">jQuery 版本1。5</span><span class="sxs-lookup"><span data-stu-id="22aa9-251">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="22aa9-252">jQuery 版本 sqoop-user-guide-1.4。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-252">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="22aa9-253">jQuery 版本1.4。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-253">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="22aa9-254">jQuery 版本1.4。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-254">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="22aa9-255">jQuery 版本1.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-255">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="22aa9-256">jQuery 版本1。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-256">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="22aa9-257">jQuery 版本1.3。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-257">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="22aa9-258">在 CDN 上的 jQuery 迁移版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-258">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="22aa9-259">以下版本的 jQuery 迁移在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-259">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="22aa9-260">jQuery 迁移版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-260">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="22aa9-261">jQuery 迁移版本1.2。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-261">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="22aa9-262">jQuery 迁移版本1.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-262">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="22aa9-263">jQuery 迁移版本1.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-263">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="22aa9-264">jQuery 迁移版本1.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-264">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="22aa9-265">jQuery 迁移版本1.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-265">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="22aa9-266">CDN 上的 jQuery UI 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-266">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="22aa9-267">此 CDN 上承载了下面的 jQuery UI 库版本。</span><span class="sxs-lookup"><span data-stu-id="22aa9-267">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-268">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-268">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-269">jQuery UI 1.12。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-269">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN 的 jQuery UI 1.12.1")
- [<span data-ttu-id="22aa9-270">jQuery UI 1.12。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-270">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN 的 jQuery UI 1.12.0")
- [<span data-ttu-id="22aa9-271">jQuery UI 1.11。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-271">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN 的 jQuery UI 1.11.4")
- [<span data-ttu-id="22aa9-272">jQuery UI 1.11。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-272">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN 的 jQuery UI 1.11.3")
- [<span data-ttu-id="22aa9-273">jQuery UI 1.11。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-273">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN 的 jQuery UI 1.11.2")
- [<span data-ttu-id="22aa9-274">jQuery UI 1.11。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-274">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN 的 jQuery UI 1.11.1")
- [<span data-ttu-id="22aa9-275">jQuery UI 1.11。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-275">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN 的 jQuery UI 1.11.0")
- [<span data-ttu-id="22aa9-276">jQuery UI 1.10。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-276">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN 的 jQuery UI 1.10.4")
- [<span data-ttu-id="22aa9-277">jQuery UI 1.10。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-277">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN 的 jQuery UI 1.10.3")
- [<span data-ttu-id="22aa9-278">jQuery UI 1.10。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-278">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN 的 jQuery UI 1.10.2")
- [<span data-ttu-id="22aa9-279">jQuery UI 1.10。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-279">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN 的 jQuery UI 1.10.1")
- [<span data-ttu-id="22aa9-280">jQuery UI 1.10。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-280">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN 的 jQuery UI 1.10.0")
- [<span data-ttu-id="22aa9-281">jQuery UI 1.9。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-281">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN 的 jQuery UI 1.9.2")
- [<span data-ttu-id="22aa9-282">jQuery UI 1.9。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-282">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN 的 jQuery UI 1.9.1")
- [<span data-ttu-id="22aa9-283">jQuery UI 1.9。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-283">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN 的 jQuery UI 1.9.0")
- [<span data-ttu-id="22aa9-284">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="22aa9-284">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN 的 jQuery UI 1.8.24")
- [<span data-ttu-id="22aa9-285">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="22aa9-285">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN 的 jQuery UI 1.8.23")
- [<span data-ttu-id="22aa9-286">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="22aa9-286">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN 的 jQuery UI 1.8.22")
- [<span data-ttu-id="22aa9-287">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="22aa9-287">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN 的 jQuery UI 1.8.21")
- [<span data-ttu-id="22aa9-288">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="22aa9-288">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN 的 jQuery UI 1.8.20")
- [<span data-ttu-id="22aa9-289">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="22aa9-289">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN 的 jQuery UI 1.8.19")
- [<span data-ttu-id="22aa9-290">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="22aa9-290">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN 的 jQuery UI 1.8.18")
- [<span data-ttu-id="22aa9-291">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="22aa9-291">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN 的 jQuery UI 1.8.17")
- [<span data-ttu-id="22aa9-292">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="22aa9-292">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN 的 jQuery UI 1.8.16")
- [<span data-ttu-id="22aa9-293">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="22aa9-293">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN 的 jQuery UI 1.8.15")
- [<span data-ttu-id="22aa9-294">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="22aa9-294">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN 的 jQuery UI 1.8.14")
- [<span data-ttu-id="22aa9-295">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="22aa9-295">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN 的 jQuery UI 1.8.13")
- [<span data-ttu-id="22aa9-296">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="22aa9-296">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN 的 jQuery UI 1.8.12")
- [<span data-ttu-id="22aa9-297">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="22aa9-297">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN 的 jQuery UI 1.8.11")
- [<span data-ttu-id="22aa9-298">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="22aa9-298">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN 的 jQuery UI 1.8.10")
- [<span data-ttu-id="22aa9-299">jQuery UI 1.8。9</span><span class="sxs-lookup"><span data-stu-id="22aa9-299">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN 的 jQuery UI 1.8.9")
- [<span data-ttu-id="22aa9-300">jQuery UI 1.8。8</span><span class="sxs-lookup"><span data-stu-id="22aa9-300">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN 的 jQuery UI 1.8.8")
- [<span data-ttu-id="22aa9-301">jQuery UI 1.8。7</span><span class="sxs-lookup"><span data-stu-id="22aa9-301">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN 的 jQuery UI 1.8.7")
- [<span data-ttu-id="22aa9-302">jQuery UI 1.8。6</span><span class="sxs-lookup"><span data-stu-id="22aa9-302">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN 的 jQuery UI 1.8.6")
- [<span data-ttu-id="22aa9-303">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="22aa9-303">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="22aa9-304">CDN 上的 jQuery 验证版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-304">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="22aa9-305">此 CDN 上承载了以下版本的[JQuery 验证](https://jqueryvalidation.org/ "jQuery 验证插件")插件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-305">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-306">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-306">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-307">jQuery 验证1.19。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-307">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery 验证1.19。1")
- [<span data-ttu-id="22aa9-308">jQuery 验证1.19。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-308">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery 验证1.19。0")
- [<span data-ttu-id="22aa9-309">jQuery 验证1.17。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-309">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 验证1.17。0")
- [<span data-ttu-id="22aa9-310">jQuery 验证1.16。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-310">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 验证 1.16.0")
- [<span data-ttu-id="22aa9-311">jQuery 验证 busybox-1.15.1-20.el6.x86</span><span class="sxs-lookup"><span data-stu-id="22aa9-311">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 验证 1.15.1")
- [<span data-ttu-id="22aa9-312">jQuery 验证1.15。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-312">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 验证 1.15.0")
- [<span data-ttu-id="22aa9-313">jQuery 验证1.14。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-313">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 验证 1.14.0")
- [<span data-ttu-id="22aa9-314">jQuery 验证1.13。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-314">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 验证 1.13.1")
- [<span data-ttu-id="22aa9-315">jQuery 验证1.13。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-315">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 验证 1.13.0")
- [<span data-ttu-id="22aa9-316">jQuery 验证1.12。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-316">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 验证 1.12.0")
- [<span data-ttu-id="22aa9-317">jQuery 验证1.11。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-317">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 验证 1.11.1")
- [<span data-ttu-id="22aa9-318">jQuery 验证1.11。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-318">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 验证 1.11.0")
- [<span data-ttu-id="22aa9-319">jQuery 验证1.10。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-319">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 验证 1.10.0")
- [<span data-ttu-id="22aa9-320">jQuery 验证1。9</span><span class="sxs-lookup"><span data-stu-id="22aa9-320">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 版本 1.9")
- [<span data-ttu-id="22aa9-321">jQuery 验证1.8。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-321">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 版本 1.8.1")
- [<span data-ttu-id="22aa9-322">jQuery 验证1。8</span><span class="sxs-lookup"><span data-stu-id="22aa9-322">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 版本 1.8")
- [<span data-ttu-id="22aa9-323">jQuery 验证1。7</span><span class="sxs-lookup"><span data-stu-id="22aa9-323">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 版本 1.7")
- [<span data-ttu-id="22aa9-324">jQuery 验证 1.6</span><span class="sxs-lookup"><span data-stu-id="22aa9-324">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 验证 1.6")
- [<span data-ttu-id="22aa9-325">jQuery 验证 1.5.5</span><span class="sxs-lookup"><span data-stu-id="22aa9-325">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 验证 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="22aa9-326">CDN 上的 jQuery Mobile 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-326">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="22aa9-327">此 CDN 上承载了下面的 jQuery Mobile 库版本。</span><span class="sxs-lookup"><span data-stu-id="22aa9-327">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-328">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-328">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-329">jQuery Mobile 1.4。5</span><span class="sxs-lookup"><span data-stu-id="22aa9-329">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.5")
- [<span data-ttu-id="22aa9-330">jQuery Mobile 1.4。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-330">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.2")
- [<span data-ttu-id="22aa9-331">jQuery Mobile 1.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-331">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.1")
- [<span data-ttu-id="22aa9-332">jQuery Mobile 1.4。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-332">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN 的 jQuery Mobile 1.4.0")
- [<span data-ttu-id="22aa9-333">jQuery Mobile 1.3。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-333">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.2")
- [<span data-ttu-id="22aa9-334">jQuery Mobile 1.3。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-334">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.1")
- [<span data-ttu-id="22aa9-335">jQuery Mobile 1.3。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-335">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN 的 jQuery Mobile 1.3.0")
- [<span data-ttu-id="22aa9-336">jQuery Mobile 1.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-336">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN 的 jQuery Mobile 1.2.0")
- [<span data-ttu-id="22aa9-337">jQuery Mobile 1.1。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-337">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.2")
- [<span data-ttu-id="22aa9-338">jQuery Mobile 1.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-338">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.1")
- [<span data-ttu-id="22aa9-339">jQuery Mobile 1.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-339">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.0")
- [<span data-ttu-id="22aa9-340">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="22aa9-340">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN 的 jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="22aa9-341">jQuery Mobile 1.0。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-341">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0.1")
- [<span data-ttu-id="22aa9-342">jQuery Mobile 1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-342">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0")
- [<span data-ttu-id="22aa9-343">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="22aa9-343">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="22aa9-344">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="22aa9-344">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="22aa9-345">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="22aa9-345">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="22aa9-346">在 CDN 上发布 jQuery 模板</span><span class="sxs-lookup"><span data-stu-id="22aa9-346">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="22aa9-347">此 CDN 上托管了以下版本的 jQuery 模板插件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-347">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-348">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-348">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-349">jQuery 模板 Beta 1</span><span class="sxs-lookup"><span data-stu-id="22aa9-349">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 模板 Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="22aa9-350">CDN 上的 jQuery 循环版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-350">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="22aa9-351">此 CDN 上承载了以下版本的 jQuery 循环插件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-351">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-352">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-352">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-353">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="22aa9-353">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="22aa9-354">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="22aa9-354">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="22aa9-355">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="22aa9-355">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="22aa9-356">CDN 上的 jQuery 数据表版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-356">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="22aa9-357">此 CDN 上承载了以下版本的 jQuery Datatable 插件。</span><span class="sxs-lookup"><span data-stu-id="22aa9-357">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="22aa9-358">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-358">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-359">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="22aa9-359">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="22aa9-360">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="22aa9-360">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="22aa9-361">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="22aa9-361">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="22aa9-362">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="22aa9-362">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="22aa9-363">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="22aa9-363">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="22aa9-364">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="22aa9-364">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="22aa9-365">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-365">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="22aa9-366">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="22aa9-366">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="22aa9-367">CDN 上的 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-367">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="22aa9-368">以下版本的[Modernizr](http://www.modernizr.com "Modernizr")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="22aa9-368">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="22aa9-369">CDN 上的 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-369">JSHint Releases on the CDN</span></span>

<span data-ttu-id="22aa9-370">以下版本的[JSHint](http://www.jshint.com "JSHint")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="22aa9-370">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="22aa9-371">CDN 上的挖空版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-371">Knockout Releases on the CDN</span></span>

<span data-ttu-id="22aa9-372">以下版本的[挖空](http://www.knockoutjs.com "拆装")在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-372">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="22aa9-373">CDN 上的全球化版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-373">Globalize Releases on the CDN</span></span>

<span data-ttu-id="22aa9-374">在 CDN 上托管以下版本的[全球](https://github.com/jquery/globalize "全球化")化：</span><span class="sxs-lookup"><span data-stu-id="22aa9-374">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="22aa9-375">全球化版本1.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-375">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="22aa9-376">全球化版本0.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-376">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="22aa9-377">所有区域性</span><span class="sxs-lookup"><span data-stu-id="22aa9-377">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="22aa9-378">使用所需的区域性代码（如 en-GB = = CDN）将 "{culture}" 替换为 CDN 上的 Microsoft 文件 = = 这些库已由 Microsoft 上传。</span><span class="sxs-lookup"><span data-stu-id="22aa9-378">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="22aa9-379">在 CDN 上响应发布</span><span class="sxs-lookup"><span data-stu-id="22aa9-379">Respond Releases on the CDN</span></span>

<span data-ttu-id="22aa9-380">以下版本的[响应](https://github.com/scottjehl/Respond "响应")在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-380">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="22aa9-381">响应版本1.4。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-381">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="22aa9-382">响应版本1.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-382">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="22aa9-383">响应版本1.4。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-383">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="22aa9-384">响应版本1.3。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-384">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="22aa9-385">响应版本1.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-385">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="22aa9-386">CDN 上的启动版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-386">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="22aa9-387">以下版本的[getbootstrap.com](http://getbootstrap.com "getbootstrap.com")启动在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-387">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="22aa9-388">启动版本4.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-388">Bootstrap version 4.4.1</span></span>

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

#### <a name="bootstrap-version-431"></a><span data-ttu-id="22aa9-389">启动版本4.3。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-389">Bootstrap version 4.3.1</span></span>

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

#### <a name="bootstrap-version-421"></a><span data-ttu-id="22aa9-390">启动版本4.2。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-390">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="22aa9-391">启动版本4.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-391">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="22aa9-392">启动版本4.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-392">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-341"></a><span data-ttu-id="22aa9-393">启动版本3.4。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-393">Bootstrap version 3.4.1</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="22aa9-394">启动版本3.4。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-394">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="22aa9-395">启动版本3.3。7</span><span class="sxs-lookup"><span data-stu-id="22aa9-395">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="22aa9-396">启动版本3.3。6</span><span class="sxs-lookup"><span data-stu-id="22aa9-396">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="22aa9-397">启动版本3.3。5</span><span class="sxs-lookup"><span data-stu-id="22aa9-397">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="22aa9-398">启动版本3.3。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-398">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="22aa9-399">启动版本3.3。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-399">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="22aa9-400">启动版本3.3。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-400">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="22aa9-401">启动版本3.3。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-401">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="22aa9-402">启动版本3.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-402">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="22aa9-403">启动版本3.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-403">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="22aa9-404">启动版本3.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-404">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="22aa9-405">启动版本3.0。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-405">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="22aa9-406">启动版本3.0。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-406">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="22aa9-407">启动版本3.0。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-407">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="22aa9-408">启动版本3.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-408">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="22aa9-409">启动版本2.3。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-409">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="22aa9-410">启动版本2.3。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-410">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="22aa9-411">CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-411">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="22aa9-412">以下版本的[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel")启动 TouchCarousel 版本托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="22aa9-412">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="22aa9-413">启动 TouchCarousel 版本0.8。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-413">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="22aa9-414">CDN 上的 Hammer 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-414">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="22aa9-415">以下版本的[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer 版本在 CDN 上托管：</span><span class="sxs-lookup"><span data-stu-id="22aa9-415">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="22aa9-416">Hammer 版本2.0。4</span><span class="sxs-lookup"><span data-stu-id="22aa9-416">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="22aa9-417">CDN 上的 ASP.NET Web 窗体和 Ajax 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-417">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="22aa9-418">以下版本的 ASP.NET Ajax 库托管在 CDN 上。</span><span class="sxs-lookup"><span data-stu-id="22aa9-418">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="22aa9-419">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="22aa9-419">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="22aa9-420">ASP.NET Web 窗体和 Ajax 版本4.5。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-420">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web 窗体和 Ajax 4.5.2")
- [<span data-ttu-id="22aa9-421">ASP.NET Web 窗体和 Ajax 版本4</span><span class="sxs-lookup"><span data-stu-id="22aa9-421">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web 窗体和 Ajax 4")
- [<span data-ttu-id="22aa9-422">ASP.NET Ajax 3.5 版</span><span class="sxs-lookup"><span data-stu-id="22aa9-422">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="22aa9-423">CDN 上的 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="22aa9-423">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="22aa9-424">以下 ASP.NET MVC JavaScript 文件托管在此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="22aa9-424">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="22aa9-425">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="22aa9-425">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="22aa9-426">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="22aa9-426">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="22aa9-427">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-427">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="22aa9-428">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-428">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="22aa9-429">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-429">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="22aa9-430">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-430">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="22aa9-431">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="22aa9-431">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="22aa9-432">CDN 上的 ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="22aa9-432">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="22aa9-433">以下 ASP.NET SignalR JavaScript 文件托管在此 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="22aa9-433">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="22aa9-434">ASP.NET SignalR 2.2。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-434">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="22aa9-435">ASP.NET SignalR 2.2。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-435">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="22aa9-436">ASP.NET SignalR 2.2。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-436">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="22aa9-437">ASP.NET SignalR 2.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-437">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="22aa9-438">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="22aa9-438">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="22aa9-439">ASP.NET SignalR 2.0。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-439">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="22aa9-440">ASP.NET SignalR 2.0。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-440">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="22aa9-441">ASP.NET SignalR 2.0。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-441">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="22aa9-442">ASP.NET SignalR 1.1。3</span><span class="sxs-lookup"><span data-stu-id="22aa9-442">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="22aa9-443">ASP.NET SignalR 1.1。2</span><span class="sxs-lookup"><span data-stu-id="22aa9-443">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="22aa9-444">ASP.NET SignalR 1.1。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-444">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="22aa9-445">ASP.NET SignalR 1.1。0</span><span class="sxs-lookup"><span data-stu-id="22aa9-445">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="22aa9-446">ASP.NET SignalR 1.0。1</span><span class="sxs-lookup"><span data-stu-id="22aa9-446">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="22aa9-447">有关 CDN 使用条款的信息，请参阅[Microsoft AJAX CDN 使用条款](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用条款")。</span><span class="sxs-lookup"><span data-stu-id="22aa9-447">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>

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
ms.openlocfilehash: c153dd56fea6f19a818f8785691b022c90391b71
ms.sourcegitcommit: a256895f6160acc28d75424b8ab5d03b4e74412e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2019
ms.locfileid: "67471394"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="1c7b9-102">Microsoft Ajax 内容分发网络</span><span class="sxs-lookup"><span data-stu-id="1c7b9-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="1c7b9-103">生产应用程序不应在 CDN 资产上带有硬依赖项。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="1c7b9-104">应用程序应测试的引用，该 CDN 资产，并使用 CDN 不可用时回退资产。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="1c7b9-105">Microsoft Ajax CDN 具有超越使用 Azure CDN 不提供 SLA。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="1c7b9-106">使用[此 GitHub 问题](https://github.com/aspnet/AspNetDocs/issues/116)报告的 Microsoft Ajax CDN 的问题。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-106">Use [this GitHub issue](https://github.com/aspnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="1c7b9-107">目录</span><span class="sxs-lookup"><span data-stu-id="1c7b9-107">Table of Contents</span></span>

<span data-ttu-id="1c7b9-108">**[重命名为 ajax.aspnetcdn.com ajax.microsoft.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="1c7b9-109">**[Visual Studio.vsdoc 支持](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="1c7b9-110">**[使用 ASP.NET Ajax 从 CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="1c7b9-111">**[使用从 CDN 的 jQuery](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="1c7b9-112">**[使用 jQuery UI 从 CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="1c7b9-113">**[在 CDN 上的第三方文件](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="1c7b9-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="1c7b9-114">cdn 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="1c7b9-115">cdn 的 jQuery 迁移版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="1c7b9-116">jQuery UI 在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="1c7b9-117">jQuery 验证在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="1c7b9-118">jQuery 在 CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="1c7b9-119">jQuery 在 CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="1c7b9-120">jQuery 在 CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="1c7b9-121">jQuery DataTables 在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="1c7b9-122">在 CDN 上 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="1c7b9-123">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="1c7b9-124">在 CDN 上的 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="1c7b9-125">全球化在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="1c7b9-126">响应在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="1c7b9-127">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="1c7b9-128">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="1c7b9-129">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="1c7b9-130">ASP.NET Web 窗体和 Ajax cdn 的发行版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="1c7b9-131">在 CDN 上的 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="1c7b9-132">ASP.NET SignalR 释放 cdn</span><span class="sxs-lookup"><span data-stu-id="1c7b9-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="1c7b9-133">Microsoft Ajax 内容交付网络 (CDN) 承载 jQuery 之类的常用第三方 JavaScript 库，并使您能够轻松地将它们添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="1c7b9-134">例如，可以开始使用此 cdn 的 jQuery 是托管，只需通过添加&lt;脚本&gt;页指向 ajax.aspnetcdn.com 标记。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="1c7b9-135">通过利用 CDN，可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="1c7b9-136">CDN 的内容缓存在位于世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="1c7b9-137">此外，CDN 使浏览器可以重复使用缓存的第三方 JavaScript 文件位于不同域中的网站。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="1c7b9-138">CDN 支持 SSL (HTTPS)，以防您需要使用安全套接字层为网页提供服务。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="1c7b9-139">CDN 托管以下第三方脚本库已上传并授权给你，通过这些库的所有者：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="1c7b9-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="1c7b9-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="1c7b9-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="1c7b9-143">jQuery 验证 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-143">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="1c7b9-144">jQuery 周期 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="1c7b9-145">jQuery DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="1c7b9-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="1c7b9-146">Microsoft Ajax CDN 还包括已由 Microsoft 上传以下库：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="1c7b9-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="1c7b9-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="1c7b9-148">ASP.NET MVC JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="1c7b9-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="1c7b9-149">ASP.NET SignalR JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="1c7b9-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="1c7b9-150">Microsoft 不会声称此 CDN 上托管任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-151">这些库的版权所有者许可给您这些库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="1c7b9-152">仅由各自版权所有者授予任何权限，可能需要下载并使用这样的库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="1c7b9-153">由于这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供任何保证或知识产权版权许可证 （包括任何隐式的专利权利）。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="1c7b9-154">如果你想要提交你的 JavaScript 库，并且你的库是一个顶级的 JavaScript 库 (如上列出 http://trends.builtwith.com) 或扩展/插件的这些库的都是 （a） 受欢迎; 或 （b） 有助于在 ASP.NET 上使用，则请联系AjaxCDNSubmission@Microsoft.com 。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="1c7b9-155">重命名为 ajax.aspnetcdn.com ajax.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1c7b9-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="1c7b9-156">CDN 用于使用 microsoft.com 的域名，已将更改为使用 aspnetcdn.com 域名称。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="1c7b9-157">此更改是为了提高性能，因为浏览器引用 microsoft.com 域时它会发送任何 cookie 从域通过网络与每个请求。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="1c7b9-158">通过重命名为 microsoft.com 之外的域名称性能可以通过增加尽可能为 25%。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="1c7b9-159">请注意 ajax.microsoft.com 仍可正常工作，但是 ajax.aspnetcdn.com 建议。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="1c7b9-160">旧的格式： https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="1c7b9-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="1c7b9-161">新格式： https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="1c7b9-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="1c7b9-162">Visual Studio.vsdoc 支持</span><span class="sxs-lookup"><span data-stu-id="1c7b9-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="1c7b9-163">若要使用 Visual Studio 2008，您需要确保具有 VS 2008 SP1 正确使用.vsdoc 文件安装和安装 vsdoc 文件的修补程序。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="1c7b9-164">可以从此处获取：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-164">You can get these from here:</span></span>

- [<span data-ttu-id="1c7b9-165">下载 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "下载 Visual Studio 2008 SP1")
- [<span data-ttu-id="1c7b9-166">下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "下载.vsdoc 修补程序适用于 Visual Studio 2008 SP1")

<span data-ttu-id="1c7b9-167">Visual Studio 2010 支持.vsdoc 文件而无需任何额外的修补程序。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="1c7b9-168">使用 ASP.NET Ajax 从 CDN</span><span class="sxs-lookup"><span data-stu-id="1c7b9-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="1c7b9-169">在使用 ASP.NET 4 中，可以将 ASP.NET 框架脚本的所有请求重都定向到 CDN。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="1c7b9-170">从 CDN 而不是本地 web 服务器中检索脚本可以大大改进性能的公共 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="1c7b9-171">ScriptManager EnableCDN 属性可用于将 ASP.NET framework 脚本的所有请求重都定向到 Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="1c7b9-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="1c7b9-172">使用从 CDN 的 jQuery</span><span class="sxs-lookup"><span data-stu-id="1c7b9-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="1c7b9-173">可以使用 CDN 上托管 Web 应用程序中，通过将下面的脚本元素添加到页面的 jQuery 脚本：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="1c7b9-174">CDN 还包括的缩小的版 jQuery 脚本，就可以使用以下元素：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="1c7b9-175">若要允许在回退到从您自己的网站上的本地路径加载 jQuery，如果 CDN 碰巧不可用的页面，请立即引用 CDN 元素之后添加以下元素：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="1c7b9-176">下面的示例页使用 jQuery 库 （具有回退到的本地副本） 的 CDN 版本单击按钮时显示的 div 元素的内容。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="1c7b9-177">你可以了解有关 jQuery 的详细信息和下载 jQuery 的本地副本，请访问[jQuery](http://jquery.com/) Web 站点。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="1c7b9-178">使用 jQuery UI 从 CDN</span><span class="sxs-lookup"><span data-stu-id="1c7b9-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="1c7b9-179">CDN 还托管的 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="1c7b9-180">JQuery UI 库包含一组丰富的小组件和可以在 ASP.NET 应用程序中使用的效果。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="1c7b9-181">例如，以下页说明了如何使用 jQuery UI Datepicker 在 ASP.NET Web 窗体应用程序的上下文中显示一个弹出日历：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="1c7b9-182">将焦点移到使用键盘在文本框中，显示一个日历：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![创建用 Datepicker 快捷日历](overview/_static/image1.png)

<span data-ttu-id="1c7b9-184">请注意，必须在上面的代码中包含三个文件从 CDN:</span><span class="sxs-lookup"><span data-stu-id="1c7b9-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="1c7b9-185">JQuery 库&mdash;jQuery UI 库依赖于 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="1c7b9-186">添加 jQuery UI 库之前，必须向您的页面中添加 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="1c7b9-187">JQuery UI 库&mdash;jQuery UI 库包含所有 jQuery UI 效果和如 Datepicker 小组件在上述页面中使用的小组件。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="1c7b9-188">JQuery UI 主题&mdash;jQuery UI 支持不同的主题。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="1c7b9-189">上述页面包括一个 CSS 文件导入雷德蒙德主题的链接。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="1c7b9-190">在 CDN 上托管所有标准的 jQuery UI 主题。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="1c7b9-191">[请访问此页](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 Microsoft Ajax CDN")若要查看每个主题的缩略图。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="1c7b9-192">若要了解有关 jQuery UI 库的详细信息，请访问官方[jQuery UI 网站](http://jQueryUI.com "jQuery UI 网站")。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="1c7b9-193">在 CDN 上的第三方文件</span><span class="sxs-lookup"><span data-stu-id="1c7b9-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="1c7b9-194">CDN 托管某些最常用的第三方 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="1c7b9-195">Microsoft 不会声称此 CDN 上托管任何第三方库的所有权。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-196">这些库的版权所有者许可给您这些库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="1c7b9-197">仅由各自版权所有者授予任何权限，可能需要下载并使用这样的库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="1c7b9-198">由于这些不是 Microsoft 库，Microsoft 将为此 CDN 上托管的第三方库提供任何保证或知识产权版权许可证 （包括任何隐式的专利权利）。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-199">cdn 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-200">在 CDN 上托管以下版本的 jQuery:</span><span class="sxs-lookup"><span data-stu-id="1c7b9-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-341"></a><span data-ttu-id="1c7b9-201">3\.4.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-201">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="1c7b9-202">jQuery 版本 3.4.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-202">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="1c7b9-203">3\.3.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-203">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="1c7b9-204">3\.2.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-204">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="1c7b9-205">jQuery 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-205">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="1c7b9-206">3\.1.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-206">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="1c7b9-207">jQuery 3.1.0 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-207">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="1c7b9-208">jQuery 版本 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-208">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="1c7b9-209">2\.2.4 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-209">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="1c7b9-210">2\.2.3 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-210">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="1c7b9-211">jQuery 版本 2.2.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-211">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="1c7b9-212">jQuery 2.2.1 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-212">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="1c7b9-213">jQuery 版本 2.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-213">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="1c7b9-214">2\.1.4 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-214">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="1c7b9-215">jQuery 版本 2.1.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-215">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="1c7b9-216">jQuery 版本 2.1.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-216">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="1c7b9-217">jQuery 版本 2.1.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-217">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="1c7b9-218">jQuery 版本 2.1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-218">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="1c7b9-219">jQuery 版本 2.0.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-219">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="1c7b9-220">2\.0.2 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-220">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="1c7b9-221">jQuery 版本 2.0.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-221">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="1c7b9-222">jQuery 版本 2.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-222">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="1c7b9-223">jQuery 版本 1.12.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-223">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="1c7b9-224">jQuery 版本 1.12.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-224">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="1c7b9-225">jQuery 版本 1.12.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-225">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="1c7b9-226">jQuery 版本 1.12.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-226">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="1c7b9-227">jQuery 版本 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-227">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="1c7b9-228">jQuery 版本 1.11.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-228">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="1c7b9-229">jQuery 版本 1.11.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-229">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="1c7b9-230">jQuery 版本 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-230">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="1c7b9-231">jQuery 版本 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-231">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="1c7b9-232">jQuery 版本 1.10.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-232">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="1c7b9-233">jQuery 版本 1.10.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-233">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="1c7b9-234">jQuery 版本 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-234">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="1c7b9-235">jQuery 版本 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-235">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="1c7b9-236">jQuery 版本 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-236">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="1c7b9-237">1\.8.3 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-237">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="1c7b9-238">1\.8.2 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-238">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="1c7b9-239">jQuery 版本 1.8.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-239">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="1c7b9-240">jQuery 版本为 1.8.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-240">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="1c7b9-241">1\.7.2 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-241">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="1c7b9-242">1\.7.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-242">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="1c7b9-243">jQuery 1.7 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-243">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="1c7b9-244">jQuery 版本 1.6.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-244">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="1c7b9-245">jQuery 版本 1.6.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-245">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="1c7b9-246">jQuery 版本 1.6.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-246">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="1c7b9-247">jQuery 版本 1.6.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-247">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="1c7b9-248">jQuery 版本 1.6</span><span class="sxs-lookup"><span data-stu-id="1c7b9-248">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="1c7b9-249">1\.5.2 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-249">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="1c7b9-250">1\.5.1 的 jQuery 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-250">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="1c7b9-251">jQuery 1.5 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-251">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="1c7b9-252">jQuery 版本 1.4.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-252">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="1c7b9-253">jQuery 版本 1.4.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-253">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="1c7b9-254">jQuery 1.4.2 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-254">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="1c7b9-255">jQuery 版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-255">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="1c7b9-256">jQuery 版本 1.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-256">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="1c7b9-257">jQuery 版本 1.3.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-257">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-258">cdn 的 jQuery 迁移版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-258">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-259">以下版本的 jQuery 迁移托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-259">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="1c7b9-260">jQuery 迁移 3.0.0 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-260">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="1c7b9-261">jQuery 迁移版本 1.2.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-261">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="1c7b9-262">jQuery 迁移版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-262">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="1c7b9-263">jQuery 迁移 1.1.1 版之前</span><span class="sxs-lookup"><span data-stu-id="1c7b9-263">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="1c7b9-264">jQuery 版本 1.1.0 迁移</span><span class="sxs-lookup"><span data-stu-id="1c7b9-264">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="1c7b9-265">jQuery 版本 1.0.0 迁移</span><span class="sxs-lookup"><span data-stu-id="1c7b9-265">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-266">jQuery UI 在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-266">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-267">此 CDN 上托管以下版本的 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-267">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-268">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-268">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-269">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-269">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "的 jQuery UI 1.12.1 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-270">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-270">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "的 jQuery UI 1.12.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-271">jQuery UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-271">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "的 jQuery UI 1.11.4 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-272">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-272">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "的 jQuery UI 1.11.3 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-273">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-273">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "的 jQuery UI 1.11.2 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-274">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-274">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "的 jQuery UI 1.11.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-275">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-275">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "的 jQuery UI 1.11.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-276">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-276">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "的 jQuery UI 1.10.4 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-277">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-277">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "的 jQuery UI 1.10.3 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-278">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-278">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "的 jQuery UI 1.10.2 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-279">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-279">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "的 jQuery UI 1.10.1 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-280">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-280">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "的 jQuery UI 1.10.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-281">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-281">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "的 jQuery UI 1.9.2 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-282">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-282">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "的 jQuery UI 1.9.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-283">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-283">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "的 jQuery UI 1.9.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-284">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="1c7b9-284">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "的 jQuery UI 1.8.24 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-285">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="1c7b9-285">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "的 jQuery UI 1.8.23 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-286">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="1c7b9-286">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "的 jQuery UI 1.8.22 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-287">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="1c7b9-287">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "的 jQuery UI 1.8.21 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-288">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="1c7b9-288">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "的 jQuery UI 1.8.20 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-289">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="1c7b9-289">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "的 jQuery UI 1.8.19 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-290">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="1c7b9-290">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "的 jQuery UI 1.8.18 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-291">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="1c7b9-291">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "的 jQuery UI 1.8.17 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-292">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="1c7b9-292">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "的 jQuery UI 1.8.16 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-293">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="1c7b9-293">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "的 jQuery UI 1.8.15 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-294">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="1c7b9-294">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "的 jQuery UI 1.8.14 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-295">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="1c7b9-295">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "的 jQuery UI 1.8.13 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-296">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="1c7b9-296">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "的 jQuery UI 1.8.12 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-297">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="1c7b9-297">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "的 jQuery UI 1.8.11 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-298">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="1c7b9-298">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "的 jQuery UI 1.8.10 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-299">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="1c7b9-299">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "的 jQuery UI 1.8.9 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-300">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="1c7b9-300">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "的 jQuery UI 1.8.8 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-301">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="1c7b9-301">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "的 jQuery UI 1.8.7 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-302">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="1c7b9-302">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "的 jQuery UI 1.8.6 Microsoft Ajax cdn")
- [<span data-ttu-id="1c7b9-303">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-303">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-304">jQuery 验证在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-304">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-305">此 CDN 上托管的 jQuery 验证库的以下版本。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-305">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-306">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-306">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-307">jQuery 验证 1.19.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-307">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery 验证 1.19.1")
- [<span data-ttu-id="1c7b9-308">jQuery 验证 1.19.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-308">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery 验证 1.19.0")
- [<span data-ttu-id="1c7b9-309">jQuery 验证 1.17.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-309">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 验证 1.17.0")
- [<span data-ttu-id="1c7b9-310">jQuery 验证 1.16.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-310">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery 验证 1.16.0")
- [<span data-ttu-id="1c7b9-311">jQuery 验证 1.15.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-311">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery 验证 1.15.1")
- [<span data-ttu-id="1c7b9-312">jQuery 验证 1.15.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-312">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery 验证 1.15.0")
- [<span data-ttu-id="1c7b9-313">jQuery 验证 1.14.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-313">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery 验证 1.14.0")
- [<span data-ttu-id="1c7b9-314">jQuery 验证 1.13.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-314">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery 验证 1.13.1")
- [<span data-ttu-id="1c7b9-315">jQuery 验证 1.13.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-315">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery 验证 1.13.0")
- [<span data-ttu-id="1c7b9-316">jQuery 验证 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-316">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery 验证 1.12.0")
- [<span data-ttu-id="1c7b9-317">jQuery 验证 1.11.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-317">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery 验证 1.11.1")
- [<span data-ttu-id="1c7b9-318">jQuery 验证 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-318">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 验证 1.11.0")
- [<span data-ttu-id="1c7b9-319">jQuery 验证 1.10.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-319">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 验证 1.10.0")
- [<span data-ttu-id="1c7b9-320">jQuery 验证 1.9</span><span class="sxs-lookup"><span data-stu-id="1c7b9-320">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 版本 1.9")
- [<span data-ttu-id="1c7b9-321">jQuery 验证 1.8.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-321">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 版本 1.8.1")
- [<span data-ttu-id="1c7b9-322">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="1c7b9-322">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 版本 1.8")
- [<span data-ttu-id="1c7b9-323">jQuery 验证 1.7</span><span class="sxs-lookup"><span data-stu-id="1c7b9-323">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 版本 1.7")
- [<span data-ttu-id="1c7b9-324">jQuery 验证 1.6</span><span class="sxs-lookup"><span data-stu-id="1c7b9-324">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery 验证 1.6")
- [<span data-ttu-id="1c7b9-325">jQuery 验证 1.5.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-325">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery 验证 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-326">jQuery 在 CDN 上的移动版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-326">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-327">此 CDN 上托管以下版本的 jQuery Mobile 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-327">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-328">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-328">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-329">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-329">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "的 jQuery Mobile 1.4.5 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-330">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-330">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "的 jQuery Mobile 1.4.2 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-331">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-331">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "的 jQuery Mobile 1.4.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-332">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-332">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "的 jQuery Mobile 1.4.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-333">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-333">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "的 jQuery Mobile 1.3.2 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-334">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-334">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "的 jQuery Mobile 1.3.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-335">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-335">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "的 jQuery Mobile 1.3.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-336">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-336">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "的 jQuery Mobile 1.2.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-337">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-337">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "的 jQuery Mobile 1.1.2 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-338">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-338">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "的 jQuery Mobile 1.1.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-339">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-339">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "的 jQuery Mobile 1.1.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-340">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-340">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "的 jQuery Mobile 1.1.0 RC2 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-341">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-341">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "的 jQuery Mobile 1.0.1 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-342">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-342">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "的 jQuery Mobile 1.0 Microsoft Ajax CDN")
- [<span data-ttu-id="1c7b9-343">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-343">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="1c7b9-344">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-344">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="1c7b9-345">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-345">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN 的 jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-346">jQuery 在 CDN 上的模板版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-346">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-347">此 CDN 上托管以下版本的 jQuery 模板插件。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-347">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-348">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-348">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-349">jQuery 模板 Beta 1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-349">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 模板 Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-350">jQuery 在 CDN 上的周期版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-350">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-351">此 CDN 上托管以下版本的 jQuery 周期插件。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-351">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-352">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-352">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-353">jQuery 周期 2.99</span><span class="sxs-lookup"><span data-stu-id="1c7b9-353">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery 周期 2.99")
- [<span data-ttu-id="1c7b9-354">jQuery 周期 2.94</span><span class="sxs-lookup"><span data-stu-id="1c7b9-354">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery 周期 2.94")
- [<span data-ttu-id="1c7b9-355">jQuery 周期 2.88</span><span class="sxs-lookup"><span data-stu-id="1c7b9-355">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery 周期 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-356">jQuery DataTables 在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-356">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-357">此 CDN 上托管以下版本的 jQuery DataTables 插件。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-357">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="1c7b9-358">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-358">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-359">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-359">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="1c7b9-360">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-360">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="1c7b9-361">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-361">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="1c7b9-362">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-362">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="1c7b9-363">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-363">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="1c7b9-364">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-364">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="1c7b9-365">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-365">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="1c7b9-366">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-366">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-367">在 CDN 上 Modernizr 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-367">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-368">以下版本的[Modernizr](http://www.modernizr.com "Modernizr")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-368">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-369">在 CDN 上 JSHint 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-369">JSHint Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-370">以下版本的[JSHint](http://www.jshint.com "JSHint")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-370">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-371">在 CDN 上的 knockout 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-371">Knockout Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-372">以下版本的[Knockout](http://www.knockoutjs.com "Knockout")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-372">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-373">全球化在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-373">Globalize Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-374">以下版本的[Globalize](https://github.com/jquery/globalize "Globalize")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-374">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="1c7b9-375">全球化版本 1.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-375">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="1c7b9-376">全球化版本 0.1.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-376">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="1c7b9-377">所有区域性</span><span class="sxs-lookup"><span data-stu-id="1c7b9-377">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="1c7b9-378">"{区域性代码}"替换为所需的区域性代码、 globalize.culture.en GB.js== Microsoft 在 CDN 上的文件例如 = = 这些库已上传由 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-378">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-379">响应在 CDN 上的版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-379">Respond Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-380">以下版本的[响应](https://github.com/scottjehl/Respond "响应")托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-380">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="1c7b9-381">响应版本 1.4.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-381">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="1c7b9-382">响应版本 1.4.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-382">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="1c7b9-383">响应版本.1.4.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-383">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="1c7b9-384">响应版本 1.3.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-384">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="1c7b9-385">响应版本 1.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-385">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-386">在 CDN 上的 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-386">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-387">以下版本的[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap 托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-387">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-431"></a><span data-ttu-id="1c7b9-388">Bootstrap 版本 4.3.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-388">Bootstrap version 4.3.1</span></span>

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

#### <a name="bootstrap-version-421"></a><span data-ttu-id="1c7b9-389">Bootstrap 版本 4.2.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-389">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="1c7b9-390">Bootstrap 版 4.1.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-390">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="1c7b9-391">Bootstrap 版本 4.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-391">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-341"></a><span data-ttu-id="1c7b9-392">Bootstrap 版本 3.4.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-392">Bootstrap version 3.4.1</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="1c7b9-393">Bootstrap 版本 3.4.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-393">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="1c7b9-394">Bootstrap 版本 3.3.7</span><span class="sxs-lookup"><span data-stu-id="1c7b9-394">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="1c7b9-395">Bootstrap 版本 3.3.6</span><span class="sxs-lookup"><span data-stu-id="1c7b9-395">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="1c7b9-396">Bootstrap 版本 3.3.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-396">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="1c7b9-397">3\.3.4 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-397">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="1c7b9-398">3\.3.2 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-398">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="1c7b9-399">3\.3.1 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-399">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="1c7b9-400">Bootstrap 版本 3.3.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-400">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="1c7b9-401">Bootstrap 版本 3.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-401">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="1c7b9-402">3\.1.1 bootstrap 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-402">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="1c7b9-403">启动 3.1.0 版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-403">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="1c7b9-404">Bootstrap 3.0.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-404">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="1c7b9-405">Bootstrap 版本 3.0.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-405">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="1c7b9-406">Bootstrap 版本 3.0.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-406">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="1c7b9-407">Bootstrap 版本 3.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-407">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="1c7b9-408">Bootstrap 版本 2.3.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-408">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="1c7b9-409">Bootstrap 版本 2.3.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-409">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-410">在 CDN 上的启动 TouchCarousel 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-410">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-411">以下版本的[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel 发布托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-411">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="1c7b9-412">Bootstrap TouchCarousel 0.8.0 版本开始</span><span class="sxs-lookup"><span data-stu-id="1c7b9-412">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-413">在 CDN 上 Hammer.js 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-413">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-414">以下版本的[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js 发布托管在 CDN 上：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-414">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="1c7b9-415">Hammer.js 2.0.4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-415">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-416">ASP.NET Web 窗体和 Ajax cdn 的发行版</span><span class="sxs-lookup"><span data-stu-id="1c7b9-416">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-417">在 CDN 上托管以下版本的 ASP.NET Ajax 库。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-417">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="1c7b9-418">单击每个链接以查看文件的实际列表。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-418">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="1c7b9-419">ASP.NET Web 窗体和 Ajax 版本 4.5.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-419">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web 窗体和 Ajax 4.5.2")
- [<span data-ttu-id="1c7b9-420">ASP.NET Web 窗体和 Ajax 版本 4</span><span class="sxs-lookup"><span data-stu-id="1c7b9-420">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web 窗体和 Ajax 4")
- [<span data-ttu-id="1c7b9-421">ASP.NET Ajax 版本 3.5</span><span class="sxs-lookup"><span data-stu-id="1c7b9-421">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-422">在 CDN 上的 ASP.NET MVC 版本</span><span class="sxs-lookup"><span data-stu-id="1c7b9-422">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-423">此 CDN 上托管以下 ASP.NET MVC JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-423">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="1c7b9-424">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-424">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="1c7b9-425">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-425">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="1c7b9-426">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-426">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="1c7b9-427">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-427">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="1c7b9-428">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-428">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="1c7b9-429">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-429">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="1c7b9-430">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-430">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="1c7b9-431">ASP.NET SignalR 释放 cdn</span><span class="sxs-lookup"><span data-stu-id="1c7b9-431">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="1c7b9-432">此 CDN 上托管以下 ASP.NET SignalR JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="1c7b9-432">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="1c7b9-433">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-433">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="1c7b9-434">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-434">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="1c7b9-435">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-435">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="1c7b9-436">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-436">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="1c7b9-437">ASP.NET SignalR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-437">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="1c7b9-438">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-438">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="1c7b9-439">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-439">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="1c7b9-440">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-440">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="1c7b9-441">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="1c7b9-441">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="1c7b9-442">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="1c7b9-442">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="1c7b9-443">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-443">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="1c7b9-444">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1c7b9-444">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="1c7b9-445">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="1c7b9-445">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="1c7b9-446">有关为 CDN 使用条款的信息，请参阅[Microsoft Ajax CDN 使用条款](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 使用条款")。</span><span class="sxs-lookup"><span data-stu-id="1c7b9-446">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>

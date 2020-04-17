---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: 捆绑和将资产捆绑在ASP.NET网页（Razor）网站 |微软文档
author: rick-anderson
description: 捆绑和小化是使您的网站更快的方法。 捆绑允许您组合多个 JavaScript （.js ） 文件或多个级联样式表 （...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539906"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c3ee7-104">在 ASP.NET 网页 (Razor) 中绑定和缩小资产</span><span class="sxs-lookup"><span data-stu-id="c3ee7-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c3ee7-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c3ee7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c3ee7-106">捆绑和小化是使您的网站更快的方法。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="c3ee7-107">捆绑允许您组合多个 JavaScript *（.js*） 文件或多个级联样式表 *（.css）* 文件，以便它们可以作为一个单元下载，而不是一次下载一个。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="c3ee7-108">最小化挤压出空白，并执行其他类型的压缩，使下载的文件尽可能小。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="c3ee7-109">ASP.NET网页 2 的 RC 版本不支持捆绑和小化，因为包含所需元素的包在 Microsoft WebMatrix 中尚不可用。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="c3ee7-110">由此产生的不便，我们深表歉意。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="c3ee7-111">该软件包预计将在ASP.NET网页2和WebMatrix 2的最终版本中提供。</span><span class="sxs-lookup"><span data-stu-id="c3ee7-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>

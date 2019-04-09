---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[如何实现:]缓存 ASP.NET 页面的基于自定义信息的控件 |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何控制缓存 ASP.NET 页面基于自定义信息的条件。 创建一个示例页面，然后 O....
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381401"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="8934c-104">[如何实现:]缓存 ASP.NET 页面的基于自定义信息的控件</span><span class="sxs-lookup"><span data-stu-id="8934c-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="8934c-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="8934c-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="8934c-106">在此视频的 Chris Pels 中显示了如何控制缓存 ASP.NET 页面基于自定义信息的条件。</span><span class="sxs-lookup"><span data-stu-id="8934c-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="8934c-107">创建一个示例页面，然后将 OutputCache 指令使用与 VaryByCustom 特性，其中包含自定义值。</span><span class="sxs-lookup"><span data-stu-id="8934c-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="8934c-108">接下来，GetVaryCustomByString() 方法是在 global.asax 模块提供了自定义属性的处理中重写。</span><span class="sxs-lookup"><span data-stu-id="8934c-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="8934c-109">在该方法中的唯一标识的缓存的版本的页面返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="8934c-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="8934c-110">最后，是有关如何缓存使用的自定义值使用以下几种方式为网站的讨论。</span><span class="sxs-lookup"><span data-stu-id="8934c-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="8934c-111">&#9654;观看视频 （12 分钟）</span><span class="sxs-lookup"><span data-stu-id="8934c-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)

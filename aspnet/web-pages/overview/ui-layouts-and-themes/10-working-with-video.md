---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET 网页（Razor）站点中显示视频 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何使用 Razor 语法页面在 ASP.NET 网页中显示视频。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510380"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="f3b12-103">在 ASP.NET 网页（Razor）站点中显示视频</span><span class="sxs-lookup"><span data-stu-id="f3b12-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="f3b12-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f3b12-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f3b12-105">本文介绍如何在 ASP.NET 网页（Razor）网站中使用视频（媒体）播放器，使用户能够查看存储在网站上的视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="f3b12-106">利用 Razor 语法 ASP.NET 网页，可以播放 Flash （*swf*）、Media Player （ *.Wmv*）和 Silverlight （ *.xap*）视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="f3b12-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="f3b12-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f3b12-108">如何选择视频播放器。</span><span class="sxs-lookup"><span data-stu-id="f3b12-108">How to choose a video player.</span></span>
> - <span data-ttu-id="f3b12-109">如何将视频添加到网页。</span><span class="sxs-lookup"><span data-stu-id="f3b12-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="f3b12-110">如何设置视频播放器属性。</span><span class="sxs-lookup"><span data-stu-id="f3b12-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="f3b12-111">下面是本文中介绍的 ASP.NET Razor 页面功能：</span><span class="sxs-lookup"><span data-stu-id="f3b12-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="f3b12-112">`Video` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f3b12-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f3b12-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f3b12-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f3b12-114">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="f3b12-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f3b12-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="f3b12-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="f3b12-116">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="f3b12-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="f3b12-117">简介</span><span class="sxs-lookup"><span data-stu-id="f3b12-117">Introduction</span></span>

<span data-ttu-id="f3b12-118">你可能想要在你的站点上显示视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-118">You might want to display a video on your site.</span></span> <span data-ttu-id="f3b12-119">实现此目的的一种方法是链接到已包含视频的站点，例如 YouTube。</span><span class="sxs-lookup"><span data-stu-id="f3b12-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="f3b12-120">如果要在自己的页面中直接嵌入来自这些网站的视频，通常可以从网站获取 HTML 标记，然后将其复制到页面中。</span><span class="sxs-lookup"><span data-stu-id="f3b12-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="f3b12-121">例如，以下示例演示了如何嵌入 YouTube 视频：</span><span class="sxs-lookup"><span data-stu-id="f3b12-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="f3b12-122">如果你想要播放位于你自己的网站上的视频（而不是在公共视频共享网站上），则不能使用此类嵌入的标记直接链接到它。</span><span class="sxs-lookup"><span data-stu-id="f3b12-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="f3b12-123">不过，你可以使用 `Video` 帮助程序播放来自你的网站的视频，这会直接在页面中呈现媒体播放器。</span><span class="sxs-lookup"><span data-stu-id="f3b12-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="f3b12-124">选择视频播放器</span><span class="sxs-lookup"><span data-stu-id="f3b12-124">Choosing a Video Player</span></span>

<span data-ttu-id="f3b12-125">视频文件有很多格式，每种格式通常都需要使用不同的播放机和不同的方式来配置播放机。</span><span class="sxs-lookup"><span data-stu-id="f3b12-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="f3b12-126">在 ASP.NET Razor 页面中，可以使用 `Video` 帮助程序在网页上播放视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="f3b12-127">`Video` helper 简化了在网页中嵌入视频的过程，因为它会自动生成 `object`，并 `embed` 通常用于向页面添加视频的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="f3b12-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="f3b12-128">`Video` 帮助程序支持以下媒体播放器：</span><span class="sxs-lookup"><span data-stu-id="f3b12-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="f3b12-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="f3b12-129">Adobe Flash</span></span>
- <span data-ttu-id="f3b12-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="f3b12-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="f3b12-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="f3b12-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="f3b12-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="f3b12-132">The Flash Player</span></span>

<span data-ttu-id="f3b12-133">使用 `Video` 帮助器的 `Flash` 播放器，可以在网页中播放 Flash 视频（*swf*文件）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="f3b12-134">至少必须提供视频文件的路径。</span><span class="sxs-lookup"><span data-stu-id="f3b12-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="f3b12-135">如果不指定路径，播放机将使用当前闪存版本设置的默认值。</span><span class="sxs-lookup"><span data-stu-id="f3b12-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="f3b12-136">典型的默认设置为：</span><span class="sxs-lookup"><span data-stu-id="f3b12-136">Typical default settings are:</span></span>

- <span data-ttu-id="f3b12-137">该视频使用其默认宽度和高度显示，而不使用背景色显示。</span><span class="sxs-lookup"><span data-stu-id="f3b12-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="f3b12-138">加载页面时，视频会自动播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="f3b12-139">视频会一直循环，直到它被显式停止。</span><span class="sxs-lookup"><span data-stu-id="f3b12-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="f3b12-140">视频缩放以显示所有视频，而不是裁剪视频以适应特定大小。</span><span class="sxs-lookup"><span data-stu-id="f3b12-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="f3b12-141">视频在窗口中播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="f3b12-142">MediaPlayer 播放器</span><span class="sxs-lookup"><span data-stu-id="f3b12-142">The MediaPlayer Player</span></span>

<span data-ttu-id="f3b12-143">使用 `Video` 帮助器的 `MediaPlayer` 播放器，可以在网页中播放 Windows Media 视频（ *.wmv*文件）、windows media 音频（*wma*文件）和 mp3 （*mp3*文件）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="f3b12-144">必须包含要播放的媒体文件的路径;所有其他参数都是可选的。</span><span class="sxs-lookup"><span data-stu-id="f3b12-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="f3b12-145">如果仅指定路径，播放机将使用当前版本的 MediaPlayer 设置的默认设置，例如：</span><span class="sxs-lookup"><span data-stu-id="f3b12-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="f3b12-146">该视频使用其默认宽度和高度显示。</span><span class="sxs-lookup"><span data-stu-id="f3b12-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="f3b12-147">加载页面时，视频会自动播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="f3b12-148">视频播放一次（不循环）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="f3b12-149">播放机在用户界面中显示完整的控件集。</span><span class="sxs-lookup"><span data-stu-id="f3b12-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="f3b12-150">视频在窗口中播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="f3b12-151">Silverlight 播放器</span><span class="sxs-lookup"><span data-stu-id="f3b12-151">The Silverlight Player</span></span>

<span data-ttu-id="f3b12-152">`Video` 帮助器的 `Silverlight` 播放机使你可以播放 Windows Media 视频（ *.wmv*文件）、Windows Media 音频（ *.wma*文件）和 mp3 （*mp3*文件）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="f3b12-153">必须将 path 参数设置为指向基于 Silverlight 的应用程序包（ *.xap*文件）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="f3b12-154">还必须设置 width 和 height 参数。</span><span class="sxs-lookup"><span data-stu-id="f3b12-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="f3b12-155">其他所有参数都是可选参数。</span><span class="sxs-lookup"><span data-stu-id="f3b12-155">All other parameters are optional.</span></span> <span data-ttu-id="f3b12-156">当你使用 Silverlight 播放视频时，如果仅设置所需的参数，则 Silverlight 播放机将显示不带背景色的视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b12-157">如果你尚未知道 Silverlight： *.xap*文件是一个压缩文件，其中包含 *.xaml*文件中的布局说明、程序集中的托管代码和可选资源。</span><span class="sxs-lookup"><span data-stu-id="f3b12-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="f3b12-158">你可以在 Visual Studio 中创建一个 *.xap*文件作为 Silverlight 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="f3b12-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="f3b12-159">`Silverlight` 视频播放器使用您为播放机提供的设置和 *.xap*文件中提供的设置。</span><span class="sxs-lookup"><span data-stu-id="f3b12-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="f3b12-160">MIME 类型</span><span class="sxs-lookup"><span data-stu-id="f3b12-160">MIME Types</span></span>
> 
> <span data-ttu-id="f3b12-161">当浏览器下载文件时，浏览器会确保文件类型与为正在呈现的文档指定的 MIME 类型匹配。</span><span class="sxs-lookup"><span data-stu-id="f3b12-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="f3b12-162">MIME 类型是文件的内容类型或媒体类型。</span><span class="sxs-lookup"><span data-stu-id="f3b12-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="f3b12-163">`Video` 帮助器使用以下 MIME 类型：</span><span class="sxs-lookup"><span data-stu-id="f3b12-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="f3b12-164">播放 Flash （swf）视频</span><span class="sxs-lookup"><span data-stu-id="f3b12-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="f3b12-165">此过程说明如何播放名为*sample*的 Flash 视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="f3b12-166">此过程假设你已在站点上获取一个名为 "*媒体*" 的文件夹，并且该*swf*文件位于该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f3b12-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="f3b12-167">如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="f3b12-168">在网站中，添加一个页面，并将其命名为*FlashVideo*。</span><span class="sxs-lookup"><span data-stu-id="f3b12-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="f3b12-169">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="f3b12-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="f3b12-170">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="f3b12-170">Run the page in a browser.</span></span> <span data-ttu-id="f3b12-171">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）页面随即显示，视频会自动播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="f3b12-172">![影像](10-working-with-video/_static/image1.jpg "ch08_video-1")</span><span class="sxs-lookup"><span data-stu-id="f3b12-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="f3b12-173">可以将闪存视频的 `quality` 参数设置为 `low`、`autolow`、`autohigh`、`medium`、`high`和 `best`：</span><span class="sxs-lookup"><span data-stu-id="f3b12-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="f3b12-174">您可以使用 `scale` 参数更改 Flash 视频以特定大小播放，可以将该参数设置为以下内容：</span><span class="sxs-lookup"><span data-stu-id="f3b12-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="f3b12-175">`showall`。</span><span class="sxs-lookup"><span data-stu-id="f3b12-175">`showall`.</span></span> <span data-ttu-id="f3b12-176">这会使整个视频可见，同时保持原始纵横比。</span><span class="sxs-lookup"><span data-stu-id="f3b12-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="f3b12-177">不过，您可能会在每一端上都有边框。</span><span class="sxs-lookup"><span data-stu-id="f3b12-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="f3b12-178">`noorder`。</span><span class="sxs-lookup"><span data-stu-id="f3b12-178">`noorder`.</span></span> <span data-ttu-id="f3b12-179">这会在保持原始纵横比的同时缩放视频，但可能会被裁剪。</span><span class="sxs-lookup"><span data-stu-id="f3b12-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="f3b12-180">`exactfit`。</span><span class="sxs-lookup"><span data-stu-id="f3b12-180">`exactfit`.</span></span> <span data-ttu-id="f3b12-181">这样可以在不保留原始纵横比的情况下显示整个视频，但可能会发生失真。</span><span class="sxs-lookup"><span data-stu-id="f3b12-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="f3b12-182">如果没有指定 `scale` 参数，则整个视频将可见，并且在不进行任何裁剪的情况下将保持原始纵横比。</span><span class="sxs-lookup"><span data-stu-id="f3b12-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="f3b12-183">下面的示例演示如何使用 `scale` 参数：</span><span class="sxs-lookup"><span data-stu-id="f3b12-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="f3b12-184">Flash player 支持名为 `windowMode`的视频模式设置。</span><span class="sxs-lookup"><span data-stu-id="f3b12-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="f3b12-185">可以将此设置为 `window`、`opaque`和 `transparent`。</span><span class="sxs-lookup"><span data-stu-id="f3b12-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="f3b12-186">默认情况下，`windowMode` 设置为 `window`，这会在网页的单独窗口中显示视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="f3b12-187">`opaque` 设置将隐藏网页上的所有内容。</span><span class="sxs-lookup"><span data-stu-id="f3b12-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="f3b12-188">"`transparent`" 设置允许网页的背景透过视频显示，假设视频的任何部分都是透明的。</span><span class="sxs-lookup"><span data-stu-id="f3b12-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="f3b12-189">播放 MediaPlayer （ *.wmv*）视频</span><span class="sxs-lookup"><span data-stu-id="f3b12-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="f3b12-190">以下过程说明如何播放名为*sample*的窗口媒体视频，该视频位于*media*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f3b12-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="f3b12-191">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f3b12-192">创建名为*MediaPlayerVideo*的新页面。</span><span class="sxs-lookup"><span data-stu-id="f3b12-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="f3b12-193">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="f3b12-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="f3b12-194">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="f3b12-194">Run the page in a browser.</span></span> <span data-ttu-id="f3b12-195">视频会自动加载和播放。</span><span class="sxs-lookup"><span data-stu-id="f3b12-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="f3b12-196">![影像](10-working-with-video/_static/image2.jpg "ch08_video-2")</span><span class="sxs-lookup"><span data-stu-id="f3b12-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="f3b12-197">可以将 `playCount` 设置为一个整数，该整数指示自动播放视频的次数：</span><span class="sxs-lookup"><span data-stu-id="f3b12-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="f3b12-198">`uiMode` 参数可用于指定在用户界面中显示的控件。</span><span class="sxs-lookup"><span data-stu-id="f3b12-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="f3b12-199">可以将 `uiMode` 设置为 `invisible`、`none`、`mini`或 `full`。</span><span class="sxs-lookup"><span data-stu-id="f3b12-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="f3b12-200">如果没有指定 `uiMode` 参数，则除了视频窗口外，视频还将显示 "状态" 窗口、"搜索栏"、"控制按钮" 和 "音量" 控件。</span><span class="sxs-lookup"><span data-stu-id="f3b12-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="f3b12-201">如果使用播放机播放音频文件，也会显示这些控件。</span><span class="sxs-lookup"><span data-stu-id="f3b12-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="f3b12-202">下面是有关如何使用 `uiMode` 参数的示例：</span><span class="sxs-lookup"><span data-stu-id="f3b12-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="f3b12-203">默认情况下，播放视频时音频处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="f3b12-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="f3b12-204">可以通过将 `mute` 参数设置为 true 来使音频静音：</span><span class="sxs-lookup"><span data-stu-id="f3b12-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="f3b12-205">可以通过将 `volume` 参数设置为介于0到100之间的值来控制 MediaPlayer 视频的音频级别。</span><span class="sxs-lookup"><span data-stu-id="f3b12-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="f3b12-206">默认值为 50。</span><span class="sxs-lookup"><span data-stu-id="f3b12-206">The default value is 50.</span></span> <span data-ttu-id="f3b12-207">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="f3b12-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="f3b12-208">播放 Silverlight 视频</span><span class="sxs-lookup"><span data-stu-id="f3b12-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="f3b12-209">此过程说明如何播放包含在名为*Media*的文件夹中的 Silverlight *.xap*页面中的视频。</span><span class="sxs-lookup"><span data-stu-id="f3b12-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="f3b12-210">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="f3b12-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="f3b12-211">创建名为*SilverlightVideo*的新页面。</span><span class="sxs-lookup"><span data-stu-id="f3b12-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="f3b12-212">将以下标记添加到页面：</span><span class="sxs-lookup"><span data-stu-id="f3b12-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="f3b12-213">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="f3b12-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="f3b12-214">![影像](10-working-with-video/_static/image3.jpg "ch08_video-3")</span><span class="sxs-lookup"><span data-stu-id="f3b12-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f3b12-215">其他资源</span><span class="sxs-lookup"><span data-stu-id="f3b12-215">Additional Resources</span></span>

<span data-ttu-id="f3b12-216">[Silverlight 概述](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="f3b12-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="f3b12-217">Flash 对象和嵌入标记属性</span><span class="sxs-lookup"><span data-stu-id="f3b12-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="f3b12-218">[Windows Media Player 11 SDK 参数标记](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="f3b12-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>

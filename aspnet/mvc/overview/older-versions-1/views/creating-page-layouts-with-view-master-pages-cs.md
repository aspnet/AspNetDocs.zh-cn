---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 使用视图母版页 （C#） 创建页面布局 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。 您可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542516"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="11c51-104">使用视图母版页创建页面布局 (C#)</span><span class="sxs-lookup"><span data-stu-id="11c51-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="11c51-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="11c51-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="11c51-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="11c51-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="11c51-107">在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="11c51-108">例如，可以使用视图母版页定义两列页面布局，并为 Web 应用程序中的所有页面使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="11c51-109">使用查看母版页创建页面布局</span><span class="sxs-lookup"><span data-stu-id="11c51-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="11c51-110">在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="11c51-111">例如，可以使用视图母版页定义两列页面布局，并为 Web 应用程序中的所有页面使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="11c51-112">您还可以利用查看母版页在应用程序中多个页面之间共享常见内容。</span><span class="sxs-lookup"><span data-stu-id="11c51-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="11c51-113">例如，您可以将网站徽标、导航链接和横幅广告放在视图母版页中。</span><span class="sxs-lookup"><span data-stu-id="11c51-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="11c51-114">这样，应用程序中的每个页面都会自动显示此内容。</span><span class="sxs-lookup"><span data-stu-id="11c51-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="11c51-115">在本教程中，您将了解如何创建新的视图母版页，并根据母版页创建新的视图内容页。</span><span class="sxs-lookup"><span data-stu-id="11c51-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="11c51-116">创建视图母版页</span><span class="sxs-lookup"><span data-stu-id="11c51-116">Creating a View Master Page</span></span>

<span data-ttu-id="11c51-117">让我们首先创建定义两列布局的视图母版页。</span><span class="sxs-lookup"><span data-stu-id="11c51-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="11c51-118">通过右键单击"视图+共享"文件夹、选择菜单选项 **"添加、新建项目**"以及选择**MVC 视图母版页**模板（参见图 1），将新的视图母版页添加到 MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="11c51-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="11c51-119">[![添加视图母版页](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="11c51-120">**图 01**： 添加视图母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="11c51-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="11c51-121">您可以在应用程序中创建多个视图母版页。</span><span class="sxs-lookup"><span data-stu-id="11c51-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="11c51-122">每个视图母版页可以定义不同的页面布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="11c51-123">例如，您可能希望某些页面具有两列布局和其他页面具有三列布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="11c51-124">视图母版页看起来非常类似于标准ASP.NET MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="11c51-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="11c51-125">但是，与普通视图不同，视图母版页包含一个或多个`<asp:ContentPlaceHolder>`标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="11c51-126">这些`<contentplaceholder>`标记用于标记可在单个内容页中重写的母版页区域。</span><span class="sxs-lookup"><span data-stu-id="11c51-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="11c51-127">例如，清单 1 中的视图母版页定义两列布局。</span><span class="sxs-lookup"><span data-stu-id="11c51-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="11c51-128">它包含两`<contentplaceholder>`个标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="11c51-129">每`<ContentPlaceHolder>`列一列。</span><span class="sxs-lookup"><span data-stu-id="11c51-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="11c51-130">**清单1 |`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="11c51-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="11c51-131">清单1中的视图母版页的正文包含两`<div>`个对应于两列的标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="11c51-132">"级联样式表"列类应用于这两个`<div>`标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="11c51-133">此类在母版页顶部声明的样式表中定义。</span><span class="sxs-lookup"><span data-stu-id="11c51-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="11c51-134">您可以通过切换到"设计"视图来预览视图母版页的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="11c51-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="11c51-135">单击源代码编辑器左下角的"设计"选项卡（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="11c51-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="11c51-136">[![在设计器中预览母版页](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="11c51-137">**图 02**： 预览设计器中的母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="11c51-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="11c51-138">创建查看内容页面</span><span class="sxs-lookup"><span data-stu-id="11c51-138">Creating a View Content Page</span></span>

<span data-ttu-id="11c51-139">创建视图母版页后，可以基于视图母版页创建一个或多个视图内容页。</span><span class="sxs-lookup"><span data-stu-id="11c51-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="11c51-140">例如，您可以通过右键单击"视图+主页"文件夹、选择 **"添加、新建项目"、** 选择**MVC 查看内容页**模板、输入名称 Index.aspx 以及单击 **"添加**"按钮（参见图 3）为主控制器创建索引视图内容页。</span><span class="sxs-lookup"><span data-stu-id="11c51-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="11c51-141">[![添加视图内容页](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="11c51-142">**图 03**： 添加视图内容页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="11c51-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="11c51-143">单击"添加"按钮后，将出现一个新对话框，使您能够选择视图母版页以与视图内容页关联（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="11c51-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="11c51-144">您可以导航到我们在上一节中创建的 Site.master 视图母版页。</span><span class="sxs-lookup"><span data-stu-id="11c51-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="11c51-145">[![选择母版页](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="11c51-146">**图 04**： 选择母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="11c51-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="11c51-147">基于 Site.master 母版页创建新的视图内容页后，您将在清单 2 中获取该文件。</span><span class="sxs-lookup"><span data-stu-id="11c51-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="11c51-148">**清单2 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="11c51-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="11c51-149">请注意，此视图包含一个`<asp:Content>`对应于视图母版页中每个`<asp:ContentPlaceHolder>`标记的标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="11c51-150">每个`<asp:Content>`标记都包含一个 ContentPlaceHolderID 属性，`<asp:ContentPlaceHolder>`该属性指向它覆盖的特定。</span><span class="sxs-lookup"><span data-stu-id="11c51-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="11c51-151">此外，请注意，清单 2 中的内容视图页不包含任何正常的打开和关闭 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="11c51-152">例如，它不包含打开和关闭`<html>`或`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="11c51-153">所有正常的打开和关闭标记都包含在视图母版页中。</span><span class="sxs-lookup"><span data-stu-id="11c51-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="11c51-154">要在视图内容页中显示的任何内容都必须放置在`<asp:Content>`标记中。</span><span class="sxs-lookup"><span data-stu-id="11c51-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="11c51-155">如果将这些标记之外放置任何 HTML 或其他内容，则当您尝试查看页面时，将出现错误。</span><span class="sxs-lookup"><span data-stu-id="11c51-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="11c51-156">您无需覆盖内容视图页中母`<asp:ContentPlaceHolder>`版页中的每个标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="11c51-157">仅当要将`<asp:ContentPlaceHolder>`标记替换为特定内容时，才需要覆盖标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="11c51-158">例如，清单 3 中修改的索引视图仅包含两`<asp:Content>`个标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="11c51-159">每个`<asp:Content>`标记都包含一些文本。</span><span class="sxs-lookup"><span data-stu-id="11c51-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="11c51-160">**清单3 |`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="11c51-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="11c51-161">当请求清单 3 中的视图时，它将呈现图 5 中的页面。</span><span class="sxs-lookup"><span data-stu-id="11c51-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="11c51-162">请注意，视图呈现具有两列的页面。</span><span class="sxs-lookup"><span data-stu-id="11c51-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="11c51-163">此外，请注意，视图内容页中的内容将与视图母版页中的内容合并</span><span class="sxs-lookup"><span data-stu-id="11c51-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="11c51-164">[![索引视图内容页](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="11c51-165">**图 05**： 索引视图内容页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)）</span><span class="sxs-lookup"><span data-stu-id="11c51-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="11c51-166">修改查看母版页内容</span><span class="sxs-lookup"><span data-stu-id="11c51-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="11c51-167">在使用视图母版页时，您几乎立即遇到的一个问题是，当请求不同的视图内容页时，会修改视图母版页内容。</span><span class="sxs-lookup"><span data-stu-id="11c51-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="11c51-168">例如，您希望 Web 应用程序中的每个页面都有唯一的标题。</span><span class="sxs-lookup"><span data-stu-id="11c51-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="11c51-169">但是，标题在视图母版页中声明，而不是在视图内容页中声明。</span><span class="sxs-lookup"><span data-stu-id="11c51-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="11c51-170">那么，如何为每个视图内容页面自定义页面标题？</span><span class="sxs-lookup"><span data-stu-id="11c51-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="11c51-171">有两种方法可以修改视图内容页显示的标题。</span><span class="sxs-lookup"><span data-stu-id="11c51-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="11c51-172">首先，您可以将页面标题分配给视图内容页顶部声明的`<%@ page %>`指令的标题属性。</span><span class="sxs-lookup"><span data-stu-id="11c51-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="11c51-173">例如，如果要将页面标题"超级大网站"分配给索引视图，则可以在 Index 视图的顶部包括以下指令：</span><span class="sxs-lookup"><span data-stu-id="11c51-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="11c51-174">当"索引"视图呈现给浏览器时，所需的标题将显示在浏览器标题栏中：</span><span class="sxs-lookup"><span data-stu-id="11c51-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="11c51-175">[![浏览器标题栏](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="11c51-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="11c51-176">主视图页必须满足一个重要要求，以便标题属性正常工作。</span><span class="sxs-lookup"><span data-stu-id="11c51-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="11c51-177">视图母版页必须包含`<head runat="server">`标记，而不是其标题的正常`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="11c51-178">如果`<head>`标记不包含 runat_"server"属性，则标题将不会显示。</span><span class="sxs-lookup"><span data-stu-id="11c51-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="11c51-179">默认视图母版页包括所需的`<head runat="server">`标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="11c51-180">从单个视图内容页修改母版页内容的另一种方法是包装要在`<asp:ContentPlaceHolder>`标记中修改的区域。</span><span class="sxs-lookup"><span data-stu-id="11c51-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="11c51-181">例如，假设您不仅希望更改标题，还要更改由母版视图页呈现的元标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="11c51-182">清单4中的主视图页在其`<asp:ContentPlaceHolder>``<head>`标记中包含一个标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="11c51-183">**清单4 |`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="11c51-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="11c51-184">请注意，`<asp:ContentPlaceHolder>`清单 4 中的标记包括默认内容：默认标题和默认元标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="11c51-185">如果不在单个视图内容页中`<asp:ContentPlaceHolder>`覆盖此标记，则将显示默认内容。</span><span class="sxs-lookup"><span data-stu-id="11c51-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="11c51-186">清单5中的内容视图页将覆盖`<asp:ContentPlaceHolder>`标记，以便显示自定义标题和自定义元标记。</span><span class="sxs-lookup"><span data-stu-id="11c51-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="11c51-187">**清单5 |`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="11c51-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="11c51-188">总结</span><span class="sxs-lookup"><span data-stu-id="11c51-188">Summary</span></span>

<span data-ttu-id="11c51-189">本教程为您提供查看母版页和查看内容页的基本介绍。</span><span class="sxs-lookup"><span data-stu-id="11c51-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="11c51-190">您学习了如何创建新的视图母版页，并基于它们创建视图内容页。</span><span class="sxs-lookup"><span data-stu-id="11c51-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="11c51-191">我们还研究了如何从特定视图内容页修改视图母版页的内容。</span><span class="sxs-lookup"><span data-stu-id="11c51-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11c51-192">[上一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一页](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="11c51-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>

---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 使用视图母版页 (C#) 创建页面布局 |Microsoft Docs
author: microsoft
description: 在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。 可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d09a38c2bea9e8beb91e322ed7e4a9d337fa0843
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412627"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="58b95-104">使用视图母版页创建页面布局 (C#)</span><span class="sxs-lookup"><span data-stu-id="58b95-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="58b95-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="58b95-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="58b95-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="58b95-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="58b95-107">在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。</span><span class="sxs-lookup"><span data-stu-id="58b95-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="58b95-108">可用于视图的主页面，例如，定义两列的页面布局和两列布局用于所有 web 应用程序中的页。</span><span class="sxs-lookup"><span data-stu-id="58b95-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>


## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="58b95-109">使用视图母版页创建页面布局</span><span class="sxs-lookup"><span data-stu-id="58b95-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="58b95-110">在本教程中，您将学习如何通过利用视图母版页创建应用程序中的多个页面的常规页面布局。</span><span class="sxs-lookup"><span data-stu-id="58b95-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="58b95-111">可用于视图的主页面，例如，定义两列的页面布局和两列布局用于所有 web 应用程序中的页。</span><span class="sxs-lookup"><span data-stu-id="58b95-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="58b95-112">您还可以利用视图的主页面，用于跨应用程序中的多个页共享常见的内容。</span><span class="sxs-lookup"><span data-stu-id="58b95-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="58b95-113">例如，您可以在视图母版页中将网站徽标、 导航链接和横幅广告。</span><span class="sxs-lookup"><span data-stu-id="58b95-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="58b95-114">这样一来，在应用程序中的每一页将自动显示此内容。</span><span class="sxs-lookup"><span data-stu-id="58b95-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="58b95-115">在本教程中，您将了解如何创建新视图母版页，并创建新视图内容页基于母版页。</span><span class="sxs-lookup"><span data-stu-id="58b95-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="58b95-116">创建视图母版页</span><span class="sxs-lookup"><span data-stu-id="58b95-116">Creating a View Master Page</span></span>

<span data-ttu-id="58b95-117">让我们首先创建定义了两列布局视图母版页。</span><span class="sxs-lookup"><span data-stu-id="58b95-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="58b95-118">您将添加新视图母版页到 MVC 项目，请右键单击 views/shared 文件夹中，选择菜单选项**添加、 新建项**，然后选择**MVC 视图母版页**模板 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="58b95-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>


[![A<span data-ttu-id="58b95-119">dding 视图母版页]</span><span class="sxs-lookup"><span data-stu-id="58b95-119">dding a view master page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

<span data-ttu-id="58b95-120">**图 01**:添加视图母版页 ([单击此项可查看原尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="58b95-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="58b95-121">应用程序中，可以创建多个视图母版页。</span><span class="sxs-lookup"><span data-stu-id="58b95-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="58b95-122">每个视图母版页可以定义不同的页面布局。</span><span class="sxs-lookup"><span data-stu-id="58b95-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="58b95-123">例如，您可能希望某些页具有两列布局和其他页面具有三列布局。</span><span class="sxs-lookup"><span data-stu-id="58b95-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="58b95-124">视图的主页面看起来很像标准的 ASP.NET MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="58b95-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="58b95-125">但是，与普通视图中，不同视图母版页包含一个或多个`<asp:ContentPlaceHolder>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="58b95-126">`<contentplaceholder>`标记用于标记可以在单个内容页面中重写的母版页的区域。</span><span class="sxs-lookup"><span data-stu-id="58b95-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="58b95-127">例如，在列表 1 中的视图母版页定义两列布局。</span><span class="sxs-lookup"><span data-stu-id="58b95-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="58b95-128">它包含两个`<contentplaceholder>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="58b95-129">一个`<ContentPlaceHolder>`的每个列。</span><span class="sxs-lookup"><span data-stu-id="58b95-129">One `<ContentPlaceHolder>` for each column.</span></span>

**<span data-ttu-id="58b95-130">代码清单 1 –</span><span class="sxs-lookup"><span data-stu-id="58b95-130">Listing 1 –</span></span> `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="58b95-131">在列表 1 中的主页面包含两个视图的正文`<div>`对应于两个列的标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="58b95-132">级联样式表的列类应用于这两`<div>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="58b95-133">此类定义中声明顶部的主页面的样式表。</span><span class="sxs-lookup"><span data-stu-id="58b95-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="58b95-134">您可以预览视图母版页通过切换到设计视图中的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="58b95-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="58b95-135">单击左下角的源代码编辑器的设计选项卡 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="58b95-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>


[![P<span data-ttu-id="58b95-136">查看设计器中的主页面]</span><span class="sxs-lookup"><span data-stu-id="58b95-136">reviewing a master page in the designer]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

<span data-ttu-id="58b95-137">**图 02**:预览设计器中的母版页 ([单击此项可查看原尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="58b95-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>


### <a name="creating-a-view-content-page"></a><span data-ttu-id="58b95-138">创建视图内容页</span><span class="sxs-lookup"><span data-stu-id="58b95-138">Creating a View Content Page</span></span>

<span data-ttu-id="58b95-139">创建视图母版页后，您可以创建一个或多个视图基于视图母版页的内容页面。</span><span class="sxs-lookup"><span data-stu-id="58b95-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="58b95-140">例如，可以通过右键单击 views/home 文件夹中，创建主控制器的索引视图内容页选择**添加、 新建项**，选择**MVC 视图内容页**模板中，输入名称 Index.aspx，并单击**添加**按钮 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="58b95-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>


[![A<span data-ttu-id="58b95-141">dding 视图内容页]</span><span class="sxs-lookup"><span data-stu-id="58b95-141">dding a view content page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

<span data-ttu-id="58b95-142">**图 03**:添加视图内容页 ([单击此项可查看原尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="58b95-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>


<span data-ttu-id="58b95-143">单击添加按钮后，新会出现一个对话框，可用于选择要将视图内容页与相关联的视图主页面 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="58b95-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="58b95-144">您可以导航到 Site.master 视图母版页，我们在上一节中创建。</span><span class="sxs-lookup"><span data-stu-id="58b95-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>


[![S<span data-ttu-id="58b95-145">选择母版页]</span><span class="sxs-lookup"><span data-stu-id="58b95-145">electing a master page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

<span data-ttu-id="58b95-146">**图 04**:选择母版页 ([单击此项可查看原尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="58b95-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>


<span data-ttu-id="58b95-147">创建新视图内容页基于 Site.master 母版页后，获取代码清单 2 中的文件。</span><span class="sxs-lookup"><span data-stu-id="58b95-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

**<span data-ttu-id="58b95-148">代码清单 2 –</span><span class="sxs-lookup"><span data-stu-id="58b95-148">Listing 2 –</span></span> `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="58b95-149">请注意，此视图包含`<asp:Content>`对应于每个标记`<asp:ContentPlaceHolder>`视图母版页中的标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="58b95-150">每个`<asp:Content>`标记包含指向特定 ContentPlaceHolderID 属性`<asp:ContentPlaceHolder>`它重写。</span><span class="sxs-lookup"><span data-stu-id="58b95-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="58b95-151">此外，请注意，代码清单 2 中的内容视图页不包含任何普通的开始和结束 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="58b95-152">例如，它不包含在开始和结束`<html>`或`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="58b95-153">正常的开始和结束标记的所有包含在视图母版页。</span><span class="sxs-lookup"><span data-stu-id="58b95-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="58b95-154">你想要在视图内容页中显示任何内容必须位于`<asp:Content>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="58b95-155">如果将任何 HTML 或这些标记之外的其他内容，然后当您尝试查看的页面时将会出错。</span><span class="sxs-lookup"><span data-stu-id="58b95-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="58b95-156">无需重写每个`<asp:ContentPlaceHolder>`从母版页内容视图页中的标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="58b95-157">只需重写`<asp:ContentPlaceHolder>`标记时想要将标记替换为特定的内容。</span><span class="sxs-lookup"><span data-stu-id="58b95-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="58b95-158">例如，清单 3 中的已修改的索引视图仅包含两个`<asp:Content>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="58b95-159">每个`<asp:Content>`标记包含一些文本。</span><span class="sxs-lookup"><span data-stu-id="58b95-159">Each of the `<asp:Content>` tags includes some text.</span></span>

**<span data-ttu-id="58b95-160">代码清单 3 –</span><span class="sxs-lookup"><span data-stu-id="58b95-160">Listing 3 –</span></span> `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="58b95-161">当请求清单 3 中的视图时，它将呈现在图 5 中的页。</span><span class="sxs-lookup"><span data-stu-id="58b95-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="58b95-162">请注意视图呈现的页面包含两个列。</span><span class="sxs-lookup"><span data-stu-id="58b95-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="58b95-163">此外，请注意，从视图内容页的内容将与来自视图母版页的内容合并</span><span class="sxs-lookup"><span data-stu-id="58b95-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>


[![T<span data-ttu-id="58b95-164">他索引视图内容页]</span><span class="sxs-lookup"><span data-stu-id="58b95-164">he Index view content page]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

<span data-ttu-id="58b95-165">**图 05**:索引视图内容页 ([单击此项可查看原尺寸图像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="58b95-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>


### <a name="modifying-view-master-page-content"></a><span data-ttu-id="58b95-166">修改查看主页面内容</span><span class="sxs-lookup"><span data-stu-id="58b95-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="58b95-167">使用视图母版页时立即几乎会遇到的一个问题是修改视图母版页内容，当请求不同的视图内容页时的问题。</span><span class="sxs-lookup"><span data-stu-id="58b95-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="58b95-168">例如，希望每个页面中将 web 应用程序具有唯一的标题。</span><span class="sxs-lookup"><span data-stu-id="58b95-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="58b95-169">但是，标题被声明视图母版页中并不在视图内容页。</span><span class="sxs-lookup"><span data-stu-id="58b95-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="58b95-170">因此，如何执行自定义每个视图内容页的页面标题？</span><span class="sxs-lookup"><span data-stu-id="58b95-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="58b95-171">有两种方法，你可以修改视图内容页所显示的标题。</span><span class="sxs-lookup"><span data-stu-id="58b95-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="58b95-172">首先，将分配到的 title 属性页标题`<%@ page %>`指令声明顶部的视图内容页。</span><span class="sxs-lookup"><span data-stu-id="58b95-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="58b95-173">例如，如果你想要将页标题"超级出色的网站"分配给索引视图，您可以包括在索引视图的顶部的以下指令：</span><span class="sxs-lookup"><span data-stu-id="58b95-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="58b95-174">索引视图呈现给浏览器，浏览器标题栏中会显示所需的标题：</span><span class="sxs-lookup"><span data-stu-id="58b95-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>


[![B<span data-ttu-id="58b95-175">rowser 标题栏]</span><span class="sxs-lookup"><span data-stu-id="58b95-175">rowser title bar]</span></span>(creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)


<span data-ttu-id="58b95-176">没有母版视图页中的 title 属性，若要运行的顺序必须满足的一个重要要求。</span><span class="sxs-lookup"><span data-stu-id="58b95-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="58b95-177">必须包含视图母版页`<head runat="server">`而不是普通的标记`<head>`其标头标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="58b95-178">如果`<head>`标记不包含 runat ="server"特性，则不会显示标题。</span><span class="sxs-lookup"><span data-stu-id="58b95-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="58b95-179">母版页包含所需的默认视图`<head runat="server">`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="58b95-180">从单独的视图内容页修改母版页内容的备用方法是以包装您想要在修改的区域`<asp:ContentPlaceHolder>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="58b95-181">例如，假设你想要更改不仅标题，而且还呈现的母版视图页的 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="58b95-182">列表 4 中的母版视图页包含`<asp:ContentPlaceHolder>`标记内其`<head>`标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

**<span data-ttu-id="58b95-183">列表 4 –</span><span class="sxs-lookup"><span data-stu-id="58b95-183">Listing 4 –</span></span> `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="58b95-184">请注意，`<asp:ContentPlaceHolder>`列表 4 中的标记包括默认内容： 默认标题和默认 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="58b95-185">如果不替代这`<asp:ContentPlaceHolder>`标记中单独的视图内容页上，则将显示默认内容。</span><span class="sxs-lookup"><span data-stu-id="58b95-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="58b95-186">列表 5 中的内容视图页重写`<asp:ContentPlaceHolder>`以便显示一个自定义标题和自定义 meta 标记的标记。</span><span class="sxs-lookup"><span data-stu-id="58b95-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

**<span data-ttu-id="58b95-187">列表 5 –</span><span class="sxs-lookup"><span data-stu-id="58b95-187">Listing 5 –</span></span> `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="58b95-188">总结</span><span class="sxs-lookup"><span data-stu-id="58b95-188">Summary</span></span>

<span data-ttu-id="58b95-189">本教程向你提供的基本介绍查看母版页和内容页面。</span><span class="sxs-lookup"><span data-stu-id="58b95-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="58b95-190">您学习了如何创建新视图母版页和创建基于它们的视图内容页。</span><span class="sxs-lookup"><span data-stu-id="58b95-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="58b95-191">我们还探讨了如何修改视图母版页从特定视图内容页的内容。</span><span class="sxs-lookup"><span data-stu-id="58b95-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58b95-192">[上一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一页](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="58b95-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>

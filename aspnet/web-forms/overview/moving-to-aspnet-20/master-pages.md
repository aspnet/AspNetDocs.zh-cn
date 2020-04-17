---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |微软文档
author: rick-anderson
description: 成功网站的关键组件之一是外观一致。 在ASP.NET 1.x 中，开发人员使用用户控件来复制通用页面 elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543179"
---
# <a name="master-pages"></a><span data-ttu-id="3985a-104">母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-104">Master Pages</span></span>

<span data-ttu-id="3985a-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3985a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3985a-106">成功网站的关键组件之一是外观一致。</span><span class="sxs-lookup"><span data-stu-id="3985a-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="3985a-107">在ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制公共页面元素。</span><span class="sxs-lookup"><span data-stu-id="3985a-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="3985a-108">虽然这当然是一个可行的解决方案，但使用用户控件确实有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="3985a-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="3985a-109">例如，更改用户控件的位置需要更改到站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="3985a-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="3985a-110">在页面上插入后，用户控件也不会在"设计"视图中呈现。</span><span class="sxs-lookup"><span data-stu-id="3985a-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="3985a-111">成功网站的关键组件之一是外观一致。</span><span class="sxs-lookup"><span data-stu-id="3985a-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="3985a-112">在ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制公共页面元素。</span><span class="sxs-lookup"><span data-stu-id="3985a-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="3985a-113">虽然这当然是一个可行的解决方案，但使用用户控件确实有一些缺点。</span><span class="sxs-lookup"><span data-stu-id="3985a-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="3985a-114">例如，更改用户控件的位置需要更改到站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="3985a-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="3985a-115">在页面上插入后，用户控件也不会在"设计"视图中呈现。</span><span class="sxs-lookup"><span data-stu-id="3985a-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="3985a-116">ASP.NET 2.0 引入母版页作为保持一致外观和感觉的一种方式，正如您很快就会看到的那样，母版页代表了对用户控制方法的重大改进。</span><span class="sxs-lookup"><span data-stu-id="3985a-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="3985a-117">为什么选择母版页？</span><span class="sxs-lookup"><span data-stu-id="3985a-117">Why Master Pages?</span></span>

<span data-ttu-id="3985a-118">您可能想知道为什么 ASP.NET 2.0 需要母版页。</span><span class="sxs-lookup"><span data-stu-id="3985a-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="3985a-119">毕竟，网站开发人员已经在ASP.NET 1.x 中使用用户控件在页面之间共享内容区域。</span><span class="sxs-lookup"><span data-stu-id="3985a-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="3985a-120">实际上，用户控件是创建公共布局的不太理想的解决方案的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="3985a-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="3985a-121">用户控件实际上不定义页面布局。</span><span class="sxs-lookup"><span data-stu-id="3985a-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="3985a-122">相反，它们定义页面的一部分的布局和功能。</span><span class="sxs-lookup"><span data-stu-id="3985a-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="3985a-123">这两者之间的区别很重要，因为它使用户控制解决方案的可管理性变得更加困难。</span><span class="sxs-lookup"><span data-stu-id="3985a-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="3985a-124">例如，如果要更改页面上的用户控件的位置，必须编辑显示用户控件的实际页面。</span><span class="sxs-lookup"><span data-stu-id="3985a-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="3985a-125">如果你只有几页，这很好，但在大型网站，它迅速成为一个网站管理噩梦！</span><span class="sxs-lookup"><span data-stu-id="3985a-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="3985a-126">使用用户控件定义公共布局的另一个缺点是ASP.NET本身的体系结构。</span><span class="sxs-lookup"><span data-stu-id="3985a-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="3985a-127">如果更改了用户控件的任何公共成员，则需要重新编译使用用户控件的所有页面。</span><span class="sxs-lookup"><span data-stu-id="3985a-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="3985a-128">反过来，ASP.NET将在首次访问页面时重新 JIT。</span><span class="sxs-lookup"><span data-stu-id="3985a-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="3985a-129">这再次产生了一个不可扩展的体系结构和大型站点的站点管理问题。</span><span class="sxs-lookup"><span data-stu-id="3985a-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="3985a-130">ASP.NET 2.0 中的母版页很好地解决了这两个问题（以及更多问题）。</span><span class="sxs-lookup"><span data-stu-id="3985a-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="3985a-131">母版页的工作原理</span><span class="sxs-lookup"><span data-stu-id="3985a-131">How Master Pages Work</span></span>

<span data-ttu-id="3985a-132">母版页类似于其他页面的模板。</span><span class="sxs-lookup"><span data-stu-id="3985a-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="3985a-133">应在其他页面（即菜单、边框等）之间共享的页面元素将添加到母版页中。</span><span class="sxs-lookup"><span data-stu-id="3985a-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="3985a-134">将新页面添加到网站时，可以将它们与母版页相关联。</span><span class="sxs-lookup"><span data-stu-id="3985a-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="3985a-135">与母版页关联的页面称为**内容页**。</span><span class="sxs-lookup"><span data-stu-id="3985a-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="3985a-136">默认情况下，内容页从母版页中呈现外观。</span><span class="sxs-lookup"><span data-stu-id="3985a-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="3985a-137">但是，在创建母版页时，可以定义内容页可以替换为其自己的内容的部分内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="3985a-138">这些部分使用 ASP.NET 2.0 中引入的新控件进行定义;**ContentPlaceHolder 控件**。</span><span class="sxs-lookup"><span data-stu-id="3985a-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="3985a-139">母版页可以包含任意数量的 ContentPlaceHolder 控件（或根本没有。在内容页上，"ContentPlaceHolder"控件中的内容将显示在**内容**控件中，这是 ASP.NET 2.0 中的另一个新控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="3985a-140">默认情况下，内容页 内容控件为空，以便您可以提供自己的内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="3985a-141">如果要使用内容控件内母版页中的内容，可以执行此操作，正如您将在此模块的后面部分看到的。</span><span class="sxs-lookup"><span data-stu-id="3985a-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="3985a-142">内容控件通过内容控件的"内容霍尔德ID"属性映射到 ContentPlaceHolderId 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="3985a-143">下面的代码将内容控件映射到主页上称为 mainBody 的 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="3985a-144">您经常会听到人们将母版页描述为其他页面的基类。</span><span class="sxs-lookup"><span data-stu-id="3985a-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="3985a-145">这实际上不是真的。</span><span class="sxs-lookup"><span data-stu-id="3985a-145">Thats actually not true.</span></span> <span data-ttu-id="3985a-146">母版页和内容页之间的关系不是继承关系。</span><span class="sxs-lookup"><span data-stu-id="3985a-146">The relationship between master pages and content pages is not one of inheritance.</span></span>

<span data-ttu-id="3985a-147">**图 1**显示了母版页和关联的内容页，因为它们出现在 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="3985a-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="3985a-148">您可以在母版页中查看 ContentPlaceHolder 控件，并在内容页中看到相应的内容控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="3985a-149">请注意，内容霍尔德持有人外部的母版页内容可见，但在内容页中显示为灰色。</span><span class="sxs-lookup"><span data-stu-id="3985a-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="3985a-150">只有 ContentPlaceHolder 中的内容可以由内容页取代。</span><span class="sxs-lookup"><span data-stu-id="3985a-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="3985a-151">来自母版页的所有其他内容是不可改变的。</span><span class="sxs-lookup"><span data-stu-id="3985a-151">All other content that comes from the master page is immutable.</span></span>

![母版页及其关联内容页](master-pages/_static/image1.jpg)

<span data-ttu-id="3985a-153">**图 1**： 母版页及其关联内容页</span><span class="sxs-lookup"><span data-stu-id="3985a-153">**Figure 1**: A master page and its associated content page</span></span>

## <a name="creating-a-master-page"></a><span data-ttu-id="3985a-154">创建母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-154">Creating a Master Page</span></span>

<span data-ttu-id="3985a-155">要创建新的母版页，</span><span class="sxs-lookup"><span data-stu-id="3985a-155">To create a new master page:</span></span>

1. <span data-ttu-id="3985a-156">打开 Visual Studio 2005 并创建新网站。</span><span class="sxs-lookup"><span data-stu-id="3985a-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="3985a-157">单击"文件，新建，文件"。</span><span class="sxs-lookup"><span data-stu-id="3985a-157">Click File, New, File.</span></span>
3. <span data-ttu-id="3985a-158">从"添加新项目"对话框中选择主文件，如图**2**所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="3985a-159">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="3985a-159">Click Add.</span></span>

![创建新母版页](master-pages/_static/image2.jpg)

<span data-ttu-id="3985a-161">**图 2**： 创建新母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-161">**Figure 2**: Creating a New Master Page</span></span>

<span data-ttu-id="3985a-162">请注意，母版页的文件扩展名是 *.master*。</span><span class="sxs-lookup"><span data-stu-id="3985a-162">Notice that the file extension for a master page is *.master*.</span></span> <span data-ttu-id="3985a-163">这是母版页与普通页面不同的方式之一。</span><span class="sxs-lookup"><span data-stu-id="3985a-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="3985a-164">另一个主要区别是，母版页代替指令@Page，包含一个@Master指令。</span><span class="sxs-lookup"><span data-stu-id="3985a-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="3985a-165">切换到您刚刚创建的母版页的源视图并查看代码。</span><span class="sxs-lookup"><span data-stu-id="3985a-165">Switch to Source View for the master page you've just created and review the code.</span></span>

<span data-ttu-id="3985a-166">默认情况下，新的母版页将有一个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="3985a-167">在大多数情况下，首先创建公共页面元素，然后插入需要自定义内容的 ContentPlaceHolder 控件更有意义。</span><span class="sxs-lookup"><span data-stu-id="3985a-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="3985a-168">在这些情况下，开发人员将希望删除默认的 ContentPlaceHolder 控件，并在页面开发时插入新的控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="3985a-169">ContentPlaceHolder 控件虽然确实显示大小调整句柄，但它们不会调整大小。</span><span class="sxs-lookup"><span data-stu-id="3985a-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="3985a-170">ContentPlaceHolder 控件的大小会自动基于它包含的内容，但有一个例外;如果将 ContentPlaceHolder 控件放置在块元素（如表单元格）内，则该控件将根据元素的大小进行大小调整。</span><span class="sxs-lookup"><span data-stu-id="3985a-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="3985a-171">实验室 1 使用母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="3985a-172">在本实验中，您将创建一个新的母版页，并定义三个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="3985a-173">然后，您将创建新的内容页，并至少从其中一个 ContentPlaceHolder 控制中替换内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="3985a-174">创建母版页并插入内容霍尔德控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="3985a-175">如上文所述，创建新的母版页。</span><span class="sxs-lookup"><span data-stu-id="3985a-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="3985a-176">删除默认的"内容放置"控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="3985a-177">通过单击控件的上边框，然后点击键盘上的 DEL 键将其删除，选择 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="3985a-178">使用*标题和侧*模板插入新表，如图 3 所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="3985a-179">将宽度和高度更改为 90%，以便整个表在设计器中可见。</span><span class="sxs-lookup"><span data-stu-id="3985a-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>

![](master-pages/_static/image3.jpg)

<span data-ttu-id="3985a-180">**图 3**</span><span class="sxs-lookup"><span data-stu-id="3985a-180">**Figure 3**</span></span>

1. <span data-ttu-id="3985a-181">将光标放入表的每个单元格中，并将*valign*属性设置为*顶部*。</span><span class="sxs-lookup"><span data-stu-id="3985a-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="3985a-182">在工具箱中，在表的顶部单元格（标题单元格）中插入 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="3985a-183">插入此 ContentPlaceHolder 控件时，您会注意到行高度将占用几乎整个页面，如图 4 所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="3985a-184">在这一点上不要担心。</span><span class="sxs-lookup"><span data-stu-id="3985a-184">Don't be concerned about that at this point.</span></span>

![空白空间与内容霍尔德位于同一单元格中](master-pages/_static/image1.gif)

<span data-ttu-id="3985a-186">**图 4**： 空白空间与内容霍尔德位于同一单元格中</span><span class="sxs-lookup"><span data-stu-id="3985a-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>

1. <span data-ttu-id="3985a-187">将 ContentPlaceHolder 控件放在其他两个单元格中。</span><span class="sxs-lookup"><span data-stu-id="3985a-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="3985a-188">插入其他 ContentPlaceHolder 控件后，表单元格的大小应如您所料。</span><span class="sxs-lookup"><span data-stu-id="3985a-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="3985a-189">该页现在应类似于**图 5**所示的页面。</span><span class="sxs-lookup"><span data-stu-id="3985a-189">The page should now look like the page shown in **figure 5**.</span></span>

![包含所有内容位置所有者控件的主控形状。](master-pages/_static/image2.gif)

<span data-ttu-id="3985a-192">**图 5**： 包含所有内容霍尔德控件的主控形状。</span><span class="sxs-lookup"><span data-stu-id="3985a-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="3985a-193">请注意，头单元格的单元格高度现在正是它应该的</span><span class="sxs-lookup"><span data-stu-id="3985a-193">Notice that the cell height for the header cell is now what it should be</span></span>

1. <span data-ttu-id="3985a-194">在三个 ContentPlaceHolder 控件中的每个控件中输入您选择的文本。</span><span class="sxs-lookup"><span data-stu-id="3985a-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="3985a-195">将母版页另存为练习1.master。</span><span class="sxs-lookup"><span data-stu-id="3985a-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="3985a-196">创建新的 Web 窗体并将其与练习1.master 页相关联。</span><span class="sxs-lookup"><span data-stu-id="3985a-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="3985a-197">选择文件，新建，文件在可视化工作室2005年。</span><span class="sxs-lookup"><span data-stu-id="3985a-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="3985a-198">在"添加新项目"对话框中选择 **"Web 窗体**"。</span><span class="sxs-lookup"><span data-stu-id="3985a-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="3985a-199">确保选中"选择母版页"复选框，如图 6 所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>

![添加新的内容页](master-pages/_static/image3.gif)

<span data-ttu-id="3985a-201">**图 6**： 添加新的内容页</span><span class="sxs-lookup"><span data-stu-id="3985a-201">**Figure 6**: Adding a new Content Page</span></span>

1. <span data-ttu-id="3985a-202">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="3985a-202">Click Add.</span></span>
2. <span data-ttu-id="3985a-203">在"选择母版页对话框中选择练习1.master，如图 7 所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="3985a-204">单击"确定"以添加新内容页。</span><span class="sxs-lookup"><span data-stu-id="3985a-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="3985a-205">新内容页显示在 Visual Studio 中，母版页上每个 ContentPlaceHolder 控件都有一个内容控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="3985a-206">默认情况下，内容控件为空，以便您可以添加自己的内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="3985a-207">如果您希望他们使用母版页上的 ContentPlaceHolder 控件中的内容，只需单击智能标记符号（控件右上角的小黑箭头），然后从智能标记中选择 *"默认到母版内容*"，如图**8**所示。</span><span class="sxs-lookup"><span data-stu-id="3985a-207">If you'd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="3985a-208">执行此操作时，菜单项将更改为 *"创建自定义内容*"。</span><span class="sxs-lookup"><span data-stu-id="3985a-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="3985a-209">此时单击它会从母版页中删除内容，允许您为该特定内容控件定义自定义内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>

![将内容控件设置为默认为母版页内容](master-pages/_static/image4.gif)

<span data-ttu-id="3985a-211">**图 7**：将内容控件设置为默认为母版页内容</span><span class="sxs-lookup"><span data-stu-id="3985a-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>

## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="3985a-212">连接母版页和内容页</span><span class="sxs-lookup"><span data-stu-id="3985a-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="3985a-213">母版页和内容页之间的关联可以通过以下四种不同方式之一进行配置：</span><span class="sxs-lookup"><span data-stu-id="3985a-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="3985a-214">指令的@Page<strong>母版页面文件</strong>属性</span><span class="sxs-lookup"><span data-stu-id="3985a-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="3985a-215">在代码中设置**Page.MasterPageFile**属性。</span><span class="sxs-lookup"><span data-stu-id="3985a-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="3985a-216">应用程序配置文件中的**&lt;页面&gt;** 元素（应用程序根文件夹中的 Web.config）</span><span class="sxs-lookup"><span data-stu-id="3985a-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="3985a-217">子文件夹配置文件中的**&lt;页面&gt;** 元素（子文件夹中的 Web.config）</span><span class="sxs-lookup"><span data-stu-id="3985a-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="3985a-218">母版文件属性</span><span class="sxs-lookup"><span data-stu-id="3985a-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="3985a-219">MasterPageFile 属性使将母版页应用于特定ASP.NET页面变得容易。</span><span class="sxs-lookup"><span data-stu-id="3985a-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="3985a-220">当您选中 **"选择母版页**"复选框时，它也是用于应用母版页的方法，就像练习 1 中所做的那样。</span><span class="sxs-lookup"><span data-stu-id="3985a-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="3985a-221">设置页面.MasterPage文件代码</span><span class="sxs-lookup"><span data-stu-id="3985a-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="3985a-222">通过在代码中设置 MasterPageFile 属性，可以在运行时将特定的母版页应用于您的内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="3985a-223">在可能需要根据用户角色或其他一些条件应用特定母版页的情况下，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="3985a-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="3985a-224">必须在 PreInit 方法中设置 MasterPageFile 属性。</span><span class="sxs-lookup"><span data-stu-id="3985a-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="3985a-225">如果在 PreInit 方法之后设置，将引发无效操作异常。</span><span class="sxs-lookup"><span data-stu-id="3985a-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="3985a-226">正在设置此属性的页面还必须具有"内容"控件作为该页的顶级控件。</span><span class="sxs-lookup"><span data-stu-id="3985a-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="3985a-227">否则，在设置 MasterPageFile 属性时，将引发 HttpException。</span><span class="sxs-lookup"><span data-stu-id="3985a-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="3985a-228">使用&lt;页面&gt;元素</span><span class="sxs-lookup"><span data-stu-id="3985a-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="3985a-229">您可以通过在 Web.config 文件的&lt;页面&gt;元素中设置 masterPageFile 属性来配置页面的母版页。</span><span class="sxs-lookup"><span data-stu-id="3985a-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="3985a-230">使用此方法时，请记住，应用程序结构中较低的 Web.config 文件可以覆盖此设置。</span><span class="sxs-lookup"><span data-stu-id="3985a-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="3985a-231">@Page指令中的任何 MasterPageFile 属性集也将覆盖此设置。</span><span class="sxs-lookup"><span data-stu-id="3985a-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="3985a-232">使用&lt;页面&gt;元素可以创建可在特定文件夹或文件中在必要时重写*的主版*页变得简单。</span><span class="sxs-lookup"><span data-stu-id="3985a-232">Using the &lt;pages&gt; element makes it simple to create a *master* master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="3985a-233">母版页中的属性</span><span class="sxs-lookup"><span data-stu-id="3985a-233">Properties in Master Pages</span></span>

<span data-ttu-id="3985a-234">母版页只需在母版页中公开这些属性，即可公开属性。</span><span class="sxs-lookup"><span data-stu-id="3985a-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="3985a-235">例如，以下代码定义名为"某些属性"的属性：</span><span class="sxs-lookup"><span data-stu-id="3985a-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="3985a-236">要从"内容"页访问"某些属性"属性，您需要使用"主"属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3985a-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="3985a-237">嵌套母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-237">Nesting Master Pages</span></span>

<span data-ttu-id="3985a-238">母版页是确保大型 Web 应用程序的共同外观的完美解决方案。</span><span class="sxs-lookup"><span data-stu-id="3985a-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="3985a-239">但是，大型站点的某些部分共享公共接口，而其他部分共享不同的接口的情况并不少见。</span><span class="sxs-lookup"><span data-stu-id="3985a-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="3985a-240">为了满足这一需求，多个母版页是完美的解决方案。</span><span class="sxs-lookup"><span data-stu-id="3985a-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="3985a-241">但是，这仍然不能解决大型应用程序可能具有某些组件（例如菜单）这一事实，这些组件仅在网站的某些部分之间共享的所有页面和其他组件之间共享。</span><span class="sxs-lookup"><span data-stu-id="3985a-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="3985a-242">对于这种情况，嵌套母版页很好地满足了需求。</span><span class="sxs-lookup"><span data-stu-id="3985a-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="3985a-243">正如您所看到的，普通母版页由母版页和内容页组成。</span><span class="sxs-lookup"><span data-stu-id="3985a-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="3985a-244">在嵌套母版页的情况下，有两个母版页;父主控形状和子母版。</span><span class="sxs-lookup"><span data-stu-id="3985a-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="3985a-245">子母版页也是内容页，其母版页是父母版页。</span><span class="sxs-lookup"><span data-stu-id="3985a-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="3985a-246">下面是典型母版页的代码：</span><span class="sxs-lookup"><span data-stu-id="3985a-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="3985a-247">在嵌套主方案中，这将是父主控形状。</span><span class="sxs-lookup"><span data-stu-id="3985a-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="3985a-248">另一个母版页将使用此页作为其母版页，该代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="3985a-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="3985a-249">请注意，在这种情况下，子母版也是父主控形状的内容页。</span><span class="sxs-lookup"><span data-stu-id="3985a-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="3985a-250">所有子主控内容都显示在内容控件中，该控件从父级的 ContentPlaceHolder 控件中获取其内容。</span><span class="sxs-lookup"><span data-stu-id="3985a-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="3985a-251">设计器支持不适用于嵌套母版页。</span><span class="sxs-lookup"><span data-stu-id="3985a-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="3985a-252">使用嵌套母版进行开发时，需要使用源视图。</span><span class="sxs-lookup"><span data-stu-id="3985a-252">When you are developing using nested masters, you will need to use source view.</span></span>

<span data-ttu-id="3985a-253">此视频显示了使用嵌套母版页的演练。</span><span class="sxs-lookup"><span data-stu-id="3985a-253">This video shows a walkthrough of using nested master pages.</span></span>

![](master-pages/_static/image1.png)

[<span data-ttu-id="3985a-254">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="3985a-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)

![选择母版页](master-pages/_static/image4.jpg)

<span data-ttu-id="3985a-256">**图 8**： 选择母版页</span><span class="sxs-lookup"><span data-stu-id="3985a-256">**Figure 8**: Selecting a Master Page</span></span>

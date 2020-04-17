---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何使用 HTML 编辑器控件？ （C#） |微软文档
author: rick-anderson
description: HTMLEditor 是一个ASP.NET AJAX 控件，允许您通过工具栏中的按钮轻松创建和编辑 HTML 内容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: eb3a87f914c24ada52ebb5a315a7e242e96158f7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543114"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="57fa4-104">如何使用 HTML 编辑器控件？</span><span class="sxs-lookup"><span data-stu-id="57fa4-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="57fa4-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="57fa4-105">(C#)</span></span>

<span data-ttu-id="57fa4-106">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="57fa4-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="57fa4-107">HTMLEditor 是一个ASP.NET AJAX 控件，允许您通过工具栏中的按钮轻松创建和编辑 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="57fa4-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="57fa4-108">本教程的目标是为您提供 AJAX 控制工具包中包含的 HTML 编辑器控件的概述。</span><span class="sxs-lookup"><span data-stu-id="57fa4-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="57fa4-109">HTML 编辑器包括用于更改字体大小、选择字体、更改背景颜色、修改前景颜色、添加链接、添加图像、更改文本对齐以及执行剪切、复制和粘贴操作的选项（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="57fa4-110">[![HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="57fa4-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="57fa4-111">**图 01**： HTML 编辑器（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="57fa4-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="57fa4-112">HTML 编辑器允许您使用设计模式输入内容，也可以直接输入 HTML。</span><span class="sxs-lookup"><span data-stu-id="57fa4-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="57fa4-113">此外，您还可以提供预览 HTML 内容的选项（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="57fa4-114">[![设计、HTML 和预览按钮](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="57fa4-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="57fa4-115">**图 02**：设计、HTML 和预览按钮（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="57fa4-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="57fa4-116">在本教程中，您将了解如何显示 HTML 编辑器、如何自定义 HTML 编辑器中显示的工具栏按钮以及如何避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="57fa4-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="57fa4-117">显示 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="57fa4-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="57fa4-118">在ASP.NET页中使用 HTML 编辑器之前，必须先向该页添加脚本管理器控件。</span><span class="sxs-lookup"><span data-stu-id="57fa4-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="57fa4-119">脚本管理器控件位于可视化工作室/可视化 Web 开发人员快速工具箱中的 AJAX 扩展选项卡下方。</span><span class="sxs-lookup"><span data-stu-id="57fa4-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="57fa4-120">您应该在页面的任何其他控件之前将脚本管理器控件放在页面顶部。</span><span class="sxs-lookup"><span data-stu-id="57fa4-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="57fa4-121">例如，您可以将它放在打开的服务器端&lt;窗体&gt;标记的下方。</span><span class="sxs-lookup"><span data-stu-id="57fa4-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="57fa4-122">HTML 编辑器控件与 AJAX 控件工具包控件的其余部分一起位于工具箱中。</span><span class="sxs-lookup"><span data-stu-id="57fa4-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="57fa4-123">它被命名为编辑器控件（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="57fa4-124">[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="57fa4-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="57fa4-125">**图 03**： HTML 编辑器控件（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="57fa4-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="57fa4-126">将 HTML 编辑器拖到页面上后，可以在属性表中设置其属性。</span><span class="sxs-lookup"><span data-stu-id="57fa4-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="57fa4-127">例如，您通常要设置"宽度"和"高度"属性。</span><span class="sxs-lookup"><span data-stu-id="57fa4-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="57fa4-128">清单 1 包含包含 HTML 编辑器的ASP.NET页的源。</span><span class="sxs-lookup"><span data-stu-id="57fa4-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="57fa4-129">**清单 1 - 简单编辑器.aspx**</span><span class="sxs-lookup"><span data-stu-id="57fa4-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="57fa4-130">清单1中的页面包含 HTML 编辑器控件、按钮控件和文本控件。</span><span class="sxs-lookup"><span data-stu-id="57fa4-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="57fa4-131">单击该按钮时，HTML 编辑器的内容将显示在"文本"控件中（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="57fa4-132">[![使用 HTML 编辑器提交表单](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="57fa4-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="57fa4-133">**图 04**： 提交带有 HTML 编辑器的表单（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="57fa4-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="57fa4-134">HTML 编辑器内容属性用于检索输入到 HTML 编辑器中的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="57fa4-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="57fa4-135">请注意，此 HTML 内容可能包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="57fa4-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="57fa4-136">在下一节中，我们将讨论如何防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="57fa4-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="57fa4-137">自定义 HTML 编辑器工具栏</span><span class="sxs-lookup"><span data-stu-id="57fa4-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="57fa4-138">您可以准确自定义编辑器中显示的按钮。</span><span class="sxs-lookup"><span data-stu-id="57fa4-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="57fa4-139">例如，您可能希望删除 HTML 选项卡，以防止用户将 HTML 编辑器切换到 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="57fa4-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="57fa4-140">或者，您可能希望删除字体大小下拉列表，以防止用户在论坛消息帖子中创建过大的文本（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="57fa4-141">[![自定义 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="57fa4-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="57fa4-142">**图 05**： 自定义 HTML 编辑器（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="57fa4-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="57fa4-143">通过从基本编辑器类派生新的 HTML 编辑器来自定义工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="57fa4-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="57fa4-144">例如，清单 2 中的自定义编辑器仅包含粗体和斜体工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="57fa4-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="57fa4-145">所有其他工具栏按钮已被删除。</span><span class="sxs-lookup"><span data-stu-id="57fa4-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="57fa4-146">此外，HTML 选项卡已从编辑器的底部删除（但"设计和预览"选项卡仍然存在）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="57fa4-147">**清单2 -\_应用代码_自定义编辑器.cs**</span><span class="sxs-lookup"><span data-stu-id="57fa4-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="57fa4-148">您必须将清单 2 中的类添加到应用\_代码文件夹，以便自动编译该类。</span><span class="sxs-lookup"><span data-stu-id="57fa4-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="57fa4-149">如果网站中\_不存在应用代码文件夹，则只需添加该文件夹即可。</span><span class="sxs-lookup"><span data-stu-id="57fa4-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="57fa4-150">创建自定义编辑器后，可以将其添加到ASP.NET页，其方式与添加普通 HTML 编辑器的方式相同（请参阅清单 3）。</span><span class="sxs-lookup"><span data-stu-id="57fa4-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="57fa4-151">**清单3 - 显示自定义编辑器.aspx**</span><span class="sxs-lookup"><span data-stu-id="57fa4-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="57fa4-152">避免跨站点脚本 （XSS） 攻击</span><span class="sxs-lookup"><span data-stu-id="57fa4-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="57fa4-153">每当您接受用户的输入，并在网站上重新显示该输入时，您都有可能将网站打开以进行跨站点脚本 （XSS） 攻击。</span><span class="sxs-lookup"><span data-stu-id="57fa4-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="57fa4-154">理论上，恶意黑客可以提交 JavaScript 代码，这些代码在重新显示输入时将执行。</span><span class="sxs-lookup"><span data-stu-id="57fa4-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="57fa4-155">JavaScript 可用于窃取用户密码或其他敏感信息。</span><span class="sxs-lookup"><span data-stu-id="57fa4-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="57fa4-156">通常，在网页中显示之前，可以通过 HTML 编码从用户检索的任何输入来击败 XSS 攻击。</span><span class="sxs-lookup"><span data-stu-id="57fa4-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="57fa4-157">但是，HTML 编码 HTML 编辑器的输出不仅会编码&lt;脚本&gt;标记，还会对所有 HTML 标记进行编码。</span><span class="sxs-lookup"><span data-stu-id="57fa4-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="57fa4-158">换句话说，您将丢失所有格式，如字体类型、字体大小和背景颜色。</span><span class="sxs-lookup"><span data-stu-id="57fa4-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="57fa4-159">如果要从用户收集敏感信息（如密码、信用卡号码和社会保险号），则不应显示使用 HTML 编辑器从用户检索的未编码内容。</span><span class="sxs-lookup"><span data-stu-id="57fa4-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="57fa4-160">仅当您未重新播放 HTML 内容或受信任方向您的网站提交 HTML 内容的情况时，才应使用 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="57fa4-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="57fa4-161">例如，假设您正在创建一个博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="57fa4-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="57fa4-162">在这种情况下，在撰写博客文章时使用 HTML 编辑器是有意义的。</span><span class="sxs-lookup"><span data-stu-id="57fa4-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="57fa4-163">您是唯一提交博客文章的人，而且，大概，您可以相信自己不会提交恶意的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="57fa4-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="57fa4-164">但是，在允许匿名用户发表评论时，使用 HTML 编辑器是没有意义的。</span><span class="sxs-lookup"><span data-stu-id="57fa4-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="57fa4-165">在用户提交敏感信息（如密码）时，应特别小心。</span><span class="sxs-lookup"><span data-stu-id="57fa4-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="57fa4-166">恶意用户可能会发布包含用于窃取密码的 JavaScript 的注释。</span><span class="sxs-lookup"><span data-stu-id="57fa4-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="57fa4-167">总结</span><span class="sxs-lookup"><span data-stu-id="57fa4-167">Summary</span></span>

<span data-ttu-id="57fa4-168">在本教程中，您得到了 AJAX 控制工具包中包含的 HTML 编辑器控件的简要概述。</span><span class="sxs-lookup"><span data-stu-id="57fa4-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="57fa4-169">您学习了如何使用 HTML 编辑器从用户那里接受丰富内容并将内容提交到服务器。</span><span class="sxs-lookup"><span data-stu-id="57fa4-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="57fa4-170">我们还讨论了如何自定义 HTML 编辑器显示的工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="57fa4-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="57fa4-171">最后，您学习了在使用 HTML 编辑器接受潜在的恶意输入时，如何避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="57fa4-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="57fa4-172">下一页</span><span class="sxs-lookup"><span data-stu-id="57fa4-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)

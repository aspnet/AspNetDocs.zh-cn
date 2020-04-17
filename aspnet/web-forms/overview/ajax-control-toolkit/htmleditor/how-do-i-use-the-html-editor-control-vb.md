---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: 如何使用 HTML 编辑器控件？ （VB） |微软文档
author: rick-anderson
description: HTMLEditor 是一个ASP.NET AJAX 控件，允许您通过工具栏中的按钮轻松创建和编辑 HTML 内容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542828"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>如何使用 HTML 编辑器控件？ (VB)

由[微软](https://github.com/microsoft)

> HTMLEditor 是一个ASP.NET AJAX 控件，允许您通过工具栏中的按钮轻松创建和编辑 HTML 内容。

本教程的目标是为您提供 AJAX 控制工具包中包含的 HTML 编辑器控件的概述。 HTML 编辑器包括用于更改字体大小、选择字体、更改背景颜色、修改前景颜色、添加链接、添加图像、更改文本对齐以及执行剪切、复制和粘贴操作的选项（参见图 1）。

[![HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**图 01**： HTML 编辑器（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-vb/_static/image2.png)）

HTML 编辑器允许您使用设计模式输入内容，也可以直接输入 HTML。 此外，您还可以提供预览 HTML 内容的选项（参见图 2）。

[![设计、HTML 和预览按钮](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**图 02**：设计、HTML 和预览按钮（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-vb/_static/image4.png)）

在本教程中，您将了解如何显示 HTML 编辑器、如何自定义 HTML 编辑器中显示的工具栏按钮以及如何避免跨站点脚本攻击。

## <a name="displaying-the-html-editor"></a>显示 HTML 编辑器

在ASP.NET页中使用 HTML 编辑器之前，必须先向该页添加脚本管理器控件。 脚本管理器控件位于可视化工作室/可视化 Web 开发人员快速工具箱中的 AJAX 扩展选项卡下方。

您应该在页面的任何其他控件之前将脚本管理器控件放在页面顶部。 例如，您可以将它放在打开的服务器端&lt;窗体&gt;标记的下方。

HTML 编辑器控件与 AJAX 控件工具包控件的其余部分一起位于工具箱中。 它被命名为编辑器控件（参见图 3）。

[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**图 03**： HTML 编辑器控件（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-vb/_static/image6.png)）

将 HTML 编辑器拖到页面上后，可以在属性表中设置其属性。 例如，您通常要设置"宽度"和"高度"属性。 清单 1 包含包含 HTML 编辑器的ASP.NET页的源。

**清单 1 - 简单编辑器.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

清单1中的页面包含 HTML 编辑器控件、按钮控件和文本控件。 单击该按钮时，HTML 编辑器的内容将显示在"文本"控件中（参见图 4）。

[![使用 HTML 编辑器提交表单](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**图 04**： 提交带有 HTML 编辑器的表单（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-vb/_static/image8.png)）

HTML 编辑器内容属性用于检索输入到 HTML 编辑器中的 HTML 内容。 请注意，此 HTML 内容可能包含 JavaScript。 在下一节中，我们将讨论如何防止 JavaScript 注入攻击。

## <a name="customizing-the-html-editor-toolbar"></a>自定义 HTML 编辑器工具栏

您可以准确自定义编辑器中显示的按钮。 例如，您可能希望删除 HTML 选项卡，以防止用户将 HTML 编辑器切换到 HTML 模式。 或者，您可能希望删除字体大小下拉列表，以防止用户在论坛消息帖子中创建过大的文本（参见图 5）。

[![自定义 HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**图 05**： 自定义 HTML 编辑器（[单击以查看全尺寸图像](how-do-i-use-the-html-editor-control-vb/_static/image10.png)）

通过从基本编辑器类派生新的 HTML 编辑器来自定义工具栏按钮。 例如，清单 2 中的自定义编辑器仅包含粗体和斜体工具栏按钮。 所有其他工具栏按钮已被删除。 此外，HTML 选项卡已从编辑器的底部删除（但"设计和预览"选项卡仍然存在）。

**清单2 -\_应用代码_自定义编辑器.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

您必须将清单 2 中的类添加到应用\_代码文件夹，以便自动编译该类。 如果网站中\_不存在应用代码文件夹，则只需添加该文件夹即可。

创建自定义编辑器后，可以将其添加到ASP.NET页，其方式与添加普通 HTML 编辑器的方式相同（请参阅清单 3）。

**清单3 - 显示自定义编辑器.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>避免跨站点脚本 （XSS） 攻击

每当您接受用户的输入，并在网站上重新显示该输入时，您都有可能将网站打开以进行跨站点脚本 （XSS） 攻击。 理论上，恶意黑客可以提交 JavaScript 代码，这些代码在重新显示输入时将执行。 JavaScript 可用于窃取用户密码或其他敏感信息。

通常，在网页中显示之前，可以通过 HTML 编码从用户检索的任何输入来击败 XSS 攻击。 但是，HTML 编码 HTML 编辑器的输出不仅会编码&lt;脚本&gt;标记，还会对所有 HTML 标记进行编码。 换句话说，您将丢失所有格式，如字体类型、字体大小和背景颜色。

如果要从用户收集敏感信息（如密码、信用卡号码和社会保险号），则不应显示使用 HTML 编辑器从用户检索的未编码内容。 仅当您未重新播放 HTML 内容或受信任方向您的网站提交 HTML 内容的情况时，才应使用 HTML 编辑器。

例如，假设您正在创建一个博客应用程序。 在这种情况下，在撰写博客文章时使用 HTML 编辑器是有意义的。 您是唯一提交博客文章的人，而且，大概，您可以相信自己不会提交恶意的 JavaScript。 但是，在允许匿名用户发表评论时，使用 HTML 编辑器是没有意义的。 在用户提交敏感信息（如密码）时，应特别小心。 恶意用户可能会发布包含用于窃取密码的 JavaScript 的注释。

## <a name="summary"></a>总结

在本教程中，您得到了 AJAX 控制工具包中包含的 HTML 编辑器控件的简要概述。 您学习了如何使用 HTML 编辑器从用户那里接受丰富内容并将内容提交到服务器。 我们还讨论了如何自定义 HTML 编辑器显示的工具栏按钮。 最后，您学习了在使用 HTML 编辑器接受潜在的恶意输入时，如何避免跨站点脚本攻击。

> [!div class="step-by-step"]
> [上一篇](how-do-i-use-the-html-editor-control-cs.md)

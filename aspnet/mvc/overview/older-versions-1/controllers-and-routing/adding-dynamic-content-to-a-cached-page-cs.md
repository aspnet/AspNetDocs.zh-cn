---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 将动态内容添加到缓存页面 （C#） |微软文档
author: rick-anderson
description: 了解如何在同一页中混合动态和缓存的内容。 缓存后替换使您能够显示动态内容，如横幅播发。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c8cd70a15c1ae93f7cf9b0a026b37b07e489040
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542282"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>向缓存页添加动态内容 (C#)

由[微软](https://github.com/microsoft)

> 了解如何在同一页中混合动态和缓存的内容。 缓存后替换使您能够在已缓存的页面中显示动态内容，如横幅播发或新闻项目。

通过利用输出缓存，您可以显著提高ASP.NET MVC 应用程序的性能。 在每次请求页面时，该页可以生成一次，并缓存在多个用户的内存中，而不是每次请求页面时重新生成页面。

但有一个问题。 如果您需要在页面中显示动态内容，该怎么办？ 例如，假设您要在页面中显示横幅广告。 您不希望缓存横幅播发，以便每个用户看到相同的播发。 你不会这样赚钱的！

幸运的是，有一个简单的解决方案。 您可以利用称为*缓存后替换*ASP.NET框架的功能。 缓存后替换使您能够替换已缓存在内存中的页面中的动态内容。

通常，当您使用 [OutputCache] 属性输出缓存页面时，该页将缓存在服务器和客户端（Web 浏览器）上。 使用缓存后替换时，页面仅缓存在服务器上。

#### <a name="using-post-cache-substitution"></a>使用缓存后替换

使用缓存后替换需要两个步骤。 首先，您需要定义一个方法，该方法返回表示要在缓存页中显示的动态内容的字符串。 接下来，调用 HttpResponse.Write 替代（） 方法将动态内容注入页面。

例如，假设您要在缓存的页面中随机显示不同的新闻项目。 清单 1 中的类公开一个名为 RenderNews（）的方法，该方法从三个新闻项列表中随机返回一个新闻项。

**清单1 = 模型\新闻.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

要利用缓存后替换，请致电 HttpResponse.Write 替代（）方法。 Write替代（）方法设置代码，以动态内容替换缓存页的区域。 Write替代（）方法用于在清单2的视图中显示随机新闻项。

**清单 2 = 视图\home_Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

渲染新闻方法传递给写入替换（） 方法。 请注意，不调用 RenderNews 方法（没有括号）。 相反，对该方法的引用将传递给 Write 替代。）

已缓存索引视图。 视图由清单 3 中的控制器返回。 请注意，Index（） 操作用 [OutputCache] 属性进行修饰，该属性会导致索引视图缓存 60 秒。

**清单3 = 控制器\主控制器.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

即使缓存了 Index 视图，当您请求"索引"页时，也会显示不同的随机新闻项。 请求"索引"页时，页面显示的时间在 60 秒内不会更改（参见图 1）。 时间不变的事实证明页面被缓存了。 但是，Write替代（）方法（随机新闻项）注入的内容随每个请求而变化。

**图 1 = 在缓存的页面中注入动态新闻项目**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>在帮助器方法中使用缓存后替换

利用缓存后替换的一种更简单的方法是在自定义帮助器方法中封装对 Write 替代（） 方法的调用。 清单4中的帮助方法说明了此方法。

**清单4 = AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

清单4包含一个静态类，它公开了两种方法：渲染Banner（）和 RenderBanner内部（）。 RenderBanner（） 方法表示实际帮助器方法。 此方法扩展了标准ASP.NET MVC HtmlHelper 类，以便您可以像任何其他帮助器方法一样在视图中调用 Html.RenderBanner（）。

renderBanner（） 方法调用将 RenderBanner 内部（） 方法传递给 Write 替换（） 方法的 HttpResponse.Write 替换（） 方法。

RenderBanner 内部（） 方法是一种私有方法。 此方法不会作为帮助器方法公开。 RenderBanner 内部（） 方法从三个横幅广告图像列表中随机返回一个横幅广告图像。

清单5中修改后的索引视图说明了如何使用 RenderBanner（） 帮助器方法。 请注意，在视图&lt;顶部包含额外的&gt;%@ 导入 % 指令，用于导入 MvcApplication1.Helpers 命名空间。 如果忽略导入此命名空间，则 RenderBanner（） 方法将不会显示为 Html 属性上的方法。

**清单 5 = 视图\home_Index.aspx（使用 RenderBanner（） 方法）**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

请求清单 5 中由视图呈现的页面时，每个请求都会显示不同的横幅播发（参见图 2）。 页面被缓存，但横幅播发由 RenderBanner（） 帮助器方法动态注入。

**图 2 = 显示随机横幅播发的索引视图**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>总结

本教程介绍了如何动态更新缓存页中的内容。 您学习了如何使用 HttpResponse.Write 替代（） 方法，以便将动态内容注入缓存页面。 您还学习了如何在 HTML 帮助器方法中封装对 Write 替代（） 方法的调用。

尽可能利用缓存 ， 会对 Web 应用程序的性能产生显著影响。 如本教程中所述，即使您需要在页面中显示动态内容，您也可以利用缓存。

> [!div class="step-by-step"]
> [上一页](improving-performance-with-output-caching-cs.md)
> [下一页](creating-a-controller-cs.md)

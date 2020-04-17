---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 通过输出缓存 （C#） 提高性能 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何利用输出缓存来显著提高ASP.NET MVC Web 应用程序的性能。 你。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542711"
---
# <a name="improving-performance-with-output-caching-c"></a>通过输出缓存提升性能 (C#)

由[微软](https://github.com/microsoft)

> 在本教程中，您将了解如何利用输出缓存来显著提高ASP.NET MVC Web 应用程序的性能。 您将了解如何缓存从控制器操作返回的结果，以便在每次新用户调用该操作时都不需要创建相同的内容。

本教程的目的是说明如何通过利用输出缓存显著提高ASP.NET MVC 应用程序的性能。 输出缓存使您能够缓存控制器操作返回的内容。 这样，每次调用相同的控制器操作时，不需要生成相同的内容。

例如，假设您ASP.NET MVC 应用程序在名为 Index 的视图中显示数据库记录的列表。 通常，每次用户调用返回 Index 视图的控制器操作时，必须通过执行数据库查询从数据库检索数据库记录集。

另一方面，如果利用输出缓存，则可以避免在每次任何用户调用相同的控制器操作时执行数据库查询。 可以从缓存中检索视图，而不是从控制器操作中重新生成视图。 缓存使您能够避免在服务器上执行冗余工作。

## <a name="enabling-output-caching"></a>启用输出缓存

通过将 [OutputCache] 属性添加到单个控制器操作或整个控制器类来启用输出缓存。 例如，清单 1 中的控制器公开名为 Index（） 的操作。 索引（） 操作的输出缓存 10 秒。

**清单1 = 控制器\主控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

在 ASP.NET MVC 的 Beta 版本中，输出缓存不适用于像[http://www.MySite.com/](http://www.mysite.com/)的 URL。 相反，您必须输入像[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。 

在清单 1 中，索引（） 操作的输出缓存 10 秒。 如果您愿意，可以指定更长的缓存持续时间。 例如，如果要缓存控制器操作的输出一天，则可以指定 86400 秒（60 秒\*60 分钟\*24 小时）的缓存持续时间。

不能保证内容将在您指定的时间量内缓存。 当内存资源变低时，缓存将自动开始驱逐内容。

清单 1 中的主控制器返回清单 2 中的索引视图。 这个观点没有什么特别之处。 索引视图仅显示当前时间（参见图 1）。

**清单 2 = 视图\home_Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**图 1 = 缓存索引视图**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

如果通过在浏览器的地址栏中输入 URL /Home/Index 并反复点击浏览器中的"刷新/重新加载"按钮来多次调用 Index（） 操作，则 Index 视图显示的时间在 10 秒内不会更改。 将显示相同的时间，因为视图是缓存的。

请务必了解，对于访问应用程序的每个人，缓存相同的视图。 调用 Index（） 操作的任何人都可以获得相同的索引视图缓存版本。 这意味着 Web 服务器为索引视图提供服务而必须执行的工作量将大大减少。

清单2中的视图碰巧在做一些非常简单的事情。 视图仅显示当前时间。 但是，您可以同样轻松地缓存显示一组数据库记录的视图。 在这种情况下，每次调用返回视图的控制器操作时，就不需要从数据库中检索数据库记录集。 缓存可以减少 Web 服务器和数据库服务器必须执行的工作量。

不要在 MVC 视图中&lt;使用页面 %@&gt;输出缓存 % 指令。 此指令正在从 Web 窗体世界中出血，不应在 mVC 应用程序中ASP.NET中使用。

## <a name="where-content-is-cached"></a>缓存内容的位置

默认情况下，当您使用 [OutputCache] 属性时，内容缓存在三个位置：Web 服务器、任何代理服务器和 Web 浏览器。 您可以通过修改 [OutputCache] 属性的位置属性来准确控制内容的缓存位置。

您可以将"位置"属性设置为以下任一值：

> ·任何
> 
> ·客户
> 
> ·下游
> 
> ·服务器
> 
> ·没有
> 
> ·服务器和客户端

默认情况下，"位置"属性具有"Any"的值。 但是，在某些情况下，您可能只想在浏览器或服务器上缓存。 例如，如果要缓存针对每个用户进行个性化的信息，则不应在服务器上缓存信息。 如果要向不同的用户显示不同的信息，则应仅在客户端上缓存信息。

例如，清单 3 中的控制器公开名为 GetName（） 的操作，该操作返回当前用户名。 如果 Jack 登录到网站并调用 GetName（） 操作，则该操作将返回字符串"嗨杰克"。 如果，随后，Jill登录到网站并调用 GetName（） 操作，那么她也将得到字符串"嗨杰克"。 在 Jack 最初调用控制器操作后，字符串将缓存在 Web 服务器上，供所有用户使用。

**清单3 = 控制器\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

最有可能的是，清单 3 中的控制器不能以您想要的方式工作。 您不想向吉尔显示"嗨杰克"的消息。

不应在服务器缓存中缓存个性化内容。 但是，您可能希望在浏览器缓存中缓存个性化内容以提高性能。 如果在浏览器中缓存内容，并且用户多次调用同一控制器操作，则可以从浏览器缓存而不是服务器检索内容。

清单 4 中修改后的控制器缓存 GetName（） 操作的输出。 但是，内容仅缓存在浏览器上，而不是服务器上。 这样，当多个用户调用 GetName（） 方法时，每个人都会获得自己的用户名，而不是其他人的用户名。

**清单4 = 控制器\用户控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

请注意，清单 4 中的 [OutputCache] 属性包含一个位置属性设置为值输出缓存位置.客户端。 [输出缓存] 属性还包括 NoStore 属性。 NoStore 属性用于通知代理服务器和浏览器它们不应存储缓存内容的永久副本。

## <a name="varying-the-output-cache"></a>更改输出缓存

在某些情况下，您可能需要相同内容的不同缓存版本。 例如，假设您正在创建一个母版/详细信息页。 母版页显示电影标题的列表。 单击标题时，您将获得所选影片的详细信息。

如果缓存详细信息页，则无论单击哪个影片，都会显示同一影片的详细信息。 第一个用户选择的第一个影片将显示给所有将来的用户。

您可以通过利用 [OutputCache] 属性的 VaryByParam 属性来解决此问题。 此属性使您能够在窗体参数或查询字符串参数不同时创建相同内容的不同缓存版本。

例如，清单 5 中的控制器公开名为 Master（） 和详细信息（） 的两个操作。 Master（） 操作返回影片标题列表，详细信息（） 操作返回所选影片的详细信息。

**清单5 = 控制器\电影控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master（） 操作包括一个具有值"无"的 VaryByParam 属性。 调用 Master（） 操作时，将返回主视图的相同缓存版本。 忽略任何窗体参数或查询字符串参数（参见图 2）。

**图 2 = /电影/主视图**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**图 3 = /电影/详细信息视图**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

详细信息（） 操作包括一个带值"Id"的 VaryByParam 属性。 当将 Id 参数的不同值传递给控制器操作时，将生成"详细信息"视图的不同缓存版本。

请务必了解，使用 VaryByParam 属性会导致缓存更多，而不是更少。 为 Id 参数的每个不同版本创建"详细信息"视图的不同缓存版本。

您可以将 VaryByParam 属性设置为以下值：

> \*• 每当窗体或查询字符串参数发生变化时，都会创建不同的缓存版本。
> 
> 无 = 从不创建不同的缓存版本
> 
> 参数的分号列表 = 每当列表中的任何窗体或查询字符串参数发生变化时，创建不同的缓存版本

## <a name="creating-a-cache-profile"></a>创建缓存配置文件

作为通过修改 [OutputCache] 属性的属性来配置输出缓存属性的替代方法，您可以在 Web 配置 （web.config） 文件中创建缓存配置文件。 在 Web 配置文件中创建缓存配置文件具有几个重要优势。

首先，通过在 Web 配置文件中配置输出缓存，可以控制控制器操作如何在一个中心位置缓存内容。 您可以创建一个缓存配置文件，并将配置文件应用于多个控制器或控制器操作。

其次，您可以修改 Web 配置文件，而无需重新编译应用程序。 如果需要禁用已部署到生产中的应用程序的缓存，则只需修改 Web 配置文件中定义的缓存配置文件即可。 将自动检测并应用对 Web 配置文件的任何更改。

例如，清单&lt;6&gt;中的缓存 Web 配置部分定义名为 Cache1Hour 的缓存配置文件。 &lt;缓存&gt;部分必须出现在 Web 配置文件&lt;的 system.web&gt;部分中。

**清单6 = Web.config 的缓存部分**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

清单7中的控制器说明了如何将 Cache1Hour 配置文件应用于具有 [OutputCache] 属性的控制器操作。

**清单7 = 控制器\配置文件控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

如果调用清单 7 中控制器公开的 Index（） 操作，则将返回相同的时间 1 小时。

## <a name="summary"></a>总结

输出缓存为您提供了一种非常简单的方法来显著提高ASP.NET MVC 应用程序的性能。 在本教程中，您学习了如何使用 [OutputCache] 属性来缓存控制器操作的输出。 您还学习了如何修改 [OutputCache] 属性的属性，如持续时间和 VaryByParam 属性，以修改内容的缓存方式。 最后，您学习了如何在 Web 配置文件中定义缓存配置文件。

> [!div class="step-by-step"]
> [上一页](understanding-action-filters-cs.md)
> [下一页](adding-dynamic-content-to-a-cached-page-cs.md)

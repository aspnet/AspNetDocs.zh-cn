---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态类型化视图与 强类型视图 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702941"
---
# <a name="dynamic-v-strongly-typed-views"></a>动态类型化视图与 强类型化视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

有三种方法可以将信息从控制器传递到 ASP.NET MVC 3 中的视图：

1. 作为强类型化模型对象。
2. 使用动态)  (动态类型 @model
3. 使用 ViewBag

我编写了一个简单的 MVC 3 顶级博客应用程序，用于比较和对比动态和强类型化的视图。 该控制器首先提供博客的简单列表：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

右键单击 IndexNotStonglyTyped ( # A1 方法，并添加 Razor 视图。

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

请确保未选中 " **创建强类型视图** " 框。 生成的视图不包含太多内容：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

由于我们使用的是动态而不是强类型视图，intellisense 不能帮助我们。 完成的代码如下所示：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646 NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

现在，我们将添加一个强类型视图。 将以下代码添加到控制器：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

请注意，这与 topBlogs)  (的返回视图完全相同;作为非强类型视图调用。 右键单击 *StonglyTypedIndex ( # B1 * ，然后选择 " **添加视图**"。 这次选择 " **博客** 模型类"，然后选择 " **列表** " 作为基架模板。

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

在新的视图模板中，我们获得 intellisense 支持。

[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

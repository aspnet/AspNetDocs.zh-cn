---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 第6部分：使用数据批注进行模型验证 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第6部分介绍如何对模型 V 使用数据批注 .。。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044943"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a>第 6 部分：使用数据注释进行模型验证

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第6部分介绍如何使用数据批注进行模型验证。

我们在创建和编辑表单方面遇到了重大问题：它们未进行任何验证。 我们可以执行一些操作，例如将必填字段留空，或在 Price 字段中键入字母，将看到的第一个错误来自数据库。

我们可以通过将数据批注添加到我们的模型类来轻松地向应用程序添加验证。 数据批注允许我们描述要应用于模型属性的规则，ASP.NET MVC 将负责强制执行这些规则并向用户显示相应的消息。

## <a name="adding-validation-to-our-album-forms"></a>将验证添加到我们的相册窗体

我们将使用以下数据批注属性：

- **必需** –指示属性是必填字段
- **DisplayName** –定义要用于窗体字段和验证消息的文本
- **StringLength** –定义字符串字段的最大长度
- **范围** –为数值字段提供最大值和最小值
- **绑定** –在将参数或窗体值绑定到模型属性时列出要排除或包含的字段
- **ScaffoldColumn** –允许从编辑器窗体中隐藏字段

*注意：有关使用数据批注属性进行模型验证的详细信息，请参阅 MSDN 文档，网址为*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

打开唱片集类并向顶部添加以下 *using* 语句。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

接下来，更新属性以添加显示和验证属性，如下所示。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

在此过程中，我们还将流派和艺术家更改为虚拟属性。 这允许实体框架根据需要延迟加载它们。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

将这些属性添加到唱集模型后，我们的 "创建和编辑" 屏幕会立即开始验证字段并使用所选的显示名称 (例如唱片集画面 Url 而不是 AlbumArtUrl) 。 运行应用程序并浏览到/StoreManager/Create。

![](mvc-music-store-part-6/_static/image1.png)

接下来，我们将中断某些验证规则。 输入0价格，并将标题留空。 单击 "创建" 按钮时，将看到显示了验证错误消息的窗体，其中显示了哪些字段不满足我们定义的验证规则。

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>测试客户端验证

从应用程序的角度来看，服务器端验证非常重要，因为用户可以绕过客户端验证。 但是，仅实现服务器端验证的网页窗体出现三个重要问题。

1. 用户必须等待窗体发布、验证在服务器上，以及将响应发送到其浏览器。
2. 当用户更正某个字段以便现在传递验证规则时，用户不会立即获得反馈。
3. 我们会浪费服务器资源来执行验证逻辑，而不是利用用户的浏览器。

幸运的是，ASP.NET MVC 3 基架模板内置了客户端验证，无需额外的工作。

在 "标题" 字段中键入一个字母可满足验证要求，因此将立即删除验证消息。

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-5.md)
> [下一页](mvc-music-store-part-7.md)

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
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="454a7-104">第 6 部分：使用数据注释进行模型验证</span><span class="sxs-lookup"><span data-stu-id="454a7-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="454a7-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="454a7-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="454a7-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="454a7-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="454a7-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="454a7-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="454a7-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="454a7-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="454a7-109">第6部分介绍如何使用数据批注进行模型验证。</span><span class="sxs-lookup"><span data-stu-id="454a7-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="454a7-110">我们在创建和编辑表单方面遇到了重大问题：它们未进行任何验证。</span><span class="sxs-lookup"><span data-stu-id="454a7-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="454a7-111">我们可以执行一些操作，例如将必填字段留空，或在 Price 字段中键入字母，将看到的第一个错误来自数据库。</span><span class="sxs-lookup"><span data-stu-id="454a7-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="454a7-112">我们可以通过将数据批注添加到我们的模型类来轻松地向应用程序添加验证。</span><span class="sxs-lookup"><span data-stu-id="454a7-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="454a7-113">数据批注允许我们描述要应用于模型属性的规则，ASP.NET MVC 将负责强制执行这些规则并向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="454a7-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="454a7-114">将验证添加到我们的相册窗体</span><span class="sxs-lookup"><span data-stu-id="454a7-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="454a7-115">我们将使用以下数据批注属性：</span><span class="sxs-lookup"><span data-stu-id="454a7-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="454a7-116">**必需** –指示属性是必填字段</span><span class="sxs-lookup"><span data-stu-id="454a7-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="454a7-117">**DisplayName** –定义要用于窗体字段和验证消息的文本</span><span class="sxs-lookup"><span data-stu-id="454a7-117">**DisplayName** – Defines the text to use on form fields and validation messages</span></span>
- <span data-ttu-id="454a7-118">**StringLength** –定义字符串字段的最大长度</span><span class="sxs-lookup"><span data-stu-id="454a7-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="454a7-119">**范围** –为数值字段提供最大值和最小值</span><span class="sxs-lookup"><span data-stu-id="454a7-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="454a7-120">**绑定** –在将参数或窗体值绑定到模型属性时列出要排除或包含的字段</span><span class="sxs-lookup"><span data-stu-id="454a7-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="454a7-121">**ScaffoldColumn** –允许从编辑器窗体中隐藏字段</span><span class="sxs-lookup"><span data-stu-id="454a7-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="454a7-122">*注意：有关使用数据批注属性进行模型验证的详细信息，请参阅 MSDN 文档，网址为*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="454a7-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="454a7-123">打开唱片集类并向顶部添加以下 *using* 语句。</span><span class="sxs-lookup"><span data-stu-id="454a7-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="454a7-124">接下来，更新属性以添加显示和验证属性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="454a7-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="454a7-125">在此过程中，我们还将流派和艺术家更改为虚拟属性。</span><span class="sxs-lookup"><span data-stu-id="454a7-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="454a7-126">这允许实体框架根据需要延迟加载它们。</span><span class="sxs-lookup"><span data-stu-id="454a7-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="454a7-127">将这些属性添加到唱集模型后，我们的 "创建和编辑" 屏幕会立即开始验证字段并使用所选的显示名称 (例如唱片集画面 Url 而不是 AlbumArtUrl) 。</span><span class="sxs-lookup"><span data-stu-id="454a7-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="454a7-128">运行应用程序并浏览到/StoreManager/Create。</span><span class="sxs-lookup"><span data-stu-id="454a7-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="454a7-129">接下来，我们将中断某些验证规则。</span><span class="sxs-lookup"><span data-stu-id="454a7-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="454a7-130">输入0价格，并将标题留空。</span><span class="sxs-lookup"><span data-stu-id="454a7-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="454a7-131">单击 "创建" 按钮时，将看到显示了验证错误消息的窗体，其中显示了哪些字段不满足我们定义的验证规则。</span><span class="sxs-lookup"><span data-stu-id="454a7-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="454a7-132">测试客户端验证</span><span class="sxs-lookup"><span data-stu-id="454a7-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="454a7-133">从应用程序的角度来看，服务器端验证非常重要，因为用户可以绕过客户端验证。</span><span class="sxs-lookup"><span data-stu-id="454a7-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="454a7-134">但是，仅实现服务器端验证的网页窗体出现三个重要问题。</span><span class="sxs-lookup"><span data-stu-id="454a7-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="454a7-135">用户必须等待窗体发布、验证在服务器上，以及将响应发送到其浏览器。</span><span class="sxs-lookup"><span data-stu-id="454a7-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="454a7-136">当用户更正某个字段以便现在传递验证规则时，用户不会立即获得反馈。</span><span class="sxs-lookup"><span data-stu-id="454a7-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="454a7-137">我们会浪费服务器资源来执行验证逻辑，而不是利用用户的浏览器。</span><span class="sxs-lookup"><span data-stu-id="454a7-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="454a7-138">幸运的是，ASP.NET MVC 3 基架模板内置了客户端验证，无需额外的工作。</span><span class="sxs-lookup"><span data-stu-id="454a7-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="454a7-139">在 "标题" 字段中键入一个字母可满足验证要求，因此将立即删除验证消息。</span><span class="sxs-lookup"><span data-stu-id="454a7-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="454a7-140">[上一页](mvc-music-store-part-5.md)
> [下一页](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="454a7-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>

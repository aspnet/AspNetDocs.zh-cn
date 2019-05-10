---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 创建操作 (VB) |Microsoft Docs
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123452"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="d9b00-104">创建操作 (VB)</span><span class="sxs-lookup"><span data-stu-id="d9b00-104">Creating an Action (VB)</span></span>

<span data-ttu-id="d9b00-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d9b00-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d9b00-106">了解如何向 ASP.NET MVC 控制器中添加新操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="d9b00-107">了解有关该方法将被操作的要求。</span><span class="sxs-lookup"><span data-stu-id="d9b00-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="d9b00-108">本教程的目的是说明如何创建新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="d9b00-109">了解有关操作方法的要求。</span><span class="sxs-lookup"><span data-stu-id="d9b00-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="d9b00-110">你还了解如何避免方法公开为一个操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="d9b00-111">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="d9b00-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="d9b00-112">通过将新方法添加到控制器可将新的操作添加到控制器中。</span><span class="sxs-lookup"><span data-stu-id="d9b00-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="d9b00-113">例如，在列表 1 中的控制器包含名为 index （） 的操作和名为 SayHello() 操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="d9b00-114">这两种方法被称为操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="d9b00-115">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="d9b00-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="d9b00-116">以便公开到为操作领域，一种方法必须满足某些要求：</span><span class="sxs-lookup"><span data-stu-id="d9b00-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="d9b00-117">该方法必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="d9b00-117">The method must be public.</span></span>
- <span data-ttu-id="d9b00-118">该方法不能是静态方法。</span><span class="sxs-lookup"><span data-stu-id="d9b00-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="d9b00-119">该方法不能为扩展方法。</span><span class="sxs-lookup"><span data-stu-id="d9b00-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="d9b00-120">该方法不能为构造函数、 getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="d9b00-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="d9b00-121">方法不能有开放式泛型类型。</span><span class="sxs-lookup"><span data-stu-id="d9b00-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="d9b00-122">方法不是控制器基类的方法。</span><span class="sxs-lookup"><span data-stu-id="d9b00-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="d9b00-123">该方法不能包含**ref**或**出**参数。</span><span class="sxs-lookup"><span data-stu-id="d9b00-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="d9b00-124">请注意，没有任何限制控制器操作的返回类型。</span><span class="sxs-lookup"><span data-stu-id="d9b00-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="d9b00-125">控制器操作可以返回一个字符串，datetime 类型，或 void Random 类的实例。</span><span class="sxs-lookup"><span data-stu-id="d9b00-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="d9b00-126">ASP.NET MVC 框架将转换任何不是转换为字符串的操作结果的返回类型，并将呈现到浏览器的字符串。</span><span class="sxs-lookup"><span data-stu-id="d9b00-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="d9b00-127">添加时不违反这些要求到控制器的任何方法，该方法公开为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="d9b00-128">此处必须认真仔细。</span><span class="sxs-lookup"><span data-stu-id="d9b00-128">Be careful here.</span></span> <span data-ttu-id="d9b00-129">连接到 Internet 的任何人都可以调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="d9b00-130">例如，不要创建 DeleteMyWebsite() 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d9b00-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="d9b00-131">防止调用公共方法</span><span class="sxs-lookup"><span data-stu-id="d9b00-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="d9b00-132">如果需要在控制器类中创建一个公共方法，并且不想要公开为控制器操作方法，则可以防止该方法通过调用&lt;NonAction&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="d9b00-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="d9b00-133">例如，在代码清单 2 中的控制器包含一个名为 CompanySecrets() 用修饰的公共方法&lt;NonAction&gt;属性。</span><span class="sxs-lookup"><span data-stu-id="d9b00-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="d9b00-134">**Listing 2 - Controllers\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="d9b00-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="d9b00-135">如果你尝试通过在浏览器地址栏中键入 /Work/CompanySecrets 调用 CompanySecrets() 控制器操作然后将图 1 中收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="d9b00-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="d9b00-136">[![调用 NonAction 方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d9b00-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="d9b00-137">**图 01**:调用 NonAction 方法 ([单击此项可查看原尺寸图像](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d9b00-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d9b00-138">[上一页](creating-a-controller-vb.md)
> [下一页](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d9b00-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>

---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 创建操作 （VB） |微软文档
author: rick-anderson
description: 了解如何向ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542243"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="1fc71-104">创建操作 (VB)</span><span class="sxs-lookup"><span data-stu-id="1fc71-104">Creating an Action (VB)</span></span>

<span data-ttu-id="1fc71-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1fc71-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1fc71-106">了解如何向ASP.NET MVC 控制器添加新操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="1fc71-107">了解方法为操作的要求。</span><span class="sxs-lookup"><span data-stu-id="1fc71-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="1fc71-108">本教程的目的是解释如何创建新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="1fc71-109">了解操作方法的要求。</span><span class="sxs-lookup"><span data-stu-id="1fc71-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="1fc71-110">您还学习如何防止方法作为操作公开。</span><span class="sxs-lookup"><span data-stu-id="1fc71-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="1fc71-111">向控制器添加操作</span><span class="sxs-lookup"><span data-stu-id="1fc71-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="1fc71-112">通过将新方法添加到控制器，向控制器添加新操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="1fc71-113">例如，清单 1 中的控制器包含名为 Index（） 的操作和名为 SayHello（） 的操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="1fc71-114">这两种方法都公开为操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="1fc71-115">**清单1 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="1fc71-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="1fc71-116">为了作为一种行动暴露在宇宙中，一种方法必须满足某些要求：</span><span class="sxs-lookup"><span data-stu-id="1fc71-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="1fc71-117">该方法必须为公共。</span><span class="sxs-lookup"><span data-stu-id="1fc71-117">The method must be public.</span></span>
- <span data-ttu-id="1fc71-118">该方法不能是静态方法。</span><span class="sxs-lookup"><span data-stu-id="1fc71-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="1fc71-119">该方法不能是扩展方法。</span><span class="sxs-lookup"><span data-stu-id="1fc71-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="1fc71-120">该方法不能是构造函数、getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="1fc71-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="1fc71-121">该方法不能具有打开的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="1fc71-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="1fc71-122">该方法不是控制器基类的方法。</span><span class="sxs-lookup"><span data-stu-id="1fc71-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="1fc71-123">该方法不能包含**ref**或**out**参数。</span><span class="sxs-lookup"><span data-stu-id="1fc71-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="1fc71-124">请注意，对控制器操作的返回类型没有限制。</span><span class="sxs-lookup"><span data-stu-id="1fc71-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="1fc71-125">控制器操作可以返回字符串、DateTime、Random 类的实例或 void。</span><span class="sxs-lookup"><span data-stu-id="1fc71-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="1fc71-126">ASP.NET MVC 框架将任何不是操作结果的返回类型转换为字符串，并将字符串呈现给浏览器。</span><span class="sxs-lookup"><span data-stu-id="1fc71-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="1fc71-127">将不违反这些要求的任何方法添加到控制器时，该方法将作为控制器操作公开。</span><span class="sxs-lookup"><span data-stu-id="1fc71-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="1fc71-128">这里要小心。</span><span class="sxs-lookup"><span data-stu-id="1fc71-128">Be careful here.</span></span> <span data-ttu-id="1fc71-129">连接到 Internet 的任何人都可以调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="1fc71-130">例如，不要创建"删除 My网站"控制器操作。</span><span class="sxs-lookup"><span data-stu-id="1fc71-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="1fc71-131">防止调用公共方法</span><span class="sxs-lookup"><span data-stu-id="1fc71-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="1fc71-132">如果需要在控制器类中创建公共方法，并且不希望将该方法公开为控制器操作，则可以使用&lt;NonAction&gt;属性阻止调用该方法。</span><span class="sxs-lookup"><span data-stu-id="1fc71-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="1fc71-133">例如，清单 2 中的控制器包含一个名为"公司机密（）"的公共方法，该方法使用&lt;非操作&gt;属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="1fc71-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="1fc71-134">**清单2 - 控制器\工作控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="1fc71-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="1fc71-135">如果您尝试通过在浏览器的地址栏中键入 /Work/公司机密来调用公司机密（） 控制器操作，则会收到图 1 中的错误消息。</span><span class="sxs-lookup"><span data-stu-id="1fc71-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="1fc71-136">[![调用非操作方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1fc71-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="1fc71-137">**图 01**：调用非操作方法（[单击以查看全尺寸图像](creating-an-action-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="1fc71-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1fc71-138">[上一页](creating-a-controller-vb.md)
> [下一页](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1fc71-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>

---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 使用服务层进行验证（VB） |Microsoft Docs
author: StephenWalther
description: 了解如何将验证逻辑移出控制器操作和单独的服务层。 在本教程中，Stephen Walther 介绍了如何 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436574"
---
# <a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="f6427-104">使用服务层进行验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="f6427-104">Validating with a Service Layer (VB)</span></span>

<span data-ttu-id="f6427-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="f6427-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="f6427-106">了解如何将验证逻辑移出控制器操作和单独的服务层。</span><span class="sxs-lookup"><span data-stu-id="f6427-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="f6427-107">在本教程中，Stephen Walther 介绍了如何通过将服务层与控制器层隔离来保持重要的关注点。</span><span class="sxs-lookup"><span data-stu-id="f6427-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="f6427-108">本教程的目的是介绍在 ASP.NET MVC 应用程序中执行验证的一种方法。</span><span class="sxs-lookup"><span data-stu-id="f6427-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="f6427-109">在本教程中，将了解如何将验证逻辑移出控制器，并将其移到单独的服务层。</span><span class="sxs-lookup"><span data-stu-id="f6427-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="f6427-110">分离关注点</span><span class="sxs-lookup"><span data-stu-id="f6427-110">Separating Concerns</span></span>

<span data-ttu-id="f6427-111">生成 ASP.NET MVC 应用程序时，不应将数据库逻辑放在控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="f6427-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="f6427-112">混合数据库和控制器逻辑使应用程序在一段时间内更难以维护。</span><span class="sxs-lookup"><span data-stu-id="f6427-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="f6427-113">建议将所有数据库逻辑放在单独的存储库层中。</span><span class="sxs-lookup"><span data-stu-id="f6427-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="f6427-114">例如，列表1包含一个名为 "化 productrepository" 的简单存储库。</span><span class="sxs-lookup"><span data-stu-id="f6427-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="f6427-115">产品存储库包含应用程序的所有数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="f6427-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="f6427-116">此列表还包括产品存储库实现的 IProductRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="f6427-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="f6427-117">**列表 1-Models\ProductRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="f6427-118">清单2中的控制器在其 Index （）和 Create （）操作中使用存储库层。</span><span class="sxs-lookup"><span data-stu-id="f6427-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="f6427-119">请注意，此控制器不包含任何数据库逻辑。</span><span class="sxs-lookup"><span data-stu-id="f6427-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="f6427-120">通过创建存储库层，可以保持完全分离的问题。</span><span class="sxs-lookup"><span data-stu-id="f6427-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="f6427-121">控制器负责应用程序流控制逻辑，而存储库负责数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="f6427-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="f6427-122">**列表 2-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="f6427-123">创建服务层</span><span class="sxs-lookup"><span data-stu-id="f6427-123">Creating a Service Layer</span></span>

<span data-ttu-id="f6427-124">因此，应用程序流控制逻辑属于控制器，数据访问逻辑位于存储库中。</span><span class="sxs-lookup"><span data-stu-id="f6427-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="f6427-125">在这种情况下，你要将验证逻辑放在哪个位置？</span><span class="sxs-lookup"><span data-stu-id="f6427-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="f6427-126">一种选择是将验证逻辑放在*服务层*中。</span><span class="sxs-lookup"><span data-stu-id="f6427-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="f6427-127">服务层是 ASP.NET MVC 应用程序中的一个额外层，用于调节控制器和存储库层之间的通信。</span><span class="sxs-lookup"><span data-stu-id="f6427-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="f6427-128">服务层包含业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="f6427-128">The service layer contains business logic.</span></span> <span data-ttu-id="f6427-129">具体而言，它包含验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="f6427-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="f6427-130">例如，清单3中的产品服务层具有一个 CreateProduct （）方法。</span><span class="sxs-lookup"><span data-stu-id="f6427-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="f6427-131">CreateProduct （）方法调用 ValidateProduct （）方法，在将产品传递到产品存储库之前验证新产品。</span><span class="sxs-lookup"><span data-stu-id="f6427-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="f6427-132">**列表 3-Models\ProductService.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="f6427-133">产品控制器已在清单4中更新，以使用服务层而不是存储库层。</span><span class="sxs-lookup"><span data-stu-id="f6427-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="f6427-134">控制器层将与服务层通信。</span><span class="sxs-lookup"><span data-stu-id="f6427-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="f6427-135">服务层与存储库层通信。</span><span class="sxs-lookup"><span data-stu-id="f6427-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="f6427-136">每个层都有单独的责任。</span><span class="sxs-lookup"><span data-stu-id="f6427-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="f6427-137">**列表 4-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="f6427-138">请注意，产品服务是在产品控制器构造函数中创建的。</span><span class="sxs-lookup"><span data-stu-id="f6427-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="f6427-139">创建产品服务时，模型状态字典将传递给服务。</span><span class="sxs-lookup"><span data-stu-id="f6427-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="f6427-140">产品服务使用模型状态将验证错误消息传递回控制器。</span><span class="sxs-lookup"><span data-stu-id="f6427-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="f6427-141">分离服务层</span><span class="sxs-lookup"><span data-stu-id="f6427-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="f6427-142">我们无法将控制器层和服务层相互隔离。</span><span class="sxs-lookup"><span data-stu-id="f6427-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="f6427-143">控制器和服务层通过模型状态进行通信。</span><span class="sxs-lookup"><span data-stu-id="f6427-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="f6427-144">换言之，服务层依赖于 ASP.NET MVC 框架的特定功能。</span><span class="sxs-lookup"><span data-stu-id="f6427-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="f6427-145">我们希望尽可能将服务层与控制器层隔离开来。</span><span class="sxs-lookup"><span data-stu-id="f6427-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="f6427-146">从理论上讲，我们应该能够将服务层用于任何类型的应用程序，而不仅是一个 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f6427-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="f6427-147">例如，在将来，我们可能要为应用程序生成 WPF 前端。</span><span class="sxs-lookup"><span data-stu-id="f6427-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="f6427-148">我们会发现一种从我们的服务层中删除 ASP.NET MVC 模型状态的依赖项的方法。</span><span class="sxs-lookup"><span data-stu-id="f6427-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="f6427-149">在列表5中，已更新服务层，使其不再使用模型状态。</span><span class="sxs-lookup"><span data-stu-id="f6427-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="f6427-150">相反，它使用实现 IValidationDictionary 接口的任何类。</span><span class="sxs-lookup"><span data-stu-id="f6427-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="f6427-151">**列表 5-Models\ProductService.vb （分离）**</span><span class="sxs-lookup"><span data-stu-id="f6427-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="f6427-152">IValidationDictionary 接口在列表6中定义。</span><span class="sxs-lookup"><span data-stu-id="f6427-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="f6427-153">此简单接口有一个方法和一个属性。</span><span class="sxs-lookup"><span data-stu-id="f6427-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="f6427-154">**列表 6-Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="f6427-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="f6427-155">名为 ModelStateWrapper 类的清单7中的类实现 IValidationDictionary 接口。</span><span class="sxs-lookup"><span data-stu-id="f6427-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="f6427-156">可以通过将模型状态字典传递到构造函数来实例化 ModelStateWrapper 类。</span><span class="sxs-lookup"><span data-stu-id="f6427-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="f6427-157">**列表 7-Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="f6427-158">最后，在其构造函数中创建服务层时，列表8中的更新的控制器使用 ModelStateWrapper。</span><span class="sxs-lookup"><span data-stu-id="f6427-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="f6427-159">**列表 8-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="f6427-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="f6427-160">通过使用 IValidationDictionary 接口和 ModelStateWrapper 类，我们可以将我们的服务层从控制器层中完全隔离开来。</span><span class="sxs-lookup"><span data-stu-id="f6427-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="f6427-161">服务层不再依赖于模型状态。</span><span class="sxs-lookup"><span data-stu-id="f6427-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="f6427-162">可以将实现 IValidationDictionary 接口的任何类传递到服务层。</span><span class="sxs-lookup"><span data-stu-id="f6427-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="f6427-163">例如，WPF 应用程序可使用简单的集合类实现 IValidationDictionary 接口。</span><span class="sxs-lookup"><span data-stu-id="f6427-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="f6427-164">摘要</span><span class="sxs-lookup"><span data-stu-id="f6427-164">Summary</span></span>

<span data-ttu-id="f6427-165">本教程的目的是讨论在 ASP.NET MVC 应用程序中执行验证的一种方法。</span><span class="sxs-lookup"><span data-stu-id="f6427-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="f6427-166">在本教程中，已学习如何将所有验证逻辑移出控制器并移到单独的服务层。</span><span class="sxs-lookup"><span data-stu-id="f6427-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="f6427-167">还了解了如何通过创建 ModelStateWrapper 类将服务层与控制器层隔离开来。</span><span class="sxs-lookup"><span data-stu-id="f6427-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6427-168">[上一页](validating-with-the-idataerrorinfo-interface-vb.md)
> [下一页](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f6427-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>

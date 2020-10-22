---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 通过 PayPal 结帐和支付 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 .。。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345657"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="47415-103">使用 PayPal 结帐和付款</span><span class="sxs-lookup"><span data-stu-id="47415-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="47415-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="47415-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="47415-105">[下载 Wingtip 玩具示例项目 (c # ) ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 或 [下载电子书 (PDF) ](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="47415-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="47415-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="47415-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="47415-107">此教程系列附带有 [c # 源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="47415-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="47415-108">本教程介绍如何使用 PayPal 修改 Wingtip 玩具示例应用程序，以包括用户授权、注册和付款。</span><span class="sxs-lookup"><span data-stu-id="47415-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="47415-109">只有登录的用户才有权购买产品。</span><span class="sxs-lookup"><span data-stu-id="47415-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="47415-110">ASP.NET 4.5 Web 窗体项目模板的内置用户注册功能已包含所需的大部分内容。</span><span class="sxs-lookup"><span data-stu-id="47415-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="47415-111">你将添加 PayPal Express 结帐功能。</span><span class="sxs-lookup"><span data-stu-id="47415-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="47415-112">在本教程中，你将使用 PayPal 开发人员测试环境，因此不会传输实际资金。</span><span class="sxs-lookup"><span data-stu-id="47415-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="47415-113">在本教程结束时，你将通过选择要添加到购物车中的产品，单击 "结帐" 按钮，然后将数据传输到 PayPal 测试网站来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="47415-114">在 PayPal 测试网站上，您将确认您的运费和付款信息，然后返回到本地 Wingtip 玩具示例应用程序以确认并完成购买。</span><span class="sxs-lookup"><span data-stu-id="47415-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="47415-115">有几个经验丰富的第三方支付处理器专用于在线购物，以应对可伸缩性和安全性。</span><span class="sxs-lookup"><span data-stu-id="47415-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="47415-116">ASP.NET 开发人员应考虑利用第三方支付解决方案的优点，然后再实施购物和采购解决方案。</span><span class="sxs-lookup"><span data-stu-id="47415-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47415-117">Wingtip 玩具示例应用程序旨在演示 ASP.NET web 开发人员可用的特定 ASP.NET 概念和功能。</span><span class="sxs-lookup"><span data-stu-id="47415-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="47415-118">此示例应用程序未针对可伸缩性和安全性方面的所有可能情况进行优化。</span><span class="sxs-lookup"><span data-stu-id="47415-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="47415-119">学习内容：</span><span class="sxs-lookup"><span data-stu-id="47415-119">What you'll learn:</span></span>

- <span data-ttu-id="47415-120">如何限制对文件夹中特定页面的访问。</span><span class="sxs-lookup"><span data-stu-id="47415-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="47415-121">如何从匿名购物车创建已知购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="47415-122">如何为项目启用 SSL。</span><span class="sxs-lookup"><span data-stu-id="47415-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="47415-123">如何将 OAuth 提供程序添加到项目。</span><span class="sxs-lookup"><span data-stu-id="47415-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="47415-124">如何使用 PayPal 测试环境购买产品。</span><span class="sxs-lookup"><span data-stu-id="47415-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="47415-125">如何在 **DetailsView** 控件中显示 PayPal 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="47415-126">如何用从 PayPal 获得的详细信息更新 Wingtip 玩具应用程序的数据库。</span><span class="sxs-lookup"><span data-stu-id="47415-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="47415-127">添加订单跟踪</span><span class="sxs-lookup"><span data-stu-id="47415-127">Adding Order Tracking</span></span>

<span data-ttu-id="47415-128">在本教程中，你将创建两个新类来跟踪用户创建的顺序中的数据。</span><span class="sxs-lookup"><span data-stu-id="47415-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="47415-129">类将跟踪有关装运信息、采购总额和付款确认的数据。</span><span class="sxs-lookup"><span data-stu-id="47415-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="47415-130">添加 Order 和 OrderDetail 模型类</span><span class="sxs-lookup"><span data-stu-id="47415-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="47415-131">在本教程的前面部分中，通过在 `Category` `Product` `CartItem` " *模型* " 文件夹中创建、和类，为类别、产品和购物车项目定义了架构。</span><span class="sxs-lookup"><span data-stu-id="47415-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="47415-132">现在，您将添加两个新类来定义产品订单的架构和订单的详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="47415-133">在 " **模型** " 文件夹中，添加名为 *Order.cs*的新类。</span><span class="sxs-lookup"><span data-stu-id="47415-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="47415-134">新的类文件将显示在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="47415-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="47415-135">将默认代码替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="47415-136">将 *OrderDetail.cs* 类添加到 " *模型* " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="47415-137">将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="47415-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="47415-138">`Order`和 `OrderDetail` 类包含架构以定义用于购买和装运的订单信息。</span><span class="sxs-lookup"><span data-stu-id="47415-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="47415-139">此外，您还需要更新管理实体类的数据库上下文类，并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="47415-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="47415-140">为此，您将向类中添加新创建的顺序和 `OrderDetail` 模型类 `ProductContext` 。</span><span class="sxs-lookup"><span data-stu-id="47415-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="47415-141">在 **解决方案资源管理器**中，找到并打开 *ProductContext.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="47415-142">将突出显示的代码添加到 *ProductContext.cs* 文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="47415-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="47415-143">如本系列教程前面所述， *ProductContext.cs* 文件中的代码将添加 `System.Data.Entity` 命名空间，以便您有权访问实体框架的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="47415-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="47415-144">此功能包括使用强类型对象查询、插入、更新和删除数据的功能。</span><span class="sxs-lookup"><span data-stu-id="47415-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="47415-145">类中的上述代码 `ProductContext` 将实体框架访问添加到新添加的 `Order` 和 `OrderDetail` 类。</span><span class="sxs-lookup"><span data-stu-id="47415-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="47415-146">添加结帐访问</span><span class="sxs-lookup"><span data-stu-id="47415-146">Adding Checkout Access</span></span>

<span data-ttu-id="47415-147">Wingtip 玩具示例应用程序允许匿名用户查看产品并将其添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="47415-148">但是，当匿名用户选择购买其添加到购物车的产品时，他们必须登录到网站。</span><span class="sxs-lookup"><span data-stu-id="47415-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="47415-149">登录后，他们可以访问处理结帐和购买过程的 Web 应用程序的受限页面。</span><span class="sxs-lookup"><span data-stu-id="47415-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="47415-150">这些受限页面包含在应用程序的 " *签出* " 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="47415-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="47415-151">添加结帐文件夹和页面</span><span class="sxs-lookup"><span data-stu-id="47415-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="47415-152">你现在将创建 *结帐* 文件夹和其中的页面，客户将在结帐过程中看到该文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="47415-153">稍后将在本教程中更新这些页面。</span><span class="sxs-lookup"><span data-stu-id="47415-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="47415-154">右键单击 " **Wingtip 玩具**) 中的项目名称 (**解决方案资源管理器** 并选择" **添加新文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="47415-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![通过 PayPal 结帐和付款-新建文件夹](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="47415-156">将新文件夹命名为 " *签出*"。</span><span class="sxs-lookup"><span data-stu-id="47415-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="47415-157">右键单击 "*签出*" 文件夹，然后选择 "**添加** - &gt; **新项**"。</span><span class="sxs-lookup"><span data-stu-id="47415-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![通过 PayPal 结帐和付款-新项目](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="47415-159">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="47415-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="47415-160">选择左侧的 " **Visual c #**  - &gt; **Web**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="47415-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="47415-161">然后，在中间窗格中，选择 " **带有母版页的 Web 窗体**" 并将其命名为 *CheckoutStart*。</span><span class="sxs-lookup"><span data-stu-id="47415-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![通过 PayPal 结帐和付款-"添加新项" 对话框](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="47415-163">与之前一样，选择 " *网站* " 作为母版页。</span><span class="sxs-lookup"><span data-stu-id="47415-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="47415-164">使用上述相同步骤将以下附加页面添加到 *结帐* 文件夹：</span><span class="sxs-lookup"><span data-stu-id="47415-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="47415-165">CheckoutReview .aspx</span><span class="sxs-lookup"><span data-stu-id="47415-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="47415-166">CheckoutComplete .aspx</span><span class="sxs-lookup"><span data-stu-id="47415-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="47415-167">CheckoutCancel .aspx</span><span class="sxs-lookup"><span data-stu-id="47415-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="47415-168">CheckoutError .aspx</span><span class="sxs-lookup"><span data-stu-id="47415-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="47415-169">添加 Web.config 文件</span><span class="sxs-lookup"><span data-stu-id="47415-169">Add a Web.config File</span></span>

<span data-ttu-id="47415-170">通过将新的 *Web.config* 文件添加到 *结帐* 文件夹，你将能够限制对文件夹中包含的所有页面的访问。</span><span class="sxs-lookup"><span data-stu-id="47415-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="47415-171">右键单击 "*签出*" 文件夹，然后选择 "**添加**  - &gt; **新项**"。</span><span class="sxs-lookup"><span data-stu-id="47415-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="47415-172">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="47415-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="47415-173">选择左侧的 " **Visual c #**  - &gt; **Web**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="47415-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="47415-174">然后，从中间窗格中选择 " **Web 配置文件**"，接受默认名称 " *Web.config*"，然后选择 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="47415-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="47415-175">将 *Web.config* 文件中的现有 XML 内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="47415-176">保存 *Web.config* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="47415-177">*Web.config*文件指定必须对 Web 应用程序的所有未知用户拒绝对*签出*文件夹中包含的页的访问权限。</span><span class="sxs-lookup"><span data-stu-id="47415-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="47415-178">但是，如果用户注册了某个帐户并登录，则这些用户将是已知用户，并且将有权访问 *签出* 文件夹中的页面。</span><span class="sxs-lookup"><span data-stu-id="47415-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="47415-179">需要注意的是，ASP.NET 配置遵循层次结构，其中每个 *Web.config* 文件都将配置设置应用到它所在的文件夹以及其下的所有子目录。</span><span class="sxs-lookup"><span data-stu-id="47415-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="47415-180">为项目启用 SSL</span><span class="sxs-lookup"><span data-stu-id="47415-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="47415-181">安全套接字层 (SSL) 是一种协议，定义为允许 Web 服务器与 Web 客户端通过使用加密以更安全的方式通信。</span><span class="sxs-lookup"><span data-stu-id="47415-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="47415-182">如果不使用 SSL，在客户端与服务器之间发送数据时，对网络具有实际访问权限的任何人都可以探查数据包。</span><span class="sxs-lookup"><span data-stu-id="47415-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="47415-183">此外，通过一般 HTTP 进行的几种常见身份验证方案也是不安全的。</span><span class="sxs-lookup"><span data-stu-id="47415-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="47415-184">尤其是，基本身份验证和窗体身份验证会发送未加密的凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="47415-185">为确保安全，这些身份验证方案必须使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="47415-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="47415-186">在 **解决方案资源管理器**中，单击 " **WingtipToys** " 项目，然后按 **F4** 以显示 " **属性** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="47415-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="47415-187">将 **SSL** 更改为启用 `true` 。</span><span class="sxs-lookup"><span data-stu-id="47415-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="47415-188">复制 **SSL URL** 以便以后使用。</span><span class="sxs-lookup"><span data-stu-id="47415-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="47415-189">SSL URL 将为， `https://localhost:44300/` 除非你之前已创建 Ssl 网站 (如下) 所示。</span><span class="sxs-lookup"><span data-stu-id="47415-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="47415-190">![项目属性](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="47415-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="47415-191">在 **解决方案资源管理器**中，右键单击 **WingtipToys** 项目，然后单击 " **属性**"。</span><span class="sxs-lookup"><span data-stu-id="47415-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="47415-192">在左侧选项卡中，单击 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="47415-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="47415-193">将 " **项目 Url** " 更改为使用前面保存的 **SSL Url** 。</span><span class="sxs-lookup"><span data-stu-id="47415-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="47415-194">![项目 Web 属性](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="47415-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="47415-195">按 **CTRL + S**保存页面。</span><span class="sxs-lookup"><span data-stu-id="47415-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="47415-196">按“Ctrl+F5”  运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="47415-197">Visual Studio 将显示一个选项用于避免 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="47415-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="47415-198">单击 **"是"** 以信任 IIS Express SSL 证书并继续。</span><span class="sxs-lookup"><span data-stu-id="47415-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="47415-199">![IIS Express SSL 证书详细信息](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="47415-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="47415-200">此时将显示一条安全警告。</span><span class="sxs-lookup"><span data-stu-id="47415-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="47415-201">单击 **"是"** 将证书安装到本地主机。</span><span class="sxs-lookup"><span data-stu-id="47415-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="47415-202">![“安全警告”对话框](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="47415-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="47415-203">此时将显示浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="47415-203">The browser window will be displayed.</span></span>

<span data-ttu-id="47415-204">你现在可以使用 SSL 在本地轻松测试 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="47415-205">添加 OAuth 2.0 提供程序</span><span class="sxs-lookup"><span data-stu-id="47415-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="47415-206">ASP.NET Web 窗体为成员资格和身份验证提供了增强的选项。</span><span class="sxs-lookup"><span data-stu-id="47415-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="47415-207">这些增强功能包括 OAuth。</span><span class="sxs-lookup"><span data-stu-id="47415-207">These enhancements include OAuth.</span></span> <span data-ttu-id="47415-208">OAuth 是一种开放协议，允许以一种简单而标准的方法从 Web、移动和桌面应用程序进行安全授权。</span><span class="sxs-lookup"><span data-stu-id="47415-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="47415-209">ASP.NET Web 窗体模板使用 OAuth 公开 Facebook、Twitter、Google 和 Microsoft 作为身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="47415-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="47415-210">虽然本教程仅使用 Google 作为身份验证提供程序，但你可轻松修改代码以使用任何提供程序。</span><span class="sxs-lookup"><span data-stu-id="47415-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="47415-211">实施其他提供程序的步骤与你将在本教程中看到的步骤非常类似。</span><span class="sxs-lookup"><span data-stu-id="47415-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="47415-212">除了身份验证外，本教程还将使用角色实施授权。</span><span class="sxs-lookup"><span data-stu-id="47415-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="47415-213">只有添加到该角色的用户才能 `canEdit` 更改数据 (创建、编辑或删除联系人) 。</span><span class="sxs-lookup"><span data-stu-id="47415-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47415-214">Windows Live 应用程序仅接受工作网站的实时 URL，因此不能使用本地网站 URL 来测试登录名。</span><span class="sxs-lookup"><span data-stu-id="47415-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="47415-215">可以执行以下步骤来添加 Google 身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="47415-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="47415-216">打开 *App \_ Start\Startup.Auth.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="47415-217">从方法中删除注释字符， `app.UseGoogleAuthentication()` 使该方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="47415-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="47415-218">导航到 [Google 开发人员控制台](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="47415-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="47415-219">你还需要使用 Google 开发人员电子邮件帐户 (gmail.com） 登录。</span><span class="sxs-lookup"><span data-stu-id="47415-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="47415-220">如果你没有 Google 帐户，请选择 " **创建帐户** " 链接。</span><span class="sxs-lookup"><span data-stu-id="47415-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="47415-221">接下来，你将看到 **Google 开发人员控制台**。</span><span class="sxs-lookup"><span data-stu-id="47415-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="47415-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="47415-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="47415-223">单击 " **创建项目** " 按钮，然后输入项目名称和 ID (你可以使用) 的默认值。</span><span class="sxs-lookup"><span data-stu-id="47415-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="47415-224">然后，单击 " **协议" 复选框** 和 " **创建** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![Google - 新建项目](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="47415-226">几秒钟后，将会创建新项目，并且浏览器将显示新项目页。</span><span class="sxs-lookup"><span data-stu-id="47415-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="47415-227">在左侧选项卡中，单击 " **api &amp; 身份验证**"，然后单击 " **凭据**"。</span><span class="sxs-lookup"><span data-stu-id="47415-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="47415-228">单击 " **OAuth**" 下的 "**创建新客户端 ID** "。</span><span class="sxs-lookup"><span data-stu-id="47415-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="47415-229">将显示 " **创建客户端 ID** " 对话框。</span><span class="sxs-lookup"><span data-stu-id="47415-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="47415-230">![Google-创建客户端 ID](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="47415-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="47415-231">在 " **创建客户端 ID** " 对话框中，保留应用程序类型的默认 **Web 应用程序** 。</span><span class="sxs-lookup"><span data-stu-id="47415-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="47415-232">将 **授权的 JavaScript** 源设置为之前在本教程中使用的 ssl URL (`https://localhost:44300/` 除非已) 创建其他 ssl 项目。</span><span class="sxs-lookup"><span data-stu-id="47415-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="47415-233">此 URL 是应用程序的来源。</span><span class="sxs-lookup"><span data-stu-id="47415-233">This URL is the origin for your application.</span></span> <span data-ttu-id="47415-234">对于此示例，你只需输入 localhost 测试 URL。</span><span class="sxs-lookup"><span data-stu-id="47415-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="47415-235">但是，您可以输入多个 Url 来为 localhost 和生产提供帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="47415-236">将 **授权的重定向 URI** 设置为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="47415-237">此值是 ASP.NET OAuth 用户与 Google OAuth 服务器通信时使用的 URI。</span><span class="sxs-lookup"><span data-stu-id="47415-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="47415-238">请记住上述 ( 的 SSL URL，    `https://localhost:44300/` 除非已) 创建其他 ssl 项目。</span><span class="sxs-lookup"><span data-stu-id="47415-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="47415-239">单击 " **创建客户端 ID** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="47415-240">在 Google 开发人员控制台的左侧菜单中，单击 " **同意屏幕** " 菜单项，然后设置你的电子邮件地址和产品名称。</span><span class="sxs-lookup"><span data-stu-id="47415-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="47415-241">完成表单后，单击 " **保存**"。</span><span class="sxs-lookup"><span data-stu-id="47415-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="47415-242">单击 " **api** " 菜单项，向下滚动并单击 " **Google + API**" 旁边的 "**关闭**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="47415-243">接受此选项将启用 Google + API。</span><span class="sxs-lookup"><span data-stu-id="47415-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="47415-244">还必须将 **Owin** NuGet 包更新到版本3.0.0。</span><span class="sxs-lookup"><span data-stu-id="47415-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="47415-245">从 " **工具** " 菜单中，选择 " **Nuget 包管理器** "，然后选择 " **管理解决方案的 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="47415-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="47415-246">在 " **管理 NuGet 包** " 窗口中，找到并将 **Owin** 包更新到版本3.0.0。</span><span class="sxs-lookup"><span data-stu-id="47415-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="47415-247">在 Visual Studio 中， `UseGoogleAuthentication` 通过将**客户端 ID**和**客户端密码**复制并粘贴到方法中，更新*Startup.Auth.cs*页的方法。</span><span class="sxs-lookup"><span data-stu-id="47415-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="47415-248">下面显示的 **客户端 ID** 和 **客户端机密** 值为示例，将不起作用。</span><span class="sxs-lookup"><span data-stu-id="47415-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="47415-249">按 **CTRL + F5** 生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="47415-250">单击 " **登录** " 链接。</span><span class="sxs-lookup"><span data-stu-id="47415-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="47415-251">在 " **使用其他服务进行登录**" 下，单击 " **Google**"。</span><span class="sxs-lookup"><span data-stu-id="47415-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="47415-252">![登录](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="47415-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="47415-253">如果你需要输入你的凭据，你将重定向到 google 站点将在此输入你的凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google - 登录](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="47415-255">输入凭据后，系统会提示你向刚创建的 web 应用程序授予权限。</span><span class="sxs-lookup"><span data-stu-id="47415-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![项目默认服务帐户](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="47415-257">单击“接受”。</span><span class="sxs-lookup"><span data-stu-id="47415-257">Click **Accept**.</span></span> <span data-ttu-id="47415-258">你现在将重定向回**WingtipToys**应用程序的 "**注册**" 页，你可以在该应用程序中注册 Google 帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="47415-259">![使用你的 Google 帐户注册](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="47415-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="47415-260">你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。</span><span class="sxs-lookup"><span data-stu-id="47415-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="47415-261">单击 " **登录"** ，如上所示。</span><span class="sxs-lookup"><span data-stu-id="47415-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="47415-262">修改登录功能</span><span class="sxs-lookup"><span data-stu-id="47415-262">Modifying Login Functionality</span></span>

<span data-ttu-id="47415-263">如本系列教程前面所述，在默认情况下，ASP.NET Web 窗体模板中包含了许多用户注册功能。</span><span class="sxs-lookup"><span data-stu-id="47415-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="47415-264">现在，你将修改默认的 *登录 .aspx* ，并 *注册 .aspx* 页以调用 `MigrateCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="47415-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="47415-265">`MigrateCart`方法将新登录的用户与匿名购物车关联。</span><span class="sxs-lookup"><span data-stu-id="47415-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="47415-266">通过关联用户和购物车，Wingtip 玩具示例应用程序将能够在访问之间维护用户的购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="47415-267">在 **解决方案资源管理器**中，找到并打开 *帐户* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="47415-268">修改名为 *Login.aspx.cs* 的代码隐藏页面，使其包含黄色突出显示的代码，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="47415-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="47415-269">保存 *Login.aspx.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="47415-270">现在，你可以忽略此方法没有定义的警告 `MigrateCart` 。</span><span class="sxs-lookup"><span data-stu-id="47415-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="47415-271">你将在本教程的稍后部分中添加它。</span><span class="sxs-lookup"><span data-stu-id="47415-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="47415-272">*Login.aspx.cs*代码隐藏文件支持登录方法。</span><span class="sxs-lookup"><span data-stu-id="47415-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="47415-273">通过检查 "登录 .aspx" 页，您将看到此页包含一个 "登录" 按钮，当单击此按钮时，将触发 `LogIn` 代码隐藏中的处理程序。</span><span class="sxs-lookup"><span data-stu-id="47415-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="47415-274">`Login`调用*Login.aspx.cs*上的方法时，将创建一个名为的购物车的新实例 `usersShoppingCart` 。</span><span class="sxs-lookup"><span data-stu-id="47415-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="47415-275">将检索 (GUID) 的购物车 ID 并将其设置为 `cartId` 变量。</span><span class="sxs-lookup"><span data-stu-id="47415-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="47415-276">然后， `MigrateCart` 调用方法，同时将 `cartId` 已登录用户的和名称传递到此方法。</span><span class="sxs-lookup"><span data-stu-id="47415-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="47415-277">迁移购物车时，用于标识匿名购物车的 GUID 将替换为用户名。</span><span class="sxs-lookup"><span data-stu-id="47415-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="47415-278">除了修改 *Login.aspx.cs* 代码隐藏文件以便在用户登录时迁移购物车，还必须修改 *Register.aspx.cs 代码隐藏文件* ，以便在用户创建新帐户并登录时迁移购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="47415-279">在 *帐户* 文件夹中，打开名为 *Register.aspx.cs*的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="47415-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="47415-280">通过将代码包括为黄色来修改代码隐藏文件，使其如下所示：</span><span class="sxs-lookup"><span data-stu-id="47415-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="47415-281">保存 *Register.aspx.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="47415-282">再次忽略关于方法的警告 `MigrateCart` 。</span><span class="sxs-lookup"><span data-stu-id="47415-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="47415-283">请注意，在事件处理程序中使用的代码与 `CreateUser_Click` 在方法中使用的代码非常相似 `LogIn` 。</span><span class="sxs-lookup"><span data-stu-id="47415-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="47415-284">当用户注册或登录到站点时， `MigrateCart` 将对方法进行调用。</span><span class="sxs-lookup"><span data-stu-id="47415-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="47415-285">迁移购物车</span><span class="sxs-lookup"><span data-stu-id="47415-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="47415-286">现在已更新登录和注册过程，可以使用方法添加代码以迁移购物车 `MigrateCart` 。</span><span class="sxs-lookup"><span data-stu-id="47415-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="47415-287">在 **解决方案资源管理器**中，找到 *逻辑* 文件夹，然后打开 *ShoppingCartActions.cs* 类文件。</span><span class="sxs-lookup"><span data-stu-id="47415-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="47415-288">将黄色突出显示的代码添加到 *ShoppingCartActions.cs* 文件中的现有代码，以便 *ShoppingCartActions.cs* 文件中的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="47415-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="47415-289">`MigrateCart`方法使用现有的 cartId 查找用户的购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="47415-290">接下来，该代码遍历所有购物车项，并 `CartId` `CartItem` 使用已登录的用户名替换架构) 指定的属性 (。</span><span class="sxs-lookup"><span data-stu-id="47415-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="47415-291">更新数据库连接</span><span class="sxs-lookup"><span data-stu-id="47415-291">Updating the Database Connection</span></span>

<span data-ttu-id="47415-292">如果在本教程中使用 **预** 生成的 Wingtip 玩具示例应用程序，则必须重新创建默认的成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="47415-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="47415-293">通过修改默认连接字符串，将在下一次运行应用程序时创建成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="47415-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="47415-294">打开位于项目根目录的 *Web.config* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="47415-295">更新默认连接字符串，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="47415-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="47415-296">集成 PayPal</span><span class="sxs-lookup"><span data-stu-id="47415-296">Integrating PayPal</span></span>

<span data-ttu-id="47415-297">PayPal 是一种基于 web 的计费平台，它接受在线商家支付的费用。</span><span class="sxs-lookup"><span data-stu-id="47415-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="47415-298">接下来，本教程介绍如何将 PayPal 的快速结帐功能集成到你的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="47415-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="47415-299">快速结帐允许客户使用 PayPal 来支付他们已添加到购物车的物品。</span><span class="sxs-lookup"><span data-stu-id="47415-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="47415-300">创建 PayPal 测试帐户</span><span class="sxs-lookup"><span data-stu-id="47415-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="47415-301">若要使用 PayPal 测试环境，必须创建并验证开发人员测试帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="47415-302">您将使用开发人员测试帐户来创建买家测试帐户和卖方测试帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="47415-303">开发人员测试帐户凭据还会允许 Wingtip 玩具示例应用程序访问 PayPal 测试环境。</span><span class="sxs-lookup"><span data-stu-id="47415-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="47415-304">在浏览器中，导航到 PayPal 开发人员测试网站：</span><span class="sxs-lookup"><span data-stu-id="47415-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="47415-305">如果没有 PayPal 开发人员帐户，请单击 " **注册**" 并按照注册步骤创建一个新帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="47415-306">如果拥有现有的 PayPal 开发人员帐户，请单击 " **登录**" 以登录。</span><span class="sxs-lookup"><span data-stu-id="47415-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="47415-307">稍后在本教程中，你将需要 PayPal 开发人员帐户来测试 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="47415-308">如果你刚刚注册了 PayPal 开发者帐户，则可能需要使用 PayPal 验证 PayPal 开发人员帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="47415-309">可以按照 PayPal 发送到你的电子邮件帐户的步骤来验证你的帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="47415-310">验证 PayPal 开发人员帐户后，请重新登录到 PayPal 开发人员测试站点。</span><span class="sxs-lookup"><span data-stu-id="47415-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="47415-311">使用 PayPal 开发人员帐户登录到 PayPal 开发人员站点后，需要创建一个 PayPal 买家测试帐户（如果还没有）。</span><span class="sxs-lookup"><span data-stu-id="47415-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="47415-312">若要创建买家测试帐户，请在 PayPal 网站上单击 " **应用程序** " 选项卡，然后单击 " **沙盒帐户**"。</span><span class="sxs-lookup"><span data-stu-id="47415-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="47415-313">将显示 " **沙盒测试帐户** " 页。</span><span class="sxs-lookup"><span data-stu-id="47415-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="47415-314">PayPal 开发人员网站已经提供了一个商家测试帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![通过 PayPal-沙盒测试帐户结帐和付款](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="47415-316">在 "沙盒测试帐户" 页上，单击 " **创建帐户**"。</span><span class="sxs-lookup"><span data-stu-id="47415-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="47415-317">在 " **创建测试帐户** " 页上，选择所选的买方测试帐户电子邮件和密码。</span><span class="sxs-lookup"><span data-stu-id="47415-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="47415-318">在本教程结束时，你将需要购买者电子邮件地址和密码来测试 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![通过 PayPal-沙盒测试帐户结帐和付款](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="47415-320">单击 " **创建帐户** " 按钮，创建买家测试帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="47415-321">将显示 " **沙盒测试帐户** " 页。</span><span class="sxs-lookup"><span data-stu-id="47415-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![用 PayPal-PayPal 帐户结帐和付款](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="47415-323">在 " **沙盒测试帐户** " 页上，单击 **主持人** 电子邮件帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="47415-324">显示**配置文件**和**通知**选项。</span><span class="sxs-lookup"><span data-stu-id="47415-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="47415-325">选择 " **配置文件** " 选项，然后单击 " **API 凭据** " 查看商家测试帐户的 API 凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="47415-326">将测试 API 凭据复制到记事本。</span><span class="sxs-lookup"><span data-stu-id="47415-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="47415-327">需要 (用户名、密码和签名) 显示的经典测试 API 凭据，才能从 Wingtip 玩具示例应用程序向 PayPal 测试环境进行 API 调用。</span><span class="sxs-lookup"><span data-stu-id="47415-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="47415-328">你将在下一步中添加凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="47415-329">添加 PayPal 类和 API 凭据</span><span class="sxs-lookup"><span data-stu-id="47415-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="47415-330">将大部分 PayPal 代码放在一个类中。</span><span class="sxs-lookup"><span data-stu-id="47415-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="47415-331">此类包含用于与 PayPal 进行通信的方法。</span><span class="sxs-lookup"><span data-stu-id="47415-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="47415-332">此外，还需要将 PayPal 凭据添加到此类。</span><span class="sxs-lookup"><span data-stu-id="47415-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="47415-333">在 Visual Studio 中的 Wingtip 玩具示例应用程序中，右键单击**逻辑**文件夹，然后选择 "**添加**  - &gt; **新项**"。</span><span class="sxs-lookup"><span data-stu-id="47415-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="47415-334">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="47415-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="47415-335">在 **Visual c #** 中，从左侧的 " **已安装** " 窗格中选择 " **代码**"。</span><span class="sxs-lookup"><span data-stu-id="47415-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="47415-336">从中间窗格中选择 " **类**"。</span><span class="sxs-lookup"><span data-stu-id="47415-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="47415-337">将此新类命名为 **PayPalFunctions.cs**。</span><span class="sxs-lookup"><span data-stu-id="47415-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="47415-338">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="47415-338">Click **Add**.</span></span>  
   <span data-ttu-id="47415-339">新的类文件将显示在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="47415-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="47415-340">将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="47415-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="47415-341">在本教程前面部分中显示的 " (用户名"、"密码" 和 "签名") 添加商家 API 凭据，以便可以对 PayPal 测试环境进行函数调用。</span><span class="sxs-lookup"><span data-stu-id="47415-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="47415-342">在此示例应用程序中，只需将凭据添加到 c # 文件 ( .cs) 。</span><span class="sxs-lookup"><span data-stu-id="47415-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="47415-343">但是，在实现的解决方案中，应考虑在配置文件中加密凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="47415-344">NVPAPICaller 类包含 PayPal 的大部分功能。</span><span class="sxs-lookup"><span data-stu-id="47415-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="47415-345">类中的代码提供了在 PayPal 测试环境中进行测试购买所需的方法。</span><span class="sxs-lookup"><span data-stu-id="47415-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="47415-346">以下三个 PayPal 函数用于进行购买：</span><span class="sxs-lookup"><span data-stu-id="47415-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="47415-347">`SetExpressCheckout` 函数</span><span class="sxs-lookup"><span data-stu-id="47415-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="47415-348">`GetExpressCheckoutDetails` 函数</span><span class="sxs-lookup"><span data-stu-id="47415-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="47415-349">`DoExpressCheckoutPayment` 函数</span><span class="sxs-lookup"><span data-stu-id="47415-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="47415-350">`ShortcutExpressCheckout`方法收集购物车的测试购买信息和产品详细信息，并调用 `SetExpressCheckout` PayPal 函数。</span><span class="sxs-lookup"><span data-stu-id="47415-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="47415-351">此 `GetCheckoutDetails` 方法在进行测试前确认购买详细信息，并调用 `GetExpressCheckoutDetails` PayPal 函数。</span><span class="sxs-lookup"><span data-stu-id="47415-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="47415-352">`DoCheckoutPayment`方法通过调用 PayPal 函数完成测试环境中的测试购买 `DoExpressCheckoutPayment` 。</span><span class="sxs-lookup"><span data-stu-id="47415-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="47415-353">其余代码支持 PayPal 方法和过程，如编码字符串、对字符串进行解码、处理数组和确定凭据。</span><span class="sxs-lookup"><span data-stu-id="47415-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47415-354">PayPal 允许根据 [paypal 的 API 规范](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)包含可选的购买详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="47415-355">通过扩展 Wingtip 玩具示例应用程序中的代码，你可以包括本地化详细信息、产品说明、税务、客户服务编号以及许多其他可选字段。</span><span class="sxs-lookup"><span data-stu-id="47415-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="47415-356">请注意， **ShortcutExpressCheckout** 方法中指定的返回和取消 url 使用端口号。</span><span class="sxs-lookup"><span data-stu-id="47415-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="47415-357">当 Visual Web Developer 使用 SSL 运行 web 项目时，通常会将端口44300用于 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="47415-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="47415-358">如上所示，端口号为44300。</span><span class="sxs-lookup"><span data-stu-id="47415-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="47415-359">运行应用程序时，可能会看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="47415-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="47415-360">需要在代码中正确设置端口号，以便在本教程结束时可以成功运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="47415-361">本教程的下一部分介绍如何检索本地主机端口号并更新 PayPal 类。</span><span class="sxs-lookup"><span data-stu-id="47415-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="47415-362">更新 PayPal 类中的 LocalHost 端口号</span><span class="sxs-lookup"><span data-stu-id="47415-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="47415-363">Wingtip 玩具示例应用程序通过导航到 PayPal 测试网站并返回到 Wingtip 玩具示例应用程序的本地实例来购买产品。</span><span class="sxs-lookup"><span data-stu-id="47415-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="47415-364">为了让 PayPal 返回到正确的 URL，你需要在上面提到的 PayPal 代码中指定本地运行的示例应用程序的端口号。</span><span class="sxs-lookup"><span data-stu-id="47415-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="47415-365">右键单击项目名称 ("中的" **WingtipToys**) " **解决方案资源管理器** 并选择" **属性**"。</span><span class="sxs-lookup"><span data-stu-id="47415-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="47415-366">在左列中，选择 " **Web** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="47415-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="47415-367">从 " **项目 Url** " 框中检索端口号。</span><span class="sxs-lookup"><span data-stu-id="47415-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="47415-368">如有必要，请 `returnURL` 在 `cancelURL` PayPalFunctions.cs 文件中更新 PayPal 类 (`NVPAPICaller`) *PayPalFunctions.cs* ，以便使用 web 应用程序的端口号：</span><span class="sxs-lookup"><span data-stu-id="47415-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="47415-369">现在，你添加的代码将与本地 Web 应用程序的所需端口匹配。</span><span class="sxs-lookup"><span data-stu-id="47415-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="47415-370">PayPal 将能够返回到你的本地计算机上的正确 URL。</span><span class="sxs-lookup"><span data-stu-id="47415-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="47415-371">添加 PayPal 结帐按钮</span><span class="sxs-lookup"><span data-stu-id="47415-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="47415-372">由于已将主要 PayPal 函数添加到示例应用程序中，因此可以开始添加调用这些函数所需的标记和代码。</span><span class="sxs-lookup"><span data-stu-id="47415-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="47415-373">首先，必须添加用户将在 "购物车" 页上看到的 "签出" 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="47415-374">打开 *ShoppingCart* 文件。</span><span class="sxs-lookup"><span data-stu-id="47415-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="47415-375">滚动到文件的底部，找到 `<!--Checkout Placeholder -->` 注释。</span><span class="sxs-lookup"><span data-stu-id="47415-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="47415-376">将注释替换为 `ImageButton` 控件，以便按如下所示替换标记：</span><span class="sxs-lookup"><span data-stu-id="47415-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="47415-377">在 *ShoppingCart.aspx.cs* 文件中， `UpdateBtn_Click` 将事件处理程序添加到文件末尾附近，添加 `CheckOutBtn_Click` 事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="47415-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="47415-378">同样，在 *ShoppingCart.aspx.cs* 文件中，添加对的引用 `CheckoutBtn` ，以便按如下所示引用 "新图像" 按钮：</span><span class="sxs-lookup"><span data-stu-id="47415-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="47415-379">保存对 *ShoppingCart* 文件和 *ShoppingCart.aspx.cs* 文件的更改。</span><span class="sxs-lookup"><span data-stu-id="47415-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="47415-380">从菜单中选择 "**调试** - &gt; **生成 WingtipToys**"。</span><span class="sxs-lookup"><span data-stu-id="47415-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="47415-381">将用新添加的 **ImageButton** 控件重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="47415-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="47415-382">向 PayPal 发送购买详细信息</span><span class="sxs-lookup"><span data-stu-id="47415-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="47415-383">当用户单击 "购物车" 页上的 " **签出** " 按钮 (*ShoppingCart*) 时，他们将开始购买过程。</span><span class="sxs-lookup"><span data-stu-id="47415-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="47415-384">以下代码调用购买产品所需的第一个 PayPal 函数。</span><span class="sxs-lookup"><span data-stu-id="47415-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="47415-385">在 *签出* 文件夹中，打开名为 *CheckoutStart.aspx.cs*的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="47415-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="47415-386">请确保打开代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="47415-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="47415-387">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="47415-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="47415-388">当应用程序的用户在 "购物车" 页上单击 " **签出** " 按钮时，浏览器将导航到 *CheckoutStart* 页。</span><span class="sxs-lookup"><span data-stu-id="47415-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="47415-389">加载 *CheckoutStart* 页面时，将 `ShortcutExpressCheckout` 调用方法。</span><span class="sxs-lookup"><span data-stu-id="47415-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="47415-390">此时，用户会传输到 PayPal 测试网站。</span><span class="sxs-lookup"><span data-stu-id="47415-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="47415-391">在 PayPal 网站上，用户输入其 PayPal 凭据，查看购买详细信息，接受 PayPal 协议，并返回到该方法完成的 Wingtip 玩具示例应用程序 `ShortcutExpressCheckout` 。</span><span class="sxs-lookup"><span data-stu-id="47415-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="47415-392">当 `ShortcutExpressCheckout` 方法完成时，它会将用户重定向到方法中指定的*CheckoutReview*页面。 `ShortcutExpressCheckout`</span><span class="sxs-lookup"><span data-stu-id="47415-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="47415-393">这允许用户在 Wingtip 玩具示例应用程序中查看订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="47415-394">查看订单详细信息</span><span class="sxs-lookup"><span data-stu-id="47415-394">Review Order Details</span></span>

<span data-ttu-id="47415-395">从 PayPal 返回后，Wingtip 玩具示例应用程序的 *CheckoutReview* 页将显示订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="47415-396">此页允许用户在购买产品之前查看订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="47415-397">必须按如下所示创建 *CheckoutReview* 页：</span><span class="sxs-lookup"><span data-stu-id="47415-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="47415-398">在 " *签出* " 文件夹中，打开名为 *CheckoutReview*的页。</span><span class="sxs-lookup"><span data-stu-id="47415-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="47415-399">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="47415-400">打开名为 *CheckoutReview.aspx.cs* 的代码隐藏页，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="47415-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="47415-401">" **DetailsView** " 控件用于显示从 PayPal 返回的订单详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="47415-402">此外，上述代码将订单详细信息以对象的形式保存到 Wingtip 玩具数据库 `OrderDetail` 。</span><span class="sxs-lookup"><span data-stu-id="47415-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="47415-403">当用户单击 " **完成订单** " 按钮时，会将其重定向到 *CheckoutComplete* 页。</span><span class="sxs-lookup"><span data-stu-id="47415-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="47415-404">**提示**</span><span class="sxs-lookup"><span data-stu-id="47415-404">**Tip**</span></span>
> 
> <span data-ttu-id="47415-405">在 *CheckoutReview* 页的标记中，请注意， `<ItemStyle>` 标记用于更改 **DetailsView** 控件内靠近页面底部的项的样式。</span><span class="sxs-lookup"><span data-stu-id="47415-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="47415-406">通过在 "设计" **视图** 中查看页面 (选择 Visual Studio 左下角的 " **设计** ") ，然后选择 " **DetailsView** " 控件，并选择 **智能标记** (控件) 右上角的箭头图标，你将能够看到 **DetailsView 任务**。</span><span class="sxs-lookup"><span data-stu-id="47415-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![通过 PayPal 编辑字段结帐和付款](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="47415-408">通过选择 " **编辑字段**"，将显示 " **字段** " 对话框。</span><span class="sxs-lookup"><span data-stu-id="47415-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="47415-409">在此对话框中，可以轻松控制**DetailsView**控件的可视属性，如**ItemStyle**。</span><span class="sxs-lookup"><span data-stu-id="47415-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> !["PayPal-字段" 对话框的 "结帐和付款"](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="47415-411">完成购买</span><span class="sxs-lookup"><span data-stu-id="47415-411">Complete Purchase</span></span>

<span data-ttu-id="47415-412">*CheckoutComplete* 页可从 PayPal 购买。</span><span class="sxs-lookup"><span data-stu-id="47415-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="47415-413">如上所述，用户必须单击 " **完成订单** " 按钮，然后应用程序才会导航到 *CheckoutComplete* 页。</span><span class="sxs-lookup"><span data-stu-id="47415-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="47415-414">在 " *签出* " 文件夹中，打开名为 *CheckoutComplete*的页。</span><span class="sxs-lookup"><span data-stu-id="47415-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="47415-415">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="47415-416">打开名为 *CheckoutComplete.aspx.cs* 的代码隐藏页，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="47415-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="47415-417">加载 *CheckoutComplete* 页面时，将 `DoCheckoutPayment` 调用方法。</span><span class="sxs-lookup"><span data-stu-id="47415-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="47415-418">如前文所述，该 `DoCheckoutPayment` 方法从 PayPal 测试环境中完成购买。</span><span class="sxs-lookup"><span data-stu-id="47415-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="47415-419">一旦 PayPal 完成了订单的购买， *CheckoutComplete* 页面就会向买方显示付款交易 `ID` 。</span><span class="sxs-lookup"><span data-stu-id="47415-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="47415-420">处理取消购买</span><span class="sxs-lookup"><span data-stu-id="47415-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="47415-421">如果用户决定取消购买，则会将其定向到 " *CheckoutCancel* " 页，在该页面中，他们将看到已取消的订单。</span><span class="sxs-lookup"><span data-stu-id="47415-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="47415-422">在*签出*文件夹中打开名为*CheckoutCancel*的页。</span><span class="sxs-lookup"><span data-stu-id="47415-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="47415-423">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="47415-424">处理采购错误</span><span class="sxs-lookup"><span data-stu-id="47415-424">Handle Purchase Errors</span></span>

<span data-ttu-id="47415-425">在购买过程中的错误将由 *CheckoutError* 页面处理。</span><span class="sxs-lookup"><span data-stu-id="47415-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="47415-426">如果发生错误，则 *CheckoutStart* 页的代码隐藏、 *CheckoutReview* 页和 *CheckoutComplete* 页将每个都重定向到 *CheckoutError* 页。</span><span class="sxs-lookup"><span data-stu-id="47415-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="47415-427">在*签出*文件夹中打开名为*CheckoutError*的页。</span><span class="sxs-lookup"><span data-stu-id="47415-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="47415-428">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="47415-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="47415-429">在签出过程中出现错误时，会显示 *CheckoutError* 页，其中包含错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="47415-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="47415-430">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="47415-430">Running the Application</span></span>

<span data-ttu-id="47415-431">运行应用程序以了解如何购买产品。</span><span class="sxs-lookup"><span data-stu-id="47415-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="47415-432">请注意，你将在 PayPal 测试环境中运行。</span><span class="sxs-lookup"><span data-stu-id="47415-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="47415-433">不会交换实际资金。</span><span class="sxs-lookup"><span data-stu-id="47415-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="47415-434">请确保所有文件都保存在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="47415-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="47415-435">打开 Web 浏览器并导航到 [https://developer.paypal.com](https://developer.paypal.com/) 。</span><span class="sxs-lookup"><span data-stu-id="47415-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="47415-436">登录到你之前在本教程中创建的 PayPal 开发人员帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="47415-437">对于 PayPal 的开发人员沙箱，你需要登录 [https://developer.paypal.com](https://developer.paypal.com/) 到，以便测试快速结帐。</span><span class="sxs-lookup"><span data-stu-id="47415-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="47415-438">这仅适用于 PayPal 的沙箱测试，而不适用于 PayPal 的实时环境。</span><span class="sxs-lookup"><span data-stu-id="47415-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="47415-439">在 Visual Studio 中，按 **F5** 运行 "Wingtip 玩具" 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="47415-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="47415-440">重新生成数据库后，浏览器将打开并显示 *default.aspx* 页。</span><span class="sxs-lookup"><span data-stu-id="47415-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="47415-441">选择产品类别（如 "汽车"），然后单击每个产品旁边的 " **添加到购物车** "，将三个不同的产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="47415-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="47415-442">购物车将显示您选择的产品。</span><span class="sxs-lookup"><span data-stu-id="47415-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="47415-443">单击 **PayPal** 按钮以结帐。</span><span class="sxs-lookup"><span data-stu-id="47415-443">Click the **PayPal** button to checkout.</span></span> 

    ![通过 PayPal 购物车结帐和付款](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="47415-445">签出将要求你拥有 Wingtip 玩具示例应用程序的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="47415-446">单击页面右侧的 **Google** 链接，使用现有的 gmail.com 电子邮件帐户登录。</span><span class="sxs-lookup"><span data-stu-id="47415-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="47415-447">如果没有 gmail.com 帐户，可以在 [www.gmail.com](https://www.gmail.com/)上创建一个用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="47415-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="47415-448">还可以通过单击 "注册" 来使用标准本地帐户。</span><span class="sxs-lookup"><span data-stu-id="47415-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![签入并支付 PayPal-登录](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="47415-450">用 gmail 帐户和密码登录。</span><span class="sxs-lookup"><span data-stu-id="47415-450">Sign in with your gmail account and password.</span></span> 

    ![通过 PayPal 登录进行结帐和付款](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="47415-452">单击 " **登录** " 按钮，将 gmail 帐户注册到 Wingtip 玩具示例应用程序用户名。</span><span class="sxs-lookup"><span data-stu-id="47415-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![签出并支付 PayPal-注册帐户](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="47415-454">在 PayPal 测试网站上，添加之前在本教程中创建的 **买家** 电子邮件地址和密码，并单击 " **登录** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![通过 PayPal-PayPal 登录进行结帐和付款](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="47415-456">同意 PayPal 政策，并单击 " **同意并继续** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="47415-457">请注意，仅当首次使用此 PayPal 帐户时，才会显示此页。</span><span class="sxs-lookup"><span data-stu-id="47415-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="47415-458">再次请注意，这是一个测试帐户，不会交换真正的资金。</span><span class="sxs-lookup"><span data-stu-id="47415-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![结帐和支付 PayPal-PayPal 政策](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="47415-460">查看 PayPal 测试环境检查页上的订单信息，然后单击 " **继续**"。</span><span class="sxs-lookup"><span data-stu-id="47415-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![结帐和支付 PayPal-查看信息](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="47415-462">在 " *CheckoutReview* " 页上，验证订单量并查看生成的寄送地址。</span><span class="sxs-lookup"><span data-stu-id="47415-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="47415-463">然后单击 " **完成顺序** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="47415-463">Then, click the **Complete Order** button.</span></span> 

    ![通过 PayPal 订购审核结帐和付款](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="47415-465">将显示 **CheckoutComplete** 页，其中包含付款事务 ID。</span><span class="sxs-lookup"><span data-stu-id="47415-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![通过 PayPal 结帐和付款-结帐完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="47415-467">查看数据库</span><span class="sxs-lookup"><span data-stu-id="47415-467">Reviewing the Database</span></span>

<span data-ttu-id="47415-468">在运行应用程序后，通过查看 Wingtip 玩具示例应用程序数据库中的更新数据，可以看到该应用程序已成功记录产品的购买情况。</span><span class="sxs-lookup"><span data-stu-id="47415-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="47415-469">您可以使用 Visual) Studio 中的 "**数据库资源管理器**" 窗口 (**服务器资源管理器**"窗口中检查包含在*Wingtiptoys*数据库文件中的数据，如本系列教程前面所述。</span><span class="sxs-lookup"><span data-stu-id="47415-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="47415-470">如果浏览器窗口仍处于打开状态，请将其关闭。</span><span class="sxs-lookup"><span data-stu-id="47415-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="47415-471">在 Visual Studio 中，选择 "**解决方案资源管理器**顶部的"**显示所有文件**"图标，以允许你展开"**应用程序 \_ 数据**"文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="47415-472">展开 " **应用程序 \_ 数据** " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="47415-473">可能需要选择文件夹的 " **显示所有文件** " 图标。</span><span class="sxs-lookup"><span data-stu-id="47415-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="47415-474">右键单击 *Wingtiptoys* 数据库文件，然后选择 " **打开**"。</span><span class="sxs-lookup"><span data-stu-id="47415-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="47415-475">将显示**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="47415-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="47415-476">展开 **“表”** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="47415-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="47415-477">右键单击 **Orders**表，然后选择 " **显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="47415-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="47415-478">显示 " **订单** " 表。</span><span class="sxs-lookup"><span data-stu-id="47415-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="47415-479">查看 " **PaymentTransactionID** " 列以确认事务是否成功。</span><span class="sxs-lookup"><span data-stu-id="47415-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![签出和支付 PayPal-查看数据库](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="47415-481">关闭 " **订单** 表" 窗口。</span><span class="sxs-lookup"><span data-stu-id="47415-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="47415-482">在服务器资源管理器中，右键单击 **OrderDetails** 表并选择 " **显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="47415-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="47415-483">查看 `OrderId` `Username` **OrderDetails** 表中的和值。</span><span class="sxs-lookup"><span data-stu-id="47415-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="47415-484">请注意，这些值匹配 `OrderId` `Username` **Orders** 表中包含的和值。</span><span class="sxs-lookup"><span data-stu-id="47415-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="47415-485">关闭 " **OrderDetails** 表" 窗口。</span><span class="sxs-lookup"><span data-stu-id="47415-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="47415-486">右键单击 "Wingtip 玩具" 数据库文件 (*Wingtiptoys*) 并选择 " **关闭连接**"。</span><span class="sxs-lookup"><span data-stu-id="47415-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="47415-487">如果看不到 "**解决方案资源管理器**" 窗口，请单击 "**服务器资源管理器**" 窗口底部的 "**解决方案资源管理器**以再次显示**解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="47415-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="47415-488">总结</span><span class="sxs-lookup"><span data-stu-id="47415-488">Summary</span></span>

<span data-ttu-id="47415-489">在本教程中，您添加了订单和订单详细信息架构以跟踪产品的购买情况。</span><span class="sxs-lookup"><span data-stu-id="47415-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="47415-490">还将 PayPal 功能集成到了 Wingtip 玩具示例应用程序中。</span><span class="sxs-lookup"><span data-stu-id="47415-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47415-491">其他资源</span><span class="sxs-lookup"><span data-stu-id="47415-491">Additional Resources</span></span>

<span data-ttu-id="47415-492">[ASP.NET 配置概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="47415-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="47415-493">使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="47415-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="47415-494">Microsoft Azure 免费试用版</span><span class="sxs-lookup"><span data-stu-id="47415-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="47415-495">免责声明</span><span class="sxs-lookup"><span data-stu-id="47415-495">Disclaimer</span></span>

<span data-ttu-id="47415-496">本教程包含示例代码。</span><span class="sxs-lookup"><span data-stu-id="47415-496">This tutorial contains sample code.</span></span> <span data-ttu-id="47415-497">此类示例代码 "按原样" 提供，不提供任何形式的保证。</span><span class="sxs-lookup"><span data-stu-id="47415-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="47415-498">因此，Microsoft 不保证代码的准确性、完整性或质量。</span><span class="sxs-lookup"><span data-stu-id="47415-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="47415-499">您同意使用此示例代码的风险由您自己承担。</span><span class="sxs-lookup"><span data-stu-id="47415-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="47415-500">在任何情况下，Microsoft 都不会对任何示例代码、内容（包括但不限于）任何代码、内容或任何类型的任何错误或遗漏的任何错误或遗漏提供任何错误或遗漏，因为使用任何示例代码。</span><span class="sxs-lookup"><span data-stu-id="47415-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="47415-501">你将被特此通知，并在特此同意赔偿、节省和保持 Microsoft 免受任何损失、损失索赔、伤害或损坏（包括但不限于通过发布、传输、使用或依赖的内容，包括但不限于这些 occasioned，但不限于）。</span><span class="sxs-lookup"><span data-stu-id="47415-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="47415-502">[上一页](shopping-cart.md)
> [下一页](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="47415-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>

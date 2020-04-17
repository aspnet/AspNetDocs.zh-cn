---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 了解ASP.NET MVC 执行流程 |微软文档
author: rick-anderson
description: 了解ASP.NET MVC 框架如何逐步处理浏览器请求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541021"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="04645-103">了解 ASP.NET MVC 的执行流程</span><span class="sxs-lookup"><span data-stu-id="04645-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="04645-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="04645-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="04645-105">了解ASP.NET MVC 框架如何逐步处理浏览器请求。</span><span class="sxs-lookup"><span data-stu-id="04645-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="04645-106">对基于ASP.NET MVC 的 Web 应用程序的请求首先通过**UrlRoutingModule**对象，该对象是一个 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="04645-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="04645-107">此模块将分析请求并执行路由选择。</span><span class="sxs-lookup"><span data-stu-id="04645-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="04645-108">**UrlRoutingModule**对象选择与当前请求匹配的第一个路由对象。</span><span class="sxs-lookup"><span data-stu-id="04645-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="04645-109">（路由对象是实现**RouteBase**的类，通常是**路由**类的实例。如果没有路由匹配 **，UrlRoutingModule**对象将不执行任何操作，并让请求回退到常规ASP.NET或 IIS 请求处理。</span><span class="sxs-lookup"><span data-stu-id="04645-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="04645-110">从选定的**路由**对象中 **，UrlRouteModule**对象获取与**路由**对象关联的**IRouteHandler**对象。</span><span class="sxs-lookup"><span data-stu-id="04645-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="04645-111">通常，在 MVC 应用程序中，这将是**MvcRouteHandler**的实例。</span><span class="sxs-lookup"><span data-stu-id="04645-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="04645-112">**IRouteHandler**实例创建一个**IHttpHandler**对象，并将其传递给**IHttpContext**对象。</span><span class="sxs-lookup"><span data-stu-id="04645-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="04645-113">默认情况下，MVC 的**IHttpHandler**实例是**MvcHandler**对象。</span><span class="sxs-lookup"><span data-stu-id="04645-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="04645-114">**然后，MvcHandler**对象选择最终将处理请求的控制器。</span><span class="sxs-lookup"><span data-stu-id="04645-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="04645-115">如果 ASP.NET MVC Web 应用程序运行在 IIS 7.0 中，则 MVC 项目不需要文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="04645-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="04645-116">但是，在 IIS 6.0 中，处理程序要求将 .mvc 文件扩展名映射到 ASP.NET ISAPI DLL。</span><span class="sxs-lookup"><span data-stu-id="04645-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="04645-117">模块和处理程序是 mVC 框架ASP.NET的入口点。</span><span class="sxs-lookup"><span data-stu-id="04645-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="04645-118">它们执行下列操作：</span><span class="sxs-lookup"><span data-stu-id="04645-118">They perform the following actions:</span></span>

- <span data-ttu-id="04645-119">选择 MVC Web 应用程序中合适的控制器。</span><span class="sxs-lookup"><span data-stu-id="04645-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="04645-120">获取特定的控制器实例。</span><span class="sxs-lookup"><span data-stu-id="04645-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="04645-121">调用**控制器的执行方法**。</span><span class="sxs-lookup"><span data-stu-id="04645-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="04645-122">下面列出了 MVC Web 项目的执行阶段：</span><span class="sxs-lookup"><span data-stu-id="04645-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="04645-123">接收对应用程序的第一个请求</span><span class="sxs-lookup"><span data-stu-id="04645-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="04645-124">在 Global.asax 文件中，**路由**对象将添加到**RouteTable**对象。</span><span class="sxs-lookup"><span data-stu-id="04645-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="04645-125">执行路由</span><span class="sxs-lookup"><span data-stu-id="04645-125">Perform routing</span></span> 

    - <span data-ttu-id="04645-126">**UrlRoutingModule 模块**使用**RouteTable**集合中的第一个匹配**路由**对象来创建**RouteData**对象，然后使用它创建**请求上下文**（**IHttpContext**） 对象。</span><span class="sxs-lookup"><span data-stu-id="04645-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="04645-127">创建 MVC 请求处理程序</span><span class="sxs-lookup"><span data-stu-id="04645-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="04645-128">**MvcRouteHandler**对象创建**MvcHandler**类的实例，并将其传递给**请求上下文**实例。</span><span class="sxs-lookup"><span data-stu-id="04645-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="04645-129">创建控制器</span><span class="sxs-lookup"><span data-stu-id="04645-129">Create controller</span></span> 

    - <span data-ttu-id="04645-130">**MvcHandler**对象使用**RequestContext**实例来标识**IControllerFactory**对象（通常是**默认控制器工厂**类的实例）来使用来创建控制器实例。</span><span class="sxs-lookup"><span data-stu-id="04645-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="04645-131">执行控制器 - **MvcHandler**实例调用控制器**的执行方法**。</span><span class="sxs-lookup"><span data-stu-id="04645-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="04645-132">调用操作</span><span class="sxs-lookup"><span data-stu-id="04645-132">Invoke action</span></span> 

    - <span data-ttu-id="04645-133">大多数控制器从**控制器**基类继承。</span><span class="sxs-lookup"><span data-stu-id="04645-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="04645-134">对于这样做的控制器，与控制器关联的**ControllerActionInvoker**对象确定要调用的控制器类的操作方法，然后调用该方法。</span><span class="sxs-lookup"><span data-stu-id="04645-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="04645-135">执行结果</span><span class="sxs-lookup"><span data-stu-id="04645-135">Execute result</span></span> 

    - <span data-ttu-id="04645-136">典型的操作方法可能会接收用户输入、准备适当的响应数据，然后通过返回结果类型来执行结果。</span><span class="sxs-lookup"><span data-stu-id="04645-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="04645-137">可以执行的内置结果类型包括 **：ViewResult（** 呈现视图，是最常用的结果类型）、**重定向到路由结果**、**重定向结果**、**内容结果\*\*\*\*、JsonResult**和**空结果**。</span><span class="sxs-lookup"><span data-stu-id="04645-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>

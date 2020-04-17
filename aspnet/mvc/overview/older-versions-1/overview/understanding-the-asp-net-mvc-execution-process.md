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
# <a name="understanding-the-aspnet-mvc-execution-process"></a>了解 ASP.NET MVC 的执行流程

由[微软](https://github.com/microsoft)

> 了解ASP.NET MVC 框架如何逐步处理浏览器请求。

对基于ASP.NET MVC 的 Web 应用程序的请求首先通过**UrlRoutingModule**对象，该对象是一个 HTTP 模块。 此模块将分析请求并执行路由选择。 **UrlRoutingModule**对象选择与当前请求匹配的第一个路由对象。 （路由对象是实现**RouteBase**的类，通常是**路由**类的实例。如果没有路由匹配 **，UrlRoutingModule**对象将不执行任何操作，并让请求回退到常规ASP.NET或 IIS 请求处理。

从选定的**路由**对象中 **，UrlRouteModule**对象获取与**路由**对象关联的**IRouteHandler**对象。 通常，在 MVC 应用程序中，这将是**MvcRouteHandler**的实例。 **IRouteHandler**实例创建一个**IHttpHandler**对象，并将其传递给**IHttpContext**对象。 默认情况下，MVC 的**IHttpHandler**实例是**MvcHandler**对象。 **然后，MvcHandler**对象选择最终将处理请求的控制器。

> [!NOTE]
> 如果 ASP.NET MVC Web 应用程序运行在 IIS 7.0 中，则 MVC 项目不需要文件扩展名。 但是，在 IIS 6.0 中，处理程序要求将 .mvc 文件扩展名映射到 ASP.NET ISAPI DLL。

模块和处理程序是 mVC 框架ASP.NET的入口点。 它们执行下列操作：

- 选择 MVC Web 应用程序中合适的控制器。
- 获取特定的控制器实例。
- 调用**控制器的执行方法**。

下面列出了 MVC Web 项目的执行阶段：

- 接收对应用程序的第一个请求 

    - 在 Global.asax 文件中，**路由**对象将添加到**RouteTable**对象。
- 执行路由 

    - **UrlRoutingModule 模块**使用**RouteTable**集合中的第一个匹配**路由**对象来创建**RouteData**对象，然后使用它创建**请求上下文**（**IHttpContext**） 对象。
- 创建 MVC 请求处理程序 

    - **MvcRouteHandler**对象创建**MvcHandler**类的实例，并将其传递给**请求上下文**实例。
- 创建控制器 

    - **MvcHandler**对象使用**RequestContext**实例来标识**IControllerFactory**对象（通常是**默认控制器工厂**类的实例）来使用来创建控制器实例。
- 执行控制器 - **MvcHandler**实例调用控制器**的执行方法**。 |
- 调用操作 

    - 大多数控制器从**控制器**基类继承。 对于这样做的控制器，与控制器关联的**ControllerActionInvoker**对象确定要调用的控制器类的操作方法，然后调用该方法。
- 执行结果 

    - 典型的操作方法可能会接收用户输入、准备适当的响应数据，然后通过返回结果类型来执行结果。 可以执行的内置结果类型包括 **：ViewResult（** 呈现视图，是最常用的结果类型）、**重定向到路由结果**、**重定向结果**、**内容结果****、JsonResult**和**空结果**。

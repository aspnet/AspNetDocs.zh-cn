---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: 检查详细信息和删除方法 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 9c4e66454d6995bd750b62ef8b461bcfbdfb4b4f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045086"
---
# <a name="examining-the-details-and-delete-methods"></a>检查 Details 和 Delete 方法

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本教程的此部分，您将检查自动生成的 `Details` 和 `Delete` 方法。

## <a name="examining-the-details-and-delete-methods"></a>检查 Details 和 Delete 方法

打开 `Movie` 控制器并检查 `Details` 方法。

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

创建此操作方法的 MVC 基架引擎添加注释，该注释显示调用方法的 HTTP 请求。 在这种情况下，它是一个 `GET` 包含三个 URL 段、 `Movies` 控制器、 `Details` 方法和 `ID` 值的请求。

Code First 可以使用方法轻松搜索数据 `Find` 。 内置于方法中的一个重要的安全功能是，代码验证 `Find` 方法在代码尝试使用影片之前是否找到了电影。 例如，黑客可以通过将链接创建的 URL 从更改 `http://localhost:xxxx/Movies/Details/1` 为类似 `http://localhost:xxxx/Movies/Details/12345` (或其他不表示实际电影) 的其他值，将错误引入到站点中。 如果未检查是否有空电影，空电影会导致数据库错误。

检查 `Delete` 和 `DeleteConfirmed` 方法。

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

请注意，HTTP GET `Delete` 方法不会删除指定的电影，它会返回电影视图，你可以在其中提交 (`HttpPost`) 删除。 执行删除操作以响应 GET 请求（或者说，执行编辑操作、创建操作或更改数据的任何其他操作）会打开安全漏洞。 有关此操作的详细信息，请参阅 Stephen Walther 的博客文章 [ASP.NET MVC Tip #46 —不要使用删除链接，因为它们创建了安全漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。

删除数据的 `HttpPost` 方法命名为 `DeleteConfirmed`，以便为 HTTP POST 方法提供一个唯一的签名或名称。 下面显示了两个方法签名：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

公共语言运行时 (CLR) 需要重载方法拥有唯一的参数签名（相同的方法名称但不同的参数列表）。 但在这里，你需要两个删除方法-一个用于 GET，一个用于 POST，这两个方法具有相同的参数签名。 （它们都需要接受单个整数作为参数。）

为此，可以执行几项操作。 一种方式是为方法指定不同的名称。 这正是前面的示例中的基架机制进行的操作。 但是，这会造成一个小问题：ASP.NET 按名称将 URL 段映射到操作方法，如果重命名方法，则路由通常无法找到该方法。 该示例中也提供了解决方案，即向 `DeleteConfirmed` 方法添加 `ActionName("Delete")` 属性。 这会有效地为路由系统执行映射，以便包含 POST 请求的 */Delete/* 的 URL 将查找 `DeleteConfirmed` 方法。

避免使用具有相同名称和签名的方法的问题的另一种常见方法是：人为更改 POST 方法的签名以包含未使用的参数。 例如，某些开发人员添加一个 `FormCollection` 传递给 POST 方法的参数类型，然后仅使用参数：

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a>摘要

现在，你有了一个完整的 ASP.NET MVC 应用程序，它将数据存储在本地数据库中。 你可以创建、读取、更新、删除和搜索电影。

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a>后续步骤

生成并测试 web 应用程序后，下一步就是使其可供其他人通过 Internet 使用。 为此，必须将其部署到 web 宿主提供程序。 Microsoft 为免费的 [Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)提供免费的 web 托管，最多10个网站。 建议你接下来按照教程 [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 应用程序部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 好的教程是 Tom Dykstra 为 [ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 [Stackoverflow](http://stackoverflow.com/help) 和 [ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx) 是提出问题的好地方。 请在 twitter 上关注 [我](https://twitter.com/RickAndMSFT) ，以便可以在我的最新教程中获取更新。

欢迎提供反馈。

- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter： [@RickAndMSFT](https://twitter.com/RickAndMSFT)  
- [Scott Hanselman](http://www.hanselman.com/blog/) twitter： [@shanselman](https://twitter.com/shanselman)

> [!div class="step-by-step"]
> [上一页](adding-validation.md)

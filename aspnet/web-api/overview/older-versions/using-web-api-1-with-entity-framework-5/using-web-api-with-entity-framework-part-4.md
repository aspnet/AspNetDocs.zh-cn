---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第 4 部分：添加管理员视图 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 54b3afac9b19962b02336a35909b208c4e3f7504
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400550"
---
# <a name="part-4-adding-an-admin-view"></a>第 4 部分：添加管理员视图

通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>添加管理员视图

现在我们将向客户端，并添加一个页面，可以使用管理控制器中的数据。 页面将允许用户创建、 编辑或删除产品，通过向控制器发送 AJAX 请求。

在解决方案资源管理器，展开 Controllers 文件夹并打开名为 HomeController.cs 文件。 此文件包含一个 MVC 控制器。 添加一个名为`Admin`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl**方法用于创建 web API 的 URI，而我们将此存储在视图包的更高版本。

接下来，在将文本光标的位置`Admin`操作方法，然后右键单击并选择**添加视图**。 此时会弹出**添加视图**对话框。

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

在中**添加视图**对话框中，名称查看"Admin"。 选择标记的复选框**创建强类型化视图**。 下**模型类**，选择"Product (ProductStore.Models)"。 将所有其他选项保留为其默认值。

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

单击**添加**将添加一个名为 Views/Home 下的 Admin.cshtml 文件。 打开此文件并添加以下 HTML。 此 HTML 定义的结构页上，但尚未建立连接的功能。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>创建到管理员页的链接

在解决方案资源管理器，展开 Views 文件夹，然后展开共享文件夹。 打开名为的文件\_Layout.cshtml。 找到**ul**元素 id ="菜单"和管理员视图的操作链接：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> 在示例项目中，我进行了几个其他修饰性更改，如替换字符串"Your logo here"。 这些不会影响应用程序的功能。 可以下载该项目，并比较文件。


运行应用程序并单击显示在主页页面顶部的"管理员"链接。 管理员页应如下所示：

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

右现在，页面不会执行任何操作。 在下一步部分中，我们将使用 Knockout.js 创建动态 UI。

## <a name="add-authorization"></a>添加授权

当前访问网站的任何人都可访问管理员页。 让我们更改此设置以限制对管理员的权限。

首先，通过添加一个"管理员"角色和管理员用户。 在解决方案资源管理器，展开筛选器文件夹并打开名为 InitializeSimpleMembershipAttribute.cs 的文件。 找到`SimpleMembershipInitializer`构造函数。 在调用**WebSecurity.InitializeDatabaseConnection**，添加以下代码：

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

这是添加的"管理员"角色和创建用户角色的应急方法。

在解决方案资源管理器，展开 Controllers 文件夹并打开 HomeController.cs 文件。 添加**Authorize**属性为`Admin`方法。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

打开 AdminController.cs 文件并添加**Authorize**属性为整个`AdminController`类。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC 和 Web API 都定义**Authorize**的属性，在不同的命名空间。 MVC 将使用**System.Web.Mvc.AuthorizeAttribute**，而 Web API 使用**System.Web.Http.AuthorizeAttribute**。


现在只有管理员可以查看管理页。 此外，如果您向管理员控制器发送 HTTP 请求，请求必须包含的身份验证 cookie。 否则，服务器发送 HTTP 401 （未经授权） 响应。 可以通过发送 GET 请求到看到这在 Fiddler 中`http://localhost:*port*/api/admin`。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-3.md)
> [下一页](using-web-api-with-entity-framework-part-5.md)

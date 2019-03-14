---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第 1 部分：概述和创建项目 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0e4021402e8deccd2395f23b6b512679b5e9d281
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050524"
---
<a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="88fcf-102">第 1 部分：概述和创建项目</span><span class="sxs-lookup"><span data-stu-id="88fcf-102">Part 1: Overview and Creating the Project</span></span>
====================
<span data-ttu-id="88fcf-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="88fcf-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="88fcf-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="88fcf-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="88fcf-105">Entity Framework 是一个对象/关系映射框架。</span><span class="sxs-lookup"><span data-stu-id="88fcf-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="88fcf-106">它将在代码中的域对象映射到关系数据库中的实体。</span><span class="sxs-lookup"><span data-stu-id="88fcf-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="88fcf-107">大多数情况下，您无需担心数据库层，因为实体框架将为您处理它。</span><span class="sxs-lookup"><span data-stu-id="88fcf-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="88fcf-108">你的代码操作对象，并更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="88fcf-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="88fcf-109">有关本教程</span><span class="sxs-lookup"><span data-stu-id="88fcf-109">About the Tutorial</span></span>

<span data-ttu-id="88fcf-110">在本教程中，将创建一个简单的应用商店应用程序。</span><span class="sxs-lookup"><span data-stu-id="88fcf-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="88fcf-111">有两个主要部分： 应用程序。</span><span class="sxs-lookup"><span data-stu-id="88fcf-111">There are two main parts to the application.</span></span> <span data-ttu-id="88fcf-112">普通用户可以查看产品，并创建订单：</span><span class="sxs-lookup"><span data-stu-id="88fcf-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="88fcf-113">管理员可以创建、 删除或编辑产品：</span><span class="sxs-lookup"><span data-stu-id="88fcf-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="88fcf-114">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="88fcf-114">Skills You'll Learn</span></span>

<span data-ttu-id="88fcf-115">下面是你将了解：</span><span class="sxs-lookup"><span data-stu-id="88fcf-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="88fcf-116">如何使用实体框架和 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="88fcf-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="88fcf-117">如何使用 knockout.js 创建动态客户端 UI。</span><span class="sxs-lookup"><span data-stu-id="88fcf-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="88fcf-118">如何使用与 Web API 的窗体身份验证来对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="88fcf-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="88fcf-119">虽然本教程是自包含，但你可能想要先阅读以下教程：</span><span class="sxs-lookup"><span data-stu-id="88fcf-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="88fcf-120">第一个 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="88fcf-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="88fcf-121">创建 Web API 支持 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="88fcf-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="88fcf-122">有一定的了解[ASP.NET MVC](../../../../mvc/index.md)也会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="88fcf-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="88fcf-123">概述</span><span class="sxs-lookup"><span data-stu-id="88fcf-123">Overview</span></span>

<span data-ttu-id="88fcf-124">在高级别中，下面是应用程序的体系结构：</span><span class="sxs-lookup"><span data-stu-id="88fcf-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="88fcf-125">ASP.NET MVC 为客户端生成的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="88fcf-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="88fcf-126">ASP.NET Web API 公开的数据 （产品和订单） 的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="88fcf-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="88fcf-127">实体框架将转换成数据库的实体使用 Web API 的 C# 模型。</span><span class="sxs-lookup"><span data-stu-id="88fcf-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="88fcf-128">下图显示了如何在应用程序的各层表示域对象：数据库层、 对象模型，以及最后连网格式，用于将数据传输到客户端通过 HTTP。</span><span class="sxs-lookup"><span data-stu-id="88fcf-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="88fcf-129">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="88fcf-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="88fcf-130">可以创建使用 Visual Web Developer 速成版或 Visual Studio 的完整版本的教程项目。</span><span class="sxs-lookup"><span data-stu-id="88fcf-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="88fcf-131">从**启动**页上，单击**新项目**。</span><span class="sxs-lookup"><span data-stu-id="88fcf-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="88fcf-132">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="88fcf-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="88fcf-133">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="88fcf-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="88fcf-134">在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="88fcf-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="88fcf-135">命名项目"ProductStore"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="88fcf-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="88fcf-136">在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="88fcf-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="88fcf-137">"Internet 应用程序"模板创建支持窗体身份验证的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="88fcf-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="88fcf-138">如果您运行应用程序现在，它已包含一些功能：</span><span class="sxs-lookup"><span data-stu-id="88fcf-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="88fcf-139">新用户可以通过单击右上角的"注册"链接注册。</span><span class="sxs-lookup"><span data-stu-id="88fcf-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="88fcf-140">已注册的用户可以通过单击"登录"链接登录。</span><span class="sxs-lookup"><span data-stu-id="88fcf-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="88fcf-141">会自动创建的数据库中保留成员身份信息。</span><span class="sxs-lookup"><span data-stu-id="88fcf-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="88fcf-142">有关在 ASP.NET MVC 中的窗体身份验证的详细信息，请参阅[演练：在 ASP.NET MVC 中使用窗体身份验证](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="88fcf-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="88fcf-143">更新 CSS 文件</span><span class="sxs-lookup"><span data-stu-id="88fcf-143">Update the CSS File</span></span>

<span data-ttu-id="88fcf-144">此步骤是表面的但它将使呈现等早期的屏幕截图的页。</span><span class="sxs-lookup"><span data-stu-id="88fcf-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="88fcf-145">在解决方案资源管理器，展开内容文件夹并打开名为 Site.css 文件。</span><span class="sxs-lookup"><span data-stu-id="88fcf-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="88fcf-146">添加以下 CSS 样式：</span><span class="sxs-lookup"><span data-stu-id="88fcf-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="88fcf-147">下一页</span><span class="sxs-lookup"><span data-stu-id="88fcf-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)

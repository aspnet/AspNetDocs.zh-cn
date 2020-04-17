---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权的安全应用程序 |微软文档
author: rick-anderson
description: 步骤 9 演示如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站以创建...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542568"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="8744c-103">使用身份验证和授权保护应用程序</span><span class="sxs-lookup"><span data-stu-id="8744c-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="8744c-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8744c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8744c-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="8744c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="8744c-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第9步，该教程演示如何使用mVC 1 构建小型但完整的 Web 应用程序ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="8744c-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="8744c-107">步骤 9 演示如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站以创建新的晚餐，并且只有主持晚宴的用户才能稍后对其进行编辑。</span><span class="sxs-lookup"><span data-stu-id="8744c-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="8744c-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="8744c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="8744c-109">神经晚餐步骤 9：身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="8744c-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="8744c-110">现在，我们的NerdDinner应用程序允许任何访问该网站的人能够创建和编辑任何晚餐的细节。</span><span class="sxs-lookup"><span data-stu-id="8744c-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="8744c-111">让我们更改此内容，以便用户需要注册并登录到网站以创建新的晚餐，并添加限制，以便只有主持晚宴的用户才能稍后对其进行编辑。</span><span class="sxs-lookup"><span data-stu-id="8744c-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="8744c-112">为了启用此功能，我们将使用身份验证和授权来保护我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8744c-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="8744c-113">了解身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="8744c-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="8744c-114">*身份验证*是标识和验证访问应用程序的客户端的标识的过程。</span><span class="sxs-lookup"><span data-stu-id="8744c-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="8744c-115">简单地说，它是关于确定最终用户在访问网站时的"谁"。</span><span class="sxs-lookup"><span data-stu-id="8744c-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="8744c-116">ASP.NET支持对浏览器用户进行身份验证的多种方法。</span><span class="sxs-lookup"><span data-stu-id="8744c-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="8744c-117">对于 Internet Web 应用程序，最常用的身份验证方法称为"表单身份验证"。</span><span class="sxs-lookup"><span data-stu-id="8744c-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="8744c-118">窗体身份验证使开发人员能够在其应用程序中创作 HTML 登录表单，然后根据数据库或其他密码凭据存储验证最终用户提交的用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="8744c-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="8744c-119">如果用户名/密码组合正确，开发人员可以请求ASP.NET发出加密的 HTTP Cookie，以识别用户在未来的请求。</span><span class="sxs-lookup"><span data-stu-id="8744c-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="8744c-120">我们将使用表单身份验证来使用我们的 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8744c-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="8744c-121">*授权*是确定经过身份验证的用户是否具有访问特定 URL/资源或执行某些操作的权限的过程。</span><span class="sxs-lookup"><span data-stu-id="8744c-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="8744c-122">例如，在我们的 NerdDinner 应用程序中，我们希望授权只有登录的用户才能访问 */Dinners/创建*URL 并创建新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="8744c-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="8744c-123">我们还希望添加授权逻辑，以便只有主持晚宴的用户才能对其进行编辑，并拒绝对所有其他用户进行编辑访问。</span><span class="sxs-lookup"><span data-stu-id="8744c-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="8744c-124">窗体身份验证和帐户控制器</span><span class="sxs-lookup"><span data-stu-id="8744c-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="8744c-125">ASP.NET MVC 的默认 Visual Studio 项目模板在创建新ASP.NET MVC 应用程序时自动启用表单身份验证。</span><span class="sxs-lookup"><span data-stu-id="8744c-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="8744c-126">它还会自动向项目添加预构建的帐户登录页实现，从而在站点中集成安全性非常容易。</span><span class="sxs-lookup"><span data-stu-id="8744c-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="8744c-127">默认的 Site.master 页在网站右上角显示"登录"链接，当用户访问该网站时未进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="8744c-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="8744c-128">单击"登录"链接会将用户带到 */帐户/登录*URL：</span><span class="sxs-lookup"><span data-stu-id="8744c-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="8744c-129">尚未注册的访问者可以通过单击"注册"链接（该链接将他们带到 */帐户/注册*URL）并允许您输入帐户详细信息来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="8744c-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="8744c-130">单击"注册"按钮将在ASP.NET成员资格系统中创建新用户，并使用表单身份验证对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="8744c-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="8744c-131">当用户登录时，Site.master 会更改页面的右上角以输出"欢迎 [用户名]！</span><span class="sxs-lookup"><span data-stu-id="8744c-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="8744c-132">消息并呈现"注销"链接，而不是"登录"链接。</span><span class="sxs-lookup"><span data-stu-id="8744c-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="8744c-133">单击"注销"链接会注销用户：</span><span class="sxs-lookup"><span data-stu-id="8744c-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="8744c-134">上述登录、注销和注册功能在帐户控制器类中实现，该类在创建项目时由 Visual Studio 添加到我们的项目中。</span><span class="sxs-lookup"><span data-stu-id="8744c-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="8744c-135">帐户控制器的 UI 使用 [Views_帐户目录中的视图模板] 实现：</span><span class="sxs-lookup"><span data-stu-id="8744c-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="8744c-136">帐户控制器类使用ASP.NET表单身份验证系统来发出加密的身份验证 Cookie，ASP.NET成员资格 API 来存储和验证用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="8744c-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="8744c-137">ASP.NET成员资格 API 是可扩展的，并且允许使用任何密码凭据存储。</span><span class="sxs-lookup"><span data-stu-id="8744c-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="8744c-138">ASP.NET附带将用户名/密码存储在 SQL 数据库或活动目录中的内置成员资格提供程序实现。</span><span class="sxs-lookup"><span data-stu-id="8744c-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="8744c-139">我们可以通过打开项目根目录的"Web.config"文件并在其中查找&lt;成员资格&gt;部分来配置我们的 NerdDinner 应用程序应该使用的成员提供商。</span><span class="sxs-lookup"><span data-stu-id="8744c-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="8744c-140">创建项目时添加的默认 Web.config 会注册 SQL 成员资格提供程序，并将其配置为使用名为"应用程序服务"的连接字符串来指定数据库位置。</span><span class="sxs-lookup"><span data-stu-id="8744c-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="8744c-141">默认的"应用程序服务"连接字符串（在 Web.config &lt;&gt;文件的连接字符串部分中指定）配置为使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="8744c-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="8744c-142">它指向名为"ASPNETDB"的 SQL Express 数据库。MDF"在应用程序的"应用\_数据"目录下。</span><span class="sxs-lookup"><span data-stu-id="8744c-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="8744c-143">如果首次在应用程序中使用成员资格 API 时此数据库不存在，ASP.NET将自动创建数据库并在其中预配适当的成员资格数据库架构：</span><span class="sxs-lookup"><span data-stu-id="8744c-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="8744c-144">如果我们不想使用 SQL Express，而是想要使用完整的 SQL Server 实例（或连接到远程数据库），我们只需更新 Web.config 文件中的"应用程序服务"连接字符串，并确保适当的成员资格架构已添加到它指向的数据库。</span><span class="sxs-lookup"><span data-stu-id="8744c-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="8744c-145">您可以在 [Windows_Microsoft.NET_Framework_v2.0.50727] 目录中运行"aspnet\_regsql.exe"实用程序，以将成员资格和其他ASP.NET应用程序服务的适当架构添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="8744c-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="8744c-146">使用 [授权] 筛选器授权 /Dinners/创建 URL</span><span class="sxs-lookup"><span data-stu-id="8744c-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="8744c-147">我们不必编写任何代码来为 NerdDinner 应用程序启用安全的身份验证和帐户管理实现。</span><span class="sxs-lookup"><span data-stu-id="8744c-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="8744c-148">用户可以在我们的应用程序中注册新帐户，以及网站登录/注销。</span><span class="sxs-lookup"><span data-stu-id="8744c-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="8744c-149">现在，我们可以向应用程序添加授权逻辑，并使用访问者的身份验证状态和用户名来控制他们在网站内可以做什么和不能做什么。</span><span class="sxs-lookup"><span data-stu-id="8744c-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="8744c-150">让我们首先将授权逻辑添加到 DinnersController 类的"创建"操作方法。</span><span class="sxs-lookup"><span data-stu-id="8744c-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="8744c-151">具体来说，我们将要求访问 */Dinner/Create* URL 的用户必须登录。</span><span class="sxs-lookup"><span data-stu-id="8744c-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="8744c-152">如果他们没有登录，我们会将其重定向到登录页面，以便他们可以登录。</span><span class="sxs-lookup"><span data-stu-id="8744c-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="8744c-153">实现此逻辑非常简单。</span><span class="sxs-lookup"><span data-stu-id="8744c-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="8744c-154">我们只需要将 [授权] 筛选器属性添加到我们的"创建操作方法"中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8744c-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="8744c-155">ASP.NET MVC 支持创建"操作筛选器"的能力，该筛选器可用于实现可声明应用于操作方法的可重用逻辑。</span><span class="sxs-lookup"><span data-stu-id="8744c-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="8744c-156">[授权] 筛选器是 ASP.NET MVC 提供的内置操作筛选器之一，它使开发人员能够声明授权规则应用于操作方法和控制器类。</span><span class="sxs-lookup"><span data-stu-id="8744c-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="8744c-157">在没有任何参数的情况下应用时（如上文所述），[授权] 筛选器强制必须登录执行操作方法请求的用户，如果浏览器未登录，则会自动将浏览器重定向到登录 URL。</span><span class="sxs-lookup"><span data-stu-id="8744c-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="8744c-158">执行此操作重定向时，最初请求的 URL 将作为查询字符串参数传递（例如：/帐户/LogOn？返回Url_%2fDinners%2f创建）。</span><span class="sxs-lookup"><span data-stu-id="8744c-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="8744c-159">然后，帐户控制器将在用户登录后将用户重定向回最初请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="8744c-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="8744c-160">[授权] 筛选器可以选择支持指定"用户"或"角色"属性的能力，该属性可用于要求用户同时登录并登录允许的用户或允许的安全角色的成员列表中。</span><span class="sxs-lookup"><span data-stu-id="8744c-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="8744c-161">例如，下面的代码只允许两个特定用户"scottgu"和"billg"访问 /Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="8744c-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="8744c-162">不过，在代码中嵌入特定的用户名往往非常无法维护。</span><span class="sxs-lookup"><span data-stu-id="8744c-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="8744c-163">更好的方法是定义代码所针对的更高级别的"角色"，然后使用数据库或活动目录系统将用户映射到角色（使实际用户映射列表能够从代码外部存储）。</span><span class="sxs-lookup"><span data-stu-id="8744c-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="8744c-164">ASP.NET包括内置角色管理 API 以及一组内置角色提供程序（包括 SQL 和 Active Directory 的内置角色提供程序），可帮助执行此用户/角色映射。</span><span class="sxs-lookup"><span data-stu-id="8744c-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="8744c-165">然后，我们可以更新代码，仅允许特定"管理员"角色中的用户访问 /Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="8744c-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="8744c-166">创建晚餐时使用User.Identity.Name属性</span><span class="sxs-lookup"><span data-stu-id="8744c-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="8744c-167">我们可以使用 Controller 基类上公开的User.Identity.Name属性检索请求当前登录用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="8744c-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="8744c-168">早些时候，当我们实现我们的Create（） 操作方法的HTTP-POST版本时，我们已经将 Dinner 的"托管比"属性硬编码为静态字符串。</span><span class="sxs-lookup"><span data-stu-id="8744c-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="8744c-169">我们现在可以更新此代码以改用User.Identity.Name属性，并为创建 Dinner 的主机自动添加 RSVP：</span><span class="sxs-lookup"><span data-stu-id="8744c-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="8744c-170">由于我们已经向 Create（） 方法添加了 [授权] 属性，因此ASP.NET MVC 可确保仅当访问 /Dinners/Create URL 的用户登录站点时，才会执行操作方法。</span><span class="sxs-lookup"><span data-stu-id="8744c-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="8744c-171">因此，User.Identity.Name属性值将始终包含有效的用户名。</span><span class="sxs-lookup"><span data-stu-id="8744c-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="8744c-172">编辑晚餐时使用User.Identity.Name属性</span><span class="sxs-lookup"><span data-stu-id="8744c-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="8744c-173">现在，让我们添加一些限制用户的授权逻辑，以便他们只能编辑自己托管的晚餐的属性。</span><span class="sxs-lookup"><span data-stu-id="8744c-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="8744c-174">为了帮助达到这一目的，我们将首先向 Dinner 对象添加"Is托管By（用户名）"帮助器方法（在之前构建的Dinner.cs部分类中）。</span><span class="sxs-lookup"><span data-stu-id="8744c-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="8744c-175">此帮助程序方法返回 true 或 false，具体取决于提供的用户名是否与 Dinner 托管 By 属性匹配，并封装执行不区分大小写的字符串比较所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="8744c-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="8744c-176">然后，我们将向 DinnersController 类中的 Edit（） 操作方法添加 [授权] 属性。</span><span class="sxs-lookup"><span data-stu-id="8744c-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="8744c-177">这将确保用户必须登录才能请求 */Dinners/Edit/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="8744c-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="8744c-178">然后，我们可以向使用 Dinner.IsHostBy（用户名）帮助器方法的"编辑"方法添加代码，以验证登录用户是否与 Dinner 主机匹配。</span><span class="sxs-lookup"><span data-stu-id="8744c-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="8744c-179">如果用户不是主机，我们将显示"无效所有者"视图并终止请求。</span><span class="sxs-lookup"><span data-stu-id="8744c-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="8744c-180">执行此操作的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="8744c-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="8744c-181">然后，我们可以右键单击 [Views_Dinners]目录，然后选择"添加&gt;-视图"菜单命令以创建新的"无效所有者"视图。</span><span class="sxs-lookup"><span data-stu-id="8744c-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="8744c-182">我们将用以下错误消息填充它：</span><span class="sxs-lookup"><span data-stu-id="8744c-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="8744c-183">现在，当用户尝试编辑他们不拥有的晚餐时，他们会得到一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="8744c-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="8744c-184">我们可以对控制器中的 Delete（） 操作方法重复相同的步骤，以锁定删除 Dinner 的权限，并确保只有晚餐的主持人才能删除它。</span><span class="sxs-lookup"><span data-stu-id="8744c-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="8744c-185">显示/隐藏编辑和删除链接</span><span class="sxs-lookup"><span data-stu-id="8744c-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="8744c-186">我们正在从"详细信息"URL 链接到"晚餐控制器"类的编辑和删除操作方法：</span><span class="sxs-lookup"><span data-stu-id="8744c-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="8744c-187">目前，我们显示"编辑和删除"操作链接，无论详细信息 URL 的访问者是否是晚宴的东道主。</span><span class="sxs-lookup"><span data-stu-id="8744c-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="8744c-188">让我们更改此内容，以便仅当访问用户是晚餐的所有者时才会显示链接。</span><span class="sxs-lookup"><span data-stu-id="8744c-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="8744c-189">晚餐控制器中的"详细信息（）"操作方法检索 Dinner 对象，然后将其作为模型对象传递给视图模板：</span><span class="sxs-lookup"><span data-stu-id="8744c-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="8744c-190">我们可以更新视图模板，以便使用"晚餐.Is托管By"（）帮助器方法有条件地显示/隐藏"编辑"和"删除"链接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8744c-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="8744c-191">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8744c-191">Next Steps</span></span>

<span data-ttu-id="8744c-192">现在，让我们来看看如何启用经过身份验证的用户到RSVP的晚餐使用AJAX。</span><span class="sxs-lookup"><span data-stu-id="8744c-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8744c-193">[上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="8744c-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>

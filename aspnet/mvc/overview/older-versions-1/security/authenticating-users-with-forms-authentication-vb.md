---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 使用表单身份验证 （VB） 对用户进行身份验证 |微软文档
author: rick-anderson
description: 了解如何使用 [授权] 属性来密码保护 MVC 应用程序中的特定页面。 您也了解如何使用网站管理...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540813"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="27e3a-104">使用 Forms 身份验证对用户进行身份验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="27e3a-104">Authenticating Users with Forms Authentication (VB)</span></span>

<span data-ttu-id="27e3a-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="27e3a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="27e3a-106">了解如何使用 [授权] 属性来密码保护 MVC 应用程序中的特定页面。</span><span class="sxs-lookup"><span data-stu-id="27e3a-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="27e3a-107">您将了解如何使用网站管理工具创建和管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="27e3a-108">您还了解如何配置用户帐户和角色信息的存储位置。</span><span class="sxs-lookup"><span data-stu-id="27e3a-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="27e3a-109">本教程的目的是说明如何使用窗体身份验证来密码保护ASP.NET MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="27e3a-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="27e3a-110">您将了解如何使用网站管理工具创建用户和角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="27e3a-111">您还学习如何防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="27e3a-112">最后，您将了解如何配置用户名和密码的存储位置。</span><span class="sxs-lookup"><span data-stu-id="27e3a-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="27e3a-113">使用网站管理工具</span><span class="sxs-lookup"><span data-stu-id="27e3a-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="27e3a-114">在做其他事情之前，我们应该从创建一些用户和角色开始。</span><span class="sxs-lookup"><span data-stu-id="27e3a-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="27e3a-115">创建新用户和角色的最简单方法是利用 Visual Studio 2008 网站管理工具。</span><span class="sxs-lookup"><span data-stu-id="27e3a-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="27e3a-116">您可以通过选择菜单选项 **"项目"ASP.NET 配置**启动此工具。</span><span class="sxs-lookup"><span data-stu-id="27e3a-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="27e3a-117">或者，您可以通过单击位于解决方案资源管理器窗口顶部的锤子（有点可怕）图标启动网站管理工具（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="27e3a-118">**图 1 – 启动网站管理工具**</span><span class="sxs-lookup"><span data-stu-id="27e3a-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="27e3a-120">在网站管理工具中，您可以通过选择"安全"选项卡创建新用户和角色。单击"**创建用户**"链接以创建名为 Stephen 的新用户（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="27e3a-121">向 Stephen 用户提供所需的任何密码（例如，*机密*）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="27e3a-122">**图 2 = 创建新用户**</span><span class="sxs-lookup"><span data-stu-id="27e3a-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="27e3a-124">通过首先启用角色和定义一个或多个角色来创建新角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="27e3a-125">通过单击 **"启用角色"链接启用角色**。</span><span class="sxs-lookup"><span data-stu-id="27e3a-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="27e3a-126">接下来，通过单击 **"创建或管理角色"链接创建**名为 *"管理员*"的角色（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="27e3a-127">**图 3 • 创建新角色**</span><span class="sxs-lookup"><span data-stu-id="27e3a-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="27e3a-129">最后，通过单击"创建用户"链接并在创建 Sally 时选择管理员（参见图 4），创建名为 Sally 的新用户并将 Sally 与管理员角色相关联。</span><span class="sxs-lookup"><span data-stu-id="27e3a-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="27e3a-130">**图 4 = 将用户添加到角色**</span><span class="sxs-lookup"><span data-stu-id="27e3a-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="27e3a-132">当所有说和完成，你应该有两个新的用户叫斯蒂芬和莎莉。</span><span class="sxs-lookup"><span data-stu-id="27e3a-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="27e3a-133">您还应具有名为"管理员"的新角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="27e3a-134">Sally 是管理员角色的成员，而斯蒂芬不是。</span><span class="sxs-lookup"><span data-stu-id="27e3a-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="27e3a-135">需要授权</span><span class="sxs-lookup"><span data-stu-id="27e3a-135">Requiring Authorization</span></span>

<span data-ttu-id="27e3a-136">在用户调用控制器操作之前，可以通过将 [授权] 属性添加到操作，要求用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="27e3a-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="27e3a-137">您可以将 [授权] 属性应用于单个控制器操作，也可以将此属性应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="27e3a-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="27e3a-138">例如，清单 1 中的控制器公开名为"公司机密"的操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="27e3a-139">由于此操作使用 [授权] 属性进行修饰，因此除非对用户进行身份验证，否则无法调用此操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="27e3a-140">**清单1 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="27e3a-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="27e3a-141">如果您在浏览器的地址栏中输入 URL/Home/CompanySecrets 来调用公司机密（）操作，而您不是经过身份验证的用户，则将自动重定向到登录视图（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="27e3a-142">**图 5 = 登录视图**</span><span class="sxs-lookup"><span data-stu-id="27e3a-142">**Figure 5 – The Login view**</span></span>

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="27e3a-144">您可以使用"登录"视图输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="27e3a-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="27e3a-145">如果您不是注册用户，则可以单击**注册**链接以导航到"注册"视图（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="27e3a-146">您可以使用"注册"视图创建新用户帐户。</span><span class="sxs-lookup"><span data-stu-id="27e3a-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="27e3a-147">**图 6 = 寄存器视图**</span><span class="sxs-lookup"><span data-stu-id="27e3a-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="27e3a-149">成功登录后，您可以看到公司机密视图（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="27e3a-150">默认情况下，您将继续登录，直到关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="27e3a-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="27e3a-151">**图 7 = 公司机密视图**</span><span class="sxs-lookup"><span data-stu-id="27e3a-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="27e3a-153">按用户名或用户角色授权</span><span class="sxs-lookup"><span data-stu-id="27e3a-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="27e3a-154">可以使用 [授权] 属性将对控制器操作的访问限制为一组特定用户或一组特定的用户角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="27e3a-155">例如，清单 2 中修改后的主控制器包含名为 StephenSecrets（） 和管理员机密（） 的两个新操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="27e3a-156">**清单2 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="27e3a-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="27e3a-157">只有用户名为 Stephen 的用户才能调用 StephenSecrets（） 操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="27e3a-158">所有其他用户都重定向到"登录"视图。</span><span class="sxs-lookup"><span data-stu-id="27e3a-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="27e3a-159">"用户"属性接受用户帐户名称的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="27e3a-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="27e3a-160">只有管理员角色中的用户可以调用管理员机密（） 操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="27e3a-161">例如，由于 Sally 是管理员组的成员，因此她可以调用管理员机密（）操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="27e3a-162">所有其他用户都重定向到"登录"视图。</span><span class="sxs-lookup"><span data-stu-id="27e3a-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="27e3a-163">角色属性接受角色名称的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="27e3a-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="27e3a-164">配置身份验证</span><span class="sxs-lookup"><span data-stu-id="27e3a-164">Configuring Authentication</span></span>

<span data-ttu-id="27e3a-165">此时，您可能想知道用户帐户和角色信息的存储位置。</span><span class="sxs-lookup"><span data-stu-id="27e3a-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="27e3a-166">默认情况下，信息存储在 MVC 应用程序的应用程序\_数据文件夹中，名为 ASPNETDB.mdf 的 （RANU） SQL Express 数据库中。</span><span class="sxs-lookup"><span data-stu-id="27e3a-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="27e3a-167">当您开始使用成员资格时，此数据库由ASP.NET框架自动生成。</span><span class="sxs-lookup"><span data-stu-id="27e3a-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="27e3a-168">要查看解决方案资源管理器窗口中的 ASPNETDB.mdf 数据库，首先需要选择菜单选项"项目"，显示所有文件。</span><span class="sxs-lookup"><span data-stu-id="27e3a-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="27e3a-169">开发应用程序时，可以使用默认 SQL Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="27e3a-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="27e3a-170">但是，您很可能不希望为生产应用程序使用默认的 ASPNETDB.mdf 数据库。</span><span class="sxs-lookup"><span data-stu-id="27e3a-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="27e3a-171">在这种情况下，您可以通过完成以下两个步骤来更改用户帐户信息的存储位置：</span><span class="sxs-lookup"><span data-stu-id="27e3a-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="27e3a-172">将应用程序服务数据库对象添加到生产数据库 - 更改应用程序连接字符串以指向生产数据库</span><span class="sxs-lookup"><span data-stu-id="27e3a-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="27e3a-173">第一步是将所有必要的数据库对象（表和存储过程）添加到生产数据库中。</span><span class="sxs-lookup"><span data-stu-id="27e3a-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="27e3a-174">将这些对象添加到新数据库的最简单方法是利用ASP.NET SQL 服务器设置向导（参见图 8）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="27e3a-175">您可以通过从 Microsoft Visual Studio 2008 程序组打开 Visual Studio 2008 命令提示符并从命令提示符执行以下命令来启动此工具：</span><span class="sxs-lookup"><span data-stu-id="27e3a-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="27e3a-176">阿斯普内\_雷格斯</span><span class="sxs-lookup"><span data-stu-id="27e3a-176">aspnet\_regsql</span></span>

<span data-ttu-id="27e3a-177">**图 8 = ASP.NET SQL 服务器设置向导**</span><span class="sxs-lookup"><span data-stu-id="27e3a-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="27e3a-179">ASP.NET SQL 服务器设置向导使您能够在网络上选择 SQL Server 数据库，并安装ASP.NET应用程序服务所需的所有数据库对象。</span><span class="sxs-lookup"><span data-stu-id="27e3a-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="27e3a-180">数据库服务器不需要位于本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="27e3a-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="27e3a-181">如果不想使用ASP.NET SQL 服务器设置向导，则可以在以下文件夹中找到用于添加应用程序服务数据库对象的 SQL 脚本：</span><span class="sxs-lookup"><span data-stu-id="27e3a-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="27e3a-182">C：[视窗]微软.NET_框架_v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="27e3a-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="27e3a-183">创建必要的数据库对象后，需要修改 MVC 应用程序使用的数据库连接。</span><span class="sxs-lookup"><span data-stu-id="27e3a-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="27e3a-184">修改 Web 配置 （Web.config） 文件中的应用程序服务连接字符串，以便它指向生产数据库。</span><span class="sxs-lookup"><span data-stu-id="27e3a-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="27e3a-185">例如，清单中修改的连接指向名为 MyProductionDB 的数据库（原始应用程序服务连接字符串已注释掉）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="27e3a-186">**清单3 = Web.config**</span><span class="sxs-lookup"><span data-stu-id="27e3a-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="27e3a-187">配置数据库权限</span><span class="sxs-lookup"><span data-stu-id="27e3a-187">Configuring Database Permissions</span></span>

<span data-ttu-id="27e3a-188">如果使用集成安全连接到数据库，则需要添加正确的 Windows 用户帐户作为数据库的登录。</span><span class="sxs-lookup"><span data-stu-id="27e3a-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="27e3a-189">正确的帐户取决于您是使用ASP.NET开发服务器还是 Internet 信息服务作为 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="27e3a-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="27e3a-190">正确的用户帐户还取决于您的操作系统。</span><span class="sxs-lookup"><span data-stu-id="27e3a-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="27e3a-191">如果使用ASP.NET开发服务器（Visual Studio 使用的默认 Web 服务器），则应用程序将在 Windows 用户帐户的上下文中执行。</span><span class="sxs-lookup"><span data-stu-id="27e3a-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="27e3a-192">在这种情况下，您需要将 Windows 用户帐户添加为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="27e3a-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="27e3a-193">或者，如果您使用的是互联网信息服务，则需要将 ASPNET 帐户或 NT AUTHORITY/网络服务帐户添加为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="27e3a-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="27e3a-194">如果使用 Windows XP，则添加 ASPNET 帐户作为数据库的登录名。</span><span class="sxs-lookup"><span data-stu-id="27e3a-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="27e3a-195">如果您使用的是较新的操作系统，如 Windows Vista 或 Windows Server 2008，则添加 NT AUTHORITY/网络服务帐户作为数据库登录。</span><span class="sxs-lookup"><span data-stu-id="27e3a-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="27e3a-196">您可以使用 Microsoft SQL 服务器管理工作室向数据库添加新用户帐户（参见图 9）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="27e3a-197">**图 9 = 创建新的 Microsoft SQL Server 登录名**</span><span class="sxs-lookup"><span data-stu-id="27e3a-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="27e3a-199">创建所需的登录后，需要将登录映射到具有正确数据库角色的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="27e3a-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="27e3a-200">双击登录名并选择"用户映射"选项卡。选择一个或多个应用程序服务数据库角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="27e3a-201">例如，为了对用户进行身份验证，您需要启用 aspnet\_成员资格\_基本访问数据库角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="27e3a-202">要创建新用户，您需要启用 aspnet\_成员资格\_完全访问数据库角色（参见图 10）。</span><span class="sxs-lookup"><span data-stu-id="27e3a-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="27e3a-203">**图 10 = 添加应用程序服务数据库角色**</span><span class="sxs-lookup"><span data-stu-id="27e3a-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="27e3a-205">总结</span><span class="sxs-lookup"><span data-stu-id="27e3a-205">Summary</span></span>

<span data-ttu-id="27e3a-206">在本教程中，您学习了在构建 ASP.NET MVC 应用程序时如何使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="27e3a-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="27e3a-207">首先，您学习了如何通过利用网站管理工具创建新用户和角色。</span><span class="sxs-lookup"><span data-stu-id="27e3a-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="27e3a-208">接下来，您学习了如何使用 [授权] 属性来防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="27e3a-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="27e3a-209">最后，您学习了如何配置 MVC 应用程序以在生产数据库中存储用户和角色信息。</span><span class="sxs-lookup"><span data-stu-id="27e3a-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="27e3a-210">[上一页](preventing-javascript-injection-attacks-cs.md)
> [下一页](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="27e3a-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>

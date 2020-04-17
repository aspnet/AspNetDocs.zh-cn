---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 会员 |微软文档
author: rick-anderson
description: ASP.NET成员资格基于表单身份验证模型从 ASP.NET 1.x 的成功为基础。 ASP.NET窗体身份验证提供了一种便捷的方法来进行体形...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543764"
---
# <a name="membership"></a><span data-ttu-id="d1d85-104">Membership</span><span class="sxs-lookup"><span data-stu-id="d1d85-104">Membership</span></span>

<span data-ttu-id="d1d85-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d1d85-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d1d85-106">ASP.NET成员资格基于表单身份验证模型从 ASP.NET 1.x 的成功为基础。</span><span class="sxs-lookup"><span data-stu-id="d1d85-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="d1d85-107">ASP.NET窗体身份验证提供了将登录表单合并到ASP.NET应用程序中以及根据数据库或其他数据存储验证用户的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="d1d85-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>

<span data-ttu-id="d1d85-108">ASP.NET成员资格基于表单身份验证模型从 ASP.NET 1.x 的成功为基础。</span><span class="sxs-lookup"><span data-stu-id="d1d85-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="d1d85-109">ASP.NET窗体身份验证提供了将登录表单合并到ASP.NET应用程序中以及根据数据库或其他数据存储验证用户的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="d1d85-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="d1d85-110">窗体身份验证类的成员可以处理 Cookie 进行身份验证、检查有效登录、注销用户等。但是，在ASP.NET 1.x 应用程序中实现窗体身份验证可能需要大量代码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="d1d85-111">ASP.NET 2.0 中的成员资格是单独使用窗体身份验证的一大进步。</span><span class="sxs-lookup"><span data-stu-id="d1d85-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="d1d85-112">（与窗体身份验证结合时，成员资格最可靠，但使用窗体身份验证不是要求。正如您很快就会看到的那样，您可以使用ASP.NET 2.0 中的ASP.NET成员资格和登录控件来实现强大的成员资格系统，而无需编写大量代码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="d1d85-113">在 ASP.NET 2.0 中实施成员资格</span><span class="sxs-lookup"><span data-stu-id="d1d85-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="d1d85-114">成员资格通过以下四个步骤实现。</span><span class="sxs-lookup"><span data-stu-id="d1d85-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="d1d85-115">请记住，涉及许多子步骤以及可选配置，也可以实现。</span><span class="sxs-lookup"><span data-stu-id="d1d85-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="d1d85-116">这些步骤旨在说明配置成员资格的大图景。</span><span class="sxs-lookup"><span data-stu-id="d1d85-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="d1d85-117">创建成员资格数据库（如果 SQL Server 用作成员资格存储。</span><span class="sxs-lookup"><span data-stu-id="d1d85-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="d1d85-118">指定应用程序配置文件中的成员资格选项。</span><span class="sxs-lookup"><span data-stu-id="d1d85-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="d1d85-119">（默认情况下启用成员资格。</span><span class="sxs-lookup"><span data-stu-id="d1d85-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="d1d85-120">确定要使用的成员资格存储的类型。</span><span class="sxs-lookup"><span data-stu-id="d1d85-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="d1d85-121">选项有：</span><span class="sxs-lookup"><span data-stu-id="d1d85-121">Options are:</span></span> 

    - <span data-ttu-id="d1d85-122">微软 SQL 服务器（版本 7.0 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="d1d85-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="d1d85-123">活动目录存储</span><span class="sxs-lookup"><span data-stu-id="d1d85-123">Active Directory Store</span></span>
    - <span data-ttu-id="d1d85-124">自定义成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="d1d85-124">Custom membership provider</span></span>
4. <span data-ttu-id="d1d85-125">配置应用程序以进行ASP.NET窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="d1d85-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="d1d85-126">再次，成员资格旨在利用窗体身份验证，但使用窗体身份验证不是一项要求。</span><span class="sxs-lookup"><span data-stu-id="d1d85-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="d1d85-127">为成员资格定义用户帐户，并根据需要配置角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="d1d85-128">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="d1d85-128">Creating the Membership Database</span></span>

<span data-ttu-id="d1d85-129">如果您使用 SQL Server 7.0 或更高版本作为成员资格存储，则可以使用 aspnet\_regsql 实用程序（从 Visual Studio .NET 2005 命令提示符中最容易使用）来配置数据库。</span><span class="sxs-lookup"><span data-stu-id="d1d85-129">If you're using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="d1d85-130">aspnet\_regsql 实用程序可用作命令提示工具或通过 GUI 向导。</span><span class="sxs-lookup"><span data-stu-id="d1d85-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="d1d85-131">向导方法是配置数据库的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="d1d85-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="d1d85-132">要访问向导，只需运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d1d85-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="d1d85-133">运行该命令后，将显示ASP.NET SQL 服务器设置向导，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>

![](membership/_static/image1.jpg)

<span data-ttu-id="d1d85-134">**图 1**</span><span class="sxs-lookup"><span data-stu-id="d1d85-134">**Figure 1**</span></span>

<span data-ttu-id="d1d85-135">ASP.NET SQL 服务器设置向导会在向导中指定的实例中创建网站。</span><span class="sxs-lookup"><span data-stu-id="d1d85-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="d1d85-136">但是，ASP.NET将使用计算机中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d1d85-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="d1d85-137">默认情况下，此连接字符串将指向 SQL Server 2005 实例，因此，如果您使用的是 SQL Server 2000 或 SQL Server 7.0 实例，则需要修改计算机中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d1d85-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="d1d85-138">该连接字符串可以位于此处：</span><span class="sxs-lookup"><span data-stu-id="d1d85-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="d1d85-139">遗憾的是，如果不修改连接字符串，ASP.NET不会给您带来描述性错误。</span><span class="sxs-lookup"><span data-stu-id="d1d85-139">Unfortunately, if you don't modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="d1d85-140">它会继续抱怨说，你还没有创建数据库。</span><span class="sxs-lookup"><span data-stu-id="d1d85-140">It will just continue to complain saying that you haven't created the database.</span></span> <span data-ttu-id="d1d85-141">在上面的案例中，我修改了连接字符串以指向我的本地 SQL Server 2000 实例。</span><span class="sxs-lookup"><span data-stu-id="d1d85-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="d1d85-142">指定配置和添加用户和角色</span><span class="sxs-lookup"><span data-stu-id="d1d85-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="d1d85-143">配置成员资格的下一步是向应用程序的 Web.config 文件添加必要的信息。</span><span class="sxs-lookup"><span data-stu-id="d1d85-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="d1d85-144">在ASP.NET 1.x 中，由于使用较低CamelCase和缺乏 Intellisense，修改 Web.config 文件有时很困难。</span><span class="sxs-lookup"><span data-stu-id="d1d85-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="d1d85-145">Visual Studio .NET 2005 使配置文件的 Intellisense 任务更加轻松，但 ASP.NET 2.0 通过提供用于编辑配置文件的 Web 界面更进一步。</span><span class="sxs-lookup"><span data-stu-id="d1d85-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="d1d85-146">您可以通过单击解决方案资源管理器工具栏上的ASP.NET配置按钮来启动 Web 界面，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="d1d85-147">您还可以通过插入登录控件时显示的弹出窗口启动 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="d1d85-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>

![](membership/_static/image2.jpg)

<span data-ttu-id="d1d85-148">**图 2**</span><span class="sxs-lookup"><span data-stu-id="d1d85-148">**Figure 2**</span></span>

<span data-ttu-id="d1d85-149">这将启动下面所示的ASP.NET网站管理工具。</span><span class="sxs-lookup"><span data-stu-id="d1d85-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="d1d85-150">ASP.NET网站管理是一个四选项卡界面，便于管理应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="d1d85-151">以下选项卡可用：</span><span class="sxs-lookup"><span data-stu-id="d1d85-151">The following tabs are available:</span></span>

- <span data-ttu-id="d1d85-152">**主页**</span><span class="sxs-lookup"><span data-stu-id="d1d85-152">**Home**</span></span>
- <span data-ttu-id="d1d85-153">**安全性**配置用户、角色和访问权限。</span><span class="sxs-lookup"><span data-stu-id="d1d85-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="d1d85-154">**应用**配置应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="d1d85-155">**提供商**配置和测试应用程序成员资格提供程序。</span><span class="sxs-lookup"><span data-stu-id="d1d85-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="d1d85-156">网站管理工具允许您轻松创建新用户、创建新角色以及管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="d1d85-157">此功能在 Windows 界面中不可用。</span><span class="sxs-lookup"><span data-stu-id="d1d85-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="d1d85-158">Windows 界面允许您轻松定义授权设置，并添加、删除和管理不在网站管理工具中的提供程序。</span><span class="sxs-lookup"><span data-stu-id="d1d85-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="d1d85-159">要启动 Windows 界面，请打开 Internet 信息服务卡入，右键单击应用程序，然后选择"属性"。</span><span class="sxs-lookup"><span data-stu-id="d1d85-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="d1d85-160">单击ASP.NET选项卡，然后单击"编辑配置"按钮。</span><span class="sxs-lookup"><span data-stu-id="d1d85-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="d1d85-161">（应用程序必须在 2.0 ASP.NET下运行才能启用"编辑配置"按钮。</span><span class="sxs-lookup"><span data-stu-id="d1d85-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="d1d85-162">您还可以在ASP.NET对话框中配置ASP.NET版本。ASP.NET 配置设置对话框如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>

![](membership/_static/image3.jpg)

<span data-ttu-id="d1d85-163">**图 3**</span><span class="sxs-lookup"><span data-stu-id="d1d85-163">**Figure 3**</span></span>

<span data-ttu-id="d1d85-164">在"常规"选项卡上，将列出连接字符串和应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="d1d85-165">斜体的任何设置都在父配置文件（机器.config 或更高级别的 Web.config）中定义，而斜体化的设置来自应用程序配置文件。</span><span class="sxs-lookup"><span data-stu-id="d1d85-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="d1d85-166">如果在应用程序级别添加、删除或编辑设置，ASP.NET将在应用程序级别 Web.config 上添加、删除或修改该设置，而不是从继承该设置的配置文件中删除该设置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="d1d85-167">"身份验证"选项卡如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="d1d85-168">这是您将配置成员资格设置的位置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="d1d85-169">可以在此处配置窗体身份验证设置、成员资格提供程序和角色提供程序。</span><span class="sxs-lookup"><span data-stu-id="d1d85-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>

![](membership/_static/image4.jpg)

<span data-ttu-id="d1d85-170">**图 4**</span><span class="sxs-lookup"><span data-stu-id="d1d85-170">**Figure 4**</span></span>

## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="d1d85-171">在应用程序中实现成员资格</span><span class="sxs-lookup"><span data-stu-id="d1d85-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="d1d85-172">实现应用程序中ASP.NET 2.0 成员资格的最简单方法是使用提供的登录控件。</span><span class="sxs-lookup"><span data-stu-id="d1d85-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="d1d85-173">此方法允许您实现ASP.NET 2.0 成员资格的基础知识，而无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="d1d85-174">以下登录控件在 2.0 ASP.NET中可用：</span><span class="sxs-lookup"><span data-stu-id="d1d85-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="d1d85-175">登录控制</span><span class="sxs-lookup"><span data-stu-id="d1d85-175">Login Control</span></span>

<span data-ttu-id="d1d85-176">登录控件为某人提供登录您的成员资格系统的界面。</span><span class="sxs-lookup"><span data-stu-id="d1d85-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="d1d85-177">它为您提供用户名和密码文本框和登录按钮。</span><span class="sxs-lookup"><span data-stu-id="d1d85-177">It provides you with a username and password textbox and a login button.</span></span> <span data-ttu-id="d1d85-178">许多其他常见功能，例如尚未注册的用户的链接、允许用户在后续访问时自动登录的复选框、密码提醒链接等。登录控件的所有功能都可通过控件的属性进行自定义。</span><span class="sxs-lookup"><span data-stu-id="d1d85-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="d1d85-179">在ASP.NET 1.x 中，开发人员在使用窗体身份验证时必须编写相当数量的代码来执行查找。</span><span class="sxs-lookup"><span data-stu-id="d1d85-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="d1d85-180">使用ASP.NET 2.0 成员资格，无需编写任何代码即可验证用户。</span><span class="sxs-lookup"><span data-stu-id="d1d85-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="d1d85-181">ASP.NET会自动为您查找用户。</span><span class="sxs-lookup"><span data-stu-id="d1d85-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="d1d85-182">（如果您使用登录控件而不使用ASP.NET成员资格，则可以使用**OnAuthenticate**方法验证用户。</span><span class="sxs-lookup"><span data-stu-id="d1d85-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="d1d85-183">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="d1d85-183">LoginView Control</span></span>

<span data-ttu-id="d1d85-184">LoginView 控件是一个模板化控件，默认情况下提供两个模板;匿名模板和登录模板。</span><span class="sxs-lookup"><span data-stu-id="d1d85-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="d1d85-185">显示的模板由用户是否登录到您的成员资格系统决定。</span><span class="sxs-lookup"><span data-stu-id="d1d85-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="d1d85-186">此控件通常用于在用户尚未登录时显示登录控件，以及用户登录时的登录状态控件和/或其他登录控件。</span><span class="sxs-lookup"><span data-stu-id="d1d85-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="d1d85-187">如果在ASP.NET应用程序中使用角色管理，则 LoginView 控件可以基于用户角色显示特定的模板。</span><span class="sxs-lookup"><span data-stu-id="d1d85-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="d1d85-188">（稍后将介绍有关ASP.NET角色管理的更多内容。</span><span class="sxs-lookup"><span data-stu-id="d1d85-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="d1d85-189">密码恢复控制</span><span class="sxs-lookup"><span data-stu-id="d1d85-189">PasswordRecovery Control</span></span>

<span data-ttu-id="d1d85-190">密码恢复控件允许用户接收包含其当前密码的电子邮件或重置其密码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="d1d85-191">可以恢复明文和加密的密码并通过电子邮件发送给用户。</span><span class="sxs-lookup"><span data-stu-id="d1d85-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="d1d85-192">如果密码已哈希，则无法恢复密码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="d1d85-193">相反，用户将需要执行密码重置。</span><span class="sxs-lookup"><span data-stu-id="d1d85-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="d1d85-194">登录状态控制</span><span class="sxs-lookup"><span data-stu-id="d1d85-194">LoginStatus Control</span></span>

<span data-ttu-id="d1d85-195">登录状态控件用于向未登录的用户显示登录指示器，向当前登录的用户显示注销指示器。</span><span class="sxs-lookup"><span data-stu-id="d1d85-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="d1d85-196">"请求.已验证"属性用于确定要显示的指示器。</span><span class="sxs-lookup"><span data-stu-id="d1d85-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="d1d85-197">登录状态控件显示的指示器可以是文本（通过**登录文本**和**注销文本**属性实现）或图像（通过**登录图像Url**和**LogoutImageUrl**属性实现）。</span><span class="sxs-lookup"><span data-stu-id="d1d85-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="d1d85-198">当用户通过登录状态控件注销时，他或她将重定向到**LogoutPageUrl**属性指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="d1d85-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="d1d85-199">如果未设置该属性，则刷新当前页面。</span><span class="sxs-lookup"><span data-stu-id="d1d85-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="d1d85-200">由于网站可能受窗体身份验证保护，因此当前页面的刷新将用户重定向到站点的登录页。</span><span class="sxs-lookup"><span data-stu-id="d1d85-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="d1d85-201">登录名控制</span><span class="sxs-lookup"><span data-stu-id="d1d85-201">LoginName Control</span></span>

<span data-ttu-id="d1d85-202">"登录名称"控件显示当前登录到站点的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="d1d85-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="d1d85-203">创建用户向导控件</span><span class="sxs-lookup"><span data-stu-id="d1d85-203">CreateUserWizard Control</span></span>

<span data-ttu-id="d1d85-204">CreateUserWizard 控件为用户提供了注册会员系统的便捷方式。</span><span class="sxs-lookup"><span data-stu-id="d1d85-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="d1d85-205">您可以通过如下所示的界面添加步骤（作为向导步骤的集合实现）。</span><span class="sxs-lookup"><span data-stu-id="d1d85-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>

![](membership/_static/image5.jpg)

<span data-ttu-id="d1d85-206">**图 5**</span><span class="sxs-lookup"><span data-stu-id="d1d85-206">**Figure 5**</span></span>

<span data-ttu-id="d1d85-207">CreateUserWizard 是一个模板化控件，派生自向导类并提供以下模板：</span><span class="sxs-lookup"><span data-stu-id="d1d85-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="d1d85-208">**标题模板**此模板控制向导标头的外观。</span><span class="sxs-lookup"><span data-stu-id="d1d85-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="d1d85-209">**侧边栏模板**此模板控制向导侧边栏的外观。</span><span class="sxs-lookup"><span data-stu-id="d1d85-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="d1d85-210">**启动导航模板**此模板控制导航的外观是向导在开始步骤。</span><span class="sxs-lookup"><span data-stu-id="d1d85-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="d1d85-211">**步进导航模板**此模板控制在导航区域的外观时不在开始或完成步骤中。</span><span class="sxs-lookup"><span data-stu-id="d1d85-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="d1d85-212">**完成导航模板**此模板控制导航区域在完成步骤上的外观。</span><span class="sxs-lookup"><span data-stu-id="d1d85-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="d1d85-213">此外，对于添加到向导的每个步骤，ASP.NET将创建一个自定义模板，其中包含该步骤的内容模板和自定义导航模板。</span><span class="sxs-lookup"><span data-stu-id="d1d85-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="d1d85-214">有关自定义 CreateUserWizard 的完整详细信息，请参阅 2005 年VS.NET文档：</span><span class="sxs-lookup"><span data-stu-id="d1d85-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="d1d85-215">更改密码控制</span><span class="sxs-lookup"><span data-stu-id="d1d85-215">ChangePassword Control</span></span>

<span data-ttu-id="d1d85-216">更改密码控件允许用户更改其密码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="d1d85-217">如果 DisplayUserName 属性为 true（默认情况下为 false），则用户可以在未登录时更改其密码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="d1d85-218">如果用户*已*登录，并且 DisplayUserName 属性为 true，则用户将能够更改未登录的其他用户的密码，前提是他们知道该用户的用户 ID。</span><span class="sxs-lookup"><span data-stu-id="d1d85-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="d1d85-219">请记住，如果您希望用户能够在无需登录的情况下更改密码，则需要确保显示更改密码控件的页面允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="d1d85-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="d1d85-220">显然，用户必须提供其旧密码才能更改其密码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="d1d85-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="d1d85-221">Role Management</span></span>

<span data-ttu-id="d1d85-222">角色管理允许您将用户分配给特定角色，然后根据该角色限制对某些文件或文件夹的访问。</span><span class="sxs-lookup"><span data-stu-id="d1d85-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="d1d85-223">角色管理还提供 API，以便您可以以编程方式确定某人的角色或确定特定角色的所有用户并做出相应响应。</span><span class="sxs-lookup"><span data-stu-id="d1d85-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="d1d85-224">角色管理不是ASP.NET成员的要求，也不是使用角色管理的要求。</span><span class="sxs-lookup"><span data-stu-id="d1d85-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="d1d85-225">然而，两者互相补充得很好，开发人员可能会将它们结合使用。</span><span class="sxs-lookup"><span data-stu-id="d1d85-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="d1d85-226">要在应用程序中启用角色管理，请对 Web.config 文件中进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="d1d85-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="d1d85-227">当**缓存RolesInCookie**属性设置为 true 时，ASP.NET缓存客户端 Cookie 中的用户角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="d1d85-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="d1d85-228">这允许在不调用角色提供程序的情况下进行角色查找。</span><span class="sxs-lookup"><span data-stu-id="d1d85-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="d1d85-229">使用此属性时，鼓励开发人员确保**cookie 保护**属性设置为"全部"。</span><span class="sxs-lookup"><span data-stu-id="d1d85-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="d1d85-230">（这是默认设置。这可确保 Cookie 数据经过加密，并有助于确保 Cookie 内容未被更改。</span><span class="sxs-lookup"><span data-stu-id="d1d85-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents haven't been altered.</span></span> <span data-ttu-id="d1d85-231">可以使用网站管理工具添加角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="d1d85-232">它允许您轻松定义角色、根据这些角色配置对网站部分的访问，并将用户分配给角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>

![](membership/_static/image6.jpg)

<span data-ttu-id="d1d85-233">**图 6**</span><span class="sxs-lookup"><span data-stu-id="d1d85-233">**Figure 6**</span></span>

<span data-ttu-id="d1d85-234">如上所述，只需输入角色的名称，然后单击"添加角色"即可添加新角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="d1d85-235">通过单击现有角色列表中的相应链接，可以管理或删除现有角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="d1d85-236">管理角色时，可以添加或删除用户，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-236">When you manage a role, you can add or remove users as shown below.</span></span>

![](membership/_static/image7.jpg)

<span data-ttu-id="d1d85-237">**图 7**</span><span class="sxs-lookup"><span data-stu-id="d1d85-237">**Figure 7**</span></span>

<span data-ttu-id="d1d85-238">通过选中"用户处于角色"复选框，可以轻松地将用户添加到特定角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="d1d85-239">ASP.NET将自动使用适当的条目更新您的成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="d1d85-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="d1d85-240">您还需要为应用程序配置访问规则。</span><span class="sxs-lookup"><span data-stu-id="d1d85-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="d1d85-241">ASP.NET 1.x 开发人员熟悉通过 Web.config 文件中&lt;的授权&gt;元素执行此操作，该选项在 2.0 ASP.NET中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="d1d85-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="d1d85-242">但是，它更易于使用网站管理工具管理访问规则，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1d85-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>

![](membership/_static/image8.jpg)

<span data-ttu-id="d1d85-243">**图 8**</span><span class="sxs-lookup"><span data-stu-id="d1d85-243">**Figure 8**</span></span>

<span data-ttu-id="d1d85-244">在这种情况下，管理文件夹将突出显示（由于该工具以浅灰色突出显示它而难以查看），并且管理员角色已被授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="d1d85-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="d1d85-245">所有其他用户都被拒绝。</span><span class="sxs-lookup"><span data-stu-id="d1d85-245">All other users are denied.</span></span> <span data-ttu-id="d1d85-246">您可以单击头部图标来选择规则，然后使用"向上移动"和"向下移动"按钮来排列规则。</span><span class="sxs-lookup"><span data-stu-id="d1d85-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="d1d85-247">与ASP.NET&lt;授权&gt;元素一样，规则按它们出现的顺序进行处理。</span><span class="sxs-lookup"><span data-stu-id="d1d85-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="d1d85-248">换句话说，如果上述镜头中的规则顺序颠倒，则任何人都无法访问管理文件夹，因为ASP.NET遇到的第一个规则是拒绝所有人到该文件夹的规则。</span><span class="sxs-lookup"><span data-stu-id="d1d85-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="d1d85-249">ASP.NET 2.0 将 Web.config 文件添加到要为其指定访问规则的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d1d85-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="d1d85-250">访问规则可以通过配置文件或通过网站管理工具进行编辑。</span><span class="sxs-lookup"><span data-stu-id="d1d85-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="d1d85-251">换句话说，网站管理工具只是一个界面，可以通过该界面在用户友好的环境中编辑配置文件。</span><span class="sxs-lookup"><span data-stu-id="d1d85-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="d1d85-252">在代码中使用角色</span><span class="sxs-lookup"><span data-stu-id="d1d85-252">Using Roles in Code</span></span>

<span data-ttu-id="d1d85-253">自版本 1.x 以来，用于角色管理的 API 未更改。</span><span class="sxs-lookup"><span data-stu-id="d1d85-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="d1d85-254">**IsInRole**方法用于确定用户是否处于特定角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="d1d85-255">ASP.NET还会创建作为当前上下文的成员的 RoleThe 实例。</span><span class="sxs-lookup"><span data-stu-id="d1d85-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="d1d85-256">RoleThe 对象可用于获取用户所属的所有角色，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1d85-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="d1d85-257">将角色组与登录视图控件一起使用</span><span class="sxs-lookup"><span data-stu-id="d1d85-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="d1d85-258">现在，您已经了解了角色管理和成员资格，让我们简要讨论一下 LoginView 控件如何在 ASP.NET 2.0 中利用此功能。</span><span class="sxs-lookup"><span data-stu-id="d1d85-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="d1d85-259">如前所述，LoginView 控件是一个模板化控件，默认情况下包含两个模板;默认情况下，该控件包含两个模板。匿名模板和登录模板。</span><span class="sxs-lookup"><span data-stu-id="d1d85-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="d1d85-260">在"登录查看任务"对话框中，是一个链接（如下所示），允许您编辑角色组。</span><span class="sxs-lookup"><span data-stu-id="d1d85-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>

![](membership/_static/image9.jpg)

<span data-ttu-id="d1d85-261">**图 9**</span><span class="sxs-lookup"><span data-stu-id="d1d85-261">**Figure 9**</span></span>

<span data-ttu-id="d1d85-262">每个 RoleGroup 对象都包含一个字符串数组，用于定义角色组应用于哪些角色。</span><span class="sxs-lookup"><span data-stu-id="d1d85-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="d1d85-263">要向"登录视图"控件添加新角色组，请单击"编辑角色组"链接。</span><span class="sxs-lookup"><span data-stu-id="d1d85-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="d1d85-264">在上面的映像中，您可以看到我为管理员添加了新的角色组。</span><span class="sxs-lookup"><span data-stu-id="d1d85-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="d1d85-265">通过从"视图"下拉列表中选择该角色组（RoleGroup{0}），我可以配置一个仅显示给管理员角色的模板。</span><span class="sxs-lookup"><span data-stu-id="d1d85-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="d1d85-266">在下图中，我添加了一个新的 RoleGroup，该角色组适用于销售角色和分发角色的成员。</span><span class="sxs-lookup"><span data-stu-id="d1d85-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="d1d85-267">这会将第二个角色组添加到 LoginView 任务对话框中的"视图"下拉下拉，而添加到该模板的任何内容都将被"销售"或"分发"角色中的任何用户看到。</span><span class="sxs-lookup"><span data-stu-id="d1d85-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>

![](membership/_static/image10.jpg)

<span data-ttu-id="d1d85-268">**图 10**</span><span class="sxs-lookup"><span data-stu-id="d1d85-268">**Figure 10**</span></span>

## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="d1d85-269">重写现有成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="d1d85-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="d1d85-270">有几种方法可以扩展ASP.NET成员资格的功能。</span><span class="sxs-lookup"><span data-stu-id="d1d85-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="d1d85-271">首先，您显然可以通过继承 SqlSasas提供程序类并重写其方法来更改其现有功能。</span><span class="sxs-lookup"><span data-stu-id="d1d85-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="d1d85-272">例如，如果要在创建用户时实现自己的功能，可以创建自己的类，从 SqlSaasProvider 继承，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1d85-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="d1d85-273">另一方面，如果要创建自己的提供程序（例如，将成员资格信息存储在 Access 数据库中），则可以创建自己的提供程序。</span><span class="sxs-lookup"><span data-stu-id="d1d85-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="d1d85-274">创建您自己的成员资格提供商</span><span class="sxs-lookup"><span data-stu-id="d1d85-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="d1d85-275">要创建自己的成员资格提供程序，首先需要创建从成员资格提供程序类继承的类。</span><span class="sxs-lookup"><span data-stu-id="d1d85-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="d1d85-276">如果使用VB.NET，Visual Studio 2005 将添加需要重写的所有方法的存根。</span><span class="sxs-lookup"><span data-stu-id="d1d85-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="d1d85-277">如果使用 C#，则要添加存根。</span><span class="sxs-lookup"><span data-stu-id="d1d85-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="d1d85-278">您需要重写以下内容：</span><span class="sxs-lookup"><span data-stu-id="d1d85-278">You will need to override the following:</span></span>

- <span data-ttu-id="d1d85-279">应用程序名称属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-279">ApplicationName property</span></span>
- <span data-ttu-id="d1d85-280">更改密码功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-280">ChangePassword function</span></span>
- <span data-ttu-id="d1d85-281">更改密码问答功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="d1d85-282">创建用户函数</span><span class="sxs-lookup"><span data-stu-id="d1d85-282">CreateUser function</span></span>
- <span data-ttu-id="d1d85-283">删除用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-283">DeleteUser function</span></span>
- <span data-ttu-id="d1d85-284">启用密码重置属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="d1d85-285">启用密码检索属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="d1d85-286">查找用户电子邮件功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="d1d85-287">查找用户按名称函数</span><span class="sxs-lookup"><span data-stu-id="d1d85-287">FindUsersByName function</span></span>
- <span data-ttu-id="d1d85-288">获取所有用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-288">GetAllUsers function</span></span>
- <span data-ttu-id="d1d85-289">获取用户数量联机功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="d1d85-290">获取密码功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-290">GetPassword function</span></span>
- <span data-ttu-id="d1d85-291">获取用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-291">GetUser function</span></span>
- <span data-ttu-id="d1d85-292">获取用户名通过电子邮件功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="d1d85-293">最大无效密码尝试属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="d1d85-294">最小必需的NonAlpha字符属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="d1d85-295">最小所需密码长度属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="d1d85-296">密码尝试窗口属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="d1d85-297">密码格式属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-297">PasswordFormat property</span></span>
- <span data-ttu-id="d1d85-298">密码强度正则表达式属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="d1d85-299">需要问答属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="d1d85-300">需要唯一电子邮件属性</span><span class="sxs-lookup"><span data-stu-id="d1d85-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="d1d85-301">重置密码功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-301">ResetPassword function</span></span>
- <span data-ttu-id="d1d85-302">解锁用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-302">Unlock user function</span></span>
- <span data-ttu-id="d1d85-303">更新用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-303">UpdateUser function</span></span>
- <span data-ttu-id="d1d85-304">验证用户功能</span><span class="sxs-lookup"><span data-stu-id="d1d85-304">ValidateUser function</span></span>

<span data-ttu-id="d1d85-305">这是一个相当的列表，以C#开发人员实现。</span><span class="sxs-lookup"><span data-stu-id="d1d85-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="d1d85-306">您可能会发现在没有任何实现的情况下在VB.NET中创建类会更容易，然后使用 .NET 反射器或类似工具将代码转换为 C#。</span><span class="sxs-lookup"><span data-stu-id="d1d85-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="d1d85-307">连接字符串和其他属性应设置为初始化方法中的默认值。</span><span class="sxs-lookup"><span data-stu-id="d1d85-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="d1d85-308">（在运行时加载提供程序时，将触发初始化方法。初始化方法的第二个参数是 System.集合.专业.NameValueCollection，它是对 Web.config &lt;&gt;文件中与自定义提供程序关联的添加元素的引用。</span><span class="sxs-lookup"><span data-stu-id="d1d85-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="d1d85-309">该条目如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1d85-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="d1d85-310">下面是初始化方法的示例。</span><span class="sxs-lookup"><span data-stu-id="d1d85-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="d1d85-311">为了验证用户提交登录表单时，您需要使用验证用户方法。</span><span class="sxs-lookup"><span data-stu-id="d1d85-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="d1d85-312">当用户单击登录控件中的登录按钮时，将触发此方法。</span><span class="sxs-lookup"><span data-stu-id="d1d85-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="d1d85-313">您将在此方法中放置执行用户查找的代码。</span><span class="sxs-lookup"><span data-stu-id="d1d85-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="d1d85-314">正如您所看到的，编写自己的成员资格提供程序并不困难，允许您扩展ASP.NET 2.0 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="d1d85-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>

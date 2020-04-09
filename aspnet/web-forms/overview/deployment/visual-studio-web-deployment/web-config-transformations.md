---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用可视化工作室ASP.NET Web 部署：Web.config 文件转换 |微软文档
author: tdykstra
description: 本教程系列介绍如何将ASP.NET Web 应用程序部署到 Azure 应用服务 Web 应用或第三方托管提供商（由 usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675747"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a><span data-ttu-id="06a3d-103">使用可视化工作室ASP.NET Web 部署：Web.config 文件转换</span><span class="sxs-lookup"><span data-stu-id="06a3d-103">ASP.NET Web Deployment using Visual Studio: Web.config File Transformations</span></span>

<span data-ttu-id="06a3d-104">汤姆[·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="06a3d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="06a3d-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="06a3d-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="06a3d-106">本教程系列介绍如何使用 Visual Studio 2012 或 Visual Studio 2010 将ASP.NET Web 应用程序部署到 Azure 应用服务 Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="06a3d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="06a3d-107">有关该系列的信息，请参阅[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="06a3d-108">概述</span><span class="sxs-lookup"><span data-stu-id="06a3d-108">Overview</span></span>

<span data-ttu-id="06a3d-109">本教程介绍如何在将*Web.config 文件部署到*不同目标环境时自动执行更改 Web.config 文件的过程。</span><span class="sxs-lookup"><span data-stu-id="06a3d-109">This tutorial shows you how to automate the process of changing the *Web.config* file when you deploy it to different destination environments.</span></span> <span data-ttu-id="06a3d-110">大多数应用程序在*Web.config 文件中*具有设置，在部署应用程序时必须不同。</span><span class="sxs-lookup"><span data-stu-id="06a3d-110">Most applications have settings in the *Web.config* file that must be different when the application is deployed.</span></span> <span data-ttu-id="06a3d-111">自动进行这些更改的过程使每次部署时都不必手动执行这些更改，这非常繁琐且容易出错。</span><span class="sxs-lookup"><span data-stu-id="06a3d-111">Automating the process of making these changes keeps you from having to do them manually every time you deploy, which would be tedious and error prone.</span></span>

<span data-ttu-id="06a3d-112">提醒：如果您收到错误消息或内容在浏览本教程时不起作用，请务必查看[故障排除页面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a><span data-ttu-id="06a3d-113">Web.配置转换与 Web 部署参数</span><span class="sxs-lookup"><span data-stu-id="06a3d-113">Web.config transformations versus Web Deploy parameters</span></span>

<span data-ttu-id="06a3d-114">有两种方法可以自动更改*Web.config*文件设置的过程[：Web.config 转换](https://msdn.microsoft.com/library/dd465326.aspx)和[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-114">There are two ways to automate the process of changing *Web.config* file settings: [Web.config transformations](https://msdn.microsoft.com/library/dd465326.aspx) and [Web Deploy parameters](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="06a3d-115">*Web.config*转换文件包含 XML 标记，用于指定在部署*Web.config*文件时如何更改该文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-115">A *Web.config* transformation file contains XML markup that specifies how to change the *Web.config* file when it is deployed.</span></span> <span data-ttu-id="06a3d-116">您可以为特定生成配置和特定发布配置文件指定不同的更改。</span><span class="sxs-lookup"><span data-stu-id="06a3d-116">You can specify different changes for specific build configurations and for specific publish profiles.</span></span> <span data-ttu-id="06a3d-117">默认生成配置是调试和发布，您可以创建自定义生成配置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-117">The default build configurations are Debug and Release, and you can create custom build configurations.</span></span> <span data-ttu-id="06a3d-118">发布配置文件通常对应于目标环境。</span><span class="sxs-lookup"><span data-stu-id="06a3d-118">A publish profile typically corresponds to a destination environment.</span></span> <span data-ttu-id="06a3d-119">（您将了解有关在["作为测试环境"教程部署到 IIS](deploying-to-iis.md)中的发布配置文件的更多信息。</span><span class="sxs-lookup"><span data-stu-id="06a3d-119">(You'll learn more about publish profiles in the [Deploying to IIS as a Test Environment](deploying-to-iis.md) tutorial.)</span></span>

<span data-ttu-id="06a3d-120">Web Deploy 参数可用于指定在部署期间必须配置的许多不同类型的设置，包括*Web.config 文件中*的设置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-120">Web Deploy parameters can be used to specify many different kinds of settings that must be configured during deployment, including settings that are found in *Web.config* files.</span></span> <span data-ttu-id="06a3d-121">当用于指定*Web.config*文件更改时，Web Deploy 参数的设置更为复杂，但在部署之前不知道要设置的值时，这些参数很有用。</span><span class="sxs-lookup"><span data-stu-id="06a3d-121">When used to specify *Web.config* file changes, Web Deploy parameters are more complex to set up, but they are useful when you do not know the value to be set until you deploy.</span></span> <span data-ttu-id="06a3d-122">例如，在企业环境中，您可以创建*部署包*并将其交给 IT 部门的人员以在生产中安装，并且此人必须能够输入您不知道的连接字符串或密码。</span><span class="sxs-lookup"><span data-stu-id="06a3d-122">For example, in an enterprise environment, you might create a *deployment package* and give it to a person in the IT department to install in production, and that person has to be able to enter connection strings or passwords that you do not know.</span></span>

<span data-ttu-id="06a3d-123">对于本教程系列介绍的方案，您事先知道必须对*Web.config*文件执行的所有操作，因此无需使用 Web Deploy 参数。</span><span class="sxs-lookup"><span data-stu-id="06a3d-123">For the scenario that this tutorial series covers, you know in advance everything that has to be done to the *Web.config* file, so you do not need to use Web Deploy parameters.</span></span> <span data-ttu-id="06a3d-124">您将配置一些因所使用的生成配置而异的转换，以及一些因使用的发布配置文件而异的转换。</span><span class="sxs-lookup"><span data-stu-id="06a3d-124">You'll configure some transformations that differ depending on the build configuration used, and some that differ depending on the publish profile used.</span></span>

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a><span data-ttu-id="06a3d-125">在 Azure 中指定 Web.配置设置</span><span class="sxs-lookup"><span data-stu-id="06a3d-125">Specifying Web.config settings in Azure</span></span>

<span data-ttu-id="06a3d-126">如果要更改的*Web.config*文件设置位于`<connectionStrings>`或`<appSettings>`元素中，并且如果要在 Azure 应用服务中部署到 Web 应用，则可以在部署期间自动更改另一个选项。</span><span class="sxs-lookup"><span data-stu-id="06a3d-126">If the *Web.config* file settings that you want to change are in the `<connectionStrings>` or the `<appSettings>` element, and if you are deploying to Web Apps in Azure App Service, you have another option for automating changes during deployment.</span></span> <span data-ttu-id="06a3d-127">您可以在 Web 应用的管理门户页的 **"配置"** 选项卡中输入要在 Azure 中生效的设置（向下滚动到**应用设置**和**连接字符串**部分）。</span><span class="sxs-lookup"><span data-stu-id="06a3d-127">You can enter the settings that you want to take effect in Azure in the **Configure** tab of the management portal page for your web app (scroll down to the **app settings** and **connection strings** sections).</span></span> <span data-ttu-id="06a3d-128">部署项目时，Azure 会自动应用更改。</span><span class="sxs-lookup"><span data-stu-id="06a3d-128">When you deploy the project, Azure automatically applies the changes.</span></span> <span data-ttu-id="06a3d-129">有关详细信息，请参阅[Windows Azure 网站：应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-129">For more information, see [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

## <a name="default-transformation-files"></a><span data-ttu-id="06a3d-130">默认转换文件</span><span class="sxs-lookup"><span data-stu-id="06a3d-130">Default transformation files</span></span>

<span data-ttu-id="06a3d-131">在**解决方案资源管理器**中，展开*Web.config*以查看*Web.Debug.config*和*Web.Release.config*为两个默认生成配置默认创建的转换文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-131">In **Solution Explorer**, expand *Web.config* to see the *Web.Debug.config* and *Web.Release.config* transformation files that are created by default for the two default build configurations.</span></span>

![Web.config_transform_files](web-config-transformations/_static/image1.png)

<span data-ttu-id="06a3d-133">您可以通过右键单击 Web.config 文件并从上下文菜单中选择 **"添加配置转换"** 来创建自定义生成配置的转换文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-133">You can create transformation files for custom build configurations by right-clicking the Web.config file and choosing **Add Config Transforms** from the context menu.</span></span> <span data-ttu-id="06a3d-134">对于本教程，您不需要执行此操作，并且菜单选项已禁用，因为您尚未创建任何自定义生成配置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-134">For this tutorial you don't need to do that, and the menu option is disabled, because you haven't created any custom build configurations.</span></span>

<span data-ttu-id="06a3d-135">稍后，您将再创建三个转换文件，每个文件用于测试、暂存和生产发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-135">Later you'll create three more transformation files, one each for the test, staging, and production publish profiles.</span></span> <span data-ttu-id="06a3d-136">在发布配置文件转换文件中处理的设置的典型示例是 WCF 终结点，用于测试和生产。</span><span class="sxs-lookup"><span data-stu-id="06a3d-136">A typical example of a setting that you would handle in a publish profile transformation file because it depends on the destination environment is a WCF endpoint that is different for test versus production.</span></span> <span data-ttu-id="06a3d-137">在创建与它们一起的发布配置文件后，您将在以后的教程中创建发布配置文件转换文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-137">You'll create publish profile transformation files in later tutorials after you create the publish profiles that they go with.</span></span>

## <a name="disable-debug-mode"></a><span data-ttu-id="06a3d-138">禁用调试模式</span><span class="sxs-lookup"><span data-stu-id="06a3d-138">Disable debug mode</span></span>

<span data-ttu-id="06a3d-139">属性是依赖于生成配置而不是目标环境的设置示例`debug`。</span><span class="sxs-lookup"><span data-stu-id="06a3d-139">An example of a setting that depends on build configuration rather than destination environment is the `debug` attribute.</span></span> <span data-ttu-id="06a3d-140">对于发布生成，您通常希望禁用调试，而不管要部署到哪个环境。</span><span class="sxs-lookup"><span data-stu-id="06a3d-140">For a Release build, you typically want debugging disabled regardless of which environment you are deploying to.</span></span> <span data-ttu-id="06a3d-141">因此，默认情况下，Visual Studio 项目模板创建*Web.Release.config*转换文件，这些转换`debug`文件的代码从`compilation`元素中删除该属性。</span><span class="sxs-lookup"><span data-stu-id="06a3d-141">Therefore, by default the Visual Studio project templates create *Web.Release.config* transform files with code that removes the `debug` attribute from the `compilation` element.</span></span> <span data-ttu-id="06a3d-142">下面是默认的*Web.Release.config*：除了注释掉的一些示例转换代码外，它还在`compilation`元素中包括删除`debug`属性的代码：</span><span class="sxs-lookup"><span data-stu-id="06a3d-142">Here is the default *Web.Release.config*: in addition to some sample transformation code that is commented out, it includes code in the `compilation` element that removes the `debug` attribute:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

<span data-ttu-id="06a3d-143">该`xdt:Transform="RemoveAttributes(debug)"`属性指定您希望从已部署`debug`的`system.web/compilation`*Web.config*文件中的元素中删除该属性。</span><span class="sxs-lookup"><span data-stu-id="06a3d-143">The `xdt:Transform="RemoveAttributes(debug)"` attribute specifies that you want the `debug` attribute to be removed from the `system.web/compilation` element in the deployed *Web.config* file.</span></span> <span data-ttu-id="06a3d-144">这将在每次部署发布版本时完成。</span><span class="sxs-lookup"><span data-stu-id="06a3d-144">This will be done every time you deploy a Release build.</span></span>

## <a name="limit-error-log-access-to-administrators"></a><span data-ttu-id="06a3d-145">限制对管理员的错误日志访问</span><span class="sxs-lookup"><span data-stu-id="06a3d-145">Limit error log access to administrators</span></span>

<span data-ttu-id="06a3d-146">如果应用程序运行时出现错误，应用程序将显示一个通用错误页，以代替系统生成的错误页，并且它使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)进行错误日志记录和报告。</span><span class="sxs-lookup"><span data-stu-id="06a3d-146">If there's an error while the application runs, the application displays a generic error page in place of the system-generated error page, and it uses the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) for error logging and reporting.</span></span> <span data-ttu-id="06a3d-147">应用程序`customErrors` *Web.config*文件中的元素指定错误页：</span><span class="sxs-lookup"><span data-stu-id="06a3d-147">The `customErrors` element in the application *Web.config* file specifies the error page:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

<span data-ttu-id="06a3d-148">要查看错误页，请暂时将`mode``customErrors`元素的属性从"仅远程"更改为"打开"，并从 Visual Studio 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="06a3d-148">To see the error page, temporarily change the `mode` attribute of the `customErrors` element from "RemoteOnly" to "On" and run the application from Visual Studio.</span></span> <span data-ttu-id="06a3d-149">通过请求无效 URL（如*学生xxx.aspx）* 导致错误。</span><span class="sxs-lookup"><span data-stu-id="06a3d-149">Cause an error by requesting an invalid URL, such as *Studentsxxx.aspx*.</span></span> <span data-ttu-id="06a3d-150">您看到的不是 IIS 生成的"找不到资源"错误页，而是看到*泛错误Page.aspx*页面。</span><span class="sxs-lookup"><span data-stu-id="06a3d-150">Instead of an IIS-generated "The resource cannot be found" error page, you see the *GenericErrorPage.aspx* page.</span></span>

![错误页](web-config-transformations/_static/image2.png)

<span data-ttu-id="06a3d-152">要查看错误日志，请将端口号后 URL 中的所有内容替换为*elmah.axd（* 例如`http://localhost:51130/elmah.axd`），然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="06a3d-152">To see the error log, replace everything in the URL after the port number with *elmah.axd* (for example, `http://localhost:51130/elmah.axd`) and press Enter:</span></span>

![ELMAH 页面](web-config-transformations/_static/image3.png)

<span data-ttu-id="06a3d-154">完成后，不要忘记将`customErrors`元素设置为"仅远程"模式。</span><span class="sxs-lookup"><span data-stu-id="06a3d-154">Don't forget to set the `customErrors` element back to "RemoteOnly" mode when you're done.</span></span>

<span data-ttu-id="06a3d-155">在开发计算机上，允许免费访问错误日志页很方便，但在生产中，这将存在安全风险。</span><span class="sxs-lookup"><span data-stu-id="06a3d-155">On your development computer it's convenient to allow free access to the error log page, but in production that would be a security risk.</span></span> <span data-ttu-id="06a3d-156">对于生产站点，要添加一个授权规则，该规则限制管理员对错误日志的访问，并确保该限制在测试和暂存中也正常工作。</span><span class="sxs-lookup"><span data-stu-id="06a3d-156">For the production site, you want to add an authorization rule that restricts error log access to administrators, and to make sure that the restriction works you want it in test and staging also.</span></span> <span data-ttu-id="06a3d-157">因此，这是每次部署发布生成时要实现的另一个更改，因此它属于*Web.Release.config*文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-157">Therefore this is another change that you want to implement every time you deploy a Release build, and so it belongs in the *Web.Release.config* file.</span></span>

<span data-ttu-id="06a3d-158">打开*Web.Release.config，* 并在结束`location``configuration`标记之前添加新元素，如下所示。</span><span class="sxs-lookup"><span data-stu-id="06a3d-158">Open *Web.Release.config* and add a new `location` element immediately before the closing `configuration` tag, as shown here.</span></span>

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

<span data-ttu-id="06a3d-159">属性`Transform`值"Insert"会导致此`location`元素作为同级添加到*Web.config*文件中的任何`location`现有元素。</span><span class="sxs-lookup"><span data-stu-id="06a3d-159">The `Transform` attribute value of "Insert" causes this `location` element to be added as a sibling to any existing `location` elements in the *Web.config* file.</span></span> <span data-ttu-id="06a3d-160">（已经有一个`location`元素指定**更新积分**页的授权规则。</span><span class="sxs-lookup"><span data-stu-id="06a3d-160">(There is already one `location` element that specifies authorization rules for the **Update Credits** page.)</span></span>

<span data-ttu-id="06a3d-161">现在，您可以预览转换，以确保正确编码它。</span><span class="sxs-lookup"><span data-stu-id="06a3d-161">Now you can preview the transform to make sure that you coded it correctly.</span></span>

<span data-ttu-id="06a3d-162">在**解决方案资源管理器**中，右键单击*Web.Release.config，* 然后单击 **"预览转换**"。</span><span class="sxs-lookup"><span data-stu-id="06a3d-162">In **Solution Explorer**, right-click *Web.Release.config* and click **Preview Transform**.</span></span>

![预览转换菜单](web-config-transformations/_static/image4.png)

<span data-ttu-id="06a3d-164">将打开一个页面，显示左侧的开发*Web.config*文件以及部署的*Web.config*文件在右侧的外观，并突出显示更改。</span><span class="sxs-lookup"><span data-stu-id="06a3d-164">A page opens that shows you the development *Web.config* file on the left and what the deployed *Web.config* file will look like on the right, with changes highlighted.</span></span>

![调试转换预览](web-config-transformations/_static/image5.png)

![位置转换预览](web-config-transformations/_static/image6.png)

<span data-ttu-id="06a3d-167">（在预览中，您可能会注意到一些未为这些更改编写转换的其他更改：这些更改通常涉及删除不影响功能的空白。</span><span class="sxs-lookup"><span data-stu-id="06a3d-167">( In the preview, you might notice some additional changes that you didn't write transforms for: these typically involve the removal of white space that doesn't affect functionality.)</span></span>

<span data-ttu-id="06a3d-168">部署后测试站点时，还将进行测试以验证授权规则是否有效。</span><span class="sxs-lookup"><span data-stu-id="06a3d-168">When you test the site after deployment, you'll also test to verify that the authorization rule is effective.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="06a3d-169">**安全说明**切勿在生产应用程序中向公众显示错误详细信息，也不要将该信息存储在公共位置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-169">**Security Note** Never display error details to the public in a production application, or store that information in a public location.</span></span> <span data-ttu-id="06a3d-170">攻击者可以使用错误信息来发现站点中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="06a3d-170">Attackers can use error information to discover vulnerabilities in a site.</span></span> <span data-ttu-id="06a3d-171">如果您在自己的应用程序中使用 ELMAH，请配置 ELMAH 以最大程度地降低安全风险。</span><span class="sxs-lookup"><span data-stu-id="06a3d-171">If you use ELMAH in your own application, configure ELMAH to minimize security risks.</span></span> <span data-ttu-id="06a3d-172">本教程中的 ELMAH 示例不应视为推荐的配置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-172">The ELMAH example in this tutorial should not be considered a recommended configuration.</span></span> <span data-ttu-id="06a3d-173">这是一个示例，用于说明如何处理应用程序必须能够在 中创建文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="06a3d-173">It is an example that was chosen in order to illustrate how to handle a folder that the application must be able to create files in.</span></span> <span data-ttu-id="06a3d-174">有关详细信息，请参阅保护[ELMAH 终结点](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-174">For more information, see [securing the ELMAH endpoint](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).</span></span>

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a><span data-ttu-id="06a3d-175">在发布配置文件转换文件中要处理的设置</span><span class="sxs-lookup"><span data-stu-id="06a3d-175">A setting that you'll handle in publish profile transformation files</span></span>

<span data-ttu-id="06a3d-176">常见方案是具有在部署到的每个环境中必须不同的*Web.config*文件设置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-176">A common scenario is to have *Web.config* file settings that must be different in each environment that you deploy to.</span></span> <span data-ttu-id="06a3d-177">例如，调用 WCF 服务的应用程序在测试和生产环境中可能需要不同的终结点。</span><span class="sxs-lookup"><span data-stu-id="06a3d-177">For example, an application that calls a WCF service might need a different endpoint in test and production environments.</span></span> <span data-ttu-id="06a3d-178">康托索大学的申请还包括这种设置。</span><span class="sxs-lookup"><span data-stu-id="06a3d-178">The Contoso University application includes a setting of this kind also.</span></span> <span data-ttu-id="06a3d-179">此设置控制网站页面上的可见指示器，该指示器告诉您处于哪个环境，例如开发、测试或生产。</span><span class="sxs-lookup"><span data-stu-id="06a3d-179">This setting controls a visible indicator on a site's pages that tells you which environment you are in, such as development, test, or production.</span></span> <span data-ttu-id="06a3d-180">设置值确定应用程序是否会将"（Dev）"或"（测试）"追加到*Site.master*页中的主标题：</span><span class="sxs-lookup"><span data-stu-id="06a3d-180">The setting value determines whether the application will append "(Dev)" or "(Test)" to the main heading in the *Site.Master* master page:</span></span>

![环境指示器](web-config-transformations/_static/image7.png)

<span data-ttu-id="06a3d-182">当应用程序在暂存或生产中运行时，环境指示器将被省略。</span><span class="sxs-lookup"><span data-stu-id="06a3d-182">The environment indicator is omitted when the application is running in staging or production.</span></span>

<span data-ttu-id="06a3d-183">Contoso 大学网页读取在*Web.config* `appSettings`文件中设置的值，以便确定应用程序在以下环境中运行的环境：</span><span class="sxs-lookup"><span data-stu-id="06a3d-183">The Contoso University web pages read a value that is set in `appSettings` in the *Web.config* file in order to determine what environment the application is running in:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

<span data-ttu-id="06a3d-184">在测试环境中的值应为"测试"，对于暂存和生产来说应为"Prod"。</span><span class="sxs-lookup"><span data-stu-id="06a3d-184">The value should be "Test" in the test environment, and "Prod" for staging and production.</span></span>

<span data-ttu-id="06a3d-185">转换文件中的以下代码将实现此转换：</span><span class="sxs-lookup"><span data-stu-id="06a3d-185">The following code in a transform file will implement this transformation:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

<span data-ttu-id="06a3d-186">`xdt:Transform`属性值"SetAttributes"表示此转换的目的是更改*Web.config*文件中现有元素的属性值。</span><span class="sxs-lookup"><span data-stu-id="06a3d-186">The `xdt:Transform` attribute value "SetAttributes" indicates that the purpose of this transform is to change attribute values of an existing element in the *Web.config* file.</span></span> <span data-ttu-id="06a3d-187">`xdt:Locator`属性值"Match（键）"表示要修改的元素是其`key`属性与此处指定的`key`属性匹配的元素。</span><span class="sxs-lookup"><span data-stu-id="06a3d-187">The `xdt:Locator` attribute value "Match(key)" indicates that the element to be modified is the one whose `key` attribute matches the `key` attribute specified here.</span></span> <span data-ttu-id="06a3d-188">元素的唯一`add`其他属性是`value`，这就是将在部署的*Web.config 文件中*更改的内容。</span><span class="sxs-lookup"><span data-stu-id="06a3d-188">The only other attribute of the `add` element is `value`, and that is what will be changed in the deployed *Web.config* file.</span></span> <span data-ttu-id="06a3d-189">`value`此处显示的代码会导致`Environment``appSettings`元素的属性设置为部署的*Web.config*文件中的"Test"。</span><span class="sxs-lookup"><span data-stu-id="06a3d-189">The code shown here causes the `value` attribute of the `Environment` `appSettings` element to be set to "Test" in the *Web.config* file that is deployed.</span></span>

<span data-ttu-id="06a3d-190">此转换属于尚未创建的发布配置文件转换文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-190">This transform belongs in the publish profile transform files, which you haven't created yet.</span></span> <span data-ttu-id="06a3d-191">在为测试、暂存和生产环境创建发布配置文件时，您将创建和更新实现此更改的转换文件。</span><span class="sxs-lookup"><span data-stu-id="06a3d-191">You'll create and update the transform files that implement this change when you create the publish profiles for the test, staging, and production environments.</span></span> <span data-ttu-id="06a3d-192">您将在[部署到 IIS](deploying-to-iis.md)并[部署到生产](deploying-to-production.md)教程中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="06a3d-192">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

> [!NOTE]
> <span data-ttu-id="06a3d-193">由于此设置位于`<appSettings>`元素中，因此在本主题前面介绍的 Azure 中，在 Azure 应用服务中部署到 Web 应用时，还有另一种用于指定转换的替代方法。请参阅[在本主题前面指定 Azure 中的 Web.config 设置](#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-193">Because this setting is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Web Apps in Azure App Service See [Specifying Web.config settings in Azure](#watransforms) earlier in this topic.</span></span>

## <a name="setting-connection-strings"></a><span data-ttu-id="06a3d-194">设置连接字符串</span><span class="sxs-lookup"><span data-stu-id="06a3d-194">Setting connection strings</span></span>

<span data-ttu-id="06a3d-195">尽管默认转换文件包含一个示例，其中演示如何更新连接字符串，但在大多数情况下，您不需要设置连接字符串转换，因为您可以在发布配置文件中指定连接字符串。</span><span class="sxs-lookup"><span data-stu-id="06a3d-195">Although the default transform file contains an example that shows how to update a connection string, in most cases you do not need to set up connection string transformations, because you can specify connection strings in the publish profile.</span></span> <span data-ttu-id="06a3d-196">您将在[部署到 IIS](deploying-to-iis.md)并[部署到生产](deploying-to-production.md)教程中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="06a3d-196">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

## <a name="summary"></a><span data-ttu-id="06a3d-197">总结</span><span class="sxs-lookup"><span data-stu-id="06a3d-197">Summary</span></span>

<span data-ttu-id="06a3d-198">现在，在创建发布配置文件之前，您已经尽可能多地使用*Web.config*转换，并且您已经看到了部署的 Web.config 文件中的内容的预览。</span><span class="sxs-lookup"><span data-stu-id="06a3d-198">You have now done as much as you can with *Web.config* transformations before you create the publish profiles, and you've seen a preview of what will be in the deployed Web.config file.</span></span>

![位置转换预览](web-config-transformations/_static/image8.png)

<span data-ttu-id="06a3d-200">在下面的教程中，您将处理需要设置项目属性的部署设置任务。</span><span class="sxs-lookup"><span data-stu-id="06a3d-200">In the following tutorial, you'll take care of deployment set-up tasks that require setting project properties.</span></span>

## <a name="more-information"></a><span data-ttu-id="06a3d-201">更多信息</span><span class="sxs-lookup"><span data-stu-id="06a3d-201">More Information</span></span>

<span data-ttu-id="06a3d-202">有关本教程涵盖的主题的详细信息，请参阅在 Visual Studio 和 ASP.NET的 Web 部署内容映射中[使用 Web.config 转换来更改目标 Web.config 文件或 app.config 文件中的设置](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。</span><span class="sxs-lookup"><span data-stu-id="06a3d-202">For more information about topics covered by this tutorial, see [Using Web.config transformations to change settings in the destination Web.config file or app.config file during deployment](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="06a3d-203">[上一页](preparing-databases.md)
> [下一页](project-properties.md)</span><span class="sxs-lookup"><span data-stu-id="06a3d-203">[Previous](preparing-databases.md)
[Next](project-properties.md)</span></span>

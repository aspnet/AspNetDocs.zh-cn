---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 源控件 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5df863762523b62759bb4f7849ca2635e5241b0a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056354"
---
<a name="source-control-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="ca656-104">源代码管理 （使用 Azure 构建实际云应用）</span><span class="sxs-lookup"><span data-stu-id="ca656-104">Source Control (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="ca656-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ca656-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="ca656-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="ca656-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="ca656-107">**构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="ca656-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="ca656-108">它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="ca656-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="ca656-109">有关电子书的信息，请参阅[的第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ca656-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="ca656-110">源代码管理的所有云开发项目，而不仅仅是团队环境至关重要。</span><span class="sxs-lookup"><span data-stu-id="ca656-110">Source control is essential for all cloud development projects, not just team environments.</span></span> <span data-ttu-id="ca656-111">您不会将编辑源代码或甚至无需撤消的功能和自动备份和源代码管理的 Word 文档为您提供这些函数在项目级别，它们可以在其中保存时出现问题的更多时间。</span><span class="sxs-lookup"><span data-stu-id="ca656-111">You wouldn't think of editing source code or even a Word document without an undo function and automatic backups, and source control gives you those functions at a project level where they can save even more time when something goes wrong.</span></span> <span data-ttu-id="ca656-112">使用云的源代码管理服务，不再需要担心复杂的设置，并可以为最多 5 个用户使用免费的 Azure 存储库的源代码管理。</span><span class="sxs-lookup"><span data-stu-id="ca656-112">With cloud source control services, you no longer have to worry about complicated set-up, and you can use Azure Repos source control free for up to 5 users.</span></span>

<span data-ttu-id="ca656-113">这一章中的第一部分介绍了三个关键的最佳实践要时刻牢记：</span><span class="sxs-lookup"><span data-stu-id="ca656-113">The first part of this chapter explains three key best practices to keep in mind:</span></span>

- <span data-ttu-id="ca656-114">[自动化脚本视为源代码](#scripts)和版本以及应用程序代码对其。</span><span class="sxs-lookup"><span data-stu-id="ca656-114">[Treat automation scripts as source code](#scripts) and version them together with your application code.</span></span>
- <span data-ttu-id="ca656-115">[中的机密永远不会检查](#secrets)（例如凭据的敏感数据） 到源代码存储库。</span><span class="sxs-lookup"><span data-stu-id="ca656-115">[Never check in secrets](#secrets) (sensitive data such as credentials) into a source code repository.</span></span>
- <span data-ttu-id="ca656-116">[设置源分支](#devops)启用 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="ca656-116">[Set up source branches](#devops) to enable the DevOps workflow.</span></span>

<span data-ttu-id="ca656-117">本章的其余部分提供了 Visual Studio、 Azure 和 Azure 存储库中的这些模式的一些示例实现：</span><span class="sxs-lookup"><span data-stu-id="ca656-117">The remainder of the chapter gives some sample implementations of these patterns in Visual Studio, Azure, and Azure Repos:</span></span>

- [<span data-ttu-id="ca656-118">将脚本添加到 Visual Studio 中的源控件</span><span class="sxs-lookup"><span data-stu-id="ca656-118">Add scripts to source control in Visual Studio</span></span>](#vsscripts)
- [<span data-ttu-id="ca656-119">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="ca656-119">Store sensitive data in Azure</span></span>](#appsettings)
- [<span data-ttu-id="ca656-120">使用 Visual Studio 和 Azure 存储库中的 Git</span><span class="sxs-lookup"><span data-stu-id="ca656-120">Use Git in Visual Studio and Azure Repos</span></span>](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a><span data-ttu-id="ca656-121">自动化脚本视为源代码</span><span class="sxs-lookup"><span data-stu-id="ca656-121">Treat automation scripts as source code</span></span>

<span data-ttu-id="ca656-122">当您在处理云项目时要频繁地更改内容，并且你想要能够快速响应客户报告的问题的能力。</span><span class="sxs-lookup"><span data-stu-id="ca656-122">When you're working on a cloud project you're changing things frequently and you want to be able to react quickly to issues reported by your customers.</span></span> <span data-ttu-id="ca656-123">快速响应，需使用自动化脚本中所述[使一切自动化](automate-everything.md)一章。</span><span class="sxs-lookup"><span data-stu-id="ca656-123">Responding quickly involves using automation scripts, as explained in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="ca656-124">所有脚本用来创建你的环境，将部署到其规模，等等，需要与应用程序源代码保持同步。</span><span class="sxs-lookup"><span data-stu-id="ca656-124">All of the scripts that you use to create your environment, deploy to it, scale it, etc., need to be in sync with your application source code.</span></span>

<span data-ttu-id="ca656-125">若要使脚本与代码保持同步，请将其存储在源代码管理系统。</span><span class="sxs-lookup"><span data-stu-id="ca656-125">To keep scripts in sync with code, store them in your source control system.</span></span> <span data-ttu-id="ca656-126">然后如果需要回滚更改或快速修复生产代码不同于开发代码，您无需浪费时间尝试跟踪哪些设置已更改或哪些团队成员具有所需的版本的副本。</span><span class="sxs-lookup"><span data-stu-id="ca656-126">Then if you ever need to roll back changes or make a quick fix to production code which is different from development code, you don't have to waste time trying to track down which settings have changed or which team members have copies of the version you need.</span></span> <span data-ttu-id="ca656-127">也可以确保所需的脚本将与基本代码，你需要它们，您就可以保证所有团队成员都正在使用相同脚本保持同步。</span><span class="sxs-lookup"><span data-stu-id="ca656-127">You're assured that the scripts you need are in sync with the code base that you need them for, and you're assured that all team members are working with the same scripts.</span></span> <span data-ttu-id="ca656-128">然后你是否需要自动测试和部署到生产或新功能开发了修补，您必须为需要更新的代码正确的脚本。</span><span class="sxs-lookup"><span data-stu-id="ca656-128">Then whether you need to automate testing and deployment of a hot fix to production or new feature development, you'll have the right script for the code that needs to be updated.</span></span>

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a><span data-ttu-id="ca656-129">不签入机密</span><span class="sxs-lookup"><span data-stu-id="ca656-129">Don't check in secrets</span></span>

<span data-ttu-id="ca656-130">源代码存储库都太多的人，它为相应安全的位置的敏感数据，如密码通常可以访问。</span><span class="sxs-lookup"><span data-stu-id="ca656-130">A source code repository is typically accessible to too many people for it to be an appropriately secure place for sensitive data such as passwords.</span></span> <span data-ttu-id="ca656-131">如果脚本依赖于如密码的机密，参数化这些设置，以便它们不会保存在源代码中，并存储在其他地方的机密。</span><span class="sxs-lookup"><span data-stu-id="ca656-131">If scripts rely on secrets such as passwords, parameterize those settings so that they don't get saved in source code, and store your secrets somewhere else.</span></span>

<span data-ttu-id="ca656-132">例如，Azure 可让您下载文件，其中包含发布设置以自动创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="ca656-132">For example, Azure lets you download files that contain publish settings in order to automate the creation of publish profiles.</span></span> <span data-ttu-id="ca656-133">这些文件包括用户名和密码有权管理 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="ca656-133">These files include user names and passwords that are authorized to manage your Azure services.</span></span> <span data-ttu-id="ca656-134">如果您使用此方法来创建发布配置文件，并签入到源代码管理这些文件时，如果有权访问你的存储库的任何人都可以看到这些用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="ca656-134">If you use this method to create publish profiles, and if you check in these files to source control, anyone with access to your repository can see those user names and passwords.</span></span> <span data-ttu-id="ca656-135">您可以安全地将密码存储在发布配置文件本身由于对其进行加密，它位于 *.pubxml 用户*默认情况下不包含在源代码管理中的文件。</span><span class="sxs-lookup"><span data-stu-id="ca656-135">You can safely store the password in the publish profile itself because it's encrypted and it's in a *.pubxml.user* file that by default is not included in source control.</span></span>

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a><span data-ttu-id="ca656-136">结构源分支，以便于 DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="ca656-136">Structure source branches to facilitate DevOps workflow</span></span>

<span data-ttu-id="ca656-137">如何在存储库中实现分支会影响开发新的功能和在生产环境中解决问题的能力。</span><span class="sxs-lookup"><span data-stu-id="ca656-137">How you implement branches in your repository affects your ability to both develop new features and fix issues in production.</span></span> <span data-ttu-id="ca656-138">此处是中等的大量大小的团队使用的模式：</span><span class="sxs-lookup"><span data-stu-id="ca656-138">Here is a pattern that a lot of medium sized teams use:</span></span>

![源分支结构](source-control/_static/image1.png)

<span data-ttu-id="ca656-140">主分支与在生产环境中的代码始终匹配。</span><span class="sxs-lookup"><span data-stu-id="ca656-140">The master branch always matches code that is in production.</span></span> <span data-ttu-id="ca656-141">在开发生命周期中，下方 master 分支对应于不同的阶段。</span><span class="sxs-lookup"><span data-stu-id="ca656-141">Branches underneath master correspond to different stages in the development life cycle.</span></span> <span data-ttu-id="ca656-142">Development 分支是你在其中实施新功能。</span><span class="sxs-lookup"><span data-stu-id="ca656-142">The development branch is where you implement new features.</span></span> <span data-ttu-id="ca656-143">对于小团队可能只有 master 和开发，但我们通常建议的人员具有开发和主机之间过渡分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-143">For a small team you might just have master and development, but we often recommend that people have a staging branch between development and master.</span></span> <span data-ttu-id="ca656-144">对于最终集成测试更新移到生产环境之前，可以使用过渡环境。</span><span class="sxs-lookup"><span data-stu-id="ca656-144">You can use staging for final integration testing before an update is moved to production.</span></span>

<span data-ttu-id="ca656-145">对于较大的团队可能有不同的分支的每个新功能;对于较小的团队可能必须所有人签入到 development 分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-145">For big teams there may be separate branches for each new feature; for a smaller team you might have everyone checking in to the development branch.</span></span>

<span data-ttu-id="ca656-146">如果必须为每个功能，分支功能启用时一个准备好你合并其源代码更改向上到开发分支和其他功能分支到向下。</span><span class="sxs-lookup"><span data-stu-id="ca656-146">If you have a branch for each feature, when Feature A is ready you merge its source code changes up into the development branch and down into the other feature branches.</span></span> <span data-ttu-id="ca656-147">此合并过程的源代码会非常耗时，并且若要避免该工作的同时仍将功能分开，一些团队实现名为一种替代方法*[功能切换](http://en.wikipedia.org/wiki/Feature_toggle)* （也称为*功能标志*)。</span><span class="sxs-lookup"><span data-stu-id="ca656-147">This source code merging process can be time-consuming, and to avoid that work while still keeping features separate, some teams implement an alternative called *[feature toggles](http://en.wikipedia.org/wiki/Feature_toggle)* (also known as *feature flags*).</span></span> <span data-ttu-id="ca656-148">这意味着所有的所有功能的代码都在同一个分支，但启用或禁用每个功能在代码中使用的开关。</span><span class="sxs-lookup"><span data-stu-id="ca656-148">This means all of the code for all of the features is in the same branch, but you enable or disable each feature by using switches in the code.</span></span> <span data-ttu-id="ca656-149">例如，假设一个功能是修复其应用程序任务，新的字段，并功能 B 添加缓存功能。</span><span class="sxs-lookup"><span data-stu-id="ca656-149">For example, suppose Feature A is a new field for Fix It app tasks, and Feature B adds caching functionality.</span></span> <span data-ttu-id="ca656-150">这两项功能的代码可以是开发分支中，但应用程序将仅显示新字段时变量设置为 true，并且它将仅使用缓存时不同的变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="ca656-150">The code for both features can be in the development branch, but the app will only display the new field when a variable is set to true, and it will only use caching when a different variable is set to true.</span></span> <span data-ttu-id="ca656-151">如果功能 A 还未准备好进行升级，但功能 B 是准备就绪，可以升级到生产环境使用功能 A 开关设置为 off 的代码的所有和功能 B 切换。</span><span class="sxs-lookup"><span data-stu-id="ca656-151">If Feature A isn't ready to be promoted but the Feature B is ready, you can promote all of the code to Production with the Feature A switch off and the Feature B switch on.</span></span> <span data-ttu-id="ca656-152">然后，可以完成功能 A，并将其提升更高版本，所有与任何源的代码合并。</span><span class="sxs-lookup"><span data-stu-id="ca656-152">You can then finish Feature A and promote it later, all with no source code merging.</span></span>

<span data-ttu-id="ca656-153">指示使用分支或切换功能，如下一个分支结构，可采用敏捷且可重复的方式流动开发到生产环境中的代码。</span><span class="sxs-lookup"><span data-stu-id="ca656-153">Whether or not you use branches or toggles for features, a branching structure like this enables you to flow your code from development into production in an agile and repeatable way.</span></span>

<span data-ttu-id="ca656-154">此结构还可以快速响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="ca656-154">This structure also enables you to react quickly to customer feedback.</span></span> <span data-ttu-id="ca656-155">如果您需要进行快速修复到生产环境，您还可以执行的有效地采用灵活的方式。</span><span class="sxs-lookup"><span data-stu-id="ca656-155">If you need to make a quick fix to production, you can also do that efficiently in an agile way.</span></span> <span data-ttu-id="ca656-156">可以创建从 master 或暂存，一个分支和何时可以将其合并到主分支合并向上和向下为开发和功能分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-156">You can create a branch off of master or staging, and when it's ready merge it up into master and down into development and feature branches.</span></span>

![修补程序分支](source-control/_static/image2.png)

<span data-ttu-id="ca656-158">没有此类具有其单独的生产和开发分支的分支结构，生产问题可能使您无需提升新功能代码，以及您生产的修复程序的位置中。</span><span class="sxs-lookup"><span data-stu-id="ca656-158">Without a branching structure like this with its separation of production and development branches, a production problem could put you in the position of having to promote new feature code along with your production fix.</span></span> <span data-ttu-id="ca656-159">新的功能代码可能不是经过充分测试和准备好进行生产，您可能需要做大量工作正在放弃未准备好的更改。</span><span class="sxs-lookup"><span data-stu-id="ca656-159">The new feature code might not be fully tested and ready for production and you might have to do a lot of work backing out changes that aren't ready.</span></span> <span data-ttu-id="ca656-160">或者，可能需要延迟以测试更改，并使其准备好部署您的修复程序。</span><span class="sxs-lookup"><span data-stu-id="ca656-160">Or you might have to delay your fix in order to test changes and get them ready to deploy.</span></span>

<span data-ttu-id="ca656-161">接下来你将看到如何在 Visual Studio、 Azure 和 Azure 存储库中实现以下三种模式的示例。</span><span class="sxs-lookup"><span data-stu-id="ca656-161">Next you'll see examples of how to implement these three patterns in Visual Studio, Azure, and Azure Repos.</span></span> <span data-ttu-id="ca656-162">这些是示例而不是详细的分步说明-将执行操作的 it 说明;提供所有必需的上下文的详细说明，请参阅[资源](#resources)本章末尾部分。</span><span class="sxs-lookup"><span data-stu-id="ca656-162">These are examples rather than detailed step-by-step how-to-do-it instructions; for detailed instructions that provide all of the context necessary, see the [Resources](#resources) section at the end of the chapter.</span></span>

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a><span data-ttu-id="ca656-163">将脚本添加到 Visual Studio 中的源控件</span><span class="sxs-lookup"><span data-stu-id="ca656-163">Add scripts to source control in Visual Studio</span></span>

<span data-ttu-id="ca656-164">通过包括在 Visual Studio 解决方案文件夹中 （假设你的项目在源代码管理中），可以将脚本添加到 Visual Studio 中的源控件。</span><span class="sxs-lookup"><span data-stu-id="ca656-164">You can add scripts to source control in Visual Studio by including them in a Visual Studio solution folder (assuming your project is in source control).</span></span> <span data-ttu-id="ca656-165">下面是一种方法执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ca656-165">Here's one way to do it.</span></span>

<span data-ttu-id="ca656-166">在你的解决方案文件夹中创建的脚本的文件夹 (具有的相同文件夹你 *.sln*文件)。</span><span class="sxs-lookup"><span data-stu-id="ca656-166">Create a folder for the scripts in your solution folder (the same folder that has your *.sln* file).</span></span>

![自动化文件夹](source-control/_static/image3.png)

<span data-ttu-id="ca656-168">将脚本文件复制到的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca656-168">Copy the script files into the folder.</span></span>

![自动化文件夹内容](source-control/_static/image4.png)

<span data-ttu-id="ca656-170">在 Visual Studio 中，将添加到项目的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca656-170">In Visual Studio, add a solution folder to the project.</span></span>

![新解决方案文件夹菜单选项](source-control/_static/image5.png)

<span data-ttu-id="ca656-172">并将脚本文件添加到解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca656-172">And add the script files to the solution folder.</span></span>

![添加现有项菜单选项](source-control/_static/image6.png)

![“添加现有项”对话框](source-control/_static/image7.png)

<span data-ttu-id="ca656-175">你的项目中现在包含脚本文件和源控件正在跟踪其版本更改随相应的源代码更改。</span><span class="sxs-lookup"><span data-stu-id="ca656-175">The script files are now included in your project and source control is tracking their version changes along with corresponding source code changes.</span></span>

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a><span data-ttu-id="ca656-176">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="ca656-176">Store sensitive data in Azure</span></span>

<span data-ttu-id="ca656-177">如果在 Azure 网站中运行你的应用程序，避免将凭据存储在源代码管理中的一种方法是将其存储在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="ca656-177">If you run your application in an Azure Web Site, one way to avoid storing credentials in source control is to store them in Azure instead.</span></span>

<span data-ttu-id="ca656-178">例如，修复其应用程序将存储在其 Web.config 文件两个连接字符串会在生产环境和密钥，你的 Azure 存储帐户可以访问的密码。</span><span class="sxs-lookup"><span data-stu-id="ca656-178">For example, the Fix It application stores in its Web.config file two connection strings that will have passwords in production and a key that gives access to your Azure storage account.</span></span>

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

<span data-ttu-id="ca656-179">如果实际的生产中的这些设置的值将放在*Web.config*文件，或如果将其放在*Web.Release.config*文件来配置一个 Web.config 转换，以便将它们插入在部署期间，将源存储库中存储它们。</span><span class="sxs-lookup"><span data-stu-id="ca656-179">If you put actual production values for these settings in your *Web.config* file, or if you put them in the *Web.Release.config* file to configure a Web.config transform to insert them during deployment, they'll be stored in the source repository.</span></span> <span data-ttu-id="ca656-180">如果数据库连接字符串输入到生产环境发布配置文件，密码将在你 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="ca656-180">If you enter the database connection strings into the production publish profile, the password will be in your *.pubxml* file.</span></span> <span data-ttu-id="ca656-181">(你无法排除 *.pubxml*文件从源代码管理，但这样会失去共享所有其他部署设置的权益。)</span><span class="sxs-lookup"><span data-stu-id="ca656-181">(You could exclude the *.pubxml* file from source control, but then you lose the benefit of sharing all the other deployment settings.)</span></span>

<span data-ttu-id="ca656-182">Azure 为你提供的备用**appSettings**和连接字符串的部分*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ca656-182">Azure gives you an alternative for the **appSettings** and connection strings sections of the *Web.config* file.</span></span> <span data-ttu-id="ca656-183">下面是相关部分**配置**Azure 管理门户中的 web 站点的选项卡：</span><span class="sxs-lookup"><span data-stu-id="ca656-183">Here is the relevant part of the **Configuration** tab for a web site in the Azure management portal:</span></span>

![appSettings 和门户中的 connectionstrings 节](source-control/_static/image8.png)

<span data-ttu-id="ca656-185">在一个项目部署到此网站和应用程序运行时，已在 Azure 中存储任何值将覆盖 Web.config 文件中的任何有效值。</span><span class="sxs-lookup"><span data-stu-id="ca656-185">When you deploy a project to this web site and the application runs, whatever values you have stored in Azure override whatever values are in the Web.config file.</span></span>

<span data-ttu-id="ca656-186">通过使用管理门户或脚本，可以在 Azure 中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="ca656-186">You can set these values in Azure by using either the management portal or scripts.</span></span> <span data-ttu-id="ca656-187">在中看到的环境创建自动化脚本[使一切自动化](automate-everything.md)章创建 Azure SQL 数据库、 获取的存储和 SQL 数据库连接字符串，并将这些机密存储在您的网站的设置。</span><span class="sxs-lookup"><span data-stu-id="ca656-187">The environment creation automation script you saw in the [Automate Everything](automate-everything.md) chapter creates an Azure SQL Database, gets the storage and SQL Database connection strings, and stores these secrets in the settings for your web site.</span></span>

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

<span data-ttu-id="ca656-188">请注意，以便不获取实际值保存到源存储库参数化脚本。</span><span class="sxs-lookup"><span data-stu-id="ca656-188">Notice that the scripts are parameterized so that actual values don't get persisted to the source repository.</span></span>

<span data-ttu-id="ca656-189">当您在开发环境中本地运行时，应用读取您本地的 Web.config 文件和你的连接字符串指向 LocalDB SQL Server 数据库中*应用程序\_数据*web 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ca656-189">When you run locally in your development environment, the app reads your local Web.config file and your connection string points to a LocalDB SQL Server database in the *App\_Data* folder of your web project.</span></span> <span data-ttu-id="ca656-190">在 Azure 中运行应用并应用将尝试从 Web.config 文件中读取这些值，它将获取并使用时，对于网站，不是在 Web.config 文件中存储的值。</span><span class="sxs-lookup"><span data-stu-id="ca656-190">When you run the app in Azure and the app tries to read these values from the Web.config file, what it gets back and uses are the values stored for the Web Site, not what's actually in Web.config file.</span></span>

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a><span data-ttu-id="ca656-191">使用 Visual Studio 和 Azure DevOps 中的 Git</span><span class="sxs-lookup"><span data-stu-id="ca656-191">Use Git in Visual Studio and Azure DevOps</span></span>

<span data-ttu-id="ca656-192">可以使用任何源代码管理环境实现前面提供的 DevOps 分支结构。</span><span class="sxs-lookup"><span data-stu-id="ca656-192">You can use any source control environment to implement the DevOps branching structure presented earlier.</span></span> <span data-ttu-id="ca656-193">为分布式团队[分布式版本控制系统](http://en.wikipedia.org/wiki/Distributed_revision_control)(DVCS) 可以达到最佳效果; 对于其他团队[集中式系统](http://en.wikipedia.org/wiki/Revision_control)可能更好地工作。</span><span class="sxs-lookup"><span data-stu-id="ca656-193">For distributed teams a [distributed version control system](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) might work best; for other teams a [centralized system](http://en.wikipedia.org/wiki/Revision_control) might work better.</span></span>

<span data-ttu-id="ca656-194">[Git](http://git-scm.com/)是流行的分布式的版本控制系统。</span><span class="sxs-lookup"><span data-stu-id="ca656-194">[Git](http://git-scm.com/) is a popular distributed version control system.</span></span> <span data-ttu-id="ca656-195">当您使用 Git 进行源代码管理时，你在本地计算机上具有其历史记录的所有存储库的完整副本。</span><span class="sxs-lookup"><span data-stu-id="ca656-195">When you use Git for source control, you have a complete copy of the repository with all of its history on your local computer.</span></span> <span data-ttu-id="ca656-196">很多人喜欢，因为更容易以继续工作时不连接到网络，可以继续执行提交和回滚、 创建和切换分支，等等。</span><span class="sxs-lookup"><span data-stu-id="ca656-196">Many people prefer that because it's easier to continue working when you're not connected to the network -- you can continue to do commits and rollbacks, create and switch branches, and so forth.</span></span> <span data-ttu-id="ca656-197">即使您正在连接到网络，它是更轻松、 更快创建分支和切换分支时所有内容都是本地。</span><span class="sxs-lookup"><span data-stu-id="ca656-197">Even when you're connected to the network, it's easier and quicker to create branches and switch branches when everything is local.</span></span> <span data-ttu-id="ca656-198">此外可以执行本地提交和回滚操作不会影响对其他开发人员。</span><span class="sxs-lookup"><span data-stu-id="ca656-198">You can also do local commits and rollbacks without having an impact on other developers.</span></span> <span data-ttu-id="ca656-199">你可以执行批处理提交之前将它们发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="ca656-199">And you can batch commits before sending them to the server.</span></span>

<span data-ttu-id="ca656-200">[Azure 存储库](/azure/devops/repos/index?view=vsts)提供了这两[Git](/azure/devops/repos/git/?view=vsts)并[Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=vsts)(TFVC; 集中式源代码管理)。</span><span class="sxs-lookup"><span data-stu-id="ca656-200">[Azure Repos](/azure/devops/repos/index?view=vsts) offers both [Git](/azure/devops/repos/git/?view=vsts) and [Team Foundation Version Control](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; centralized source control).</span></span> <span data-ttu-id="ca656-201">开始使用 Azure DevOps[此处](https://app.vsaex.visualstudio.com/signup)。</span><span class="sxs-lookup"><span data-stu-id="ca656-201">Get started with Azure DevOps [here](https://app.vsaex.visualstudio.com/signup).</span></span>

<span data-ttu-id="ca656-202">Visual Studio 2017 包括内置的一流[Git 支持](https://msdn.microsoft.com/library/hh850437.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca656-202">Visual Studio 2017 includes built-in, first-class [Git support](https://msdn.microsoft.com/library/hh850437.aspx).</span></span> <span data-ttu-id="ca656-203">下面是一个快速的工作原理的演示。</span><span class="sxs-lookup"><span data-stu-id="ca656-203">Here's a quick demo of how that works.</span></span>

<span data-ttu-id="ca656-204">使用 Visual Studio 中打开项目，右键单击该解决方案中的**解决方案资源管理器**，然后选择**将解决方案添加到源代码管理**。</span><span class="sxs-lookup"><span data-stu-id="ca656-204">With a project open in Visual Studio, right-click the solution in **Solution Explorer**, and then choose **Add Solution to Source Control**.</span></span>

![将解决方案添加到源代码管理](source-control/_static/image9.png)

<span data-ttu-id="ca656-206">Visual Studio 会询问你是否想要使用 TFVC （集中式的版本控制） 或 Git。</span><span class="sxs-lookup"><span data-stu-id="ca656-206">Visual Studio asks if you want to use TFVC (centralized version control) or Git.</span></span>

![选择源代码管理](source-control/_static/image10.png)

<span data-ttu-id="ca656-208">当您选择 Git，然后单击**确定**，Visual Studio 在你的解决方案文件夹中创建新的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="ca656-208">When you select Git and click **OK**, Visual Studio creates a new local Git repository in your solution folder.</span></span> <span data-ttu-id="ca656-209">新的存储库有任何文件尚未;必须将它们添加到存储库中，通过执行操作的 Git 提交。</span><span class="sxs-lookup"><span data-stu-id="ca656-209">The new repository has no files yet; you have to add them to the repository by doing a Git commit.</span></span> <span data-ttu-id="ca656-210">右键单击该解决方案中的**解决方案资源管理器**，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="ca656-210">Right-click the solution in **Solution Explorer**, and then click **Commit**.</span></span>

![提交](source-control/_static/image11.png)

<span data-ttu-id="ca656-212">Visual Studio 自动暂存所有提交的项目文件，并列出它们**团队资源管理器**中**包含的更改**窗格。</span><span class="sxs-lookup"><span data-stu-id="ca656-212">Visual Studio automatically stages all of the project files for the commit and lists them in **Team Explorer** in the **Included Changes** pane.</span></span> <span data-ttu-id="ca656-213">(如果有一些不想包括到提交中，您可以选择它们，右键单击，然后单击**排除**。)</span><span class="sxs-lookup"><span data-stu-id="ca656-213">(If there were some you didn't want to include in the commit, you could select them, right-click, and click **Exclude**.)</span></span>

![Team Explorer](source-control/_static/image12.png)

<span data-ttu-id="ca656-215">输入提交注释，然后单击**提交**，和 Visual Studio 执行提交，并显示提交 id。</span><span class="sxs-lookup"><span data-stu-id="ca656-215">Enter a commit comment and click **Commit**, and Visual Studio executes the commit and displays the commit ID.</span></span>

![团队资源管理器更改](source-control/_static/image13.png)

<span data-ttu-id="ca656-217">现在如果您更改一些代码，以便不同于什么是存储库中，可以轻松地查看的差异。</span><span class="sxs-lookup"><span data-stu-id="ca656-217">Now if you change some code so that it's different from what's in the repository, you can easily view the differences.</span></span> <span data-ttu-id="ca656-218">右键单击你已更改的文件选择**Unmodified 与比较**，并获取比较显示它显示在未提交的更改。</span><span class="sxs-lookup"><span data-stu-id="ca656-218">Right-click a file that you've changed, select **Compare with Unmodified**, and you get a comparison display that shows your uncommitted change.</span></span>

![与未修改进行比较](source-control/_static/image14.png)

![显示更改的差异](source-control/_static/image15.png)

<span data-ttu-id="ca656-221">你可以轻松看到哪些更改需要做找出和签入。</span><span class="sxs-lookup"><span data-stu-id="ca656-221">You can easily see what changes you're making and check them in.</span></span>

<span data-ttu-id="ca656-222">假设您需要进行分支 – 你可以也可以这样做，Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="ca656-222">Suppose you need to make a branch – you can do that in Visual Studio too.</span></span> <span data-ttu-id="ca656-223">在中**团队资源管理器**，单击**新分支**。</span><span class="sxs-lookup"><span data-stu-id="ca656-223">In **Team Explorer**, click **New Branch**.</span></span>

![团队资源管理器中新的分支](source-control/_static/image16.png)

<span data-ttu-id="ca656-225">输入分支名称，单击**创建分支**，并且选中**签出分支**，Visual Studio 会自动签出新分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-225">Enter a branch name, click **Create Branch**, and if you selected **Checkout branch**, Visual Studio automatically checks out the new branch.</span></span>

![团队资源管理器中新的分支](source-control/_static/image17.png)

<span data-ttu-id="ca656-227">现在可以对文件进行更改并签入到此分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-227">You can now make changes to files and check them in to this branch.</span></span> <span data-ttu-id="ca656-228">您可以轻松地切换分支和 Visual Studio 之间自动同步到者为准分支文件已经签出。在此示例中 web 页标题中 *\_Layout.cshtml*已更改为"热修复补丁程序 1"中 HotFix1 分支。</span><span class="sxs-lookup"><span data-stu-id="ca656-228">And you can easily switch between branches and Visual Studio automatically syncs the files to whichever branch you have checked out. In this example the web page title in *\_Layout.cshtml* has been changed to "Hot Fix 1" in HotFix1 branch.</span></span>

![Hotfix1 分支](source-control/_static/image18.png)

<span data-ttu-id="ca656-230">如果切换回主分支的内容 *\_Layout.cshtml*文件自动还原到所在的主分支中。</span><span class="sxs-lookup"><span data-stu-id="ca656-230">If you switch back to the master branch, the contents of the *\_Layout.cshtml* file automatically revert to what they are in the master branch.</span></span>

![主分支](source-control/_static/image19.png)

<span data-ttu-id="ca656-232">此方式可以快速创建分支和分支之间来回切换的一个简单示例。</span><span class="sxs-lookup"><span data-stu-id="ca656-232">This a simple example of how you can quickly create a branch and flip back and forth between branches.</span></span> <span data-ttu-id="ca656-233">此功能使使用分支结构的高度灵活的工作流和自动化脚本中提供[使一切自动化](automate-everything.md)一章。</span><span class="sxs-lookup"><span data-stu-id="ca656-233">This feature enables a highly agile workflow using the branch structure and automation scripts presented in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="ca656-234">例如，可以是开发分支中工作，创建热修复补丁程序从 master 分支，切换到新分支，在那里进行更改和提交，然后切换回开发分支并继续之前进行的操作。</span><span class="sxs-lookup"><span data-stu-id="ca656-234">For example, you can be working in the Development branch, create a hot fix branch off of master, switch to the new branch, make your changes there and commit them, and then switch back to the Development branch and continue what you were doing.</span></span>

<span data-ttu-id="ca656-235">你已了解了如何使用 Visual Studio 中的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="ca656-235">What you've seen here is how you work with a local Git repository in Visual Studio.</span></span> <span data-ttu-id="ca656-236">在团队环境中你通常还将更改推送到的公共储存库。</span><span class="sxs-lookup"><span data-stu-id="ca656-236">In a team environment you typically also push changes up to a common repository.</span></span> <span data-ttu-id="ca656-237">Visual Studio 工具还可使其指向远程 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="ca656-237">The Visual Studio tools also enable you to point to a remote Git repository.</span></span> <span data-ttu-id="ca656-238">可以使用 GitHub.com 实现此目的，也可以使用[Git 和 Azure 存储库](/azure/devops/repos/git/overview?view=vsts)集成等工作项和 bug 跟踪的所有 Azure DevOps 功能。</span><span class="sxs-lookup"><span data-stu-id="ca656-238">You can use GitHub.com for that purpose, or you can use [Git and Azure Repos](/azure/devops/repos/git/overview?view=vsts) integrated with all the other Azure DevOps capabilities such as work item and bug tracking.</span></span>

<span data-ttu-id="ca656-239">这不是您可以实现敏捷的分支策略，当然的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="ca656-239">This isn't the only way you can implement an agile branching strategy, of course.</span></span> <span data-ttu-id="ca656-240">您可以使用集中式的源控件存储库相同的敏捷工作流。</span><span class="sxs-lookup"><span data-stu-id="ca656-240">You can enable the same agile workflow using a centralized source control repository.</span></span>

## <a name="summary"></a><span data-ttu-id="ca656-241">总结</span><span class="sxs-lookup"><span data-stu-id="ca656-241">Summary</span></span>

<span data-ttu-id="ca656-242">度量值基于多快的速度可以进行更改，并获取实时安全且可预测方式在源代码管理系统成功。</span><span class="sxs-lookup"><span data-stu-id="ca656-242">Measure the success of your source control system based on how quickly you can make a change and get it live in a safe and predictable way.</span></span> <span data-ttu-id="ca656-243">如果你发现自己被困难所吓倒，因为您只需一天或两个手动测试对其进行更改，您可能会问自己您需要做 process-wise 或 test-wise，以便可以使所做的更改，以分钟为单位，或在最差不再比一小时。</span><span class="sxs-lookup"><span data-stu-id="ca656-243">If you find yourself scared to make a change because you have to do a day or two of manual testing on it, you might ask yourself what you have to do process-wise or test-wise so that you can make that change in minutes or at worst no longer than an hour.</span></span> <span data-ttu-id="ca656-244">执行该操作的一种策略是实现持续集成和持续交付，我们将在中介绍[接下来的章节](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="ca656-244">One strategy for doing that is to implement continuous integration and continuous delivery, which we'll cover in the [next chapter](continuous-integration-and-continuous-delivery.md).</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="ca656-245">资源</span><span class="sxs-lookup"><span data-stu-id="ca656-245">Resources</span></span>

<span data-ttu-id="ca656-246">有关分支策略的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ca656-246">For more information about branching strategies, see the following resources:</span></span>

- <span data-ttu-id="ca656-247">[构建发布管道与 Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca656-247">[Building a Release Pipeline with Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx).</span></span> <span data-ttu-id="ca656-248">Microsoft 模式和实践文档。</span><span class="sxs-lookup"><span data-stu-id="ca656-248">Microsoft Patterns and Practices documentation.</span></span> <span data-ttu-id="ca656-249">请参阅有关的分支策略讨论第 6 章。</span><span class="sxs-lookup"><span data-stu-id="ca656-249">See chapter 6 for a discussion of branching strategies.</span></span> <span data-ttu-id="ca656-250">提倡者功能通过功能分支切换，如果使用功能分支，提倡保持其生存期较短 （小时或天至多）。</span><span class="sxs-lookup"><span data-stu-id="ca656-250">Advocates feature toggles over feature branches, and if branches for features are used, advocates keeping them short-lived (hours or days at most).</span></span>
- <span data-ttu-id="ca656-251">[版本控制指南](https://aka.ms/vsarsolutions)。</span><span class="sxs-lookup"><span data-stu-id="ca656-251">[Version Control Guide](https://aka.ms/vsarsolutions).</span></span> <span data-ttu-id="ca656-252">通过 ALM Rangers 指南分支策略。</span><span class="sxs-lookup"><span data-stu-id="ca656-252">Guide to branching strategies by the ALM Rangers.</span></span> <span data-ttu-id="ca656-253">在下载选项卡上，请参阅分支 Strategies.pdf。</span><span class="sxs-lookup"><span data-stu-id="ca656-253">See Branching Strategies.pdf on the Downloads tab.</span></span>
- <span data-ttu-id="ca656-254">[使用功能切换进行软件开发](https://msdn.microsoft.com/magazine/dn683796.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca656-254">[Software Development with Feature Toggles](https://msdn.microsoft.com/magazine/dn683796.aspx).</span></span> <span data-ttu-id="ca656-255">MSDN 杂志 》 一文。</span><span class="sxs-lookup"><span data-stu-id="ca656-255">MSDN Magazine article.</span></span>
- <span data-ttu-id="ca656-256">[功能切换](http://martinfowler.com/bliki/FeatureToggle.html)。</span><span class="sxs-lookup"><span data-stu-id="ca656-256">[Feature Toggle](http://martinfowler.com/bliki/FeatureToggle.html).</span></span> <span data-ttu-id="ca656-257">功能简介切换/Martin Fowler 的博客上的功能标志。</span><span class="sxs-lookup"><span data-stu-id="ca656-257">Introduction to feature toggles / feature flags on Martin Fowler's blog.</span></span>
- <span data-ttu-id="ca656-258">[功能切换与功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca656-258">[Feature Toggles vs Feature Branches](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx).</span></span> <span data-ttu-id="ca656-259">有关功能切换，由 Dylan Smith 的另一博客文章。</span><span class="sxs-lookup"><span data-stu-id="ca656-259">Another blog post about feature toggles, by Dylan Smith.</span></span>

<span data-ttu-id="ca656-260">有关如何处理不应保留在源代码管理存储库中的敏感信息的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ca656-260">For more information about how to handle sensitive information that should not be kept in source control repositories, see the following resources:</span></span>

- <span data-ttu-id="ca656-261">[有关密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务最佳实践](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ca656-261">[Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
- <span data-ttu-id="ca656-262">[Azure 网站：应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="ca656-262">[Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="ca656-263">介绍了重写的 Azure 功能`appSettings`并`connectionStrings`中的数据*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ca656-263">Explains the Azure feature that overrides `appSettings` and `connectionStrings` data in the *Web.config* file.</span></span>
- <span data-ttu-id="ca656-264">[自定义配置和应用程序设置在 Azure 网站-和 Stefan schackow 一起](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="ca656-264">[Custom configuration and application settings in Azure Web Sites - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).</span></span>

<span data-ttu-id="ca656-265">有关保留源代码管理中的敏感信息的其他方法的信息，请参阅[ASP.NET MVC:保留专用源代码管理设置带](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca656-265">For information about other methods for keeping sensitive information out of source control, see [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ca656-266">[上一页](automate-everything.md)
> [下一页](continuous-integration-and-continuous-delivery.md)</span><span class="sxs-lookup"><span data-stu-id="ca656-266">[Previous](automate-everything.md)
[Next](continuous-integration-and-continuous-delivery.md)</span></span>

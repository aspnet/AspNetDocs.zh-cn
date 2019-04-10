---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自动执行所有内容 （构建实际云应用与 Azure） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: d27c8c1910a79cea8ccdf4231d3bc2b80a20dc68
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418360"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="97173-104">自动执行所有内容 （构建使用 Azure 的真实世界云应用程序）</span><span class="sxs-lookup"><span data-stu-id="97173-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="97173-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="97173-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="97173-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="97173-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="97173-107">**构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="97173-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="97173-108">它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="97173-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="97173-109">电子书的简介，请参阅[的第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="97173-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="97173-110">我们将介绍的前三个模式实际上适用于任何软件开发项目中，但特别是用于云项目。</span><span class="sxs-lookup"><span data-stu-id="97173-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="97173-111">此模式是有关自动执行开发任务。</span><span class="sxs-lookup"><span data-stu-id="97173-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="97173-112">它是一个重要的主题，因为手动流程速度慢而且容易出错;尽可能多的设置的快速、 可靠且灵活的工作流可能有助于以自动执行。</span><span class="sxs-lookup"><span data-stu-id="97173-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="97173-113">它是唯一重要的云开发的因为可以轻松地自动执行各种难以或无法在本地环境中自动执行的许多任务。</span><span class="sxs-lookup"><span data-stu-id="97173-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="97173-114">例如，可以设置整个测试环境包括新的 web 服务器和后端 Vm，数据库、 blob 存储 （文件存储）、 队列等。</span><span class="sxs-lookup"><span data-stu-id="97173-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="97173-115">DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="97173-115">DevOps Workflow</span></span>

<span data-ttu-id="97173-116">越来越多地了解术语"DevOps"。</span><span class="sxs-lookup"><span data-stu-id="97173-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="97173-117">带认识，您必须集成开发和操作任务，以便有效地开发软件开发术语。</span><span class="sxs-lookup"><span data-stu-id="97173-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="97173-118">你想要启用的工作流的类型为一个在其中你可以开发应用程序、 将其部署、 学习它的生产使用情况、 将其更改以响应您已了解，和快速可靠地重复周期。</span><span class="sxs-lookup"><span data-stu-id="97173-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="97173-119">一些成功的云开发团队部署一天内多次到实时环境。</span><span class="sxs-lookup"><span data-stu-id="97173-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="97173-120">用于部署一个较大的 Azure 团队更新每隔 2-3 月，但是现在它每隔 2-3 天和主要版本每隔 2-3 周发布次要更新。</span><span class="sxs-lookup"><span data-stu-id="97173-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="97173-121">在着手创建该频率可以真正帮助您及时响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="97173-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="97173-122">为此，必须启用开发和部署周期为可重复、 可靠且可预测，并且具有较低的周期时间。</span><span class="sxs-lookup"><span data-stu-id="97173-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 工作流](automate-everything/_static/image1.png)

<span data-ttu-id="97173-124">换而言之，如果有一项功能想法和客户使用它和提供反馈时之间的时间段必须尽可能短。</span><span class="sxs-lookup"><span data-stu-id="97173-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="97173-125">前三个模式-自动化全部操作，从源代码管理和持续集成和交付-就是指我们要使这种过程建议的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="97173-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="97173-126">Azure 管理脚本</span><span class="sxs-lookup"><span data-stu-id="97173-126">Azure management scripts</span></span>

<span data-ttu-id="97173-127">在中[简介这本电子书](introduction.md)，看到了基于 web 的控制台中，Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="97173-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="97173-128">在管理门户，可监视和管理所有已在 Azure 部署的资源。</span><span class="sxs-lookup"><span data-stu-id="97173-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="97173-129">它是轻松地创建和删除 web 应用和 Vm 等服务，配置这些服务，监视服务操作，等等。</span><span class="sxs-lookup"><span data-stu-id="97173-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="97173-130">它是一个很好的工具，但使用它是一个手动过程。</span><span class="sxs-lookup"><span data-stu-id="97173-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="97173-131">如果想要开发生产应用程序的任何大小，尤其是在团队环境中，我们建议你通过门户以了解并探索 Azure 中，UI，然后自动执行需要重复执行的进程。</span><span class="sxs-lookup"><span data-stu-id="97173-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="97173-132">也可以通过调用 REST 管理 API 几乎是可以在管理门户中或从 Visual Studio 手动执行的一切。</span><span class="sxs-lookup"><span data-stu-id="97173-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="97173-133">你可以编写脚本使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)，或者可以使用的开放源代码框架，如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)。</span><span class="sxs-lookup"><span data-stu-id="97173-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="97173-134">您还可以在 Mac 或 Linux 环境中使用 Bash 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="97173-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="97173-135">Azure 具有脚本 Api 编写所有这些不同的环境，并且它具有[.NET 管理 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)以防你想要编写代码而不是脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="97173-136">我们已修复其应用创建自动执行以下过程创建测试环境，并将项目部署到该环境中，一些 Windows PowerShell 脚本和我们将回顾一些这些脚本的内容。</span><span class="sxs-lookup"><span data-stu-id="97173-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="97173-137">环境创建脚本</span><span class="sxs-lookup"><span data-stu-id="97173-137">Environment creation script</span></span>

<span data-ttu-id="97173-138">我们将介绍的第一个脚本名为*新建 AzureWebsiteEnv.ps1*。</span><span class="sxs-lookup"><span data-stu-id="97173-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="97173-139">它将创建 Azure 环境，您可以修复它将应用部署到用于测试。</span><span class="sxs-lookup"><span data-stu-id="97173-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="97173-140">此脚本执行的主要任务如下所示：</span><span class="sxs-lookup"><span data-stu-id="97173-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="97173-141">创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="97173-141">Create a web app.</span></span>
- <span data-ttu-id="97173-142">创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="97173-142">Create a storage account.</span></span> <span data-ttu-id="97173-143">（所需 blob 和队列，您将看到在后面的章节。）</span><span class="sxs-lookup"><span data-stu-id="97173-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="97173-144">创建 SQL 数据库服务器和两个数据库： 应用程序数据库和成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="97173-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="97173-145">设置存储在 Azure 应用程序将用于访问存储帐户和数据库。</span><span class="sxs-lookup"><span data-stu-id="97173-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="97173-146">创建将用于自动执行部署的设置文件。</span><span class="sxs-lookup"><span data-stu-id="97173-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="97173-147">运行脚本</span><span class="sxs-lookup"><span data-stu-id="97173-147">Run the script</span></span>


> [!NOTE]
> <span data-ttu-id="97173-148">一章的此部分显示了脚本和输入才能运行这些命令的示例。</span><span class="sxs-lookup"><span data-stu-id="97173-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="97173-149">此演示，并不提供所有需要知道，才能运行脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="97173-150">说明-将执行操作的 it 的分步说明，请参阅[附录：解决方法示例应用程序](the-fix-it-sample-application.md#deploybase)。</span><span class="sxs-lookup"><span data-stu-id="97173-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>


<span data-ttu-id="97173-151">若要运行 PowerShell 脚本，用于管理 Azure 服务，必须安装 Azure PowerShell 控制台并将其配置为使用你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="97173-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="97173-152">您正在设置后，你可以使用类似此命令的命令运行的 Fix It 环境创建脚本：</span><span class="sxs-lookup"><span data-stu-id="97173-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="97173-153">`Name`参数指定要在创建数据库和存储帐户时使用的名称和`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="97173-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="97173-154">有您可以使用，我们将在更高版本的其他参数。</span><span class="sxs-lookup"><span data-stu-id="97173-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 窗口](automate-everything/_static/image2.png)

<span data-ttu-id="97173-156">在脚本完成之后您可以在管理门户中看到已创建的内容。</span><span class="sxs-lookup"><span data-stu-id="97173-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="97173-157">您会发现两个数据库：</span><span class="sxs-lookup"><span data-stu-id="97173-157">You'll find two databases:</span></span>

![数据库](automate-everything/_static/image3.png)

<span data-ttu-id="97173-159">存储帐户：</span><span class="sxs-lookup"><span data-stu-id="97173-159">A storage account:</span></span>

![存储帐户](automate-everything/_static/image4.png)

<span data-ttu-id="97173-161">和 web 应用：</span><span class="sxs-lookup"><span data-stu-id="97173-161">And a web app:</span></span>

![网站](automate-everything/_static/image5.png)

<span data-ttu-id="97173-163">上**配置**选项卡上的 web 应用，可以看到它具有存储帐户设置和 SQL 数据库连接字符串设置为修复其应用。</span><span class="sxs-lookup"><span data-stu-id="97173-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="97173-165">*自动化*文件夹现在还包含 *&lt;websitename&gt;.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="97173-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="97173-166">此文件存储 MSBuild 将使用应用程序部署到刚创建的 Azure 环境的设置。</span><span class="sxs-lookup"><span data-stu-id="97173-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="97173-167">例如：</span><span class="sxs-lookup"><span data-stu-id="97173-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="97173-168">如您所见，创建一个完整的测试环境中，脚本，并且在大约 90 秒内完成整个过程。</span><span class="sxs-lookup"><span data-stu-id="97173-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="97173-169">如果你的团队的其他人想要创建的测试环境，它们可直接运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="97173-170">不仅速度快，而且还他们可以确信它们使用等同于正在使用的环境。</span><span class="sxs-lookup"><span data-stu-id="97173-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="97173-171">您不是完全按照确信，如果每个人都已进行设置手动使用管理门户 UI。</span><span class="sxs-lookup"><span data-stu-id="97173-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="97173-172">查看脚本</span><span class="sxs-lookup"><span data-stu-id="97173-172">A look at the scripts</span></span>

<span data-ttu-id="97173-173">有实际完成这项工作的三个脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="97173-174">调用一个从命令行并自动使用另外两个执行的一些任务：</span><span class="sxs-lookup"><span data-stu-id="97173-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="97173-175">*新 AzureWebSiteEnv.ps1*是主要的脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="97173-176">*新 AzureStorage.ps1*创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="97173-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="97173-177">*新 AzureSql.ps1*创建数据库。</span><span class="sxs-lookup"><span data-stu-id="97173-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="97173-178">主脚本中的参数</span><span class="sxs-lookup"><span data-stu-id="97173-178">Parameters in the main script</span></span>

<span data-ttu-id="97173-179">主脚本*新建 AzureWebSiteEnv.ps1*，定义了多个参数：</span><span class="sxs-lookup"><span data-stu-id="97173-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="97173-180">两个参数是必需的：</span><span class="sxs-lookup"><span data-stu-id="97173-180">Two parameters are required:</span></span>

- <span data-ttu-id="97173-181">该脚本创建的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="97173-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="97173-182">(这也用于 URL: `<name>.azurewebsites.net`。)</span><span class="sxs-lookup"><span data-stu-id="97173-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="97173-183">该脚本创建的数据库服务器的新管理用户的密码。</span><span class="sxs-lookup"><span data-stu-id="97173-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="97173-184">可选参数，你可以指定的数据中心位置 （默认为"West US"）、 数据库服务器管理员名称 （默认为"数据库用户"） 和数据库服务器的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="97173-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="97173-185">创建 web 应用</span><span class="sxs-lookup"><span data-stu-id="97173-185">Create the web app</span></span>

<span data-ttu-id="97173-186">该脚本会执行的第一件事是通过调用创建 web 应用`New-AzureWebsite`cmdlet，在将其传递给 web 应用名称和位置参数值：</span><span class="sxs-lookup"><span data-stu-id="97173-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="97173-187">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="97173-187">Create the storage account</span></span>

<span data-ttu-id="97173-188">然后运行主脚本*新建 AzureStorage.ps1*编写脚本，请指定"*&lt;websitename&gt;* 存储"的存储帐户名称和相同的数据中心位置为web 应用中。</span><span class="sxs-lookup"><span data-stu-id="97173-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;* storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="97173-189">*新 AzureStorage.ps1*调用`New-AzureStorageAccount`cmdlet 来创建存储帐户，和它返回帐户名称和访问密钥值。</span><span class="sxs-lookup"><span data-stu-id="97173-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="97173-190">若要访问的 blob 和队列的存储帐户中，应用程序将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="97173-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="97173-191">您可能并不总是希望创建新的存储帐户;通过添加参数，可以选择将定向为使用现有的存储帐户，可增强该脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="97173-192">创建数据库</span><span class="sxs-lookup"><span data-stu-id="97173-192">Create the databases</span></span>

<span data-ttu-id="97173-193">然后运行主脚本的数据库创建脚本，*新建 AzureSql.ps1*、 后设置为默认数据库和防火墙规则名称：</span><span class="sxs-lookup"><span data-stu-id="97173-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="97173-194">数据库创建脚本检索适用于开发人员计算机的 IP 地址，并设置防火墙规则，因此开发人员计算机可以连接到和管理服务器。</span><span class="sxs-lookup"><span data-stu-id="97173-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="97173-195">数据库创建脚本然后经历几个步骤来设置数据库：</span><span class="sxs-lookup"><span data-stu-id="97173-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="97173-196">通过创建服务器`New-AzureSqlDatabaseServer`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="97173-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="97173-197">创建防火墙规则以启用开发计算机来管理服务器并启用 web 应用可以连接到它。</span><span class="sxs-lookup"><span data-stu-id="97173-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="97173-198">创建的服务器名称和凭据，使用包含的数据库上下文`New-AzureSqlDatabaseServerContext`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="97173-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` <span data-ttu-id="97173-199">是调用的脚本中的函数`ConvertTo-SecureString`cmdlet 可加密密码并返回`PSCredential`对象，相同的类型的`Get-Credential`cmdlet 将返回。</span><span class="sxs-lookup"><span data-stu-id="97173-199">is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="97173-200">使用创建应用程序数据库和成员资格数据库`New-AzureSqlDatabase`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="97173-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="97173-201">调用本地定义的函数来创建每个数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="97173-201">Calls a locally defined function to create a connection string for each database.</span></span> <span data-ttu-id="97173-202">应用程序将使用这些连接字符串访问数据库。</span><span class="sxs-lookup"><span data-stu-id="97173-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="97173-203">Get SQLAzureDatabaseConnectionString 是基于为其提供的参数值创建的连接字符串在脚本中定义的函数。</span><span class="sxs-lookup"><span data-stu-id="97173-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="97173-204">返回包含的数据库服务器名称和连接字符串的哈希表。</span><span class="sxs-lookup"><span data-stu-id="97173-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="97173-205">Fix It 应用程序使用单独的成员身份和应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="97173-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="97173-206">还有可能要将成员资格和应用程序数据放在一个数据库中。</span><span class="sxs-lookup"><span data-stu-id="97173-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="97173-207">应用商店应用程序设置和连接字符串</span><span class="sxs-lookup"><span data-stu-id="97173-207">Store app settings and connection strings</span></span>

<span data-ttu-id="97173-208">Azure 有一项功能，使你能够存储设置和自动重写时返回的内容到应用程序尝试读取的连接字符串`appSettings`或`connectionStrings`Web.config 文件中的集合。</span><span class="sxs-lookup"><span data-stu-id="97173-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="97173-209">这是应用的替代方法[Web.config 转换](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)部署时。</span><span class="sxs-lookup"><span data-stu-id="97173-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="97173-210">有关详细信息，请参阅[在 Azure 中存储敏感数据](source-control.md#appsettings)此电子书中更高版本。</span><span class="sxs-lookup"><span data-stu-id="97173-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="97173-211">环境创建脚本将存储在 Azure 的所有`appSettings`和`connectionStrings`应用程序需要在 Azure 中运行时访问的存储帐户和数据库的值。</span><span class="sxs-lookup"><span data-stu-id="97173-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="97173-212">[New Relic](http://newrelic.com/)是我们将演示中的遥测数据框架[监视和遥测](monitoring-and-telemetry.md)一章。</span><span class="sxs-lookup"><span data-stu-id="97173-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="97173-213">环境创建脚本也会重启 web 应用，确保它选取的 New Relic 设置。</span><span class="sxs-lookup"><span data-stu-id="97173-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="97173-214">为部署做好准备</span><span class="sxs-lookup"><span data-stu-id="97173-214">Preparing for deployment</span></span>

<span data-ttu-id="97173-215">在该过程结束时，环境创建脚本调用两个函数来创建部署脚本将使用的文件。</span><span class="sxs-lookup"><span data-stu-id="97173-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="97173-216">这些函数之一可创建发布配置文件 *(&lt;websitename&gt;.pubxml*文件)。</span><span class="sxs-lookup"><span data-stu-id="97173-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="97173-217">该代码调用 Azure REST API 以获取发布设置，和它将保存中的信息 *.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="97173-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="97173-218">然后，它从该文件的模板文件和使用信息 (*pubxml.template*) 来创建 *.pubxml*包含发布配置文件的文件。</span><span class="sxs-lookup"><span data-stu-id="97173-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="97173-219">此两步过程模拟你在 Visual Studio 中所执行的操作： 下载 *.publishsettings*文件并导入，若要创建的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="97173-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="97173-220">其他函数使用另一个模板文件 (网站 environment.template) 来创建*网站 environment.xml*文件，其中包含部署脚本将使用与设置 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="97173-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="97173-221">故障排除和错误处理</span><span class="sxs-lookup"><span data-stu-id="97173-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="97173-222">脚本就像程序： 它们可能会失败，并且当他们做你想要知道为相关的失败，原因是什么。</span><span class="sxs-lookup"><span data-stu-id="97173-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="97173-223">出于此原因，环境创建脚本更改的值`VerbosePreference`变量从`SilentlyContinue`到`Continue`，以便显示所有详细消息。</span><span class="sxs-lookup"><span data-stu-id="97173-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="97173-224">它也会更改的值`ErrorActionPreference`变量从`Continue`到`Stop`，以便该脚本停止甚至当遇到非终止性错误：</span><span class="sxs-lookup"><span data-stu-id="97173-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="97173-225">它执行任何工作之前，该脚本将存储的开始时间，以便在完成时，它可以计算经过的时间：</span><span class="sxs-lookup"><span data-stu-id="97173-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="97173-226">完成其工作后，脚本将显示运行时间：</span><span class="sxs-lookup"><span data-stu-id="97173-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="97173-227">并为每个密钥操作脚本写入详细消息，例如：</span><span class="sxs-lookup"><span data-stu-id="97173-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="97173-228">部署脚本</span><span class="sxs-lookup"><span data-stu-id="97173-228">Deployment script</span></span>

<span data-ttu-id="97173-229">什么*新建 AzureWebsiteEnv.ps1*脚本来创建的环境，将执行*发布 AzureWebsite.ps1*脚本执行的应用程序部署。</span><span class="sxs-lookup"><span data-stu-id="97173-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="97173-230">部署脚本获取从 web 应用的名称*网站 environment.xml*创建环境创建脚本文件。</span><span class="sxs-lookup"><span data-stu-id="97173-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="97173-231">获取部署用户密码从 *.publishsettings*文件：</span><span class="sxs-lookup"><span data-stu-id="97173-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="97173-232">它将执行[MSBuild](http://msbuildbook.com/)生成并部署项目的命令：</span><span class="sxs-lookup"><span data-stu-id="97173-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="97173-233">如果已指定`Launch`在命令行参数，它调用`Show-AzureWebsite`cmdlet 打开默认浏览器访问网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="97173-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="97173-234">可以使用类似此命令的命令来运行部署脚本：</span><span class="sxs-lookup"><span data-stu-id="97173-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="97173-235">完成后，浏览器打开与在云中运行的站点和`<websitename>.azurewebsites.net`URL。</span><span class="sxs-lookup"><span data-stu-id="97173-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![修复此错误应用部署到 Windows Azure](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="97173-237">总结</span><span class="sxs-lookup"><span data-stu-id="97173-237">Summary</span></span>

<span data-ttu-id="97173-238">使用这些脚本可以确信在使用相同的选项的顺序将始终执行相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="97173-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="97173-239">这有助于确保团队每个开发人员不会漏掉了一些活动或搞得一团糟的内容或部署不会实际工作方式相同，在其他团队成员的环境中或在生产环境中他自己计算机上自定义内容。</span><span class="sxs-lookup"><span data-stu-id="97173-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="97173-240">类似的方式，您可以自动执行大多数 Azure 的管理功能均可在管理门户中，通过使用 REST API、 Windows PowerShell 脚本、.NET 语言 API 或一个 Bash 实用程序，可以运行在 Linux 或 mac。</span><span class="sxs-lookup"><span data-stu-id="97173-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="97173-241">在中[接下来的章节](source-control.md)我们将查看源代码，并解释其在源代码存储库中包含您的脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="97173-242">资源</span><span class="sxs-lookup"><span data-stu-id="97173-242">Resources</span></span>

- <span data-ttu-id="97173-243">[安装和配置适用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="97173-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="97173-244">说明如何安装 Azure PowerShell cmdlet 以及如何安装证书，你需要在您的计算机以便管理你的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="97173-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="97173-245">这是一个很好，因为它还具有用于 PowerShell 自身的资源的链接开始。</span><span class="sxs-lookup"><span data-stu-id="97173-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="97173-246">[Azure 脚本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。</span><span class="sxs-lookup"><span data-stu-id="97173-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="97173-247">适用于开发管理 Azure 服务，其中包含指向入门教程中，cmdlet 参考文档和源代码代码和示例脚本的脚本资源的 WindowsAzure.com 门户</span><span class="sxs-lookup"><span data-stu-id="97173-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="97173-248">[周末脚本专家：开始使用 Azure 和 PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97173-248">[Weekend Scripter: Getting Started with Azure and PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="97173-249">在专用于 Windows PowerShell 博客中，此文章提供了使用 PowerShell for Azure 的管理功能的出色介绍。</span><span class="sxs-lookup"><span data-stu-id="97173-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="97173-250">[安装和配置 Azure 跨平台命令行接口](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。</span><span class="sxs-lookup"><span data-stu-id="97173-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="97173-251">关于 Azure 的脚本框架，适用于 Mac 和 Linux 以及 Windows 系统的入门教程。</span><span class="sxs-lookup"><span data-stu-id="97173-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="97173-252">[下载 Azure Sdk 和工具主题的命令行工具部分](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="97173-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="97173-253">有关文档和命令行工具与适用于 Azure 相关的下载门户页面。</span><span class="sxs-lookup"><span data-stu-id="97173-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="97173-254">[使用 Azure 管理库和.NET 使一切自动化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97173-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="97173-255">Scott Hanselman 介绍了 Azure 的.NET 管理 API。</span><span class="sxs-lookup"><span data-stu-id="97173-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="97173-256">[使用 Windows PowerShell 脚本发布到开发和测试环境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97173-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="97173-257">说明如何使用的 MSDN 文档发布 Visual Studio 会自动生成用于 web 项目的脚本。</span><span class="sxs-lookup"><span data-stu-id="97173-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="97173-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。</span><span class="sxs-lookup"><span data-stu-id="97173-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="97173-259">在 Visual Studio 中添加了对 Windows PowerShell 的语言支持的 visual Studio 扩展。</span><span class="sxs-lookup"><span data-stu-id="97173-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="97173-260">[上一页](introduction.md)
> [下一页](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="97173-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>

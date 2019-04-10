---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 打包过程故障排除 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在 M 使用 EnablePackageProcessLoggingAndAssert 属性可以收集有关打包过程的详细的信息...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 79774c6a1a1d05d5a7bcd82a5d7aa888933cf089
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59420102"
---
# <a name="troubleshooting-the-packaging-process"></a>打包过程故障排除

通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用可以收集有关打包过程的详细的信息**EnablePackageProcessLoggingAndAssert** Microsoft Build Engine (MSBuild) 中的属性。
> 
> 当您将设置**EnablePackageProcessLoggingAndAssert**属性设置为**true**，MSBuild 将：
> 
> - 将有关打包过程的其他信息添加到生成日志。
> - 例如，记录在某些情况下的错误，如果在打包列表中找到重复的文件。
> - 创建中的日志目录*ProjectName*\_包文件夹并使用它来记录有关要打包的文件信息。
> 
> 如果打包过程失败，或你的 web 部署包不包含预期的文件，您可以使用此信息进程和 pinpoint 进行故障排除的使用情况问题。
> 
> > [!NOTE]
> > **EnablePackageProcessLoggingAndAssert**只有在生成项目使用，仅适用于属性**调试**配置。 在其他配置中将忽略此属性。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>了解 EnablePackageProcessLoggingAndAssert 属性

[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)描述如何为 Web 发布管道 (WPP) 提供的一组扩展的 MSBuild 功能并使其能够与 Internet 信息服务 (IIS) Web 集成的 MSBuild 目标部署工具 （Web 部署）。 在打包 web 应用程序项目时，调用 WPP 目标。

许多这些 WPP 目标包括记录的其他信息的条件逻辑时**EnablePackageProcessLoggingAndAssert**属性设置为**true**。 例如，如果您查看**包**目标，可以看到它创建一个额外的日志目录，并将文件的列表写入到一个文本文件，如果**EnablePackageProcessLoggingAndAssert**等于 **，则返回 true**。


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]


> [!NOTE]
> 在中定义的 WPP 目标*Microsoft.Web.Publishing.targets* %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。 您可以打开此文件并查看 Visual Studio 2010 或任何 XML 编辑器中的目标。 请注意不要修改该文件的内容。


## <a name="enabling-the-additional-logging"></a>启用其他日志记录

您可以提供的值**EnablePackageProcessLoggingAndAssert**以各种方式，具体取决于如何构建您的项目的属性。

如果生成你的项目从命令行，则可以提供的值**EnablePackageProcessLoggingAndAssert**属性作为命令行参数：


[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]


如果您使用自定义项目文件来生成项目，则可以包括**EnablePackageProcessLoggingAndAssert**中的值**属性**属性的**MSBuild**任务：


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]


如果要使用 Team Foundation Server (TFS) 生成定义来构建您的项目，则可以提供的值**EnablePackageProcessLoggingAndAssert**属性中的**MSBuild 参数**行：![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> 有关创建和配置生成定义的详细信息，请参阅[创建生成定义，支持部署](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。


或者，如果你想要在每次生成中包含的包，您可以修改 web 应用程序项目设置的项目文件**EnablePackageProcessLoggingAndAssert**属性设置为**true**。 应将属性添加到第一个**PropertyGroup** .csproj 或.vbproj 文件中的元素。


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]


## <a name="reviewing-the-log-files"></a>查看日志文件

当生成并打包 web 应用程序项目**EnablePackageProcessLoggingAndAssert**设置为**true**，MSBuild 将创建名为日志中的其他文件夹*ProjectName*\_包文件夹。 日志文件夹包含多个文件：

![](troubleshooting-the-packaging-process/_static/image2.png)

您看到的文件的列表将因你的项目和生成过程中的内容。 但是，这些文件通常用于记录的收集 WPP 打包过程的各个阶段的文件列表：

- *PreExcludePipelineCollectFilesPhaseFileList.txt*文件列出了进行打包删除指定排除任何文件之前的 MSBuild 收集的文件。
- *AfterExcludeFilesFilesList.txt*文件包含已修改的文件列表中移除指定排除任何文件之后。

    > [!NOTE]
    > 从打包过程中排除文件和文件夹的详细信息，请参阅[不包括文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。
- *AfterTransformWebConfig.txt*文件列出了收集后任何打包的文件*Web.config*已执行转换。 在此列表中，任何配置特定于*Web.config*转换文件，如*Web.Debug.config*并*Web.Release.config*，从适用于的文件列表中排除打包。 转换的单个*Web.config*包含在其位置。
- *PostAutoParameterizationWebConfigConnectionStrings.txt*文件后的连接字符串中包含的文件列表*Web.config*文件已参数化。 这是过程，您可以将连接字符串替换为目标环境的正确设置为部署包时。
- *Prepackage.txt*文件包含的文件要包含在包中已完成的预生成列表。

> [!NOTE]
> 额外的日志文件的名称通常与 WPP 目标相对应。 你可以通过检查来查看这些目标*Microsoft.Web.Publishing.targets* %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。


如果 web 程序包的内容不是预期的内容，查看这些文件非常有用的方式来标识在处理操作中的哪个点发生了错误。

## <a name="conclusion"></a>结束语

本主题介绍如何使用**EnablePackageProcessLoggingAndAssert**在 MSBuild 中打包过程进行故障排除的属性。 所述的不同方法可以在其中提供属性值设置为生成过程中，并描述了将属性设置为时记录的其他信息 **，则返回 true**。

## <a name="further-reading"></a>其他阅读材料

使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 WPP 和它如何管理打包过程的详细信息，请参阅[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。 有关如何从 web 部署包中排除特定文件和文件夹的指导，请参阅[不包括文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一个](running-windows-powershell-scripts-from-msbuild-project-files.md)

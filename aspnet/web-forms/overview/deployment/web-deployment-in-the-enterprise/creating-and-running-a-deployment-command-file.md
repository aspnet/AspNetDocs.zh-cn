---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 创建和运行的部署命令文件 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何生成命令文件，以便可以运行使用 Microsoft Build Engine (MSBuild) 项目文件作为单步，重新部署...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: 121df7482f7cbd70b191e518bae791f0642ccc7c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048334"
---
<a name="creating-and-running-a-deployment-command-file"></a>创建并运行部署命令文件
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何生成将允许您运行作为一个单步执行、 可重复的过程中使用 Microsoft Build Engine (MSBuild) 项目文件的部署的命令文件。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014;[联系人管理器](the-contact-manager-solution.md)解决方案&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解构建过程](understanding-the-build-process.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="process-overview"></a>过程概述

在本主题中，您将学习如何创建和运行使用这些项目文件来执行可重复部署到目标环境的命令文件。 从根本上来说，命令文件只需包含的 MSBuild 命令的：

- 告知 MSBuild 执行环境不可知*Publish.proj*文件。
- 告知*Publish.proj*哪些文件包含特定于环境的项目设置和在哪里可以找到它的文件。

## <a name="create-an-msbuild-command"></a>创建 MSBuild 命令

如中所述[了解构建过程](understanding-the-build-process.md)，特定于环境的项目文件&#x2014;等*Env Dev.proj*&#x2014;设计要导入到环境不可知*Publish.proj*在生成时的文件。 在一起，这两个文件提供一组完整的说明，告知 MSBuild 如何生成和部署你的解决方案。

*Publish.proj*文件使用**导入**元素导入特定于环境的项目文件。


[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]


在这种情况下，当您使用 MSBuild.exe 生成和部署 Contact Manager 解决方案，您需要：

- 在上运行 MSBuild.exe *Publish.proj*文件。
- 通过提供一个名为的命令行参数来指定特定于环境的项目文件的位置**TargetEnvPropsFile**。

若要执行此操作，MSBuild 命令应类似如下：


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]


在这里，它是一个简单的步骤，以将移至可重复、 单步执行部署。 您需要做是将您的 MSBuild 命令添加到.cmd 文件。 Contact Manager 解决方案，在 Publish 文件夹包含名为的文件*发布 Dev.cmd* ，正好可以实现此。


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]


> [!NOTE]
> **/Fl**开关指示 MSBuild 创建名为的日志文件*msbuild.log*调用 MSBuild.exe 时的工作目录中。


若要部署或重新部署 Contact Manager 解决方案，只需运行*发布 Dev.cmd*文件。 当您运行该文件时，则 MSBuild 将：

- 生成解决方案中的所有项目。
- 生成 web 应用程序项目的可部署 web 包。
- 生成数据库项目的.dbschema 和.deploymanifest 文件。
- 将 web 程序包部署到 web 服务器。
- 将数据库部署到数据库服务器。

## <a name="run-the-deployment"></a>运行部署

已为你的目标环境创建命令文件，应该能够完成整个部署，只需运行该文件。

**若要将 Contact Manager 解决方案部署到你的测试环境**

1. 在开发人员工作站中，打开 Windows 资源管理器，然后浏览到的位置*发布 Dev.cmd*文件。
2. 双击该文件以运行它。
3. 如果**打开文件 – 安全警告**出现对话框，请单击**运行**。
4. 如果你的配置设置和测试服务器将设置正确，在命令提示符窗口将显示**生成成功**MSBuild 已完成处理的项目文件时，消息。

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. 如果这是首次已将解决方案部署到此环境，你将需要添加到测试 web 服务器计算机帐户**db\_datawriter**并**db\_datareader**上的角色**ContactManager**数据库。 此过程所述[数据库服务器配置用于 Web 部署发布](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。

    > [!NOTE]
    > 只需创建数据库时分配这些权限。 默认情况下，生成过程将不会重新创建每个部署上的数据库&#x2014;相反，它将比较最新的架构的现有数据库并进行所需更改。 因此，只需将这些数据库角色映射第一次部署解决方案。
6. 打开 Internet Explorer 并浏览到联系人管理器应用程序的 URL (例如， `http://testweb1:85/ContactManager/`)。
7. 验证应用程序按预期方式正常工作，您可以添加联系人。

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>结束语

创建命令文件包含 MSBuild 说明为您提供构建和部署到特定的目标环境的多项目解决方案的便捷方法。 如果需要反复将你的解决方案部署到多个目标环境，可以创建多个命令文件。 在每个命令文件中，MSBuild 命令将生成相同的通用项目文件中，但它将指定不同的特定于环境的项目文件。 例如，若要将发布到开发人员或测试环境的命令文件可能包含此 MSBuild 命令：


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]


要将发布到过渡环境的命令文件可能包含此 MSBuild 命令：


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]


> [!NOTE]
> 有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。


你还可以通过重写属性或在 MSBuild 命令中设置各种其他开关来定义每个环境的生成过程。 有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。

> [!div class="step-by-step"]
> [上一页](deploying-database-projects.md)
> [下一页](manually-installing-web-packages.md)

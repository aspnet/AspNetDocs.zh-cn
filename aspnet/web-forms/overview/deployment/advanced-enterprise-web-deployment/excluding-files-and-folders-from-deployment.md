---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 从部署中排除文件和文件夹 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何您可以排除文件和文件夹从 web 部署包时生成并打包 web 应用程序项目。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133898"
---
# <a name="excluding-files-and-folders-from-deployment"></a>从部署中排除文件和文件夹

通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何您可以排除文件和文件夹从 web 部署包时生成并打包 web 应用程序项目。

本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="overview"></a>概述

生成 Visual Studio 2010 中的 web 应用程序项目时，Web 发布管道 (WPP)，可以通过打包到可部署 web 包编译的 web 应用程序来扩展此生成过程。 然后可以使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 来将此 web 包部署到远程 IIS web 服务器，或导入 web 包手动通过 IIS 管理器中。 此打包过程所述[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。

那么，如何执行控制包含在 web 中获取的内容包？ 在 Visual Studio 中，通过基础的项目文件中，项目设置为大量方案提供控制不足以满足。 但是，在某些情况下您可能想要调整到特定的目标环境 web 程序包的内容。 例如，你可能想要包括日志文件的文件夹，当您应用程序部署到测试环境，但当您应用程序部署到过渡或生产环境中排除的文件夹。 本主题将演示如何执行此操作。

## <a name="what-gets-included-by-default"></a>默认情况下获取包含的内容

在 Visual Studio 中配置 web 应用程序项目属性时**要部署的项**上列出**打包/发布 Web**页允许您指定想要包括在你的 web 部署包。 默认情况下，此设置为**仅运行此应用程序所需的文件**。

![](excluding-files-and-folders-from-deployment/_static/image1.png)

当你选择**仅运行此应用程序所需的文件**，WPP 将尝试确定哪些文件应添加到 web 包。 这包括：

- 所有生成都输出的项目。
- 生成操作的任何文件标记**内容**。

> [!NOTE]
> 确定要包括的文件的逻辑包含在此文件：   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*

## <a name="excluding-specific-files-and-folders"></a>排除特定文件和文件夹

在某些情况下，需要将更精细地控制对其部署文件和文件夹。 如果您知道哪些的文件，你想要排除的时间，并且排除适用于所有目标环境，您可以只需设置**生成操作**到每个文件的**None**。

**若要从部署中排除特定文件**

1. 在中**解决方案资源管理器**窗口中，右键单击该文件，然后依次**属性**。
2. 在中**属性**窗口，请在**生成操作**行中，选中**None**。

但是，这种方法并不总是方便。 例如，你可能想要改变哪些文件和文件夹包含根据你的目标环境中，从 Visual Studio 外部。 例如，在联系人管理器示例解决方案中，看一下 ContactManager.Mvc 项目的内容：

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 内部文件夹包含一些开发人员用于创建、 删除和填充出于开发目的的本地数据库的 SQL 脚本。 在此文件夹中为 nothing 应部署到过渡或生产环境。
- 脚本文件夹包含多个 JavaScript 文件。 单纯为支持调试，或者提供 Visual Studio 中的 IntelliSense 中包含大量这些文件。 其中某些文件不应部署到过渡或生产环境。 但是，你可能想要将其部署到开发人员的测试环境以帮助进行故障诊断。

尽管您可能会对项目文件中排除特定文件和文件夹操作，但没有更简单的方法。 WPP 包括一种机制来生成名为项列表中排除文件和文件夹**ExcludeFromPackageFolders**并**ExcludeFromPackageFiles**。 通过将您自己的项添加到这些列表，可以扩展此机制。 若要执行此操作，需要完成以下高级步骤：

1. 创建一个名为的自定义项目文件 *[项目名称].wpp.targets*项目文件所在的文件夹中。

    > [!NOTE]
    > *。 Wpp.targets*文件需要在 web 应用程序项目文件所在的文件夹&#x2014;等*ContactManager.Mvc.csproj*&#x2014;而不是任何自定义所在的文件夹中用于控制生成和部署过程的项目文件。
2. 在中 *。 wpp.targets*文件中，添加**ItemGroup**元素。
3. 在中**ItemGroup**元素中，添加**ExcludeFromPackageFolders**并**ExcludeFromPackageFiles**要排除特定文件和文件夹所需的项。

这是基本的结构 *。 wpp.targets*文件：

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

请注意，每个项包含名为的项元数据元素**FromTarget**。 这是一个可选值，不会影响生成过程中;它只是用于指示特定文件或文件夹已省略为什么如果有人查看生成日志。

## <a name="excluding-files-and-folders-from-a-web-package"></a>从 Web 包中排除文件和文件夹

下一个过程演示如何添加 *。 wpp.targets*到 web 应用程序项目以及如何使用文件来生成项目时从 web 包排除特定文件和文件夹的文件。

**若要从 web 部署包中排除文件和文件夹**

1. 在 Visual Studio 2010 中打开你的解决方案。
2. 在中**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目节点 (例如， **ContactManager.Mvc**)，指向**添加**，然后单击**新项**。
3. 在中**添加新项**对话框中，选择**XML 文件**模板。
4. 在 **名称** 框中，键入 *[项目名称]***.wpp.targets** (例如， **ContactManager.Mvc.wpp.targets**)，然后单击 **添加**.

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > 如果将新项添加到项目的根节点，在项目文件所在的同一文件夹中创建文件。 可以通过在 Windows 资源管理器中打开该文件夹对此进行验证。
5. 在文件中，添加**项目**元素和一个**ItemGroup**元素：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. 如果你想要从 web 包中排除文件夹，添加**ExcludeFromPackageFolders**元素**ItemGroup**元素：

   1. 在中**Include**属性，请提供你想要排除的文件夹的以分号分隔列表。
   2. 在中**FromTarget**元数据元素，提供有意义的值以指示文件夹会被排除的原因，类似的名称 *。 wpp.targets*文件。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. 如果你想要从 web 包中排除文件，添加**ExcludeFromPackageFiles**元素**ItemGroup**元素：

   1. 在中**Include**属性，请提供你想要排除的文件的以分号分隔列表。
   2. 在中**FromTarget**元数据元素，提供有意义的值以指示文件要排除的原因，类似的名称 *。 wpp.targets*文件。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. *[项目名称].wpp.targets*文件现在应类似如下：

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. 保存并关闭 *[项目名称].wpp.targets*文件。

下一次你生成并打包你的 web 应用程序项目，将自动检测 WPP *。 wpp.targets*文件。 不将 web 包中包括的任何文件和你指定的文件夹。

## <a name="conclusion"></a>结束语

本主题介绍了如何通过创建自定义生成 web 包时排除特定文件和文件夹 *。 wpp.targets* web 应用程序项目文件所在的文件夹中的文件。

## <a name="further-reading"></a>其他阅读材料

使用自定义 Microsoft Build Engine (MSBuild) 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 打包和部署过程的详细信息，请参阅[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)，[用于 Web 包部署的配置参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)，和[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

> [!div class="step-by-step"]
> [上一页](deploying-membership-databases-to-enterprise-environments.md)
> [下一页](taking-web-applications-offline-with-web-deploy.md)

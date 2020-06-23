---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署到生产 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ec025e757d00cbfbfbcda9408739d2593908bc07
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240627"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>使用 Visual Studio 的 ASP.NET Web 部署：部署到生产环境

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

在本教程中，您将设置一个 Microsoft Azure 帐户，创建过渡和生产环境，并使用 Visual Studio 一键式发布功能将 ASP.NET web 应用程序部署到过渡环境和生产环境。

如果愿意，可以部署到第三方托管提供商。 本教程中所述的大多数过程对于宿主提供程序或 Azure 都是相同的，只不过每个提供程序都有自己的用户界面用于帐户和网站管理。 可以在 Microsoft.com 网站上的[提供程序库](https://www.microsoft.com/web/hosting)中找到宿主提供程序。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看本系列教程中的故障排除页。

## <a name="get-a-microsoft-azure-account"></a>获取 Microsoft Azure 帐户

如果还没有 Azure 帐户，只需花费几分钟就能创建一个免费试用帐户。 有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。

## <a name="create-a-staging-environment"></a>创建过渡环境

> [!NOTE]
> 由于本教程已编写，因此 Azure App Service 添加了一项新功能来自动执行许多创建过渡和生产环境的过程。 请参阅[在 Azure App Service 中设置 web 应用的过渡环境](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。

如[部署到测试环境教程](deploying-to-iis.md)中所述，最可靠的测试环境是托管提供商的网站，就像生产网站一样。 在许多托管提供商上，你必须权衡此项的优势以增加额外成本，但在 Azure 中，可以创建其他免费的 web 应用作为暂存应用。 你还需要一个数据库，而超出生产数据库的费用的额外费用将是 "无" 或 "最小"。 在 Azure 中，你需要为你使用的数据库存储量（而不是每个数据库）付费，并且你将在暂存中使用的额外存储量将是最小值。

如[部署到测试环境教程](deploying-to-iis.md)中所述，在过渡和生产环境中，你要将两个数据库部署到一个数据库中。 如果您想要将它们分开，则该过程是相同的，只是您为每个环境创建了一个附加数据库，并在创建发布配置文件时为每个数据库选择正确的目标字符串。

在本教程的此部分中，你将创建用于过渡环境的 web 应用和数据库，并在创建并部署到生产环境之前，部署到此处进行过渡和测试。

> [!NOTE]
> 以下步骤演示如何使用 Azure 管理门户在 Azure App Service 中创建 web 应用。 在最新版本的 Azure SDK 中，你还可以通过使用服务器资源管理器，无需离开 Visual Studio 即可实现此目的。 在 Visual Studio 2013 中，还可以直接从 "发布" 对话框创建一个 web 应用。 有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. 在[Azure 管理门户](https://manage.windowsazure.com/)中，单击 "**网站**"，然后单击 "**新建**"。
2. 单击 "**网站**"，然后单击 "**自定义创建**"。

    **新网站-"自定义创建**" 向导将打开。 使用 "**自定义创建**" 向导，您可以同时创建网站和数据库。
3. 在向导的 "**创建网站**" 步骤中，在 " **URL** " 框中输入一个字符串，用作应用程序过渡环境的唯一 URL。 例如，输入 ContosoUniversity-staging123 （在末尾添加随机数，以使其在 ContosoUniversity 的情况下是唯一的）。

    完整的 URL 将包含你在此处输入的内容和你在文本框旁边看到的后缀。
4. 在 "**区域**" 下拉列表中，选择离你最近的区域。

    此设置指定 web 应用将在哪个数据中心运行。
5. 在 "**数据库**" 下拉列表中，选择 "**创建新的 SQL 数据库**"。
6. 在 "**数据库连接字符串名称**" 框中，保留默认值*DefaultConnection*。
7. 单击对话框底部的向右箭头。

    下图显示了 "**创建网站**" 对话框，其中包含示例值。 你输入的 URL 和区域将不同。

    ![创建网站步骤](deploying-to-production/_static/image1.png)

    向导转到 "**指定数据库设置**" 步骤。
8. 在 "**名称**" 框中，输入*ContosoUniversity*和随机数以使其唯一，例如*ContosoUniversity123*。
9. 在 "**服务器**" 框中，选择 "**新建 SQL 数据库服务器**"。
10. 输入管理员名称和密码。

    此处未输入现有名称和密码。 需要输入新的名称和密码，这些名称和密码需要现在定义，供以后访问数据库时使用。
11. 在 "**区域**" 框中，选择为 web 应用选择的相同区域。

    将 web 服务器和数据库服务器保留在同一区域可以获得最佳性能并最大限度地减少费用。
12. 单击框底部的复选标记以指示你已完成。

    下图显示了 "**指定数据库设置**" 对话框，其中包含示例值。 输入的值可能不同。

    !["新建网站-与数据库一起创建" 向导的 "数据库设置" 步骤](deploying-to-production/_static/image2.png)

    管理门户返回到 "网站" 页面，"**状态**" 列显示正在创建的 web 应用。 经过一段时间（通常不到一分钟），"**状态**" 列会显示已成功创建 web 应用。 在左侧的导航栏中，在 "**网站**" 图标旁边会显示你的帐户中拥有的 web 应用的数目，并且数据库的数目将显示在 " **SQL 数据库**" 图标旁边。

    ![管理门户的网站页面，网站已创建](deploying-to-production/_static/image3.png)

    你的 web 应用名称将不同于图中的示例应用。

## <a name="deploy-the-application-to-staging"></a>将应用程序部署到过渡环境

现在，你已创建用于过渡环境的 web 应用和数据库，接下来可以将项目部署到该环境中。

> [!NOTE]
> 这些说明演示如何通过下载 *.publishsettings*文件来创建发布配置文件，该文件不仅适用于 Azure，还适用于第三方托管提供商。 使用最新的 Azure SDK，你还可以从 Visual Studio 直接连接到 Azure，并从你的 Azure 帐户中的 web 应用列表中进行选择。 在 Visual Studio 2013 中，可以从**Web 发布**对话框或从**服务器资源管理器**窗口登录到 Azure。 有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。

### <a name="download-the-publishsettings-file"></a>下载 .publishsettings 文件

1. 单击刚刚创建的 web 应用的名称。

    ![单击该站点以切换到仪表板](deploying-to-production/_static/image4.png)
2. 在 "**仪表板**" 选项卡的 "**速览**" 下，单击 "**下载发布配置文件**"。

    ![下载发布配置文件链接](deploying-to-production/_static/image5.png)

    此步骤将下载一个文件，其中包含将应用程序部署到 web 应用所需的所有设置。 您将此文件导入到 Visual Studio 中，这样您就不必手动输入此信息。
3. 将 *.publishsettings*文件保存在可从 Visual Studio 访问的文件夹中。

    ![保存 .publishsettings 文件](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 安全性- *.publishsettings*文件包含用于管理 Azure 订阅和服务的凭据（未编码）。 确保此文件安全的最佳做法是，将其暂时存储在源目录的外部（例如存储在 Libraries\Documents 文件夹中），然后在完成导入后将其删除。 获得 *.publishsettings*文件访问权的恶意用户可以编辑、创建和删除你的 Azure 服务。

### <a name="create-a-publish-profile"></a>创建发布配置文件

1. 在 Visual Studio 中，右键单击**解决方案资源管理器**中的 ContosoUniversity 项目，然后从上下文菜单中选择 "**发布**"。

    “发布 Web”向导随即打开。****
2. 单击“配置文件”选项卡。****
3. 单击“导入”。
4. 导航到之前下载的 *.publishsettings*文件，然后单击 "**打开**"。

    !["导入发布设置" 对话框](deploying-to-production/_static/image7.png)
5. 在 "**连接**" 选项卡中，单击 "**验证连接**" 确保设置正确。

    验证连接后，"**验证连接**" 按钮旁边会显示一个绿色复选标记。

    对于某些宿主提供程序，单击 "**验证连接**" 时，可能会看到 "**证书错误**" 对话框。 如果执行此操作，请验证服务器名称是否与预期的相同。 如果服务器名称正确，请选择 "**为 Visual Studio 的未来会话保存此证书**"，然后单击 "**接受**"。 （此错误意味着宿主提供程序已选择避免为你要部署到的 URL 购买 SSL 证书。 如果你希望使用有效的证书建立安全连接，请与你的托管提供商联系。）
6. 单击“下一步”。

    ![“连接”选项卡中的连接成功图标和“下一步”按钮](deploying-to-production/_static/image8.png)
7. 在 "**设置**" 选项卡中，展开 "**文件发布选项**"，然后**从 "应用程序 \_ 数据" 文件夹中选择 "排除文件"**。

    有关 "**文件发布选项**" 下的其他选项的信息，请参阅[部署到 IIS](deploying-to-iis.md)教程。 在数据库配置步骤结束时，显示此步骤的结果和以下数据库配置步骤的屏幕截图。
8. 在 "**数据库**" 部分的 " **DefaultConnection** " 下，为成员资格数据库配置数据库部署。
9. 1. 选择 "**更新数据库**"。

        直接在**DefaultConnection**下的 "**远程连接字符串**" 框中填充了来自 .publishsettings 文件的连接字符串。连接字符串包含 SQL Server 凭据，这些凭据以纯文本形式存储在 *.pubxml*文件中。 如果不想将它们永久存储在该数据库中，则可以在部署数据库后将它们从发布配置文件中删除并将其存储在 Azure 中。 有关详细信息，请参阅在 Scott Hanselman 的博客上[从 ASP.NET 部署到 Azure 时如何保证你的数据库连接字符串的安全性](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx)。
      2. 单击 "**配置数据库更新**"。
      3. 在 "**配置数据库更新**" 对话框中，单击 "**添加 SQL 脚本**"。
      4. 在 "**添加 SQL 脚本**" 框中，导航到之前在 "解决方案" 文件夹中保存的*aspnet-data-prod*脚本，然后单击 "**打开**"。
      5. 关闭 "**配置数据库更新**" 对话框。
10. 在 "**数据库**" 部分的 " **SchoolContext** " 下，选择 "**执行 Code First 迁移（在应用程序启动时运行）**。

    Visual Studio 显示**Execute Code First 迁移**，而不是类的**Update 数据库** `DbContext` 。 如果要使用 dbDacFx 提供程序（而不是迁移）来部署通过使用类访问的数据库 `DbContext` ，请参阅 MSDN 上的 Visual Studio 的 Web 部署常见问题和 ASP.NET 中的[如何实现部署不迁移的 Code First 数据库？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)

    "**设置**" 选项卡现在类似于以下示例：

    ![暂存的 "设置" 选项卡](deploying-to-production/_static/image9.png)
11. 执行以下步骤以保存配置文件并将其重命名为*暂存*：

    1. 单击 "**配置文件**" 选项卡，然后单击 "**管理配置文件**"。
    2. 导入创建了两个新配置文件，一个用于 FTP，另一个用于 Web 部署。 你已配置 Web 部署配置文件：将此配置文件重命名为 "*暂存*"。

        ![将配置文件重命名为暂存](deploying-to-production/_static/image10.png)
    3. 关闭 "**编辑 Web 发布配置文件**" 对话框。
    4. 关闭 "**发布 Web** " 向导。

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>为环境指示器配置发布配置文件转换

> [!NOTE]
> 本部分说明如何设置环境指示器的 Web.config 转换。 因为指示器位于元素中，所以在 `<appSettings>` 部署到 Azure App Service 时，可以使用另一种方法来指定转换。 有关详细信息，请参阅[在 Azure 中指定 Web.config 设置](web-config-transformations.md#watransforms)。

1. 在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。
2. 右键单击 " *.pubxml*"，然后单击 "**添加配置转换**"。

    ![为暂存添加配置转换](deploying-to-production/_static/image11.png)

    Visual Studio 将创建*Web.Staging.config*转换文件并将其打开。
3. 在*Web.Staging.config*转换文件中，将以下代码插入到紧随开始 `configuration` 标记的后面。

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    当使用过渡发布配置文件时，此转换会将环境指示器设置为 "生产"。 在已部署的 web 应用中，你将看不到任何后缀，如 "Contoso 大学" H1 标题后面的 "（开发人员）" 或 "（测试）"。
4. 右键单击*Web.Staging.config*文件，然后单击 "**预览转换**"，以确保编码的转换会生成预期的更改。

    **Web.config 预览**"窗口显示应用*Web.Release.config*转换和*Web.Staging.config*转换的结果。

### <a name="prevent-public-use-of-the-test-app"></a>阻止公共使用测试应用

过渡应用程序的一个重要注意事项是它将在 Internet 上出现，但您不希望公开使用它。 若要最大程度地减少用户查找和使用它的可能性，可以使用以下一种或多种方法：

- 设置防火墙规则，仅允许从用于测试暂存的 IP 地址访问过渡应用。
- 使用不可能猜到的经过模糊处理的 URL。
- 创建一个*robots.txt*文件，以确保搜索引擎不会对测试应用进行爬网，并在搜索结果中向其报告链接。

这些方法中的第一种方法是最有效的，但在本教程中不涉及，因为这将要求你部署到 Azure 云服务而不是 Azure App Service。 有关 Azure 中的云服务和 IP 限制的详细信息，请参阅[Azure 提供的计算托管选项](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)和[阻止特定 IP 地址访问 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。 如果要部署到第三方托管提供商，请与提供商联系，以了解如何实现 IP 限制。

在本教程中，您将创建一个*robots.txt*文件。

1. 在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**添加新项**"。
2. 创建一个名为 " *robots.txt*" 的新**文本文件**，并在其中添加以下文本：

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent`该行通知搜索引擎文件中的规则适用于所有搜索引擎 web 爬网程序（机器人）， `Disallow` 行指定不应爬网网站上的任何页面。

    你确实希望搜索引擎为你的生产应用程序编目，因此你需要从生产部署中排除此文件。 为此，你将在创建生产发布配置文件时配置其设置。

### <a name="deploy-to-staging"></a>部署到过渡环境

1. 右键单击 Contoso 大学项目，然后单击 "**发布**"，打开 "**发布 Web** " 向导。
2. 请确保选择了**暂存**配置文件。
3. 单击“发布” 。

    “输出”窗口会显示已执行的部署操作并报告部署的成功完成。**** 默认浏览器会自动打开到已部署的 web 应用的 URL。

## <a name="test-in-the-staging-environment"></a>在过渡环境中测试

请注意，环境指示器不存在（"（测试）" 或 "（Dev）" 在 H1 标题之后，这表明环境指示器的*Web.config*转换已成功。

![主页过渡](deploying-to-production/_static/image12.png)

运行 "**学生**" 页，验证部署的数据库是否没有学生。

运行**讲师**页，验证 Code First 用指导员数据对数据库进行种子设定：

从 "**学生**" 菜单中选择 "**添加学生**"，添加一个学生，然后在 "**学生**" 页中查看新学生，验证是否可以成功写入到数据库。

在 "**课程**" 页上，单击 "**更新信用**"。 **更新信用**页面需要管理员权限，因此将显示 "**登录**" 页。 输入先前创建的管理员帐户凭据（"admin" 和 "prodpwd"）。 此时将显示 "**更新信用**" 页，该页面验证你在上一教程中创建的管理员帐户是否已正确部署到测试环境中。

请求一个无效的 URL 来导致 ELMAH 将跟踪的错误，然后请求 ELMAH 错误报告。 如果要部署到第三方托管提供程序，则可能会发现报表为空，原因是在上一教程中，此报表为空。 你将需要使用宿主提供程序的帐户管理工具来配置文件夹权限，以允许 ELMAH 写入日志文件夹。

你创建的应用程序现在在云中的 web 应用中运行，就像你将用于生产的应用程序一样。 由于一切都能正常运行，因此下一步是部署到生产环境。

## <a name="deploy-to-production"></a>部署到生产

除了需要从部署中排除*robots.txt*之外，创建生产 web 应用并将其部署到生产的过程与用于过渡的过程相同。 为此，你将编辑发布配置文件。

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>创建生产环境和生产发布配置文件

1. 按照用于过渡的相同过程，在 Azure 中创建生产 web 应用和数据库。

    创建数据库时，可以选择将其放在之前创建的同一服务器上，或创建新服务器。
2. 下载 *.publishsettings*文件。
3. 通过导入 *.publishsettings*文件来创建发布配置文件，遵循用于过渡的相同过程。

    别忘了在 "**设置**" 选项卡的 "**数据库**" 部分中的**DefaultConnection**下配置数据部署脚本。
4. 将发布配置文件重命名为 "*生产*"。
5. 按照用于过渡的相同过程，为环境指示器配置发布配置文件转换。

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>编辑 .pubxml 文件以排除 robots.txt

发布配置文件的名称为 &lt; profilename &gt; *. .Pubxml* ，位于*PublishProfiles*文件夹中。 *PublishProfiles*文件夹位于 c # web 应用程序项目中的 "*属性*" 文件夹下、VB web 应用程序项目的 "*我的项目*" 文件夹下或 Web 应用项目中的 "*应用 \_ 数据*" 文件夹下。 每个 *.pubxml*文件都包含适用于一个发布配置文件的设置。 您在 "发布 Web" 向导中输入的值存储在这些文件中，您可以对其进行编辑以创建或更改不能在 Visual Studio UI 中使用的设置。

默认情况下，当你创建发布配置文件时， *.pubxml*文件包含在项目中，但你可以将其从项目中排除，Visual Studio 仍将使用它们。 Visual Studio 将在*PublishProfiles*文件夹中查找 *.pubxml*文件，无论它们是否包含在项目中。

对于每个 *.pubxml*文件，都有一个 *.pubxml*文件。 如果选择了 "**保存密码**" 选项，则 *.pubxml*文件将包含加密密码，并且默认情况下会将其从项目中排除。

*.Pubxml*文件包含与特定发布配置文件相关的设置。 如果要配置适用于所有配置文件的设置，则可以创建一个 *. .targets*文件。 生成过程会将这些文件导入 *.csproj*或 *.vbproj*项目文件中，因此可以在这些文件中配置可在项目文件中配置的大多数设置。 有关 *.pubxml* *文件和 .pubxml 文件的*详细信息，请参阅[如何：在发布配置文件中编辑部署设置（.）文件和 Visual Studio Web 项目中的文件](https://msdn.microsoft.com/library/ff398069.aspx)。

1. 在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。
2. 右键单击 " *.pubxml* "，然后单击 "**打开**"。

    ![打开 .pubxml 文件](deploying-to-production/_static/image13.png)
3. 右键单击 " *.pubxml* "，然后单击 "**打开**"。
4. 紧靠在结束元素之前添加以下行 `PropertyGroup` ：

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    .Pubxml 文件现在如以下示例所示：

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    有关如何排除文件和文件夹的详细信息，请参阅 MSDN 上的**Visual Studio 和 ASP.NET 的 Web 部署常见问题解答**中的 "[能否从部署中排除特定文件或文件夹"](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 。

### <a name="deploy-to-production"></a>部署到生产

1. 打开 "**发布 Web** " 向导，确保已选择 "**生产**发布配置文件"，然后单击 "**预览**" 选项卡上的 "**开始预览**" 以验证是否不会将*robots.txt*文件复制到生产应用。

    ![要发布到生产的文件预览](deploying-to-production/_static/image14.png)

    查看要复制的文件的列表。 你将看到所有 *.cs*文件，包括*aspx.cs*、 *. aspx.designer.cs*、 *Master.cs*和*Master.designer.cs*文件。 所有此代码都已编译到*ContosoUniversity.dll*和*ContosoUniversity*文件中，这些文件将在*bin*文件夹中找到。 由于只需要 *.dll*来运行应用程序，并且您之前指定仅应部署运行应用程序所需的文件，因此，不会将 *.cs*文件复制到目标环境。 由于相同的原因，将省略*obj*文件夹和*ContosoUniversity*和 *.csproj*文件。

    单击 "**发布**" 以部署到生产环境。
2. 在生产环境中测试，遵循用于过渡的相同过程。

    除了 URL 和缺少*robots.txt*文件，所有内容都与过渡完全相同。

## <a name="summary"></a>总结

现在，你已成功部署并测试了 web 应用，并且该应用可通过 Internet 公开使用。

![主页生产](deploying-to-production/_static/image15.png)

在下一教程中，你将更新应用程序代码并将更改部署到测试、过渡和生产环境。

> [!NOTE]
> 当应用程序在生产环境中使用时，应实施恢复计划。 也就是说，应定期将数据库从生产应用备份到安全存储位置，并且应保留多代此类备份。 更新数据库时，应立即从更改之前创建备份副本。 然后，如果您在将其部署到生产环境之前，不会发现该错误，则您仍然能够将数据库恢复到其损坏之前的状态。 有关详细信息，请参阅 [Azure SQL 数据库备份和还原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。
> 
> 
> [!NOTE]
> 在本教程中，你要部署到的 SQL Server 版本是 Azure SQL 数据库。 尽管部署过程与 SQL Server 的其他版本类似，但在某些情况下，实际生产应用程序可能需要 Azure SQL 数据库的特殊代码。 有关详细信息，请参阅使用[AZURE Sql 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)和[在 SQL SERVER 和 Azure SQL 数据库之间进行选择](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。
> 
> [!div class="step-by-step"]
> [上一页](setting-folder-permissions.md)
> [下一页](deploying-a-code-update.md)

---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: 视觉工作室改进 2005 |微软文档
author: rick-anderson
description: Visual Studio 2005 为 Web 应用程序开发人员提供了 Web 项目改进和增强的一长串。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542971"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005 中的改进

由[微软](https://github.com/microsoft)

> Visual Studio 2005 为 Web 应用程序开发人员提供了 Web 项目改进和增强的一长串。

Visual Studio 2005 为 Web 应用程序开发人员提供了 Web 项目改进和增强的一长串。 与 Visual Studio .NET 2002 和 2003 一样强大，但处理 Web 项目的方式也有很多投诉。 Visual Studio 2005 增加了大量新功能，以解决这些投诉。 对于那些喜欢 Visual Studio .NET 2003 处理 Web 应用程序编译的方式的用户，请参阅[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。

在本模块中，很好地涵盖了 Web 项目创建、管理和开发方面的改进。 在后面的模块中，很好地涵盖了构建 Web 项目并部署它们的改进。

## <a name="frontpage-server-extensions"></a>首页服务器扩展

Visual Studio .NET 2002 和 2003 需要框上的 FrontPage 服务器扩展，以便创建或生成 Web 项目。 开发人员在两种不同的访问模式（FrontPage 服务器扩展名或文件访问模式）之间进行选择，这两种模式都使用 FrontPage 服务器扩展程序执行诸如在 IIS 中设置应用程序根等任务。

Visual Studio 2005 消除了对本地项目 FrontPage 服务器扩展的依赖。 Visual Studio 2005 现在直接访问 IIS 元库，而不是使用 FrontPage 服务器扩展。 Visual Studio 2005 还添加了对 FTP 的支持，该支持允许远程项目访问，而无需 FrontPage 服务器扩展。

对于那些想要在其项目中使用 FrontPage 服务器扩展的开发人员，该选项仍然可用。 但是，根据ASP.NET开发人员社区的强烈反馈，这不是一项要求。

> [!NOTE]
> 远程项目创建、打开等仍然需要 FrontPage 服务器扩展。

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005 附带了一个名为ASP.NET开发服务器的新 Web 服务器。 （此 Web 服务器以前称为卡西尼。

ASP.NET开发服务器有几个好处。

- 现在，非管理员可以针对 Web 服务器开发和调试。
- ASP.NET开发服务器动态地将虚拟目录映射到文件系统中的任何位置，从而允许灵活的项目位置。
- Windows XP 专业版上已经使用 IIS 的用户现在将能够创建新的 Web 应用程序，这些应用程序不会影响其在 IIS 中的默认网站的文件或文件夹结构。

无需特殊配置即可利用ASP.NET开发服务器。 当文件系统上托管的 Web 项目被调试或浏览时，Visual Studio 2005 将自动启动随机端口上的ASP.NET开发服务器的实例来为请求提供服务。

本模块稍后将介绍ASP.NET开发服务器的详细信息。

## <a name="improved-file-management"></a>改进的文件管理

在 Visual Studio 2002 和 2003 中，一个项目文件（VB.NET.vbproj 和 .csproj 表示 C#）存储了 Web 应用程序中所有文件的信息。 解决方案资源管理器显示基于项目文件中的文件信息。 因此，在使用外部编辑器的情况下，解决方案资源管理器通常会显示不准确的信息。 Visual Studio 2002 和 2003 通常会覆盖文件更改或不显示最新版本的文件。

Visual Studio 2005 不需要使用项目文件。 相反，它直接从磁盘读取文件和文件夹信息，从而准确显示项目中的文件。 由于 Visual Studio 2002 和 2003 中的"引用"文件夹不表示 Web 应用程序中的实际文件夹，因此 Visual Studio 2005 还会从解决方案资源管理器中删除"引用"文件夹。 要访问 Visual Studio 2005 中的项目的引用，应使用项目的属性页。

## <a name="creating-web-projects"></a>创建 Web 项目

Web 开发人员在 Visual Studio 2005 中有许多可用于项目创建的新选项。 网站现在可以在文件系统的任意位置创建，然后可以使用新的ASP.NET开发服务器进行调试或浏览。 开发人员还可以使用 FTP 创建新的网站。

单击此处查看 Visual Studio 2005 中创建 Web 项目的视频演练。

![](improvements-in-visual-studio-2005/_static/image1.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>文件系统项目

正如您在视频演练中所看到的，您可以选择通过文件共享在文件系统上或在远程位置创建网站。 使用ASP.NET开发服务器浏览和调试在文件系统上创建的网站。

> [!NOTE]
> ASP.NET开发服务器可能会给客户带来一些混乱。 如果在 IS 目录结构（即 c：/inetpub/wwwroot）的文件系统上创建了 Web 项目，则从 Visual Studio 2005 内部启动时，该网站仍将通过ASP.NET开发服务器进行浏览。 因此，任何 IIS 配置（即身份验证方法）都不适用。

默认 Web 项目还仅包括 Default.aspx 页、default.cs文件和 App/_Data 文件夹，从而删除了大量开销。 根据需要添加 Web.config 和特殊文件夹（即应用/_code）。 您的 Web 项目仅包括所需的文件和文件夹。

### <a name="http-projects"></a>HTTP 项目

HTTP 项目可以是在本地 IIS 网站或远程网站上创建的项目。 默认项目位置为`http://localhost`。 如果单击"浏览"按钮，则有两个 HTTP 选项：本地 IIS 和远程站点。 这两个选项的主要区别是在"选择位置"对话框中显示网站信息的方法以及文件复制到 Web 服务器的方式。

"本地 IIS"选项从本地计算机上的元库中读取站点信息，并使用文件系统复制文件。 远程站点选项使用 FrontPage 服务器扩展名，站点信息和文件使用 HTTP 和 FrontPage 服务器扩展程序 RPC 调用进行复制。

> [!NOTE]
> vs_/_tmp.htm 文件和 get/_aspx/_ver.aspx 不再用于确定版本信息。

默认 HTTP 选项为本地 IIS。 此选项读取 IIS 元库以确定哪些站点可用以及创建内容的位置。 您可以通过在树视图中选择其他文件夹或虚拟目录来选择它。 您还可以创建新的虚拟目录、将文件夹标记为应用程序，以及从此对话框中删除现有的虚拟目录。

![选择位置对话框](improvements-in-visual-studio-2005/_static/image1.gif)

**图 1**： 选择位置对话框

与早期版本的 Visual Studio 不同，如果选中 **"使用安全套接字层"** 复选框，并且 SSL 证书与您正在浏览的 URL 不匹配，则将显示一个安全警报对话框，询问您是否要继续。 使用 Visual Studio .NET 2003，如果证书不是匹配的，则创建项目将失败。

![有关 SSL 证书的安全警报](improvements-in-visual-studio-2005/_static/image2.gif)

**图 2**： 有关 SSL 证书的安全警报

### <a name="note-on-host-headers"></a>主机标题上的注释

如果要在绑定到特定 IP 的站点上创建 Web 应用程序，则需要确保配置主机标头。 否则，Visual Studio 将在 中`http://localhost`创建站点，但当从 IDE 内部浏览或调试站点时，IP 地址将无法正确解析。

如果选择"远程站点"选项，则对话框将更改以允许您输入新网站的目标 URL。 此 URL 必须位于已启用了 FrontPage 服务器扩展名的服务器上。 如果要使用 FrontPage 服务器扩展程序使用本地 Web 服务器，可以使用"远程站点"选项并指定本地 URL。

![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

**图 3**： 在远程服务器上创建网站

通过 SSL 在远程站点上创建应用程序时，如果 SSL 证书不匹配，则确认对话框与使用本地 IIS 选项时显示的对话框略有不同。

![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

**图 4**： 远程站点安全警报

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 引入了通过 FTP 创建网站的选项。 使用此选项时，IDE 会在用户临时文件夹中在本地创建文件，然后使用 FTP 将文件移动到 FTP 位置。

> [!NOTE]
> 临时文件夹位置为 c：/文档和设置/&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/=&lt;应用程序名称&gt;

使用 FTP 选项时，将显示"选择位置"对话框。 在此对话框中输入所需的 FTP 连接信息，如下所示。

![FTP 的"选择位置"对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

**图 5**： FTP 的"选择位置对话框"

## <a name="lab-setup-ftp-site-and-create-a-project"></a>实验室：设置 FTP 站点并创建项目

以下步骤配置 FTP 站点，以便用户具有只有他们才能通过 FTP 上载到的位置。

### <a name="install-the-ftp-service"></a>安装 FTP 服务

1. 打开"添加删除程序"，选择"添加/删除 Windows 组件"
2. 选择互联网信息服务（Windows 2003 上的应用程序服务器），然后单击 **"详细信息**"。
3. 检查**文件传输协议 （FTP） 服务**，然后单击 **"确定**"。
4. 单击 **"下一步**"以安装 FTP 服务。

### <a name="create-a-new-folder-for-content"></a>为内容创建新文件夹

1. 在 Windows 资源管理器中，在 c：/inetpub/wwwroot 内部创建名为**User1**的新文件夹。

#### <a name="configure-folders-and-permissions-on-folders"></a>配置文件夹和文件夹的权限。

1. 从管理工具打开互联网信息服务快照。 现在，您的计算机名称节点下将有一个 FTP Sites 文件夹。
2. 扩展**FTP 网站**。
3. 右键单击**默认 FTP 站点**，选择 **"新建**"，然后单击 **"****下一步**"。
4. 输入虚拟目录名称**的用户 1，** 然后单击 **"下一步**"。
5. 输入**路径的 c：/inetpub/wwwroot/User1，** 然后单击 **"下一步**"。
6. 单击 **"下一步****"，然后单击"完成"** 以完成向导。
7. 右键单击默认 FTP 站点下的**User1**虚拟目录，然后选择**属性**。
8. 选中 **"写入"** 复选框，然后单击"**确定"** 以关闭对话框。
9. 右键单击**默认 FTP 站点**并选择**属性**。
10. 在"**安全帐户"** 选项卡上，取消选中 **"允许匿名连接**"。
11. 在对话框中单击 **"是**"，询问是否要继续。
12. 单击 **“确定”**，关闭对话框。
13. 在 **"网站"** 节点下展开**默认网站**。
14. 右键单击**User1**目录并选择 **"属性"**
15. 在"**应用程序设置"** 部分中，单击"**创建**"将文件夹标记为应用程序。
16. 单击 **“确定”**，关闭对话框。
17. 关闭互联网信息服务卡入。

### <a name="create-web-project"></a>创建 Web 项目

1. 打开 Visual Studio 2005。
2. 在 **"文件"** 菜单中，选择 **"新建网站**"。
3. 在 **"位置**"下拉下列表中，选择**FTP**。
4. 单击“浏览”****。
5. 在 **"服务器**"文本框中输入**本地主机**。
6. 在"目录"文本框中输入**用户 1。**
7. 单击“打开”。 FTP 位置将输入到"新建网站"对话框中。
8. 单击 **“确定”** 。
9. 取消在 FTP 登录对话框中**打开匿名登录**，输入凭据，然后单击"**确定**"。
10. 项目的 URL 是什么？ （项目的 URL 将显示在解决方案资源管理器中。
11. 在 **"生成"** 菜单中，选择 **"生成网站**"或 **"生成解决方案**"。
12. 右键单击解决方案资源管理器中的 Default.aspx，然后选择 **"浏览器中的视图**"。
13. 在"网站网址必需"对话框中，`http://localhost/user1`输入 URL 并单击"**确定**"。

> [!NOTE]
> 如果收到指示无法加载类型 /_Default 的错误，请确保在 Web 站点上运行ASP.NET 2.0，而不是早期版本。 您可以在"互联网信息服务"中的ASP.NET选项卡上执行此操作。

## <a name="opening-web-projects"></a>打开 Web 项目

打开 Web 项目类似于创建项目。 以下各节会标注在 IDE 中工作时注意的区域。 它还涵盖使用 HTTP 和 FTP 处理 Web 项目。

要打开 Web 项目，请从"文件"菜单中选择"打开网站"。 系统、本地 IIS、FTP 和远程站点，系统将提示您使用以前介绍的相同"选择位置"对话框，并且有相同的四个选项可供您使用。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>文件系统

如本模块前面所述，Visual Studio 不再使用项目文件。 因此，如果您选择从文件系统打开网站，则实际上可以选择任何希望选择的文件夹，即使您选择的文件夹最初未在 Visual Studio 中作为 Web 项目创建。 例如，您可以选择以网站身份打开"我的文档"文件夹，Visual Studio 将愉快地打开该文件夹并显示您的文件，如下所示。

![我的文档作为网站打开](improvements-in-visual-studio-2005/_static/image3.jpg)

**图 6**：*我的文档*作为网站打开

由于 Visual Studio 仅在必要时创建其他文件和文件夹，因此不会将其他文件或文件夹添加到您打开的位置。 此体系结构的副作用是，它可以防止您在文件系统上嵌套网站。 例如，请考虑以下目录结构。

C：/我的Web网站网络项目

C：/MyWebSite/嵌套的另一个 Web 项目

当您在 c：/MyWebSite 打开网站时，"嵌套"文件夹将显示为该应用程序的子文件夹。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

通过 HTTP 打开网站时，可以从 IIS 元库（本地 IIS）或使用 FrontPage 服务器扩展（远程站点）读取设置。如果有嵌套 Web 应用程序，则这些应用程序将显示，并带有一个图标，用于标识它们为应用程序。 如果您熟悉在 FrontPage 中处理 Web 应用程序，则 Visual Studio 2005 中的行为类似。

即使 Visual Studio 将显示嵌套在 IDE 中当前打开的应用程序下方的应用程序的图标，但它也不允许扩展它们以查看其内容。 但是，您可以双击它们以打开它们。 执行此操作时，将显示一个对话框，提示您打开 Web 应用程序（并替换当前打开的解决方案）或将 Web 应用程序添加到当前解决方案。

![双击嵌套应用程序图标将显示此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

**图 7**： 双击嵌套应用程序图标将为您提供此对话框

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 站点

当您通过 FTP 打开网站时，这些文件都将在本地复制到临时文件夹。 本地存储位置的完整路径显示在项目的"属性"窗格中，并使用以下格式创建。

C：/文档和设置/&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/=&lt;应用程序名称&gt;

使用 FTP 时，Visual Studio 需要指定项目的基本 URL，以便可以浏览它，如下所示。 如果不指定基本 URL，Visual Studio 将在您首次尝试浏览网站中的页面时询问它。

![为 FTP 站点指定基本 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

**图 8**： 为 FTP 站点指定基本 URL

## <a name="improvements-in-compilation"></a>编译的改进

在 Visual Studio 2005 中处理 Web 应用程序的速度明显快于以前的版本。 这在很大程度上是由于编译体系结构的更改。

在 Visual Studio 2002 和 2003 中，Web 应用程序被编译为驻留在 /bin 文件夹中的一个主程序集。 在 Visual Studio 2005 中，添加了一个应用/_Code文件夹。 类和其他非 UI 代码将添加到应用/_Code文件夹。 当 Visual Studio 生成项目时，App/_Code 文件夹中的所有文件都将编译为单个 App/_Code.dll 文件。 此更改的结果是后续生成比早期版本快得多。

> [!NOTE]
> MSBuild 命令行实用程序还可用于构建ASP.NET Web 应用程序。 该工具将在第 9 单元中介绍。

另一个编译增强功能是"生成"菜单上的新"生成页"选项。 此功能允许开发人员仅重建当前页面（当然，以及依赖项），以便可以更快地编译更改。 由于 C# 不提供用于更新 IntelliSense 等的背景编译，因此它们将从此功能中获益匪浅，因为它将允许通过仅重建单个页面快速更新 IntelliSense。

项目的生成属性允许您配置在执行启动页之前发生的生成类型。 开发人员可以选择仅生成当前页面，以便 Visual Studio 可以在代码更改后更快地开始调试应用程序。

![生成页启动操作](improvements-in-visual-studio-2005/_static/image6.jpg)

**图 9**： 生成页开始操作

Visual Studio 和 ASP.NET架构的另一大增强是在编辑和继续方面。 在 Visual Studio 2005 中，开发人员可以开始调试项目，并在项目上进行代码更改，而无需分离调试器。 事实上，您可以从字面上开始调试项目、添加新类、向该类添加代码、向创建该类的新实例的页面添加代码以及执行类的方法，所有这些都不分离调试器。 执行新代码实际上和刷新浏览器一样简单！

单击此处查看 Visual Studio 2005 中编辑视频演练并继续功能。

![](improvements-in-visual-studio-2005/_static/image2.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 和 Visual Studio 2005 中强大的编辑和继续功能是由于ASP.NET应用程序的体系结构更改。 在 ASP.NET 1.x 中，在 Visual Studio 2002/2003 中创建的应用程序编译为存储在 /bin 文件夹中的主程序集。 应用程序的所有类、页面等都编译到该 DLL 中。 然后在运行时，ASP.NET将编译页面中的所有控件、标记和ASP.NET代码，并将这些 DLL 复制到ASP.NET临时文件夹中。

在使用 ASP.NET 2.0 的 Visual Studio 2005 中，上述两个编译模型（一个用于 Visual Studio，一个用于运行时ASP.NET）已合并为一个通用编译模型。 这意味着所有编译问题现在都在开发阶段而不是运行时捕获。 它还允许设计器和 IntelliSense 支持用户控件和母版页等功能。

单击此处查看设计器对用户控件的支持的视频演练。

![](improvements-in-visual-studio-2005/_static/image3.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> 从页面中删除用户控件时，@Register该指令将保留在标记中，并且应手动删除，以避免在从网站中删除用户控件时解析器错误。

可视化工作室编译模型的另一个改进是发布网站功能。 由于"发布"功能预先编译了网站，因此开发人员可以享受无需按需编译任何内容的额外性能。 它还将 App/_Code 文件夹中的所有源代码预编译为 DLL，以便无需部署源代码。

![发布网站对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

**图 10**： 发布网站对话框

> [!NOTE]
> aspnet/_compile.exe 实用程序也可用于预编译ASP.NET Web 应用程序。 该工具将在第 9 单元中介绍。

发布网站时，预编译文件将存储在临时ASP.NET文件文件夹中，如下所示。 具有 *.ssd*文件扩展名的文件是定义特定 DLL 依赖项的 XML 文件。 任何 Web 窗体或用户控件都编译为以*应用 _/Web/_* 开头的随机 DLL。

如果选中"*允许此预编译网站可升级"* 复选框，则 Web 窗体和用户控件内的标记将不会预先编译为 DLL，从而允许您在部署后进行更改。 如果您希望锁定标记以不允许更改已部署的内容，请取消选中此框。

*使用固定命名和单页程序集*复选框允许您禁用批处理编译，以便将每个页面编译为固定命名的程序集。 未选中此框允许您利用批处理编译。

*启用预编译程序集上的强命名*复选框允许您对预编译程序集进行强名称。

> [!NOTE]
> 在 ASP.NET 1.x 中，必须将强名称程序集安装到全局程序集缓存 （GAC）。 在 ASP.NET 2.0 中，您不需要在 GAC 中安装强名称程序集。

![ASP.NET应用程序预编译文件](improvements-in-visual-studio-2005/_static/image8.jpg)

**图11：ASP.NET**应用程序预编译文件

> [!NOTE]
> 在上面的应用程序中，没有 Web.config 文件。 如果有，它将在发布网站过程后称为*预编译App.config。*

## <a name="improvements-in-deployment"></a>部署的改进

与 Visual Studio 2002 和 2003 一样，Visual Studio 2005 提供了复制项目功能。 但是，该功能已在 Visual Studio 2005 中进行了增强，现在称为"复制网站"。

"复制网站"对话框将拆分为左侧框架和右框架。 左帧称为源网站，右框架称为远程网站。 有一件事可能会令一些开发人员感到困惑，那就是显示在正确框架中的站点不一定是远程站点。 它可以是本地文件系统或 IIS 本地实例上的站点。 此外，左侧框架中显示的网站不一定是源网站，因为对话框允许您从远程网站*发布到*源网站。

如果要将项目复制到远程网站，则该站点必须安装 FrontPage 服务器扩展程序。 如果没有，则需要使用 FTP 进行连接。 另一方面，如果要将项目复制到本地 IIS 实例，则不需要 FrontPage 服务器扩展。

> [!NOTE]
> 如果您尝试在本地 IIS 实例上创建新网站，并且安装了 FrontPage 2002 服务器扩展程序，则会收到一条错误消息，告诉您在 SharePoint 服务器上不支持创建网站。 在这种情况下，您可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展名。

单击此处查看复制网站功能的视频演练。

![](improvements-in-visual-studio-2005/_static/image4.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>调试的改进

Visual Studio 2005 中的调试有四个关键改进。

- 以非管理员身份在本地进行调试可以开箱即用。
- 默认情况下，编译元素的调试属性现在为 false。
- 远程调试设置和配置比以前更容易。
- 现在，您可以调试通过 FTP 位置打开的网站。

## <a name="debugging-as-a-non-administrator"></a>作为非管理员进行调试

添加ASP.NET开发服务器允许非管理员轻松调试ASP.NET应用程序开箱即用。 调试本地文件系统上运行ASP.NET应用程序时，Visual Studio 在登录用户的上下文中启动ASP.NET开发服务器。 然后，该用户可以调试该应用程序，而无需任何其他配置。

## <a name="debug-is-false-by-default"></a>默认情况下，调试为 false

在 ASP.NET 1.x 中，默认情况下，Web.config 文件*编译*元素中的*调试*属性设置为*true。* 始终建议开发人员在将应用程序部署到生产之前将此属性设置为*false，* 但由于大多数开发人员并不完全了解将调试属性设置为 true 的后果，因此他们只是将其保留原样。

将调试属性设置为 true 的最严重的问题是禁用 ASP.NETs 批处理编译模型。 因此，每个页面都编译成一个单独的 DLL。 如果 Web 应用程序由数千个页面组成（并非任何方法所闻所未闻），则这意味着该应用程序将创建数千个小型 DLL。 虽然这些 DLL 大小较小，但它们不会加载到内存中的任何特定位置。 因此，它们会导致系统内存中的碎片，并可能导致内存外异常事件。

在 ASP.NET 2.0 中，默认情况下调试属性设置为 false。 正如您已经看到的那样，当开发人员在 Visual Studio 2005 中调试ASP.NET应用程序时，系统会提示他们添加启用调试的 Web.config 文件。 这样做会产生与ASP.NET 1.x 中相同的缺点，但现在开发人员被明确警告，在将应用程序移动到生产之前，应将属性重置为 false。

## <a name="remote-debugging-setup-and-configuration"></a>远程调试设置和配置

在 Visual Studio 2002/2003 中，远程调试依赖于计算机调试管理器 （mdm.exe） 和 vs7jit.exe 过程。 因此，排除远程调试问题的故障通常是客户的一个黑匣子，对 PSS 通常没有多大帮助。

Visual Studio 2005 消除了对 mdm.exe 和 vs7jit.exe 进程的依赖。 相反，它现在使用远程调试监视器服务 （msvsmon.exe.）

Visual Studio 2005 远程调试的要求非常简单。 在调试之前，您需要在远程服务器上运行 msvsmon.exe。 可以从 Visual Studio CD 安装远程调试监视器，也可以简单地从共享运行 msvsmon.exe，而无需在 Web 服务器上安装任何内容。

运行 msvsmon.exe 时，可能会抱怨端口被阻止进行远程调试。 幸运的是，您可以在警告对话框中轻松取消阻止端口，如下所示。

![通知 Windows 防火墙阻止远程调试](improvements-in-visual-studio-2005/_static/image9.jpg)

**图 12**： 通知 Windows 防火墙阻止远程调试

取消阻止调试所需的端口后，您将看到远程调试监视器，如下所示。 通过此接口，您可以轻松监视连接并更改调试权限。

![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

**图 13**： 远程调试监视器

还可以远程调试通过 FTP 打开的 Web 应用程序。 步骤与之前介绍的步骤相同。 但是，您需要指定用于浏览本模块前面概述的 FTP 项目的基本 URL。

## <a name="lab-2"></a>实验室 2

## <a name="remote-debugging-with-visual-studio-2005"></a>使用可视化工作室 2005 进行远程调试

本实验将引导您通过 Visual Studio 2005 进行远程调试。

单击此处查看本实验的视频演练。

![](improvements-in-visual-studio-2005/_static/image5.png)

[打开全屏视频](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

本实验要求您拥有两台计算机，一台运行 Visual Studio 2005，另一台运行 IIS 5 或更高。

1. 打开 Visual Studio 2005 并在远程服务器上创建新的网站。

> [!NOTE]
> 您可以在远程 IIS 实例上或通过 FTP 创建网站。

1. 从远程 Web 服务器，使用 UNC 路径在开发计算机上找到 msvsmon.exe 并将其执行。  
 msvsmon.exe 的默认位置是 //服务器/c$/程序文件/微软视觉工作室 8/Common7/IDE/远程调试器/x86。
2. 如果提示取消阻止端口进行远程调试，则执行此操作。
3. 从开发计算机打开 Default.aspx 的代码后面，并在 page/_Load 方法中设置断点。
4. 从开发计算机开始调试。

您应该按预期命中断点。

## <a name="aspnet-development-server"></a>ASP.NET Development Server

正如我们已经讨论过的，Visual Studio 2005 附带了一个名为ASP.NET开发服务器的 Web 服务器。 （ASP.NET开发服务器有时称为卡西尼。此 Web 服务器是浏览和调试文件系统上运行的 Web 应用程序的便捷方法。

ASP.NET开发服务器是受限的 Web 服务器。 它不允许远程连接，它不允许来自除启动 Web 服务器的用户以外的任何用户的任何请求。 它还不能为 ASP 页提供服务。 仅提供ASP.NET资源和 HTML 资源（包括图像、CSS 文件等）。

ASP.NET开发服务器可以通过命令行启动，通过运行位于 c：/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/*的 WebDev.WebServer.exe 文件。 以下对话框显示可用的参数。

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**图 14**

> [!NOTE]
> 通过命令行显式启动时，不支持ASP.NET开发服务器。

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
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="c0bb5-103">Visual Studio 2005 中的改进</span><span class="sxs-lookup"><span data-stu-id="c0bb5-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="c0bb5-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c0bb5-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c0bb5-105">Visual Studio 2005 为 Web 应用程序开发人员提供了 Web 项目改进和增强的一长串。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="c0bb5-106">Visual Studio 2005 为 Web 应用程序开发人员提供了 Web 项目改进和增强的一长串。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="c0bb5-107">与 Visual Studio .NET 2002 和 2003 一样强大，但处理 Web 项目的方式也有很多投诉。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="c0bb5-108">Visual Studio 2005 增加了大量新功能，以解决这些投诉。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="c0bb5-109">对于那些喜欢 Visual Studio .NET 2003 处理 Web 应用程序编译的方式的用户，请参阅[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="c0bb5-110">在本模块中，很好地涵盖了 Web 项目创建、管理和开发方面的改进。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="c0bb5-111">在后面的模块中，很好地涵盖了构建 Web 项目并部署它们的改进。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="c0bb5-112">首页服务器扩展</span><span class="sxs-lookup"><span data-stu-id="c0bb5-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="c0bb5-113">Visual Studio .NET 2002 和 2003 需要框上的 FrontPage 服务器扩展，以便创建或生成 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="c0bb5-114">开发人员在两种不同的访问模式（FrontPage 服务器扩展名或文件访问模式）之间进行选择，这两种模式都使用 FrontPage 服务器扩展程序执行诸如在 IIS 中设置应用程序根等任务。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="c0bb5-115">Visual Studio 2005 消除了对本地项目 FrontPage 服务器扩展的依赖。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="c0bb5-116">Visual Studio 2005 现在直接访问 IIS 元库，而不是使用 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="c0bb5-117">Visual Studio 2005 还添加了对 FTP 的支持，该支持允许远程项目访问，而无需 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="c0bb5-118">对于那些想要在其项目中使用 FrontPage 服务器扩展的开发人员，该选项仍然可用。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="c0bb5-119">但是，根据ASP.NET开发人员社区的强烈反馈，这不是一项要求。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-120">远程项目创建、打开等仍然需要 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="c0bb5-121">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="c0bb5-121">ASP.NET Development Server</span></span>

<span data-ttu-id="c0bb5-122">Visual Studio 2005 附带了一个名为ASP.NET开发服务器的新 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="c0bb5-123">（此 Web 服务器以前称为卡西尼。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="c0bb5-124">ASP.NET开发服务器有几个好处。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="c0bb5-125">现在，非管理员可以针对 Web 服务器开发和调试。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="c0bb5-126">ASP.NET开发服务器动态地将虚拟目录映射到文件系统中的任何位置，从而允许灵活的项目位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="c0bb5-127">Windows XP 专业版上已经使用 IIS 的用户现在将能够创建新的 Web 应用程序，这些应用程序不会影响其在 IIS 中的默认网站的文件或文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="c0bb5-128">无需特殊配置即可利用ASP.NET开发服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="c0bb5-129">当文件系统上托管的 Web 项目被调试或浏览时，Visual Studio 2005 将自动启动随机端口上的ASP.NET开发服务器的实例来为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="c0bb5-130">本模块稍后将介绍ASP.NET开发服务器的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="c0bb5-131">改进的文件管理</span><span class="sxs-lookup"><span data-stu-id="c0bb5-131">Improved File Management</span></span>

<span data-ttu-id="c0bb5-132">在 Visual Studio 2002 和 2003 中，一个项目文件（VB.NET.vbproj 和 .csproj 表示 C#）存储了 Web 应用程序中所有文件的信息。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="c0bb5-133">解决方案资源管理器显示基于项目文件中的文件信息。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="c0bb5-134">因此，在使用外部编辑器的情况下，解决方案资源管理器通常会显示不准确的信息。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="c0bb5-135">Visual Studio 2002 和 2003 通常会覆盖文件更改或不显示最新版本的文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="c0bb5-136">Visual Studio 2005 不需要使用项目文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="c0bb5-137">相反，它直接从磁盘读取文件和文件夹信息，从而准确显示项目中的文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="c0bb5-138">由于 Visual Studio 2002 和 2003 中的"引用"文件夹不表示 Web 应用程序中的实际文件夹，因此 Visual Studio 2005 还会从解决方案资源管理器中删除"引用"文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="c0bb5-139">要访问 Visual Studio 2005 中的项目的引用，应使用项目的属性页。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="c0bb5-140">创建 Web 项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-140">Creating Web Projects</span></span>

<span data-ttu-id="c0bb5-141">Web 开发人员在 Visual Studio 2005 中有许多可用于项目创建的新选项。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="c0bb5-142">网站现在可以在文件系统的任意位置创建，然后可以使用新的ASP.NET开发服务器进行调试或浏览。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="c0bb5-143">开发人员还可以使用 FTP 创建新的网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="c0bb5-144">单击此处查看 Visual Studio 2005 中创建 Web 项目的视频演练。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="c0bb5-145">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="c0bb5-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="c0bb5-146">文件系统项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-146">File System Projects</span></span>

<span data-ttu-id="c0bb5-147">正如您在视频演练中所看到的，您可以选择通过文件共享在文件系统上或在远程位置创建网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="c0bb5-148">使用ASP.NET开发服务器浏览和调试在文件系统上创建的网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-149">ASP.NET开发服务器可能会给客户带来一些混乱。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="c0bb5-150">如果在 IS 目录结构（即 c：/inetpub/wwwroot）的文件系统上创建了 Web 项目，则从 Visual Studio 2005 内部启动时，该网站仍将通过ASP.NET开发服务器进行浏览。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="c0bb5-151">因此，任何 IIS 配置（即身份验证方法）都不适用。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="c0bb5-152">默认 Web 项目还仅包括 Default.aspx 页、default.cs文件和 App/_Data 文件夹，从而删除了大量开销。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="c0bb5-153">根据需要添加 Web.config 和特殊文件夹（即应用/_code）。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="c0bb5-154">您的 Web 项目仅包括所需的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="c0bb5-155">HTTP 项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-155">HTTP Projects</span></span>

<span data-ttu-id="c0bb5-156">HTTP 项目可以是在本地 IIS 网站或远程网站上创建的项目。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="c0bb5-157">默认项目位置为`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="c0bb5-158">如果单击"浏览"按钮，则有两个 HTTP 选项：本地 IIS 和远程站点。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="c0bb5-159">这两个选项的主要区别是在"选择位置"对话框中显示网站信息的方法以及文件复制到 Web 服务器的方式。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="c0bb5-160">"本地 IIS"选项从本地计算机上的元库中读取站点信息，并使用文件系统复制文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="c0bb5-161">远程站点选项使用 FrontPage 服务器扩展名，站点信息和文件使用 HTTP 和 FrontPage 服务器扩展程序 RPC 调用进行复制。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-162">vs_/_tmp.htm 文件和 get/_aspx/_ver.aspx 不再用于确定版本信息。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="c0bb5-163">默认 HTTP 选项为本地 IIS。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="c0bb5-164">此选项读取 IIS 元库以确定哪些站点可用以及创建内容的位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="c0bb5-165">您可以通过在树视图中选择其他文件夹或虚拟目录来选择它。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="c0bb5-166">您还可以创建新的虚拟目录、将文件夹标记为应用程序，以及从此对话框中删除现有的虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![选择位置对话框](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="c0bb5-168">**图 1**： 选择位置对话框</span><span class="sxs-lookup"><span data-stu-id="c0bb5-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="c0bb5-169">与早期版本的 Visual Studio 不同，如果选中 **"使用安全套接字层"** 复选框，并且 SSL 证书与您正在浏览的 URL 不匹配，则将显示一个安全警报对话框，询问您是否要继续。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="c0bb5-170">使用 Visual Studio .NET 2003，如果证书不是匹配的，则创建项目将失败。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![有关 SSL 证书的安全警报](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="c0bb5-172">**图 2**： 有关 SSL 证书的安全警报</span><span class="sxs-lookup"><span data-stu-id="c0bb5-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="c0bb5-173">主机标题上的注释</span><span class="sxs-lookup"><span data-stu-id="c0bb5-173">Note on Host Headers</span></span>

<span data-ttu-id="c0bb5-174">如果要在绑定到特定 IP 的站点上创建 Web 应用程序，则需要确保配置主机标头。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="c0bb5-175">否则，Visual Studio 将在 中`http://localhost`创建站点，但当从 IDE 内部浏览或调试站点时，IP 地址将无法正确解析。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="c0bb5-176">如果选择"远程站点"选项，则对话框将更改以允许您输入新网站的目标 URL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="c0bb5-177">此 URL 必须位于已启用了 FrontPage 服务器扩展名的服务器上。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="c0bb5-178">如果要使用 FrontPage 服务器扩展程序使用本地 Web 服务器，可以使用"远程站点"选项并指定本地 URL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="c0bb5-180">**图 3**： 在远程服务器上创建网站</span><span class="sxs-lookup"><span data-stu-id="c0bb5-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="c0bb5-181">通过 SSL 在远程站点上创建应用程序时，如果 SSL 证书不匹配，则确认对话框与使用本地 IIS 选项时显示的对话框略有不同。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="c0bb5-183">**图 4**： 远程站点安全警报</span><span class="sxs-lookup"><span data-stu-id="c0bb5-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="c0bb5-184">FTP</span><span class="sxs-lookup"><span data-stu-id="c0bb5-184">FTP</span></span>

<span data-ttu-id="c0bb5-185">Visual Studio 2005 引入了通过 FTP 创建网站的选项。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="c0bb5-186">使用此选项时，IDE 会在用户临时文件夹中在本地创建文件，然后使用 FTP 将文件移动到 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-187">临时文件夹位置为 c：/文档和设置/&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/=&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="c0bb5-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="c0bb5-188">使用 FTP 选项时，将显示"选择位置"对话框。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="c0bb5-189">在此对话框中输入所需的 FTP 连接信息，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP 的"选择位置"对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="c0bb5-191">**图 5**： FTP 的"选择位置对话框"</span><span class="sxs-lookup"><span data-stu-id="c0bb5-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="c0bb5-192">实验室：设置 FTP 站点并创建项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="c0bb5-193">以下步骤配置 FTP 站点，以便用户具有只有他们才能通过 FTP 上载到的位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="c0bb5-194">安装 FTP 服务</span><span class="sxs-lookup"><span data-stu-id="c0bb5-194">Install the FTP Service</span></span>

1. <span data-ttu-id="c0bb5-195">打开"添加删除程序"，选择"添加/删除 Windows 组件"</span><span class="sxs-lookup"><span data-stu-id="c0bb5-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="c0bb5-196">选择互联网信息服务（Windows 2003 上的应用程序服务器），然后单击 **"详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="c0bb5-197">检查**文件传输协议 （FTP） 服务**，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="c0bb5-198">单击 **"下一步**"以安装 FTP 服务。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="c0bb5-199">为内容创建新文件夹</span><span class="sxs-lookup"><span data-stu-id="c0bb5-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="c0bb5-200">在 Windows 资源管理器中，在 c：/inetpub/wwwroot 内部创建名为**User1**的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="c0bb5-201">配置文件夹和文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="c0bb5-202">从管理工具打开互联网信息服务快照。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="c0bb5-203">现在，您的计算机名称节点下将有一个 FTP Sites 文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="c0bb5-204">扩展**FTP 网站**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="c0bb5-205">右键单击**默认 FTP 站点**，选择 **"新建**"，然后单击 **"\*\*\*\*下一步**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="c0bb5-206">输入虚拟目录名称**的用户 1，** 然后单击 **"下一步**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="c0bb5-207">输入**路径的 c：/inetpub/wwwroot/User1，** 然后单击 **"下一步**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="c0bb5-208">单击 **"下一步\*\*\*\*"，然后单击"完成"** 以完成向导。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="c0bb5-209">右键单击默认 FTP 站点下的**User1**虚拟目录，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="c0bb5-210">选中 **"写入"** 复选框，然后单击"**确定"** 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="c0bb5-211">右键单击**默认 FTP 站点**并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="c0bb5-212">在"**安全帐户"** 选项卡上，取消选中 **"允许匿名连接**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="c0bb5-213">在对话框中单击 **"是**"，询问是否要继续。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="c0bb5-214">单击 **“确定”**，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="c0bb5-215">在 **"网站"** 节点下展开**默认网站**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="c0bb5-216">右键单击**User1**目录并选择 **"属性"**</span><span class="sxs-lookup"><span data-stu-id="c0bb5-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="c0bb5-217">在"**应用程序设置"** 部分中，单击"**创建**"将文件夹标记为应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="c0bb5-218">单击 **“确定”**，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="c0bb5-219">关闭互联网信息服务卡入。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="c0bb5-220">创建 Web 项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-220">Create web project</span></span>

1. <span data-ttu-id="c0bb5-221">打开 Visual Studio 2005。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="c0bb5-222">在 **"文件"** 菜单中，选择 **"新建网站**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="c0bb5-223">在 **"位置**"下拉下列表中，选择**FTP**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="c0bb5-224">单击“浏览”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-224">Click **Browse**.</span></span>
5. <span data-ttu-id="c0bb5-225">在 **"服务器**"文本框中输入**本地主机**。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="c0bb5-226">在"目录"文本框中输入**用户 1。**</span><span class="sxs-lookup"><span data-stu-id="c0bb5-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="c0bb5-227">单击“打开”。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-227">Click **Open**.</span></span> <span data-ttu-id="c0bb5-228">FTP 位置将输入到"新建网站"对话框中。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="c0bb5-229">单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-229">Click **OK**.</span></span>
9. <span data-ttu-id="c0bb5-230">取消在 FTP 登录对话框中**打开匿名登录**，输入凭据，然后单击"**确定**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="c0bb5-231">项目的 URL 是什么？</span><span class="sxs-lookup"><span data-stu-id="c0bb5-231">What is the URL for the project?</span></span> <span data-ttu-id="c0bb5-232">（项目的 URL 将显示在解决方案资源管理器中。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="c0bb5-233">在 **"生成"** 菜单中，选择 **"生成网站**"或 **"生成解决方案**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="c0bb5-234">右键单击解决方案资源管理器中的 Default.aspx，然后选择 **"浏览器中的视图**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="c0bb5-235">在"网站网址必需"对话框中，`http://localhost/user1`输入 URL 并单击"**确定**"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-236">如果收到指示无法加载类型 /_Default 的错误，请确保在 Web 站点上运行ASP.NET 2.0，而不是早期版本。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="c0bb5-237">您可以在"互联网信息服务"中的ASP.NET选项卡上执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="c0bb5-238">打开 Web 项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-238">Opening Web Projects</span></span>

<span data-ttu-id="c0bb5-239">打开 Web 项目类似于创建项目。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="c0bb5-240">以下各节会标注在 IDE 中工作时注意的区域。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="c0bb5-241">它还涵盖使用 HTTP 和 FTP 处理 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="c0bb5-242">要打开 Web 项目，请从"文件"菜单中选择"打开网站"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="c0bb5-243">系统、本地 IIS、FTP 和远程站点，系统将提示您使用以前介绍的相同"选择位置"对话框，并且有相同的四个选项可供您使用。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="c0bb5-244">文件系统</span><span class="sxs-lookup"><span data-stu-id="c0bb5-244">File System</span></span>

<span data-ttu-id="c0bb5-245">如本模块前面所述，Visual Studio 不再使用项目文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="c0bb5-246">因此，如果您选择从文件系统打开网站，则实际上可以选择任何希望选择的文件夹，即使您选择的文件夹最初未在 Visual Studio 中作为 Web 项目创建。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="c0bb5-247">例如，您可以选择以网站身份打开"我的文档"文件夹，Visual Studio 将愉快地打开该文件夹并显示您的文件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![我的文档作为网站打开](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="c0bb5-249">**图 6**：*我的文档*作为网站打开</span><span class="sxs-lookup"><span data-stu-id="c0bb5-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="c0bb5-250">由于 Visual Studio 仅在必要时创建其他文件和文件夹，因此不会将其他文件或文件夹添加到您打开的位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="c0bb5-251">此体系结构的副作用是，它可以防止您在文件系统上嵌套网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="c0bb5-252">例如，请考虑以下目录结构。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="c0bb5-253">C：/我的Web网站网络项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="c0bb5-254">C：/MyWebSite/嵌套的另一个 Web 项目</span><span class="sxs-lookup"><span data-stu-id="c0bb5-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="c0bb5-255">当您在 c：/MyWebSite 打开网站时，"嵌套"文件夹将显示为该应用程序的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="c0bb5-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="c0bb5-256">HTTP</span></span>

<span data-ttu-id="c0bb5-257">通过 HTTP 打开网站时，可以从 IIS 元库（本地 IIS）或使用 FrontPage 服务器扩展（远程站点）读取设置。如果有嵌套 Web 应用程序，则这些应用程序将显示，并带有一个图标，用于标识它们为应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="c0bb5-258">如果您熟悉在 FrontPage 中处理 Web 应用程序，则 Visual Studio 2005 中的行为类似。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="c0bb5-259">即使 Visual Studio 将显示嵌套在 IDE 中当前打开的应用程序下方的应用程序的图标，但它也不允许扩展它们以查看其内容。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="c0bb5-260">但是，您可以双击它们以打开它们。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="c0bb5-261">执行此操作时，将显示一个对话框，提示您打开 Web 应用程序（并替换当前打开的解决方案）或将 Web 应用程序添加到当前解决方案。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![双击嵌套应用程序图标将显示此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="c0bb5-263">**图 7**： 双击嵌套应用程序图标将为您提供此对话框</span><span class="sxs-lookup"><span data-stu-id="c0bb5-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="c0bb5-264">FTP 站点</span><span class="sxs-lookup"><span data-stu-id="c0bb5-264">FTP Site</span></span>

<span data-ttu-id="c0bb5-265">当您通过 FTP 打开网站时，这些文件都将在本地复制到临时文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="c0bb5-266">本地存储位置的完整路径显示在项目的"属性"窗格中，并使用以下格式创建。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="c0bb5-267">C：/文档和设置/&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/=&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="c0bb5-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="c0bb5-268">使用 FTP 时，Visual Studio 需要指定项目的基本 URL，以便可以浏览它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="c0bb5-269">如果不指定基本 URL，Visual Studio 将在您首次尝试浏览网站中的页面时询问它。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![为 FTP 站点指定基本 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="c0bb5-271">**图 8**： 为 FTP 站点指定基本 URL</span><span class="sxs-lookup"><span data-stu-id="c0bb5-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="c0bb5-272">编译的改进</span><span class="sxs-lookup"><span data-stu-id="c0bb5-272">Improvements in Compilation</span></span>

<span data-ttu-id="c0bb5-273">在 Visual Studio 2005 中处理 Web 应用程序的速度明显快于以前的版本。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="c0bb5-274">这在很大程度上是由于编译体系结构的更改。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="c0bb5-275">在 Visual Studio 2002 和 2003 中，Web 应用程序被编译为驻留在 /bin 文件夹中的一个主程序集。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="c0bb5-276">在 Visual Studio 2005 中，添加了一个应用/_Code文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="c0bb5-277">类和其他非 UI 代码将添加到应用/_Code文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="c0bb5-278">当 Visual Studio 生成项目时，App/_Code 文件夹中的所有文件都将编译为单个 App/_Code.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="c0bb5-279">此更改的结果是后续生成比早期版本快得多。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-280">MSBuild 命令行实用程序还可用于构建ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="c0bb5-281">该工具将在第 9 单元中介绍。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="c0bb5-282">另一个编译增强功能是"生成"菜单上的新"生成页"选项。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="c0bb5-283">此功能允许开发人员仅重建当前页面（当然，以及依赖项），以便可以更快地编译更改。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="c0bb5-284">由于 C# 不提供用于更新 IntelliSense 等的背景编译，因此它们将从此功能中获益匪浅，因为它将允许通过仅重建单个页面快速更新 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="c0bb5-285">项目的生成属性允许您配置在执行启动页之前发生的生成类型。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="c0bb5-286">开发人员可以选择仅生成当前页面，以便 Visual Studio 可以在代码更改后更快地开始调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![生成页启动操作](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="c0bb5-288">**图 9**： 生成页开始操作</span><span class="sxs-lookup"><span data-stu-id="c0bb5-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="c0bb5-289">Visual Studio 和 ASP.NET架构的另一大增强是在编辑和继续方面。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="c0bb5-290">在 Visual Studio 2005 中，开发人员可以开始调试项目，并在项目上进行代码更改，而无需分离调试器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="c0bb5-291">事实上，您可以从字面上开始调试项目、添加新类、向该类添加代码、向创建该类的新实例的页面添加代码以及执行类的方法，所有这些都不分离调试器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="c0bb5-292">执行新代码实际上和刷新浏览器一样简单！</span><span class="sxs-lookup"><span data-stu-id="c0bb5-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="c0bb5-293">单击此处查看 Visual Studio 2005 中编辑视频演练并继续功能。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="c0bb5-294">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="c0bb5-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="c0bb5-295">ASP.NET 2.0 和 Visual Studio 2005 中强大的编辑和继续功能是由于ASP.NET应用程序的体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="c0bb5-296">在 ASP.NET 1.x 中，在 Visual Studio 2002/2003 中创建的应用程序编译为存储在 /bin 文件夹中的主程序集。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="c0bb5-297">应用程序的所有类、页面等都编译到该 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="c0bb5-298">然后在运行时，ASP.NET将编译页面中的所有控件、标记和ASP.NET代码，并将这些 DLL 复制到ASP.NET临时文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="c0bb5-299">在使用 ASP.NET 2.0 的 Visual Studio 2005 中，上述两个编译模型（一个用于 Visual Studio，一个用于运行时ASP.NET）已合并为一个通用编译模型。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="c0bb5-300">这意味着所有编译问题现在都在开发阶段而不是运行时捕获。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="c0bb5-301">它还允许设计器和 IntelliSense 支持用户控件和母版页等功能。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="c0bb5-302">单击此处查看设计器对用户控件的支持的视频演练。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="c0bb5-303">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="c0bb5-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="c0bb5-304">从页面中删除用户控件时，@Register该指令将保留在标记中，并且应手动删除，以避免在从网站中删除用户控件时解析器错误。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="c0bb5-305">可视化工作室编译模型的另一个改进是发布网站功能。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="c0bb5-306">由于"发布"功能预先编译了网站，因此开发人员可以享受无需按需编译任何内容的额外性能。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="c0bb5-307">它还将 App/_Code 文件夹中的所有源代码预编译为 DLL，以便无需部署源代码。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![发布网站对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="c0bb5-309">**图 10**： 发布网站对话框</span><span class="sxs-lookup"><span data-stu-id="c0bb5-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-310">aspnet/_compile.exe 实用程序也可用于预编译ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="c0bb5-311">该工具将在第 9 单元中介绍。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="c0bb5-312">发布网站时，预编译文件将存储在临时ASP.NET文件文件夹中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="c0bb5-313">具有 *.ssd*文件扩展名的文件是定义特定 DLL 依赖项的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="c0bb5-314">任何 Web 窗体或用户控件都编译为以*应用 _/Web/_* 开头的随机 DLL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="c0bb5-315">如果选中"*允许此预编译网站可升级"* 复选框，则 Web 窗体和用户控件内的标记将不会预先编译为 DLL，从而允许您在部署后进行更改。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="c0bb5-316">如果您希望锁定标记以不允许更改已部署的内容，请取消选中此框。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="c0bb5-317">*使用固定命名和单页程序集*复选框允许您禁用批处理编译，以便将每个页面编译为固定命名的程序集。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="c0bb5-318">未选中此框允许您利用批处理编译。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="c0bb5-319">*启用预编译程序集上的强命名*复选框允许您对预编译程序集进行强名称。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-320">在 ASP.NET 1.x 中，必须将强名称程序集安装到全局程序集缓存 （GAC）。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="c0bb5-321">在 ASP.NET 2.0 中，您不需要在 GAC 中安装强名称程序集。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET应用程序预编译文件](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="c0bb5-323">**图11：ASP.NET**应用程序预编译文件</span><span class="sxs-lookup"><span data-stu-id="c0bb5-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-324">在上面的应用程序中，没有 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="c0bb5-325">如果有，它将在发布网站过程后称为*预编译App.config。*</span><span class="sxs-lookup"><span data-stu-id="c0bb5-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="c0bb5-326">部署的改进</span><span class="sxs-lookup"><span data-stu-id="c0bb5-326">Improvements in Deployment</span></span>

<span data-ttu-id="c0bb5-327">与 Visual Studio 2002 和 2003 一样，Visual Studio 2005 提供了复制项目功能。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="c0bb5-328">但是，该功能已在 Visual Studio 2005 中进行了增强，现在称为"复制网站"。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="c0bb5-329">"复制网站"对话框将拆分为左侧框架和右框架。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="c0bb5-330">左帧称为源网站，右框架称为远程网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="c0bb5-331">有一件事可能会令一些开发人员感到困惑，那就是显示在正确框架中的站点不一定是远程站点。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="c0bb5-332">它可以是本地文件系统或 IIS 本地实例上的站点。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="c0bb5-333">此外，左侧框架中显示的网站不一定是源网站，因为对话框允许您从远程网站*发布到*源网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="c0bb5-334">如果要将项目复制到远程网站，则该站点必须安装 FrontPage 服务器扩展程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="c0bb5-335">如果没有，则需要使用 FTP 进行连接。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="c0bb5-336">另一方面，如果要将项目复制到本地 IIS 实例，则不需要 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-337">如果您尝试在本地 IIS 实例上创建新网站，并且安装了 FrontPage 2002 服务器扩展程序，则会收到一条错误消息，告诉您在 SharePoint 服务器上不支持创建网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="c0bb5-338">在这种情况下，您可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展名。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="c0bb5-339">单击此处查看复制网站功能的视频演练。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="c0bb5-340">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="c0bb5-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="c0bb5-341">调试的改进</span><span class="sxs-lookup"><span data-stu-id="c0bb5-341">Improvements in Debugging</span></span>

<span data-ttu-id="c0bb5-342">Visual Studio 2005 中的调试有四个关键改进。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="c0bb5-343">以非管理员身份在本地进行调试可以开箱即用。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="c0bb5-344">默认情况下，编译元素的调试属性现在为 false。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="c0bb5-345">远程调试设置和配置比以前更容易。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="c0bb5-346">现在，您可以调试通过 FTP 位置打开的网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="c0bb5-347">作为非管理员进行调试</span><span class="sxs-lookup"><span data-stu-id="c0bb5-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="c0bb5-348">添加ASP.NET开发服务器允许非管理员轻松调试ASP.NET应用程序开箱即用。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="c0bb5-349">调试本地文件系统上运行ASP.NET应用程序时，Visual Studio 在登录用户的上下文中启动ASP.NET开发服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="c0bb5-350">然后，该用户可以调试该应用程序，而无需任何其他配置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="c0bb5-351">默认情况下，调试为 false</span><span class="sxs-lookup"><span data-stu-id="c0bb5-351">Debug is False by Default</span></span>

<span data-ttu-id="c0bb5-352">在 ASP.NET 1.x 中，默认情况下，Web.config 文件*编译*元素中的*调试*属性设置为*true。*</span><span class="sxs-lookup"><span data-stu-id="c0bb5-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="c0bb5-353">始终建议开发人员在将应用程序部署到生产之前将此属性设置为*false，* 但由于大多数开发人员并不完全了解将调试属性设置为 true 的后果，因此他们只是将其保留原样。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="c0bb5-354">将调试属性设置为 true 的最严重的问题是禁用 ASP.NETs 批处理编译模型。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="c0bb5-355">因此，每个页面都编译成一个单独的 DLL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="c0bb5-356">如果 Web 应用程序由数千个页面组成（并非任何方法所闻所未闻），则这意味着该应用程序将创建数千个小型 DLL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="c0bb5-357">虽然这些 DLL 大小较小，但它们不会加载到内存中的任何特定位置。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="c0bb5-358">因此，它们会导致系统内存中的碎片，并可能导致内存外异常事件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="c0bb5-359">在 ASP.NET 2.0 中，默认情况下调试属性设置为 false。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="c0bb5-360">正如您已经看到的那样，当开发人员在 Visual Studio 2005 中调试ASP.NET应用程序时，系统会提示他们添加启用调试的 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="c0bb5-361">这样做会产生与ASP.NET 1.x 中相同的缺点，但现在开发人员被明确警告，在将应用程序移动到生产之前，应将属性重置为 false。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="c0bb5-362">远程调试设置和配置</span><span class="sxs-lookup"><span data-stu-id="c0bb5-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="c0bb5-363">在 Visual Studio 2002/2003 中，远程调试依赖于计算机调试管理器 （mdm.exe） 和 vs7jit.exe 过程。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="c0bb5-364">因此，排除远程调试问题的故障通常是客户的一个黑匣子，对 PSS 通常没有多大帮助。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="c0bb5-365">Visual Studio 2005 消除了对 mdm.exe 和 vs7jit.exe 进程的依赖。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="c0bb5-366">相反，它现在使用远程调试监视器服务 （msvsmon.exe.）</span><span class="sxs-lookup"><span data-stu-id="c0bb5-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="c0bb5-367">Visual Studio 2005 远程调试的要求非常简单。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="c0bb5-368">在调试之前，您需要在远程服务器上运行 msvsmon.exe。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="c0bb5-369">可以从 Visual Studio CD 安装远程调试监视器，也可以简单地从共享运行 msvsmon.exe，而无需在 Web 服务器上安装任何内容。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="c0bb5-370">运行 msvsmon.exe 时，可能会抱怨端口被阻止进行远程调试。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="c0bb5-371">幸运的是，您可以在警告对话框中轻松取消阻止端口，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![通知 Windows 防火墙阻止远程调试](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="c0bb5-373">**图 12**： 通知 Windows 防火墙阻止远程调试</span><span class="sxs-lookup"><span data-stu-id="c0bb5-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="c0bb5-374">取消阻止调试所需的端口后，您将看到远程调试监视器，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="c0bb5-375">通过此接口，您可以轻松监视连接并更改调试权限。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="c0bb5-377">**图 13**： 远程调试监视器</span><span class="sxs-lookup"><span data-stu-id="c0bb5-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="c0bb5-378">还可以远程调试通过 FTP 打开的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="c0bb5-379">步骤与之前介绍的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="c0bb5-380">但是，您需要指定用于浏览本模块前面概述的 FTP 项目的基本 URL。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="c0bb5-381">实验室 2</span><span class="sxs-lookup"><span data-stu-id="c0bb5-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="c0bb5-382">使用可视化工作室 2005 进行远程调试</span><span class="sxs-lookup"><span data-stu-id="c0bb5-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="c0bb5-383">本实验将引导您通过 Visual Studio 2005 进行远程调试。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="c0bb5-384">单击此处查看本实验的视频演练。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="c0bb5-385">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="c0bb5-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="c0bb5-386">本实验要求您拥有两台计算机，一台运行 Visual Studio 2005，另一台运行 IIS 5 或更高。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="c0bb5-387">打开 Visual Studio 2005 并在远程服务器上创建新的网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-388">您可以在远程 IIS 实例上或通过 FTP 创建网站。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="c0bb5-389">从远程 Web 服务器，使用 UNC 路径在开发计算机上找到 msvsmon.exe 并将其执行。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="c0bb5-390">msvsmon.exe 的默认位置是 //服务器/c$/程序文件/微软视觉工作室 8/Common7/IDE/远程调试器/x86。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="c0bb5-391">如果提示取消阻止端口进行远程调试，则执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="c0bb5-392">从开发计算机打开 Default.aspx 的代码后面，并在 page/_Load 方法中设置断点。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="c0bb5-393">从开发计算机开始调试。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="c0bb5-394">您应该按预期命中断点。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="c0bb5-395">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="c0bb5-395">ASP.NET Development Server</span></span>

<span data-ttu-id="c0bb5-396">正如我们已经讨论过的，Visual Studio 2005 附带了一个名为ASP.NET开发服务器的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="c0bb5-397">（ASP.NET开发服务器有时称为卡西尼。此 Web 服务器是浏览和调试文件系统上运行的 Web 应用程序的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="c0bb5-398">ASP.NET开发服务器是受限的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="c0bb5-399">它不允许远程连接，它不允许来自除启动 Web 服务器的用户以外的任何用户的任何请求。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="c0bb5-400">它还不能为 ASP 页提供服务。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="c0bb5-401">仅提供ASP.NET资源和 HTML 资源（包括图像、CSS 文件等）。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="c0bb5-402">ASP.NET开发服务器可以通过命令行启动，通过运行位于 c：/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*的 WebDev.WebServer.exe 文件。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="c0bb5-403">以下对话框显示可用的参数。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="c0bb5-404">**图 14**</span><span class="sxs-lookup"><span data-stu-id="c0bb5-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="c0bb5-405">通过命令行显式启动时，不支持ASP.NET开发服务器。</span><span class="sxs-lookup"><span data-stu-id="c0bb5-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>

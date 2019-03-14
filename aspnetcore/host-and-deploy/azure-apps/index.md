---
title: 将 ASP.NET Core 应用部署到 Azure 应用服务
author: guardrex
description: 本文包含 Azure 主机和部署资源的链接。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: host-and-deploy/azure-apps/index
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a><span data-ttu-id="242d4-103">将 ASP.NET Core 应用部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="242d4-103">Deploy ASP.NET Core apps to Azure App Service</span></span>

<span data-ttu-id="242d4-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="242d4-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="242d4-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="242d4-105">Useful resources</span></span>

<span data-ttu-id="242d4-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="242d4-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="242d4-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="242d4-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="242d4-108">在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="242d4-108">Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="242d4-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="242d4-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="242d4-110">在 Linux 上的应用服务中创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="242d4-110">Create an ASP.NET Core app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="242d4-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="242d4-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="242d4-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="242d4-112">The following articles are available in ASP.NET Core documentation:</span></span>

<xref:tutorials/publish-to-azure-webapp-using-vs>  
<span data-ttu-id="242d4-113">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="242d4-113">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

<xref:host-and-deploy/azure-apps/azure-continuous-deployment>  
<span data-ttu-id="242d4-114">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="242d4-114">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="242d4-115">使用 Azure Pipelines 创建你的第一个管道</span><span class="sxs-lookup"><span data-stu-id="242d4-115">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)  
<span data-ttu-id="242d4-116">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="242d4-116">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="242d4-117">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="242d4-117">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="242d4-118">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="242d4-118">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="242d4-119">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="242d4-119">Application configuration</span></span>

### <a name="platform"></a><span data-ttu-id="242d4-120">平台</span><span class="sxs-lookup"><span data-stu-id="242d4-120">Platform</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="242d4-121">64 位 (x64) 和 32 位 (x86) 应用的运行时存在于 Azure 应用服务上。</span><span class="sxs-lookup"><span data-stu-id="242d4-121">Runtimes for 64-bit (x64) and 32-bit (x86) apps are present on Azure App Service.</span></span> <span data-ttu-id="242d4-122">应用服务上提供的 [.NET Core SDK](/dotnet/core/sdk) 为 32 位，但可以使用 [Kudu](https://github.com/projectkudu/kudu/wiki) 控制台或通过[使用 Visual Studio 发布配置文件或 CLI 命令的 MSDeploy](xref:host-and-deploy/visual-studio-publish-profiles) 来部署 64 位应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-122">The [.NET Core SDK](/dotnet/core/sdk) available on App Service is 32-bit, but you can deploy 64-bit apps using the [Kudu](https://github.com/projectkudu/kudu/wiki) console or via [MSDeploy with a Visual Studio publish profile or CLI command](xref:host-and-deploy/visual-studio-publish-profiles).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="242d4-123">对于具有本机依赖项的应用，32 位 (x86) 应用的运行时存在于 Azure 应用服务上。</span><span class="sxs-lookup"><span data-stu-id="242d4-123">For apps with native dependencies, runtimes for 32-bit (x86) apps are present on Azure App Service.</span></span> <span data-ttu-id="242d4-124">应用服务上提供的 [.NET Core SDK](/dotnet/core/sdk) 为 32 位。</span><span class="sxs-lookup"><span data-stu-id="242d4-124">The [.NET Core SDK](/dotnet/core/sdk) available on App Service is 32-bit.</span></span>

::: moniker-end

### <a name="packages"></a><span data-ttu-id="242d4-125">包</span><span class="sxs-lookup"><span data-stu-id="242d4-125">Packages</span></span>

<span data-ttu-id="242d4-126">包含以下 NuGet 包，以便为部署到 Azure 应用服务的应用提供自动日志记录功能：</span><span class="sxs-lookup"><span data-stu-id="242d4-126">Include the following NuGet packages to provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="242d4-127">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="242d4-127">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="242d4-128">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="242d4-128">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="242d4-129">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="242d4-129">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="242d4-130">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="242d4-130">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="242d4-131">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中不提供前述包。</span><span class="sxs-lookup"><span data-stu-id="242d4-131">The preceding packages aren't available from the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="242d4-132">面向 .NET Framework 或引用 `Microsoft.AspNetCore.App` 元包的应用必须显式引用应用的项目文件中的各个包。</span><span class="sxs-lookup"><span data-stu-id="242d4-132">Apps that target .NET Framework or reference the `Microsoft.AspNetCore.App` metapackage must explicitly reference the individual packages in the app's project file.</span></span>

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="242d4-133">使用 Azure 门户重写应用配置</span><span class="sxs-lookup"><span data-stu-id="242d4-133">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="242d4-134">Azure 门户中的应用设置允许为应用设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="242d4-134">App settings in the Azure Portal permit you to set environment variables for the app.</span></span> <span data-ttu-id="242d4-135">可以通过[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)来使用环境变量。</span><span class="sxs-lookup"><span data-stu-id="242d4-135">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="242d4-136">在 Azure 门户中创建或修改应用设置并选择“保存”按钮时，Azure 应用将重启。</span><span class="sxs-lookup"><span data-stu-id="242d4-136">When an app setting is created or modified in the Azure Portal and the **Save** button is selected, the Azure App is restarted.</span></span> <span data-ttu-id="242d4-137">服务重启后，应用即可使用环境变量。</span><span class="sxs-lookup"><span data-stu-id="242d4-137">The environment variable is available to the app after the service restarts.</span></span>

<span data-ttu-id="242d4-138">当应用使用 [Web 主机](xref:fundamentals/host/web-host)并使用 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 构建主机时，配置主机的环境变量使用 `ASPNETCORE_` 前缀。</span><span class="sxs-lookup"><span data-stu-id="242d4-138">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="242d4-139">有关详细信息，请参阅 <xref:fundamentals/host/web-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="242d4-139">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="242d4-140">当应用使用[通用主机](xref:fundamentals/host/generic-host)时，环境变量在默认情况下不会加载到应用的配置，且配置提供程序必须由开发人员添加。</span><span class="sxs-lookup"><span data-stu-id="242d4-140">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="242d4-141">在添加配置提供程序时，开发人员将确定环境变量前缀。</span><span class="sxs-lookup"><span data-stu-id="242d4-141">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="242d4-142">有关详细信息，请参阅 <xref:fundamentals/host/generic-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="242d4-142">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="242d4-143">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="242d4-143">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="242d4-144">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="242d4-144">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="242d4-145">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="242d4-145">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="242d4-146">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="242d4-146">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="242d4-147">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="242d4-147">Monitoring and logging</span></span>

<span data-ttu-id="242d4-148">部署到应用服务的 ASP.NET Core 应用自动接收应用服务扩展“ASP.NET Core 日志记录扩展”。</span><span class="sxs-lookup"><span data-stu-id="242d4-148">ASP.NET Core apps deployed to App Service automatically receive an App Service extension, **ASP.NET Core Logging Extensions**.</span></span> <span data-ttu-id="242d4-149">此扩展启用 Azure 日志记录。</span><span class="sxs-lookup"><span data-stu-id="242d4-149">The extension enables Azure logging.</span></span>

<span data-ttu-id="242d4-150">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="242d4-150">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="242d4-151">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="242d4-151">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="242d4-152">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="242d4-152">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="242d4-153">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="242d4-153">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="242d4-154">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="242d4-154">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

<xref:fundamentals/error-handling>  
<span data-ttu-id="242d4-155">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="242d4-155">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-apps/troubleshoot>  
<span data-ttu-id="242d4-156">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="242d4-156">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-iis-errors-reference>  
<span data-ttu-id="242d4-157">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="242d4-157">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="242d4-158">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="242d4-158">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="242d4-159">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="242d4-159">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="242d4-160">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="242d4-160">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="242d4-161">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="242d4-161">Keys aren't protected at rest.</span></span> <span data-ttu-id="242d4-162">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="242d4-162">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="242d4-163">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="242d4-163">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="242d4-164">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="242d4-164">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="242d4-165">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="242d4-165">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="242d4-166">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-166">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="242d4-167">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="242d4-167">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="242d4-168">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="242d4-168">Azure Blob Storage</span></span>
* <span data-ttu-id="242d4-169">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="242d4-169">Azure Key Vault</span></span>
* <span data-ttu-id="242d4-170">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="242d4-170">SQL store</span></span>
* <span data-ttu-id="242d4-171">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="242d4-171">Redis cache</span></span>

<span data-ttu-id="242d4-172">有关详细信息，请参阅 <xref:security/data-protection/implementation/key-storage-providers>。</span><span class="sxs-lookup"><span data-stu-id="242d4-172">For more information, see <xref:security/data-protection/implementation/key-storage-providers>.</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="242d4-173">将 ASP.NET Core 预览版部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="242d4-173">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="242d4-174">请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="242d4-174">Use one of the following approaches:</span></span>

* <span data-ttu-id="242d4-175">[安装预览站点扩展](#install-the-preview-site-extension)。</span><span class="sxs-lookup"><span data-stu-id="242d4-175">[Install the preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="242d4-176">[部署自包含应用](#deploy-the-app-self-contained)。</span><span class="sxs-lookup"><span data-stu-id="242d4-176">[Deploy the app self-contained](#deploy-the-app-self-contained).</span></span>
* <span data-ttu-id="242d4-177">[对用于容器的 Web 应用使用 Docker](#use-docker-with-web-apps-for-containers)。</span><span class="sxs-lookup"><span data-stu-id="242d4-177">[Use Docker with Web Apps for containers](#use-docker-with-web-apps-for-containers).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="242d4-178">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="242d4-178">Install the preview site extension</span></span>

<span data-ttu-id="242d4-179">如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。</span><span class="sxs-lookup"><span data-stu-id="242d4-179">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

1. <span data-ttu-id="242d4-180">从 Azure 门户导航到“应用服务”。</span><span class="sxs-lookup"><span data-stu-id="242d4-180">From the Azure Portal, navigate to the App Service.</span></span>
1. <span data-ttu-id="242d4-181">选择 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-181">Select the web app.</span></span>
1. <span data-ttu-id="242d4-182">在搜索框中键入“ex”以筛选“扩展”，或向下滚动管理工具列表。</span><span class="sxs-lookup"><span data-stu-id="242d4-182">Type "ex" in the search box to filter for "Extensions" or scroll down the list of management tools.</span></span>
1. <span data-ttu-id="242d4-183">选择“扩展”。</span><span class="sxs-lookup"><span data-stu-id="242d4-183">Select **Extensions**.</span></span>
1. <span data-ttu-id="242d4-184">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="242d4-184">Select **Add**.</span></span>
1. <span data-ttu-id="242d4-185">从列表选择“ASP.NET Core {X.Y} ({x64|x86}) 运行时”扩展，其中 `{X.Y}` 是 ASP.NET Core 预览版本，并且 `{x64|x86}` 指定平台。</span><span class="sxs-lookup"><span data-stu-id="242d4-185">Select the **ASP.NET Core {X.Y} ({x64|x86}) Runtime** extension from the list, where `{X.Y}` is the ASP.NET Core preview version and `{x64|x86}` specifies the platform.</span></span>
1. <span data-ttu-id="242d4-186">选择“确定”以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="242d4-186">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="242d4-187">选择“确定”安装扩展。</span><span class="sxs-lookup"><span data-stu-id="242d4-187">Select **OK** to install the extension.</span></span>

<span data-ttu-id="242d4-188">操作完成时，即表示已安装最新的 .NET Core 预览版。</span><span class="sxs-lookup"><span data-stu-id="242d4-188">When the operation completes, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="242d4-189">验证安装：</span><span class="sxs-lookup"><span data-stu-id="242d4-189">Verify the installation:</span></span>

1. <span data-ttu-id="242d4-190">选择“高级工具”。</span><span class="sxs-lookup"><span data-stu-id="242d4-190">Select **Advanced Tools**.</span></span>
1. <span data-ttu-id="242d4-191">选择“高级工具”中的“Go”。</span><span class="sxs-lookup"><span data-stu-id="242d4-191">Select **Go** in **Advanced Tools**.</span></span>
1. <span data-ttu-id="242d4-192">选择“调试控制台” > “PowerShell”菜单项。</span><span class="sxs-lookup"><span data-stu-id="242d4-192">Select the **Debug console** > **PowerShell** menu item.</span></span>
1. <span data-ttu-id="242d4-193">从 PowerShell 命令提示符处执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="242d4-193">At the PowerShell prompt, execute the following command.</span></span> <span data-ttu-id="242d4-194">在以下命令中，将 ASP.NET Core 运行时版本替换为 `{X.Y}`，并将平台替换为 `{PLATFORM}`：</span><span class="sxs-lookup"><span data-stu-id="242d4-194">Substitute the ASP.NET Core runtime version for `{X.Y}` and the platform for `{PLATFORM}` in the command:</span></span>

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.{PLATFORM}\
   ```
   <span data-ttu-id="242d4-195">如果安装 x64 预览版运行时，该命令将返回`True`。</span><span class="sxs-lookup"><span data-stu-id="242d4-195">The command returns `True` when the x64 preview runtime is installed.</span></span>

> [!NOTE]
> <span data-ttu-id="242d4-196">对于在 A 系列计算机上或更高级托管层上托管的应用，可在 Azure 门户中的应用设置中设置应用服务应用的平台体系结构 (x86/x64)。</span><span class="sxs-lookup"><span data-stu-id="242d4-196">The platform architecture (x86/x64) of an App Services app is set in the app's settings in the Azure Portal for apps that are hosted on an A-series compute or better hosting tier.</span></span> <span data-ttu-id="242d4-197">如果应用在进程内模式下运行并且平台体系结构配置为 64 位 (x64)，则 ASP.NET Core 模块会使用 64 位预览版运行时（如存在）。</span><span class="sxs-lookup"><span data-stu-id="242d4-197">If the app is run in in-process mode and the platform architecture is configured for 64-bit (x64), the ASP.NET Core Module uses the 64-bit preview runtime, if present.</span></span> <span data-ttu-id="242d4-198">安装“ASP.NET Core {X.Y} (x64) 运行时”扩展。</span><span class="sxs-lookup"><span data-stu-id="242d4-198">Install the **ASP.NET Core {X.Y} (x64) Runtime** extension.</span></span>
>
> <span data-ttu-id="242d4-199">安装 x64 预览版运行时后，在 Kudu PowerShell 命令窗口中运行以下命令以验证该安装。</span><span class="sxs-lookup"><span data-stu-id="242d4-199">After installing the x64 preview runtime, run the following command in the Kudu PowerShell command window to verify the installation.</span></span> <span data-ttu-id="242d4-200">在以下命令中，将 ASP.NET Core 运行时版本替换为 `{X.Y}` ：</span><span class="sxs-lookup"><span data-stu-id="242d4-200">Substitute the ASP.NET Core runtime version for `{X.Y}` in the command:</span></span>
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.x64\
> ```
> <span data-ttu-id="242d4-201">如果安装 x64 预览版运行时，该命令将返回`True`。</span><span class="sxs-lookup"><span data-stu-id="242d4-201">The command returns `True` when the x64 preview runtime is installed.</span></span>

> [!NOTE]
> <span data-ttu-id="242d4-202">ASP.NET Core 扩展可为 Azure 应用服务上的 ASP.NET Core 启用附加功能，例如启用 Azure 日志记录。</span><span class="sxs-lookup"><span data-stu-id="242d4-202">**ASP.NET Core Extensions** enables additional functionality for ASP.NET Core on Azure App Services, such as enabling Azure logging.</span></span> <span data-ttu-id="242d4-203">从 Visual Studio 进行部署时，将自动安装该扩展。</span><span class="sxs-lookup"><span data-stu-id="242d4-203">The extension is installed automatically when deploying from Visual Studio.</span></span> <span data-ttu-id="242d4-204">如果未安装该扩展，请为应用安装它。</span><span class="sxs-lookup"><span data-stu-id="242d4-204">If the extension isn't installed, install it for the app.</span></span>

<span data-ttu-id="242d4-205">**通过 ARM 模板使用预览站点扩展**</span><span class="sxs-lookup"><span data-stu-id="242d4-205">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="242d4-206">如果使用 ARM 模板创建和部署应用，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-206">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="242d4-207">例如：</span><span class="sxs-lookup"><span data-stu-id="242d4-207">For example:</span></span>

[!code-json[](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="242d4-208">部署自包含应用</span><span class="sxs-lookup"><span data-stu-id="242d4-208">Deploy the app self-contained</span></span>

<span data-ttu-id="242d4-209">针对预览运行时的[自包含部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd)在部署中承载预览运行时。</span><span class="sxs-lookup"><span data-stu-id="242d4-209">A [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) that targets a preview runtime carries the preview runtime in the deployment.</span></span>

<span data-ttu-id="242d4-210">部署自包含应用时：</span><span class="sxs-lookup"><span data-stu-id="242d4-210">When deploying a self-contained app:</span></span>

* <span data-ttu-id="242d4-211">Azure 应用服务中的站点不需要[预览站点扩展名](#install-the-preview-site-extension)。</span><span class="sxs-lookup"><span data-stu-id="242d4-211">The site in Azure App Service doesn't require the [preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="242d4-212">必须使用不同于发布[依赖框架部署 (FDD)](/dotnet/core/deploying#framework-dependent-deployments-fdd) 的方法发布应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-212">The app must be published following a different approach than when publishing for a [framework-dependent deployment (FDD)](/dotnet/core/deploying#framework-dependent-deployments-fdd).</span></span>

#### <a name="publish-from-visual-studio"></a><span data-ttu-id="242d4-213">使用 Visual Studio 发布</span><span class="sxs-lookup"><span data-stu-id="242d4-213">Publish from Visual Studio</span></span>

1. <span data-ttu-id="242d4-214">从 Visual Studio 工具栏中选择“构建” > “发布{应用程序名称}”。</span><span class="sxs-lookup"><span data-stu-id="242d4-214">Select **Build** > **Publish {Application Name}** from the Visual Studio toolbar.</span></span>
1. <span data-ttu-id="242d4-215">在“选择发布目标”对话框中，确认已选中“应用服务”。</span><span class="sxs-lookup"><span data-stu-id="242d4-215">In the **Pick a publish target** dialog, confirm that **App Service** is selected.</span></span>
1. <span data-ttu-id="242d4-216">选择“高级”。</span><span class="sxs-lookup"><span data-stu-id="242d4-216">Select **Advanced**.</span></span> <span data-ttu-id="242d4-217">随即会打开“发布”对话框。</span><span class="sxs-lookup"><span data-stu-id="242d4-217">The **Publish** dialog opens.</span></span>
1. <span data-ttu-id="242d4-218">在“发布”对话框中：</span><span class="sxs-lookup"><span data-stu-id="242d4-218">In the **Publish** dialog:</span></span>
   * <span data-ttu-id="242d4-219">确认已选中“发布”配置。</span><span class="sxs-lookup"><span data-stu-id="242d4-219">Confirm that the **Release** configuration is selected.</span></span>
   * <span data-ttu-id="242d4-220">打开“部署模式”下拉列表，然后选择“自包含”。</span><span class="sxs-lookup"><span data-stu-id="242d4-220">Open the **Deployment Mode** drop-down list and select **Self-Contained**.</span></span>
   * <span data-ttu-id="242d4-221">从“目标运行时”下拉列表中选择目标运行时。</span><span class="sxs-lookup"><span data-stu-id="242d4-221">Select the target runtime from the **Target Runtime** drop-down list.</span></span> <span data-ttu-id="242d4-222">默认值为 `win-x86`。</span><span class="sxs-lookup"><span data-stu-id="242d4-222">The default is `win-x86`.</span></span>
   * <span data-ttu-id="242d4-223">如果需要在部署时删除其他文件，请打开“文件发布选项”，然后选中复选框以删除目标位置的其他文件。</span><span class="sxs-lookup"><span data-stu-id="242d4-223">If you need to remove additional files upon deployment, open **File Publish Options** and select the check box to remove additional files at the destination.</span></span>
   * <span data-ttu-id="242d4-224">选择“保存”。</span><span class="sxs-lookup"><span data-stu-id="242d4-224">Select **Save**.</span></span>
1. <span data-ttu-id="242d4-225">按照发布向导的其余提示创建新站点或更新现有站点。</span><span class="sxs-lookup"><span data-stu-id="242d4-225">Create a new site or update an existing site by following the remaining prompts of the publish wizard.</span></span>

#### <a name="publish-using-command-line-interface-cli-tools"></a><span data-ttu-id="242d4-226">使用命令行接口 (CLI) 工具发布</span><span class="sxs-lookup"><span data-stu-id="242d4-226">Publish using command-line interface (CLI) tools</span></span>

1. <span data-ttu-id="242d4-227">在项目文件中，指定一个或多个[运行时标识符 (RID)](/dotnet/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="242d4-227">In the project file, specify one or more [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="242d4-228">对单个 RID 使用 `<RuntimeIdentifier>`（单数），或使用 `<RuntimeIdentifiers>`（复数）提供以分号分隔的 RID 列表。</span><span class="sxs-lookup"><span data-stu-id="242d4-228">Use `<RuntimeIdentifier>` (singular) for a single RID, or use `<RuntimeIdentifiers>` (plural) to provide a semicolon-delimited list of RIDs.</span></span> <span data-ttu-id="242d4-229">在以下示例中，指定 `win-x86` RID：</span><span class="sxs-lookup"><span data-stu-id="242d4-229">In the following example, the `win-x86` RID is specified:</span></span>

   ```xml
   <PropertyGroup>
     <TargetFramework>netcoreapp2.1</TargetFramework>
     <RuntimeIdentifier>win-x86</RuntimeIdentifier>
   </PropertyGroup>
   ```
1. <span data-ttu-id="242d4-230">在命令 shell 中，使用 [dotnet publish ](/dotnet/core/tools/dotnet-publish) 命令在主机运行时的发布配置中发布应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-230">From a command shell, publish the app in Release configuration for the host's runtime with the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="242d4-231">在以下示例中，为 `win-x86` RID 发布应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-231">In the following example, the app is published for the `win-x86` RID.</span></span> <span data-ttu-id="242d4-232">提供给 `--runtime` 选项的 RID 必须在项目文件的 `<RuntimeIdentifier>`（或 `<RuntimeIdentifiers>`）属性中提供。</span><span class="sxs-lookup"><span data-stu-id="242d4-232">The RID supplied to the `--runtime` option must be provided in the `<RuntimeIdentifier>` (or `<RuntimeIdentifiers>`) property in the project file.</span></span>

   ```console
   dotnet publish --configuration Release --runtime win-x86
   ```
1. <span data-ttu-id="242d4-233">将 bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish 目录的内容移动到应用服务中的站点。</span><span class="sxs-lookup"><span data-stu-id="242d4-233">Move the contents of the *bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* directory to the site in App Service.</span></span>

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="242d4-234">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="242d4-234">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="242d4-235">[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的预览 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="242d4-235">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="242d4-236">这些映像可以用作基础映像。</span><span class="sxs-lookup"><span data-stu-id="242d4-236">The images can be used as a base image.</span></span> <span data-ttu-id="242d4-237">按常规方法使用映像并部署到用于容器的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="242d4-237">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="protocol-settings-https"></a><span data-ttu-id="242d4-238">协议设置 (HTTPS)</span><span class="sxs-lookup"><span data-stu-id="242d4-238">Protocol settings (HTTPS)</span></span>

<span data-ttu-id="242d4-239">借助安全的协议绑定，可在通过 HTTPS 响应请求时指定要使用的证书。</span><span class="sxs-lookup"><span data-stu-id="242d4-239">Secure protocol bindings allow you specify a certificate to use when responding to requests over HTTPS.</span></span> <span data-ttu-id="242d4-240">若要绑定，需要一个为特定主机名颁发的有效专用证书 (*.pfx*)。</span><span class="sxs-lookup"><span data-stu-id="242d4-240">Binding requires a valid private certificate (*.pfx*) issued for the specific hostname.</span></span> <span data-ttu-id="242d4-241">有关详细信息，请参阅[教程：将现有自定义 SSL 证书绑定到 Azure Web 应用](/azure/app-service/app-service-web-tutorial-custom-ssl)。</span><span class="sxs-lookup"><span data-stu-id="242d4-241">For more information, see [Tutorial: Bind an existing custom SSL certificate to Azure Web Apps](/azure/app-service/app-service-web-tutorial-custom-ssl).</span></span>

## <a name="transform-webconfig"></a><span data-ttu-id="242d4-242">转换 web.config</span><span class="sxs-lookup"><span data-stu-id="242d4-242">Transform web.config</span></span>

<span data-ttu-id="242d4-243">如果需要在发布时转换 web.config（例如，基于配置、配置文件或环境设置环境变量），请参阅 <xref:host-and-deploy/iis/transform-webconfig>。</span><span class="sxs-lookup"><span data-stu-id="242d4-243">If you need to transform *web.config* on publish (for example, set environment variables based on the configuration, profile, or environment), see <xref:host-and-deploy/iis/transform-webconfig>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="242d4-244">其他资源</span><span class="sxs-lookup"><span data-stu-id="242d4-244">Additional resources</span></span>

* [<span data-ttu-id="242d4-245">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="242d4-245">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="242d4-246">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概览视频）</span><span class="sxs-lookup"><span data-stu-id="242d4-246">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="242d4-247">Azure Friday：Azure 应用服务诊断和疑难解答体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="242d4-247">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="242d4-248">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="242d4-248">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="242d4-249">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="242d4-249">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="242d4-250">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="242d4-250">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="242d4-251">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="242d4-251">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)

---
uid: webhooks/diagnostics/logging
title: ASP.NET WebHook 记录 |微软文档
author: rick-anderson
description: 如何ASP.NET WebHook 进行登录。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675345"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="96b7b-103">ASP.NET WebHooks 日志记录</span><span class="sxs-lookup"><span data-stu-id="96b7b-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="96b7b-104">微软ASP.NETWebHooks使用日志记录作为报告问题和问题的一种方式。</span><span class="sxs-lookup"><span data-stu-id="96b7b-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="96b7b-105">默认情况下，日志使用[System.诊断.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)编写，可以使用[跟踪侦听器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日志流一样进行编写日志。</span><span class="sxs-lookup"><span data-stu-id="96b7b-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="96b7b-106">将 Web 应用程序部署为 Azure Web 应用时，将自动拾取日志，并[可以与其他系统](https://msdn.microsoft.com/library/system.diagnostics.trace)一起管理。</span><span class="sxs-lookup"><span data-stu-id="96b7b-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="96b7b-107">有关详细信息，请参阅在[Azure 应用服务中为 Web 应用启用诊断日志记录](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="96b7b-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="96b7b-108">此外，可以直接从 Visual Studio 内部获取日志，如[使用 Visual Studio 在 Azure 应用服务中排除 Web 应用时](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)所述。</span><span class="sxs-lookup"><span data-stu-id="96b7b-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="96b7b-109">重定向日志</span><span class="sxs-lookup"><span data-stu-id="96b7b-109">Redirecting Logs</span></span>

<span data-ttu-id="96b7b-110">可以提供可直接登录到日志管理器（如[Log4Net](http://logging.apache.org/log4net/)和[NLog）](http://nlog-project.org/)的备用日志记录实现，而不是将日志写入[System.诊断.Trace。](https://msdn.microsoft.com/library/system.diagnostics.trace)</span><span class="sxs-lookup"><span data-stu-id="96b7b-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="96b7b-111">只需提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的实现，并将其注册到您选择的依赖项注入引擎，它将被 Microsoft ASP.NET WebHooks 拾取。</span><span class="sxs-lookup"><span data-stu-id="96b7b-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="96b7b-112">有关详细信息，请参阅[ASP.NET Web API 2 中的依赖项注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="96b7b-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>

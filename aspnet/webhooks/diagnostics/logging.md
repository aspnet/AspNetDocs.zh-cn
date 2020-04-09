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
# <a name="aspnet-webhooks-logging"></a>ASP.NET WebHooks 日志记录

微软ASP.NETWebHooks使用日志记录作为报告问题和问题的一种方式。 默认情况下，日志使用[System.诊断.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)编写，可以使用[跟踪侦听器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日志流一样进行编写日志。

将 Web 应用程序部署为 Azure Web 应用时，将自动拾取日志，并[可以与其他系统](https://msdn.microsoft.com/library/system.diagnostics.trace)一起管理。 有关详细信息，请参阅在[Azure 应用服务中为 Web 应用启用诊断日志记录](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

此外，可以直接从 Visual Studio 内部获取日志，如[使用 Visual Studio 在 Azure 应用服务中排除 Web 应用时](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)所述。

## <a name="redirecting-logs"></a>重定向日志

可以提供可直接登录到日志管理器（如[Log4Net](http://logging.apache.org/log4net/)和[NLog）](http://nlog-project.org/)的备用日志记录实现，而不是将日志写入[System.诊断.Trace。](https://msdn.microsoft.com/library/system.diagnostics.trace) 只需提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的实现，并将其注册到您选择的依赖项注入引擎，它将被 Microsoft ASP.NET WebHooks 拾取。 有关详细信息，请参阅[ASP.NET Web API 2 中的依赖项注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)。

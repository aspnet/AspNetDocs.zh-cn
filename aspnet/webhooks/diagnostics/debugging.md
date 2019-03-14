---
uid: webhooks/diagnostics/debugging
title: 调试 ASP.NET Webhook |Microsoft Docs
author: rick-anderson
description: 如何调试 ASP.NET Webhook。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062494"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="2d0b2-103">调试 ASP.NET Webhook</span><span class="sxs-lookup"><span data-stu-id="2d0b2-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="2d0b2-104">在 Azure 中进行调试</span><span class="sxs-lookup"><span data-stu-id="2d0b2-104">Debugging in Azure</span></span>

<span data-ttu-id="2d0b2-105">若要在 Azure 中运行时调试 Web 应用程序，请参阅本教程[使用 Visual Studio 的 Azure 应用服务中 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="2d0b2-106">使用源和符号进行调试</span><span class="sxs-lookup"><span data-stu-id="2d0b2-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="2d0b2-107">除了调试您自己的代码，就可以直接在 Microsoft ASP.NET Webhook 和实际进行调试的所有.NET。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="2d0b2-108">这样无论是否在本地或远程调试。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="2d0b2-109">首先，配置 Visual Studio 以找到的源和符号： 转到**调试**，然后**选项和设置**。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="2d0b2-110">设置选项如下：</span><span class="sxs-lookup"><span data-stu-id="2d0b2-110">Set the options like this:</span></span>

![选项和设置](_static/SourceSymbols.png)

<span data-ttu-id="2d0b2-112">然后添加一个链接到[symbolsource.org](http://symbolsource.org)下载的源和符号。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="2d0b2-113">转到**符号**上方的菜单选项卡，并作为符号位置添加以下：</span><span class="sxs-lookup"><span data-stu-id="2d0b2-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="2d0b2-114">此外，请确保缓存目录的短名称;否则无论文件名称这将导致要加载的符号，可能会太长。</span><span class="sxs-lookup"><span data-stu-id="2d0b2-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="2d0b2-115">示例路径为：</span><span class="sxs-lookup"><span data-stu-id="2d0b2-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="2d0b2-116">设置应类似于以下所示：</span><span class="sxs-lookup"><span data-stu-id="2d0b2-116">The settings should look similar to this:</span></span>

![选项符号文件位置示例](_static/SymSource.png)

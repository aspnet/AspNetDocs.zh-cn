---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks 调试 |微软文档
author: rick-anderson
description: 如何调试ASP.NET WebHooks。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675368"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="39313-103">ASP.NET WebHooks 调试</span><span class="sxs-lookup"><span data-stu-id="39313-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="39313-104">在 Azure 中调试</span><span class="sxs-lookup"><span data-stu-id="39313-104">Debugging in Azure</span></span>

<span data-ttu-id="39313-105">要在 Azure 中运行时调试 Web 应用程序，请参阅[使用 Visual Studio 在 Azure 应用服务中对 Web 应用进行故障排除教程](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="39313-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="39313-106">使用源和符号进行调试</span><span class="sxs-lookup"><span data-stu-id="39313-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="39313-107">除了调试自己的代码外，还可以直接调试到 Microsoft ASP.NET WebHooks，实际上还可以调试到所有 .NET。</span><span class="sxs-lookup"><span data-stu-id="39313-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="39313-108">无论您在本地调试还是远程调试，这都有效。</span><span class="sxs-lookup"><span data-stu-id="39313-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="39313-109">首先，通过去**调试**，然后选择**和设置**，配置 Visual Studio 以查找源和符号。</span><span class="sxs-lookup"><span data-stu-id="39313-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="39313-110">设置如下所示的选项：</span><span class="sxs-lookup"><span data-stu-id="39313-110">Set the options like this:</span></span>

![选项和设置](_static/SourceSymbols.png)

<span data-ttu-id="39313-112">然后添加指向[symbolsource.org](http://symbolsource.org)的链接以下载源和符号。</span><span class="sxs-lookup"><span data-stu-id="39313-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="39313-113">转到上面菜单的 **"符号"** 选项卡，并将以下内容添加为符号位置：</span><span class="sxs-lookup"><span data-stu-id="39313-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="39313-114">此外，请确保缓存目录具有短名称;否则，文件名可能会太长，这将导致符号无法加载。</span><span class="sxs-lookup"><span data-stu-id="39313-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="39313-115">示例路径是：</span><span class="sxs-lookup"><span data-stu-id="39313-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="39313-116">设置应如下所示：</span><span class="sxs-lookup"><span data-stu-id="39313-116">The settings should look similar to this:</span></span>

![选项符号文件位置示例](_static/SymSource.png)

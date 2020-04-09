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
# <a name="aspnet-webhooks-debugging"></a>ASP.NET WebHooks 调试

## <a name="debugging-in-azure"></a>在 Azure 中调试

要在 Azure 中运行时调试 Web 应用程序，请参阅[使用 Visual Studio 在 Azure 应用服务中对 Web 应用进行故障排除教程](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="debugging-with-source-and-symbols"></a>使用源和符号进行调试

除了调试自己的代码外，还可以直接调试到 Microsoft ASP.NET WebHooks，实际上还可以调试到所有 .NET。 无论您在本地调试还是远程调试，这都有效。 首先，通过去**调试**，然后选择**和设置**，配置 Visual Studio 以查找源和符号。 设置如下所示的选项：

![选项和设置](_static/SourceSymbols.png)

然后添加指向[symbolsource.org](http://symbolsource.org)的链接以下载源和符号。 转到上面菜单的 **"符号"** 选项卡，并将以下内容添加为符号位置：

```
http://srv.symbolsource.org/pdb/Public
```

此外，请确保缓存目录具有短名称;否则，文件名可能会太长，这将导致符号无法加载。 示例路径是：

```
C:\SymCache
```

设置应如下所示：

![选项符号文件位置示例](_static/SymSource.png)

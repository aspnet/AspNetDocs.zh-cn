---
ms.openlocfilehash: e5565381f44480e2531925717ee7815da92d1ff5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030034"
---
# <a name="update-the-generated-pages"></a>更新生成的页面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

我们的电影应用有个不错的开始，但是展示效果还不够理想。 我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为“Release Date”（两个词）。

![在 Chrome 中打开的显示电影数据的电影应用程序](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a>更新生成的代码

打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]

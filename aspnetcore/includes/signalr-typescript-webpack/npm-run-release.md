---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175874"
---
```console
npm run release
```

此命令在运行应用时生成要提供的客户端资产。 资产位于 wwwroot 文件夹。

Webpack 完成了以下任务：

* 清除了 wwwroot 目录的内容。
* 将 TypeScript 转换为 JavaScript，该过程称为“转译”.
* 破坏生成的 JavaScript 以降低文件大小，该过程称为“缩小”。
* 将已处理的 JavaScript、CSS 和 HTML 文件从 src 复制到 wwwroot 目录。
* 将以下元素注入 wwwroot/index.html 文件：
    * 一个引用 wwwroot/main.\<hash\>.css 文件的 `<link>` 标记。 此标记紧挨着 `</head>` 结束标记之前。
    * 一个引用缩小后的 wwwroot/main.\<hash\>.js 文件的 `<script>` 标记。 此标记紧挨着 `</body>` 结束标记之前。

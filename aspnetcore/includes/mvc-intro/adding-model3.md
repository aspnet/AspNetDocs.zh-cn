---
ms.openlocfilehash: 3940675548ad7496aab9c720ee0b7fd512bfe029
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043454"
---

## <a name="test-the-app"></a>测试应用

* 运行应用并点击“Mvc Movie”链接。
* 点击“新建”链接，创建电影。

  ![创建包含“流派”、“价格”、“上映时间”和“标题”字段的视图](~/tutorials/first-mvc-app/adding-model/_static/movies.png)

* 可能无法在 `Price` 字段中输入小数点或逗号。 若要使 [jQuery 验证](https://jqueryvalidation.org/)支持使用逗号（“,”）表示小数点的的非英语区域设置，以及支持非美国英语日期格式，必须执行使应用全球化的步骤。 有关详细信息，请参阅 [https://github.com/aspnet/Docs/issues/4076](https://github.com/aspnet/Docs/issues/4076) 和[其他资源](#additional-resources)。 目前只能输入整数，例如 10。

<a name="displayformatdatelocal"></a>

* 在一些区域设置中，需要指定日期格式。 请参阅下方突出显示的代码。

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateFormat.cs?name=snippet_1&highlight=2,10)]

我们将在本教程的后续部分中探讨 `DataAnnotations`。

点击“创建”后，窗体会发布到服务器，其中电影信息会保存在数据库中。 应用重定向到 /Movies URL，其中会显示新创建的电影信息。

![显示新创建的电影列表的电影视图](~/tutorials/first-mvc-app/adding-model/_static/h.png)

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

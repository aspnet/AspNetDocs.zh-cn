---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 添加新字段 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045138"
---
# <a name="adding-a-new-field"></a>添加新字段

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本节中，您将使用 Entity Framework Code First 迁移将某些更改迁移到模型类，以便将更改应用到数据库。

默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。 如果不同步，实体框架将引发错误。 这样，就可以更轻松地跟踪开发时的问题，否则，在运行时) 只会发现错误 (。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>设置模型更改的 Code First 迁移

导航到解决方案资源管理器。 右键单击 " *电影 .mdf* " 文件，然后选择 " **删除** " 以删除电影数据库。 如果看不到 " *电影 .mdf* " 文件，请单击红色框中显示的 " **显示所有文件** " 图标。

![](adding-a-new-field/_static/image1.png)

生成应用程序，以确保没有任何错误。

在“工具”**** 菜单中，单击“NuGet 包管理器”****，然后单击“包管理器控制台”****。

![添加包手册](adding-a-new-field/_static/image2.png)

在 " **程序包管理器控制台** " 窗口中，在 `PM>` 提示符处输入

启用-迁移-ContextTypeName MvcMovie. MovieDBContext

![](adding-a-new-field/_static/image3.png)

 (上面显示的 "**启用-迁移**" 命令) 在新的*迁移*文件夹中创建*Configuration.cs*文件。

![](adding-a-new-field/_static/image4.png)

Visual Studio 将打开 *Configuration.cs* 文件。 将 `Seed` *Configuration.cs* 文件中的方法替换为以下代码：

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

将鼠标悬停在下面的红色波浪线上 `Movie` ，并单击 `Show Potential Fixes` ，然后单击 " **使用** **MvcMovie"。**

![](adding-a-new-field/_static/image5.png)

这样做将添加以下 using 语句：

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First 迁移将在 `Seed` 每次迁移后调用方法 (即，在包管理器控制台) 中调用 **更新数据库** ，此方法会更新已插入的行，如果它们尚不存在，则将其插入。
> 
> 以下代码中的 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法执行 "upsert" 操作：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> 由于 [种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 方法随每个迁移一起运行，因此您不能只插入数据，因为在第一个创建数据库的迁移之后，您尝试添加的行将已存在。 如果尝试插入已存在的行，"[upsert](http://en.wikipedia.org/wiki/Upsert)" 操作将会阻止发生的错误，但会覆盖在测试应用程序时对数据所做的任何更改。 对于某些表中的测试数据，您可能不希望发生这种情况：在某些情况下，当您在测试时更改数据时，您希望在数据库更新后更改保持不变。 在这种情况下，需要执行条件插入操作：仅在不存在行时插入行。   
> 
> 传递给 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的第一个参数指定要用于检查行是否已存在的属性。 对于所提供的测试电影数据， `Title` 属性可用于此目的，因为列表中的每个标题都是唯一的：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 此代码假设标题是唯一的。 如果手动添加重复标题，则在下次执行迁移时，将会出现以下异常。   
> 
> *序列包含多个元素*  
> 
> 有关 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的详细信息，请参阅 [使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

**按 CTRL-SHIFT-B 生成项目。** (如果此时不生成，以下步骤将失败。 ) 

下一步是创建一个 `DbMigration` 用于初始迁移的类。 此迁移创建新的数据库，这就是在上一步中删除了 *movie .mdf* 文件的原因。

在 " **程序包管理器控制台** " 窗口中，输入命令 `add-migration Initial` 以创建初始迁移。 名称 "初始" 是任意名称，用于命名创建的迁移文件。

![](adding-a-new-field/_static/image6.png)

Code First 迁移在 " *迁移* " 文件夹中创建名为 *{日期戳} \_ Initial.cs* )  (的其他类文件，此类包含用于创建数据库架构的代码。 迁移文件名预先修复了时间戳，以帮助进行排序。 检查 *{日期戳} \_ Initial.cs* 文件，其中包含为 `Movies` 电影数据库创建表的说明。 在下面的说明中更新数据库时，此 *{日期戳} \_ Initial.cs* 文件将运行，并创建数据库架构。 然后， **Seed** 方法将运行以用测试数据填充数据库。

在 " **包管理器控制台**" 中，输入 `update-database` 用于创建数据库的命令并运行 `Seed` 方法。

![](adding-a-new-field/_static/image7.png)

如果您收到一条错误消息，指示表已存在并且无法创建，则可能是您在删除数据库之后和执行之前运行了该应用程序 `update-database` 。 在这种情况下，请再次删除此 *电影 .mdf* 文件，然后重试该 `update-database` 命令。 如果仍出现错误，请删除 "迁移" 文件夹和内容，然后从本页顶部的说明开始 (*删除 ""* ，然后继续执行 "启用-迁移) 。 如果仍出现错误，请打开 SQL Server 对象资源管理器并从列表中删除数据库。

运行应用程序并导航到 */Movies* URL。 将显示种子数据。

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先将新的 `Rating` 属性添加到现有 `Movie` 类。 打开 *Models\Movie.cs* 文件并添加 `Rating` 此属性，如下所示：

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

完整的 `Movie` 类现在如以下代码所示：

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

按 Ctrl + Shift + B)  (生成应用程序。

由于已将一个新字段添加到 `Movie` 类，因此还需要更新 "绑定" *白名单* ，以便包括此新属性。 更新的 `bind` 属性 `Create` 和 `Edit` 操作方法以包括 `Rating` 属性：

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

还需要更新视图模板，以便在浏览器视图中显示、创建和编辑新的 `Rating` 属性。

打开 *\Views\Movies\Index.cshtml* 文件，并在 `<th>Rating</th>` " **Price** " 列后添加一个列标题。 然后在 `<td>` 模板末尾附近添加一个列，以呈现 `@item.Rating` 该值。 更新后的 *索引 cshtml* 视图模板如下所示：

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

接下来，打开 *\Views\Movies\Create.cshtml* 文件并添加 `Rating` 具有以下突出显示的标记的字段。 这将呈现一个文本框，以便您可以在创建新电影时指定级别。

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

现在，你已更新了应用程序代码以支持新 `Rating` 属性。

运行应用程序并导航到 */Movies* URL。 不过，当你执行此操作时，你将看到以下错误之一：

![](adding-a-new-field/_static/image9.png)  
  
创建数据库后，支持 "MovieDBContext" 上下文的模型已发生更改。 请考虑使用 Code First 迁移更新数据库 (https://go.microsoft.com/fwlink/?LinkId=238269) 。

![](adding-a-new-field/_static/image10.png)

出现此错误的原因 `Movie` 是，应用程序中更新的模型类现在与现有数据库的表的架构不同 `Movie` 。 （数据库表中没有 `Rating` 列。）

可通过几种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 在测试数据库上进行开发时，此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。 不过，缺点在于丢失了数据库中的现有数据，因此 *不* 希望在生产数据库上使用此方法！ 使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用程序的有效方式。 有关实体框架数据库初始值设定项的详细信息，请参阅 [ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。
3. 使用 Code First 迁移更新数据库架构。

本教程使用 Code First 迁移。

更新种子方法，使其为新列提供一个值。 打开 Migrations\Configuration.cs 文件，并向每个电影对象添加分级字段。

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

生成解决方案，然后打开 " **包管理器控制台** " 窗口，并输入以下命令：

`add-migration Rating`

`add-migration`命令告诉迁移框架检查当前的电影模型和当前的 MOVIE DB 架构，并创建将数据库迁移到新模型所需的代码。 名称 *级别* 是任意的，用于对迁移文件进行命名。 为迁移步骤使用有意义的名称会很有帮助。

此命令完成后，Visual Studio 将打开定义新的派生类的类文件 `DbMigration` ，并在 `Up` 方法中可以看到创建新列的代码。

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

生成解决方案，然后 `update-database` 在 " **包管理器控制台** " 窗口中输入命令。

下图显示了 " **包管理器控制台** " 窗口中的输出 (日期戳预先计算的 *等级* 将不同。 ) 

![](adding-a-new-field/_static/image11.png)

重新运行应用程序并导航到/Movies URL。 您可以看到新的 "分级" 字段。

![](adding-a-new-field/_static/image12.png)

单击 " **新建** " 链接以添加新电影。 请注意，可以添加级别。

![7_CreateRioII](adding-a-new-field/_static/image13.png)

单击“创建”。  现在电影列表中显示了新电影，其中包括评分：

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

现在，项目正在使用迁移，因此在添加新字段或更新架构时，无需删除数据库。 在下一部分中，我们将进行更多架构更改，并使用迁移来更新数据库。

还应将字段添加 `Rating` 到 "编辑"、"详细信息" 和 "删除" 视图模板。

您可以在 " **包管理器控制台** " 窗口中再次输入 "更新数据库" 命令，而不会运行任何迁移代码，因为该架构与该模型匹配。 但是，运行 "更新数据库" 将再次运行该 `Seed` 方法，如果更改了任何种子数据，则所做的更改将会丢失，因为 `Seed` 方法 upsert 数据。 有关此方法的详细信息，请参阅 `Seed` Tom Dykstra 的热门 [ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。 还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。 这只是 Code First 的简要介绍，请参阅为 [ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) ，以获取有关主题的更完整教程。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。

> [!div class="step-by-step"]
> [上一页](adding-search.md)
> [下一页](adding-validation.md)

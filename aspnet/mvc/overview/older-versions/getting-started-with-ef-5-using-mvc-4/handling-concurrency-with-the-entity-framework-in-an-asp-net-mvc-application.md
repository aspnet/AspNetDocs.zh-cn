---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架处理并发 (第7项，共10个) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b7d6ff8d6de27ee0935bc9cb8cc053efb8751d4b
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985705"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>使用 ASP.NET MVC 应用程序中的实体框架处理并发 (第7项，共10项) 

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在之前的两个教程中，您将处理相关数据。 本教程演示如何处理并发。 您将创建使用该实体的网页 `Department` ，编辑和删除实体的页面 `Department` 将处理并发错误。 下图显示了索引和删除页，包括发生并发冲突时显示的一些消息。

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>并发冲突

当某用户显示实体数据以对其进行编辑，而另一用户在上一用户的更改写入数据库之前更新同一实体的数据时，会发生并发冲突。 如果不启用此类冲突的检测，则最后更新数据库的人员将覆盖其他用户的更改。 在许多应用程序中，此风险是可接受的：如果用户很少或更新很少，或者一些更改被覆盖并不重要，则并发编程可能弊大于利。 在此情况下，不必配置应用程序来处理并发冲突。

### <a name="pessimistic-concurrency-locking"></a>悲观并发 (锁定) 

如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。 这称为 " *悲观并发*"。 例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。 如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。 如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。

管理锁定有缺点。 编程可能很复杂。 它需要大量的数据库管理资源，并会导致性能问题，因为应用程序的用户数增加 (也就是说，它不能很好地) 缩放。 由于这些原因，并不是所有的数据库管理系统都支持悲观并发。 实体框架不提供对它的内置支持，本教程不会演示如何实现它。

### <a name="optimistic-concurrency"></a>开放式并发

保守式并发的替代方法是 *乐观并发*。 悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。 例如，John 运行 "部门编辑" 页，将英语系的 **预算** 金额从 $350000.00 更改为 $0.00。

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John 单击 " **保存**" 之前，Jane 运行相同的页面，并将 " **开始日期** " 字段从9/1/2007 更改为8/8/2013。

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John 单击 " **保存** "，然后在浏览器返回到索引页时看到其更改，然后单击 " **保存**"。 接下来的情况取决于并发冲突的处理方式。 其中一些选项包括：

- 可以跟踪用户已修改的属性，并仅更新数据库中相应的列。 在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。 下次有人浏览英语系时，他们将看到 John 和 Jane 的更改，即开始日期为8/8/2013，预算为零美元。

    这种更新方法可减少可能导致数据丢失的冲突次数，但是如果对实体的同一属性进行竞争性更改，则数据难免会丢失。 Entity Framework 是否以这种方式工作取决于更新代码的实现方式。 通常不适合在 Web 应用程序中使用，因为它要求保持大量的状态，以便跟踪实体的所有原始属性值以及新值。 维护大量状态可能会影响应用程序性能，因为它需要服务器资源或必须包含在网页本身中 (例如，在) 隐藏的字段中。
- 可以让 Jane 的更改覆盖 John 的更改。 下次有人浏览英语系时，他们将看到8/8/2013 和已还原的 $350000.00 值。 这称为“客户端优先”或“最后一个优先” 。  (客户端的值优先于数据存储中的内容。 ) 如本部分简介中所述，如果不进行并发处理的任何编码，则会自动执行此操作。
- 您可以阻止在数据库中更新 Jane 的更改。 通常情况下，会显示一条错误消息，向她显示数据的当前状态，并允许她重新应用更改（如果她仍想要进行更改）。 这称为“存储优先”方案。 （数据存储值优先于客户端提交的值。）本教程将执行“存储优先”方案。 此方法可确保用户在未收到具体发生内容的警报时，不会覆盖任何更改。

### <a name="detecting-concurrency-conflicts"></a>检测并发冲突

可以通过处理实体框架引发的 [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) 异常来解决冲突。 为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。 因此，你必须正确配置数据库和数据模型。 启用冲突检测的某些选项包括：

- 数据库表中包含一个可用于确定某行更改时间的跟踪列。 然后，可以将实体框架配置为在 `Where` SQL 或命令的子句中包含 `Update` 该列 `Delete` 。

    跟踪列的数据类型通常为 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。 [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新行时递增的序列号。 在 `Update` 或 `Delete` 命令中， `Where` 子句包括 (原始行版本) 的跟踪列的原始值。 如果正在更新的行已由其他用户更改，则列中的值与 `rowversion` 原始值不同，因此 `Update` 或 `Delete` 语句由于子句而找不到要更新的行 `Where` 。 当实体框架找不到或命令已更新任何行时 `Update` `Delete` (即，当受影响的行数为零时) 时，它会将其解释为并发冲突。
- 将实体框架配置为在和命令的子句中包含表中每一列的原始值 `Where` `Update` `Delete` 。

    在第一个选项中，如果行中的任何内容在第一次读取后发生了更改， `Where` 子句将不会返回要更新的行，实体框架会将其解释为并发冲突。 对于包含多个列的数据库表，此方法可能会产生非常大 `Where` 的子句，并可能要求你维护大量状态。 如前文所述，维护大量状态可能会影响应用程序性能，因为它需要服务器资源或必须包含在网页本身中。 因此，通常不建议使用这种方法，也不是本教程中使用的方法。

    如果确实要实现这种并发方法，则必须将 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) 属性添加到要跟踪其并发的实体中的所有非主键属性。 通过此更改，实体框架可以在 SQL `WHERE` 语句的语句中包含所有列 `UPDATE` 。

在本教程的其余部分中，你将向实体中添加一个 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 跟踪属性 `Department` ，创建一个控制器和视图，并进行测试以验证所有内容是否正常工作。

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>将乐观并发属性添加到 "部门" 实体

在 *Models\Department.cs* 中，添加一个名为的跟踪属性 `RowVersion` ：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)特性指定此列将包含在 `Where` `Update` 发送到数据库的和命令的子句中 `Delete` 。 此属性被称为[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)，这是因为以前版本的 SQL SERVER 在 sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)将其替换之前使用 sql [Timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)数据类型。 的 .Net 类型 `rowversion` 是字节数组。 如果希望使用 Fluent API，可以使用 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) 方法来指定跟踪属性，如以下示例中所示：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

请参阅 GitHub issue [Replace IsConcurrencyToken By IsRowVersion](https://github.com/dotnet/AspNetDocs/issues/302)。

通过添加属性，更改了数据库模型，因此需要再执行一次迁移。 在包管理器控制台 (PMC) 中输入以下命令：

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>创建部门控制器

`Department`使用以下设置，以与其他控制器相同的方式创建控制器和视图：

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

在 *Controllers\DepartmentController.cs* 中，添加 `using` 语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

在此文件中的任何位置将 "LastName" 改为 "FullName" (四次) ，以便 "部门管理员" 下拉列表将包含讲师的全名，而不只是姓氏。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

将方法的现有代码替换为 `HttpPost` `Edit` 以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

视图将 `RowVersion` 在隐藏字段中存储原始值。 模型联编程序创建实例时 `department` ，该对象将具有原始 `RowVersion` 属性值和其他属性的新值（在 "编辑" 页上由用户输入）。 当实体框架创建 SQL `UPDATE` 命令时，该命令将包含一个 `WHERE` 子句，该子句将查找具有原始值的行 `RowVersion` 。

如果此命令不会影响任何行 `UPDATE` (没有行) 的原始 `RowVersion` 值，实体框架将引发 `DbUpdateConcurrencyException` 异常，而块中的代码将 `catch` 从异常对象中获取受影响的 `Department` 实体。 此实体具有从数据库中读取的值和用户输入的新值：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

接下来，代码为其数据库值不同于在 "编辑" 页上输入的数据库值的每个列添加一条自定义错误消息：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

更长的错误消息说明发生了什么情况以及如何处理它：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

最后，代码将对象的 `RowVersion` 值设置 `Department` 为从数据库中检索到的新值。 重新显示“编辑”页时，这个新的 `RowVersion` 值将存储在隐藏字段中，当用户下次单击“保存”时，将只捕获自“编辑”页重新显示起发生的并发错误。

在 *Views\Department\Edit.cshtml* 中，添加隐藏字段以保存 `RowVersion` 属性值，紧跟在属性的隐藏字段之后 `DepartmentID` ：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

在 *Views\Department\Index.cshtml* 中，将现有代码替换为以下代码，以将行链接移动到左侧，并更改在 `FullName` `LastName` " **管理员** " 列中显示的页面标题和列标题，而不是：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>测试开放式并发处理

运行站点并单击 " **部门**"：

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

右键单击 "Kim Abercrombie 的 **编辑** 超链接"，然后选择 " **在新选项卡中打开"，** 然后单击 "Abercrombie 的 **编辑** 超链接"。 这两个窗口显示相同的信息。

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在第一个浏览器窗口中更改字段，然后单击 " **保存**"。

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

浏览器显示具有更改值的索引页。

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

在第二个浏览器窗口中更改 "任何" 字段，然后单击 " **保存**"。

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

在第二个浏览器窗口中单击 " **保存** "。 看见一条错误消息：

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

再次单击“保存”。 在第二个浏览器中输入的值与在第一个浏览器中更改的数据的原始值一起保存。 在索引页中出现时，可以看到已保存的值。

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>更新 "删除" 页

对于“删除”页，Entity Framework 以类似方式检测其他人编辑院系所引起的并发冲突。 当 `HttpGet` `Delete` 方法显示确认视图时，视图将 `RowVersion` 在隐藏字段中包含原始值。 然后，该值可用于 `HttpPost` `Delete` 用户确认删除时调用的方法。 当实体框架创建 SQL 命令时 `DELETE` ，它包含一个 `WHERE` 具有原始值的子句 `RowVersion` 。 如果命令导致0行受影响 (意味着在) 显示删除确认页后更改了该行，则会引发并发异常，并调用方法，并 `HttpGet Delete` 将错误标志设置为， `true` 以重新显示错误消息的确认页面。 因为行已被其他用户删除，所以也可能会影响零行，因此在这种情况下，将显示不同的错误消息。

在 *DepartmentController.cs* 中，将 `HttpGet` `Delete` 方法替换为以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

该方法接受可选参数，该参数指示是否在并发错误之后重新显示页面。 如果此标志为 `true` ，则将使用属性向视图发送错误消息 `ViewBag` 。

`HttpPost` `Delete` 将名为)  (方法中的代码替换为 `DeleteConfirmed` 以下代码：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

在刚替换的基架代码中，此方法仅接受记录 ID：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

已将此参数更改为 `Department` 模型绑定器创建的实体实例。 这使你 `RowVersion` 除了记录键外，还可以访问属性值。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。 名为方法的基架代码将为该 `HttpPost` `Delete` `DeleteConfirmed` `HttpPost` 方法指定唯一的签名。  (CLR 要求重载方法具有不同的方法参数。 ) 现在签名是唯一的，你可以坚持 MVC 约定，并为 `HttpPost` 和 delete 方法使用相同的名称 `HttpGet` 。

如果捕获到并发错误，代码将重新显示“删除”确认页，并提供一个指示它应显示并发错误消息的标志。

在 *Views\Department\Delete.cshtml* 中，将基架代码替换为以下代码，以进行一些格式更改，并添加错误消息字段。 突出显示所作更改。

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

此代码在和标题之间添加错误 `h2` 消息 `h3` ：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

它 `LastName` `FullName` 在字段中替换为 `Administrator` ：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

最后，在 `DepartmentID` 语句后添加和属性的隐藏字段 `RowVersion` `Html.BeginForm` ：

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

运行 "部门索引" 页。 右键单击英语系的 " **删除** " 超链接，然后选择 " **在新窗口中打开"，** 然后在第一个窗口中单击英语系的 " **编辑** " 超链接。

在第一个窗口中，更改其中一个值，然后单击 " **保存** "：

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

索引页确认更改。

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

在第二个窗口中，单击 " **删除**"。

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

你将看到并发错误消息，且已使用数据库中的当前内容刷新了“院系”值。

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

如果再次单击“删除”，会重定向到已删除显示院系的索引页。

## <a name="summary"></a>总结

处理并发冲突已介绍完毕。 有关处理各种并发方案的其他方法的信息，请参阅实体框架团队博客上的 [开放式并发模式](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) 和 [属性值](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) 。 下一教程介绍如何实现和实体的每个层次结构一个表 `Instructor` 继承 `Student` 。

可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

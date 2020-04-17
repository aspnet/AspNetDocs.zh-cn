---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 缓存 |微软文档
author: rick-anderson
description: 对缓存的理解对于性能良好的ASP.NET应用程序非常重要。 ASP.NET 1.x 提供了三种不同的缓存选项;输出缓存,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542932"
---
# <a name="caching"></a>Caching

由[微软](https://github.com/microsoft)

> 对缓存的理解对于性能良好的ASP.NET应用程序非常重要。 ASP.NET 1.x 提供了三种不同的缓存选项;输出缓存、片段缓存和缓存 API。

对缓存的理解对于性能良好的ASP.NET应用程序非常重要。 ASP.NET 1.x 提供了三种不同的缓存选项;输出缓存、片段缓存和缓存 API。 ASP.NET 2.0 提供了所有三种方法，但它增加了一些重要的附加功能。 有几个新的缓存依赖项，开发人员现在也可以选择创建自定义缓存依赖项。 缓存的配置在ASP.NET 2.0 中也得到了显著改善。

## <a name="new-features"></a>新增功能

## <a name="cache-profiles"></a>缓存配置文件

缓存配置文件允许开发人员定义特定的缓存设置，然后可以应用于各个页面。 例如，如果您有一些页面应在 12 小时后从缓存中过期，则可以轻松地创建可应用于这些页面的缓存配置文件。 要添加新的缓存配置文件，请使用配置文件中的&lt;输出缓存设置&gt;部分。 例如，下面是一个称为*两天的*缓存配置文件的配置，该配置文件配置的缓存持续时间为 12 小时。

[!code-xml[Main](caching/samples/sample1.xml)]

要将此缓存配置文件应用于特定页面，请使用 @ OutputCache 指令的 CacheProfile 属性，如下所示：

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>自定义缓存依赖项

ASP.NET 1.x 开发人员大声疾呼自定义缓存依赖项。 在ASP.NET 1.x 中，CacheDependency 类被密封，阻止开发人员从中派生自己的类。 在 ASP.NET 2.0 中，该限制被删除，开发人员可以自由地开发自己的自定义缓存依赖项。 CacheDependency 类允许基于文件、目录或缓存键创建自定义缓存依赖项。

例如，下面的代码基于位于 Web 应用程序根目录的名为 stuff.xml 的文件创建新的自定义缓存依赖项：

[!code-csharp[Main](caching/samples/sample3.cs)]

在这种情况下，当 stuff.xml 文件发生更改时，缓存的项将失效。

还可以使用缓存键创建自定义缓存依赖项。 使用此方法，删除缓存密钥将使缓存的数据无效。 以下示例对此进行了说明：

[!code-csharp[Main](caching/samples/sample4.cs)]

要使上面插入的项无效，只需删除插入到缓存中的项，即可充当缓存键。

[!code-csharp[Main](caching/samples/sample5.cs)]

请注意，充当缓存键的项的键必须与添加到缓存键数组的值相同。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>基于轮询的 SQL 缓存依赖项（也称为基于表的依赖项）

SQL Server 7 和 2000 使用基于轮询的模型进行 SQL 缓存依赖项。 基于轮询的模型使用数据库表上的触发器，该触发器在表中的数据更改时触发。 该触发器更新通知表中ASP.NET定期检查的**更改 Id**字段。 如果已更新**changeId**字段，ASP.NET知道数据已更改，并且会使缓存的数据无效。

> [!NOTE]
> SQL Server 2005 也可以使用基于轮询的模型，但由于基于轮询的模型不是最有效的模型，因此最好在 SQL Server 2005 中使用基于查询的模型（稍后讨论）。

为了使使用基于轮询的模型的 SQL 缓存依赖项正常工作，表必须启用通知。 这可以通过 SqlCache 独立管理类或使用 aspnet\_regsql.exe 实用程序以编程方式完成。

以下命令行在位于 SQL Server 实例上的 Northwind 数据库中注册产品表，该实例名为*dbase，* 用于 SQL 缓存依赖项。

[!code-console[Main](caching/samples/sample6.cmd)]

以下是上述命令中使用的命令行开关的说明：

| **命令行开关** | **目标** |
| --- | --- |
| -S *server* | 指定服务器名称。 |
| -ed | 指定应为 SQL 缓存依赖项启用数据库。 |
| -d *\_数据库名称* | 指定应为 SQL 缓存依赖项启用的数据库名称。 |
| -E | 指定 aspnet\_regsql 在连接到数据库时应使用 Windows 身份验证。 |
| -et | 指定我们正在为 SQL 缓存依赖项启用数据库表。 |
| -t *\_表名称* | 指定数据库表的名称，以便为 SQL 缓存依赖项启用。 |

> [!NOTE]
> 还有其他可用于 aspnet\_regsql.exe 的交换机。 对于完整列表，运行 aspnet\_regsql.exe -？ 从命令行。

运行此命令时，对 SQL Server 数据库进行了以下更改：

- 将添加**AspNet\_SqlCacheTables 用于更改通知表**。 此表包含数据库中已为其启用 SQL 缓存依赖项的每个表的一行。
- 在数据库内部创建以下存储过程：

| 阿斯普内\_SqlCache 存储过程 | 查询 AspNet\_SqlCacheTablesForChange 通知表，并返回为 SQL 缓存依赖项启用的所有表以及每个表的 changeId 值。 此存储的 proc 用于轮询以确定数据是否已更改。 |
| --- | --- |
| AspNet\_SqlCache查询注册表存储过程 | 通过查询 AspNet\_SqlCacheTablesForChange 通知表来返回为 SQL 缓存依赖项启用的所有表，并返回为 SQL 缓存依赖项启用的所有表。 |
| 阿斯普内\_SqlCache 注册表存储过程 | 通过在通知表中添加必要的条目并添加触发器来注册 SQL 缓存依赖项的表。 |
| 阿斯普内\_SqlCacheUn 寄存器表存储过程 | 通过删除通知表中的条目并删除触发器，取消注册 SQL 缓存依赖项的表。 |
| 阿斯普内\_SqlCache 更新更改存储过程 | 通过增加已更改表的 changeId 来更新通知表。 ASP.NET使用此值来确定数据是否已更改。 如下所述，此存储的 proc 由启用表时创建的触发器执行。 |

- 为表创建一个 SQL Server 触发器**_，\_称为表名称_\_AspNet\_SqlCache 通知\_触发器**。 当在表上执行插入、更新\_或删除时，此触发器将执行 AspNet SqlCache 更新更改存储过程。
- SQL Server 角色称为**\_aspnet\_更改通知接收通知仅访问**已添加到数据库中。

**aspnet\_更改通知\_仅接收通知访问**SQL 服务器角色具有对 AspNet\_SqlCache 投票存储过程的 EXEC 权限。 为了使轮询模型正常工作，您必须将进程帐户添加到 aspnet\_更改通知\_仅接收通知访问角色。 aspnet\_regsql.exe 工具不会为您执行此操作。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>配置基于轮询的 SQL 缓存依赖项

配置基于轮询的 SQL 缓存依赖项需要几个步骤。 第一步是启用数据库和表，如上所述。 完成此步骤后，配置的其余部分如下所示：

- 配置ASP.NET配置文件。
- 配置 SqlCache 依赖性

### <a name="configuring-the-aspnet-configuration-file"></a>配置ASP.NET配置文件

除了添加上一个模块中讨论的连接字符串外，&lt;还必须使用&gt;&lt;sqlCacheDependency&gt;元素配置缓存元素，如下所示：

[!code-xml[Main](caching/samples/sample7.xml)]

此配置启用对*pubs*数据库的 SQL 缓存依赖项。 请注意，sqlCache 依赖元素&lt;&gt;中的 pollTime 属性默认为 60000 毫秒或 1 分钟。 （此值不能小于 500 毫秒。在此示例中，add&lt;&gt;元素添加新数据库并覆盖轮询Time，将其设置为 9000000 毫秒。

#### <a name="configuring-the-sqlcachedependency"></a>配置 SqlCache 依赖性

下一步是配置 SqlCache 依赖性。 实现此目的的最简单方法是在 @ Outcache 指令中指定 SqlDependency 属性的值，如下所示：

[!code-aspx[Main](caching/samples/sample8.aspx)]

在上述输出缓存指令中，为*pubs*数据库中*的作者*表配置了 SQL 缓存依赖项。 可以通过将多个依赖项与分号分隔来配置，如下所示：

[!code-aspx[Main](caching/samples/sample9.aspx)]

配置 SqlCache 依赖性的另一种方法是在编程方式中配置。 以下代码在*pubs*数据库中创建对*作者*表的新 SQL 缓存依赖项。

[!code-csharp[Main](caching/samples/sample10.cs)]

以编程方式定义 SQL 缓存依赖项的好处之一是可以处理可能发生的任何异常。 例如，如果尝试为尚未为通知启用的数据库定义 SQL 缓存依赖项，则会引发**数据库未启用通知异常异常**。 在这种情况下，您可以尝试通过调用**SqlCache独立Admin.enable通知**方法并传递数据库名称来启用数据库的通知。

同样，如果尝试为尚未为通知启用的表定义 SQL 缓存依赖项，将引发**表未启用For通知异常**。 然后，您可以调用**SqlCache 独立Admin.启用TableFor通知**方法，传递数据库名称和表名称。

以下代码示例说明了在配置 SQL 缓存依赖项时如何正确配置异常处理。

[!code-csharp[Main](caching/samples/sample11.cs)]

更多信息：[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>基于查询的 SQL 缓存依赖项（仅限 SQL Server 2005）

当 SQL Server 2005 用于 SQL 缓存依赖项时，不需要基于轮询的模型。 当与 SQL Server 2005 一起使用时，SQL 缓存依赖项直接通过 SQL 连接到 SQL Server 实例（无需进一步配置）使用 SQL Server 2005 查询通知。

启用基于查询的通知的最简单方法是通过将数据源对象的**SqlCacheDependency 属性**设置为**命令通知**并将**EnableCaching**属性设置为**true**来声明性地执行此操作。 使用此方法，不需要任何代码。 如果针对数据源执行的命令的结果发生更改，它将使缓存数据失效。

以下示例为 SQL 缓存依赖项配置数据源控件：

[!code-aspx[Main](caching/samples/sample12.aspx)]

在这种情况下，如果**SelectCommand**中指定的查询返回的结果与最初的结果不同，则缓存的结果将失效。

还可以通过将 **@ OutputCache**指令的**SqlIis**属性设置为**命令通知**，指定为 SQL 缓存依赖项启用所有数据源。 下面的示例说明了这一点。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> 有关 SQL Server 2005 中的查询通知的详细信息，请参阅 SQL 服务器联机书籍。

配置基于查询的 SQL 缓存依赖项的另一种方法是使用 SqlCache 依赖类以编程方式执行此操作。 以下代码示例说明了如何实现此目的。

[!code-csharp[Main](caching/samples/sample14.cs)]

更多信息：[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>缓存后替换

缓存页面可以显著提高 Web 应用程序的性能。 但是，在某些情况下，您需要缓存大部分页面，并且页面中的某些片段是动态的。 例如，如果创建的新闻报道页面在设定的时间段内是完全静态的，则可以将整个页面设置为缓存。 如果要包含在每个页面请求中更改的旋转广告横幅，则包含广告的页面部分必须是动态的。 为了允许您缓存页面但动态替换某些内容，可以使用ASP.NET缓存后替换。 使用缓存后替换时，整个页面的输出将缓存，并带有标记为免于缓存的特定部件。 在广告横幅示例中，AdRotator 控件允许您利用缓存后替换，以便为每个用户和每个页面刷新动态创建广告。

有三种方法可以实现缓存后替换：

- 声明性，使用替换控件。
- 在编程上，使用替换控件 API。
- 隐式，使用 AdRotator 控件。

### <a name="substitution-control"></a>替代控制

ASP.NET替换控件指定以动态创建而不是缓存的缓存页面的一部分。 将替换控件放置在您希望显示动态内容的页面上的位置。 在运行时，替换控件调用使用 MethodName 属性指定的方法。 该方法必须返回一个字符串，然后替换替换控件的内容。 该方法必须是包含页面或用户控制控件上的静态方法。 使用替换控件会导致客户端可缓存性更改为服务器可缓存性，因此页面不会缓存在客户端上。 这可确保将来对页面的请求再次调用 方法以生成动态内容。

### <a name="substitution-api"></a>替换 API

要以编程方式为缓存页面创建动态内容，可以在页面代码中调用[Write替代](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)方法，将其作为参数传递方法的名称。 处理动态内容创建的方法需要单个[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)参数并返回字符串。 返回字符串是在给定位置替换的内容。 调用 Write 替代方法而不是声明性使用替换控件的优点是，您可以调用任意对象的方法，而不是调用 Page 或 UserControl 对象的静态方法。

调用 Write替代方法会导致客户端可缓存性更改为服务器可缓存性，因此页面不会缓存在客户端上。 这可确保将来对页面的请求再次调用 方法以生成动态内容。

### <a name="adrotator-control"></a>辅助器控制

AdRotator 服务器控件在内部实现对缓存后替换的支持。 如果将 AdRotator 控件放在页面上，它将在每个请求上呈现唯一的广告，而不管父页是否缓存。 因此，包含 AdRotator 控件的页面仅缓存服务器端。

## <a name="controlcachepolicy-class"></a>控件缓存策略类

ControlCachePolicy 类允许使用用户控件对片段缓存进行编程控制。 ASP.NET将用户控件嵌入[到基本部分缓存控制](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)实例中。 Base部分缓存控制类表示已启用输出缓存的用户控件。

当您访问[部分缓存控件](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)的[Base 部分缓存控制.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)属性时，您始终会收到有效的 ControlCachePolicy 对象。 但是，如果您访问[UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) [属性的用户控制控件](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx)，则只有在用户控件已由 Base 部分缓存控件包包时，才会收到有效的 ControlCachePolicy 对象。 如果未包装，则属性返回的 ControlCachePolicy 对象将引发异常，当您尝试操作它时，因为它没有关联的 BasePartialCachingControl。 要确定 UserControl 实例是否支持缓存而不生成异常，请检查["支持缓存"](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)属性。

使用 ControlCachePolicy 类是启用输出缓存的几种方法之一。 下面的列表描述了可用于启用输出缓存的方法：

- 使用[# 输出缓存](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令在声明性方案中启用输出缓存。
- 使用["部分缓存属性"属性](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)为代码背后的文件中的用户控件启用缓存。
- 使用 ControlCachePolicy 类指定在编程方案中的缓存设置，其中您正在使用以前的方法之一使用已启用缓存并使用[System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)方法动态加载的 BasePartialCacheControl 实例。

只能在控制生命周期的 Init 和预渲染阶段之间成功操作 ControlCachePolicy 实例。 如果在 PreRender 阶段后修改 ControlCachePolicy 对象，ASP.NET将引发异常，因为在呈现控件后所做的任何更改实际上不会影响缓存设置（在渲染阶段缓存控件）。 最后，用户控件实例（因此其 ControlCachePolicy 对象）仅在实际呈现时才可用于编程操作。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>对缓存配置的&lt;更改 - 缓存&gt;元素

ASP.NET 2.0 中缓存配置有几个更改。 缓存&lt;&gt;元素在 ASP.NET 2.0 中是新的，允许您在配置文件中进行更改缓存配置。 以下属性可用。

| **元素** | **说明** |
| --- | --- |
| **缓存** | 可选元素。 定义全局应用程序缓存设置。 |
| **输出缓存** | 可选元素。 指定应用程序范围的输出缓存设置。 |
| **outputCacheSettings** | 可选元素。 指定可应用于应用程序中的页面的输出缓存设置。 |
| **sqlCacheDependency** | 可选元素。 为 ASP.NET 应用程序配置 SQL 缓存依赖项。 |

### <a name="the-ltcachegt-element"></a>缓存&lt;&gt;元素

缓存&lt;&gt;元素中提供了以下属性：

| **Attribute** | **说明** |
| --- | --- |
| **禁用内存收集** | 可选**布尔属性**。 获取或设置一个值，指示计算机处于内存压力下时发生的缓存内存集合是否被禁用。 |
| **禁用过期** | 可选**布尔属性**。 获取或设置指示是否禁用缓存过期的值。 禁用后，缓存的项目不会过期，也不会发生过期缓存项的后台清理。 |
| **私有字节限制** | 可选**的 Int64**属性。 在缓存开始刷新过期项目并尝试回收内存之前获取或设置指示应用程序专用字节的最大大小的值。 此限制包括缓存使用的内存以及正在运行的应用程序的正常内存开销。 设置为零表示ASP.NET将使用自己的启发式方法来确定何时开始回收内存。 |
| **物理内存使用限制百分比** | 可选**的 Int32**属性。 获取或设置一个值，指示应用程序在开始刷新过期项目并尝试回收内存之前可以使用的计算机物理内存的最大百分比。 设置为零表示ASP.NET将使用自己的启发式方法来确定何时开始回收内存。 |
| **私人字节投票时间** | 可选**的 TimeSpan**属性。 获取或设置一个值，指示应用程序专用字节内存使用情况轮询之间的时间间隔。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;输出缓存&gt;元素

以下属性可用于&lt;输出缓存&gt;元素。

|       <strong>Attribute</strong>        |                                                                                                                                                                                                                                                       <strong>说明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>启用输出缓存</strong>    |                                                                                                                                                          可选<strong>布尔属性</strong>。 启用/禁用页面输出缓存。 如果禁用，则无论使用编程设置或声明性设置如何，都不缓存任何页面。 默认值为 <strong>true</strong>。                                                                                                                                                           |
|  <strong>启用碎片缓存</strong>   |                                                可选<strong>布尔属性</strong>。 启用/禁用应用程序片段缓存。 如果禁用，则无论使用的[# OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令或缓存配置文件如何，都无需缓存任何页面。 包括缓存控制标头，指示上游代理服务器以及浏览器客户端不应尝试缓存页面输出。 默认值为<strong>false</strong>。                                                 |
| <strong>发送缓存控制标头</strong> |                                                                                                                                                      可选<strong>布尔属性</strong>。 获取或设置一个值，指示默认情况下输出缓存模块是否发送<strong>缓存控制：私有</strong>标头。 默认值为<strong>false</strong>。                                                                                                                                                      |
|      <strong>省略VaryStar</strong>      | 可选<strong>布尔属性</strong>。 启用/禁用在响应中发送<strong>Http"Vary：/\<强<em>>"标头。使用 false 的默认设置时，</em>\*<strong>将发送输出缓存页的"_Vary："标头。发送 Vary 标头时，它允许根据 Vary 标头中指定的内容缓存不同的版本。例如<em>，Vary：用户代理</em>将基于发出请求的用户代理存储页面的不同版本。默认值为 _false</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;输出缓存设置&gt;元素

输出&lt;缓存设置&gt;元素允许创建缓存配置文件，如前面所述。 &lt;输出缓存设置&gt;元素的唯一子元素是用于配置缓存&lt;配置文件的输出&gt;缓存配置文件元素。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCache 依赖&gt;元素

以下属性可用于&lt;sqlCache 依赖元素。&gt;

| **Attribute** | **说明** |
| --- | --- |
| **启用** | 必需**布尔属性**。 指示是否轮询更改。 |
| **轮询时间** | 可选**的 Int32**属性。 设置 SqlCache 依赖项轮询数据库表以进行更改的频率。 此值对应于连续轮询之间的毫秒数。 不能将其设置为小于 500 毫秒。 默认值为 1 分钟。 |

### <a name="more-information"></a>更多信息

关于缓存配置，您应该知道一些其他信息。

- 如果未设置辅助进程专用字节限制，则缓存将使用以下限制之一： 

    - x86 2GB：800MB 或 60% 的物理 RAM，以较低者为准
    - x86 3GB：1800MB 或 60% 的物理 RAM，以较低者为准
    - x64： 1 TB 或 60% 的物理 RAM，以较低者为准
- 如果同时设置辅助进程专用字节限制和&lt;缓存专用字节限制/，&gt;则缓存将使用两个中的最小值。
- 就像在 1.x 中一样，我们删除缓存条目并调用 GC。收集有两个原因： 

    - 我们非常接近私有字节限制
    - 可用内存接近或小于 10%
- 通过将&lt;缓存百分比物理内存使用限制/&gt;设置为 100，可以有效地禁用低可用内存条件的修剪和缓存。
- 与 1.x 不同，2.0 将挂起修剪并收集上次 GC 时调用。Collect 没有将私有字节或托管堆的大小减少超过（缓存）内存限制的 1%。

## <a name="lab1-custom-cache-dependencies"></a>实验室 1：自定义缓存依赖项

1. 创建新网站。
2. 添加新的 XML 文件称为 cache.xml，并将其保存到 Web 应用程序的根目录。
3. 在 default.aspx\_的代码后面添加以下代码到页面加载方法： 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 将以下内容添加到源视图中的 default.aspx 的顶部： 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 浏览默认.aspx。 时间说什么？
6. 刷新浏览器。 时间说什么？
7. 打开 cache.xml 并添加以下代码： 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. 保存缓存.xml。
9. 刷新浏览器。 时间说什么？
10. 解释为什么时间更新而不是显示以前缓存的值：

## <a name="lab-2-using-polling-based-cache-dependencies"></a>实验 2：使用基于轮询的缓存依赖项

本实验使用您在上一个模块中创建的项目，该项目允许通过 GridView 和详细信息视图控件编辑北风数据库中的数据。

1. 在 Visual Studio 2005 中打开该项目。
2. 根据北风数据库运行\_aspnet regsql 实用程序，以启用数据库和产品表。 使用可视化工作室命令提示符中的以下命令： 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 将以下内容添加到 Web.config 文件： 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 添加新的 Web 表单，称为 showdata.aspx。
5. 将以下 = 输出缓存指令添加到 showdata.aspx 页面： 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 将以下代码添加到 showdata.aspx 的页面\_加载： 

    [!code-html[Main](caching/samples/sample21.html)]
7. 添加新的 SqlDataSource 控件以显示data.aspx，并将其配置为使用北风数据库连接。 单击“下一步”。
8. 选择"产品名称"和"产品 ID"复选框，然后单击"下一步"。
9. 单击“完成”。
10. 向 showdata.aspx 页面添加新的 GridView。
11. 从下拉列表中选择 SqlDataSource1。
12. 保存和浏览显示数据.aspx。 记下显示的时间。

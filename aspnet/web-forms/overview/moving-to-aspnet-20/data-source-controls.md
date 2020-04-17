---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 数据源控制 |微软文档
author: rick-anderson
description: ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。 然而，它并不像它本来可以的那么用户友好。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540215"
---
# <a name="data-source-controls"></a><span data-ttu-id="71d1e-104">数据源控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-104">Data Source Controls</span></span>

<span data-ttu-id="71d1e-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="71d1e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="71d1e-106">ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。</span><span class="sxs-lookup"><span data-stu-id="71d1e-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="71d1e-107">然而，它并不像它本来可以对用户友好。</span><span class="sxs-lookup"><span data-stu-id="71d1e-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="71d1e-108">它仍然需要大量的代码才能从中获得许多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="71d1e-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="71d1e-109">这就是 1.x 中所有数据访问努力中的模型。</span><span class="sxs-lookup"><span data-stu-id="71d1e-109">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="71d1e-110">ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。</span><span class="sxs-lookup"><span data-stu-id="71d1e-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="71d1e-111">然而，它并不像它本来可以对用户友好。</span><span class="sxs-lookup"><span data-stu-id="71d1e-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="71d1e-112">它仍然需要大量的代码才能从中获得许多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="71d1e-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="71d1e-113">这就是 1.x 中所有数据访问努力中的模型。</span><span class="sxs-lookup"><span data-stu-id="71d1e-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="71d1e-114">ASP.NET 2.0 部分使用数据源控件解决了这个问题。</span><span class="sxs-lookup"><span data-stu-id="71d1e-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="71d1e-115">ASP.NET 2.0 中的数据源控件为开发人员提供了用于检索数据、显示数据和编辑数据的声明性模型。</span><span class="sxs-lookup"><span data-stu-id="71d1e-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="71d1e-116">数据源控件的目的是向数据绑定控件提供数据一致的表示形式，而不管数据源如何。</span><span class="sxs-lookup"><span data-stu-id="71d1e-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="71d1e-117">ASP.NET 2.0 中数据源控件的核心是 DataSourceControl 抽象类。</span><span class="sxs-lookup"><span data-stu-id="71d1e-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="71d1e-118">DataSourceControl 类提供了 IDataSource 接口和 IListSource 接口的基本实现，后者允许您将数据源控件指定为数据绑定控件的 DataSource（通过稍后讨论的新 DataSourceId 属性），并将其中的数据公开为列表。</span><span class="sxs-lookup"><span data-stu-id="71d1e-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="71d1e-119">数据源控件的每个数据列表都公开为 DataSourceView 对象。</span><span class="sxs-lookup"><span data-stu-id="71d1e-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="71d1e-120">IDataSource 接口提供了对 DataSourceView 实例的访问。</span><span class="sxs-lookup"><span data-stu-id="71d1e-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="71d1e-121">例如，GetViewNames 方法返回一个 ICollection，允许您枚举与特定数据源控件关联的 DataSourceViews，GetView 方法允许您按名称访问特定的 DataSourceView 实例。</span><span class="sxs-lookup"><span data-stu-id="71d1e-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="71d1e-122">数据源控件没有用户界面。</span><span class="sxs-lookup"><span data-stu-id="71d1e-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="71d1e-123">它们作为服务器控件实现，以便它们可以支持声明性语法，以便根据需要访问页面状态。</span><span class="sxs-lookup"><span data-stu-id="71d1e-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="71d1e-124">数据源控件不向客户端呈现任何 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="71d1e-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="71d1e-125">稍后您将看到，使用数据源控件还可以获得缓存好处。</span><span class="sxs-lookup"><span data-stu-id="71d1e-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>

## <a name="storing-connection-strings"></a><span data-ttu-id="71d1e-126">存储连接字符串</span><span class="sxs-lookup"><span data-stu-id="71d1e-126">Storing Connection Strings</span></span>

<span data-ttu-id="71d1e-127">在研究如何配置数据源控件之前，我们应该在有关连接字符串ASP.NET 2.0 中介绍新功能。</span><span class="sxs-lookup"><span data-stu-id="71d1e-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="71d1e-128">ASP.NET 2.0 在配置文件中引入了一个新部分，允许您轻松存储可在运行时动态读取的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="71d1e-129">连接&lt;字符串&gt;部分便于存储连接字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="71d1e-130">下面的代码段添加了一个新的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="71d1e-131">&lt;与 appSettings&gt;部分一样，&lt;连接字符串&gt;部分显示在配置文件中的&lt;system.web&gt;部分之外。</span><span class="sxs-lookup"><span data-stu-id="71d1e-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>

<span data-ttu-id="71d1e-132">要使用此连接字符串，可以在设置服务器控件的 ConnectString 属性时使用以下语法。</span><span class="sxs-lookup"><span data-stu-id="71d1e-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="71d1e-133">还可以&lt;加密连接&gt;字符串部分，以便不公开敏感信息。</span><span class="sxs-lookup"><span data-stu-id="71d1e-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="71d1e-134">这一能力将在后面的模块中介绍。</span><span class="sxs-lookup"><span data-stu-id="71d1e-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="71d1e-135">缓存数据源</span><span class="sxs-lookup"><span data-stu-id="71d1e-135">Caching Data Sources</span></span>

<span data-ttu-id="71d1e-136">每个 DataSourceControl 提供四个属性来配置缓存;启用缓存、缓存持续时间、缓存过期策略和缓存密钥依赖性。</span><span class="sxs-lookup"><span data-stu-id="71d1e-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="71d1e-137">启用缓存</span><span class="sxs-lookup"><span data-stu-id="71d1e-137">EnableCaching</span></span>

<span data-ttu-id="71d1e-138">启用缓存是一个布尔属性，用于确定是否为数据源控件启用缓存。</span><span class="sxs-lookup"><span data-stu-id="71d1e-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="71d1e-139">缓存持续时间属性</span><span class="sxs-lookup"><span data-stu-id="71d1e-139">CacheDuration Property</span></span>

<span data-ttu-id="71d1e-140">"缓存持续时间"属性设置缓存保持有效的秒数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="71d1e-141">将此属性设置为**0**会导致缓存保持有效，直到显式失效。</span><span class="sxs-lookup"><span data-stu-id="71d1e-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="71d1e-142">缓存过期策略属性</span><span class="sxs-lookup"><span data-stu-id="71d1e-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="71d1e-143">缓存过期策略属性可以设置为**绝对**或**滑动**。</span><span class="sxs-lookup"><span data-stu-id="71d1e-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="71d1e-144">将其设置为"绝对"意味着缓存数据的最大时间是 CacheDuration 属性指定的秒数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="71d1e-145">通过将它设置为"滑动"，执行每个操作时将重置过期时间。</span><span class="sxs-lookup"><span data-stu-id="71d1e-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="71d1e-146">缓存密钥依赖属性</span><span class="sxs-lookup"><span data-stu-id="71d1e-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="71d1e-147">如果为 CacheKey 依赖项属性指定了字符串值，ASP.NET将基于该字符串设置新的缓存依赖项。</span><span class="sxs-lookup"><span data-stu-id="71d1e-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="71d1e-148">这允许您通过简单地更改或删除 CacheKey 依赖项来显式使缓存无效。</span><span class="sxs-lookup"><span data-stu-id="71d1e-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="71d1e-149">**重要提示**：如果启用了模拟，并且对数据源和/或数据内容的访问基于客户端标识，则建议通过设置启用缓存设置为 False 来禁用缓存。</span><span class="sxs-lookup"><span data-stu-id="71d1e-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="71d1e-150">如果在此方案中启用了缓存，并且最初请求数据的用户以外的用户发出请求，则不会强制执行对数据源的授权。</span><span class="sxs-lookup"><span data-stu-id="71d1e-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="71d1e-151">数据将仅从缓存中提供。</span><span class="sxs-lookup"><span data-stu-id="71d1e-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="71d1e-152">SqlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-152">The SqlDataSource Control</span></span>

<span data-ttu-id="71d1e-153">SqlDataSource 控件允许开发人员访问存储在支持ADO.NET的任何关系数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="71d1e-154">它可以使用 System.Data.SqlClient 提供程序访问 SQL Server 数据库、System.Data.OleDb 提供程序、系统.Data.Odbc 提供程序或 System.Data.OracleClient 提供程序来访问 Oracle。</span><span class="sxs-lookup"><span data-stu-id="71d1e-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="71d1e-155">因此，SqlDataSource 当然不仅用于访问 SQL Server 数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="71d1e-156">为了使用 SqlDataSource，您只需为 ConnectString 属性提供一个值，并指定 SQL 命令或存储过程。</span><span class="sxs-lookup"><span data-stu-id="71d1e-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="71d1e-157">SqlDataSource 控件负责使用底层ADO.NET体系结构。</span><span class="sxs-lookup"><span data-stu-id="71d1e-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="71d1e-158">它打开连接，查询数据源或执行存储过程，返回数据，然后为您关闭连接。</span><span class="sxs-lookup"><span data-stu-id="71d1e-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="71d1e-159">由于 DataSourceControl 类会自动为您关闭连接，因此它应该减少因数据库连接泄漏而生成的客户呼叫数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>

<span data-ttu-id="71d1e-160">下面的代码段使用存储在配置文件中的连接字符串将下拉列表控件绑定到 SqlDataSource 控件，如上所示。</span><span class="sxs-lookup"><span data-stu-id="71d1e-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="71d1e-161">如上所述，SqlDataSource 的 DataSourceMode 属性指定数据源的模式。</span><span class="sxs-lookup"><span data-stu-id="71d1e-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="71d1e-162">在上面的示例中，数据源模式设置为数据阅读器。</span><span class="sxs-lookup"><span data-stu-id="71d1e-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="71d1e-163">在这种情况下，SqlDataSource 将使用仅行和只读游标返回 IDataReader 对象。</span><span class="sxs-lookup"><span data-stu-id="71d1e-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="71d1e-164">返回的指定类型的对象由所使用的提供程序控制。</span><span class="sxs-lookup"><span data-stu-id="71d1e-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="71d1e-165">在这种情况下，我使用的是 Web.config 文件的&lt;connectStrings&gt;部分中指定的 System.Data.SqlClient 提供程序。</span><span class="sxs-lookup"><span data-stu-id="71d1e-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="71d1e-166">因此，返回的对象将采用 SqlDataReader 类型。</span><span class="sxs-lookup"><span data-stu-id="71d1e-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="71d1e-167">通过指定 DataSet 的 DataSourceMode 值，数据可以存储在服务器上的 DataSet 中。</span><span class="sxs-lookup"><span data-stu-id="71d1e-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="71d1e-168">此模式允许您添加排序、分页等功能。如果我将 SqlDataSource 数据绑定到 GridView 控件，我会选择 DataSet 模式。</span><span class="sxs-lookup"><span data-stu-id="71d1e-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="71d1e-169">但是，在下拉列表的情况下，数据阅读器模式是正确的选择。</span><span class="sxs-lookup"><span data-stu-id="71d1e-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="71d1e-170">缓存 SqlDataSource 或 AccessDataSource 时，必须将 DataSourceMode 属性设置为 DataSet。</span><span class="sxs-lookup"><span data-stu-id="71d1e-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="71d1e-171">如果使用 DataReader 的 DataSource 模式启用缓存，则会出现异常。</span><span class="sxs-lookup"><span data-stu-id="71d1e-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>

## <a name="sqldatasource-properties"></a><span data-ttu-id="71d1e-172">SqlDataSource 属性</span><span class="sxs-lookup"><span data-stu-id="71d1e-172">SqlDataSource Properties</span></span>

<span data-ttu-id="71d1e-173">以下是 SqlDataSource 控件的一些属性。</span><span class="sxs-lookup"><span data-stu-id="71d1e-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="71d1e-174">取消选择无效参数</span><span class="sxs-lookup"><span data-stu-id="71d1e-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="71d1e-175">布尔值，用于指定如果其中一个参数为空，是否取消选择命令。</span><span class="sxs-lookup"><span data-stu-id="71d1e-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="71d1e-176">默认值为 True。</span><span class="sxs-lookup"><span data-stu-id="71d1e-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="71d1e-177">冲突检测</span><span class="sxs-lookup"><span data-stu-id="71d1e-177">ConflictDetection</span></span>

<span data-ttu-id="71d1e-178">在多个用户可能同时更新数据源的情况下，冲突检测属性确定 SqlDataSource 控件的行为。</span><span class="sxs-lookup"><span data-stu-id="71d1e-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="71d1e-179">此属性计算为冲突选项枚举的值之一。</span><span class="sxs-lookup"><span data-stu-id="71d1e-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="71d1e-180">这些值是**比较所有值**和**覆盖更改**。</span><span class="sxs-lookup"><span data-stu-id="71d1e-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="71d1e-181">如果设置为"覆盖更改"，则最后一个将数据写入数据源的人员将覆盖任何以前的更改。</span><span class="sxs-lookup"><span data-stu-id="71d1e-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="71d1e-182">但是，如果冲突检测属性设置为比较 AllValue，则为 SelectCommand 返回的列创建参数，并创建参数以在每个列中保存原始值，从而允许 SqlDataSource 确定自执行 SelectCommand 以来值是否已更改。</span><span class="sxs-lookup"><span data-stu-id="71d1e-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="71d1e-183">删除命令</span><span class="sxs-lookup"><span data-stu-id="71d1e-183">DeleteCommand</span></span>

<span data-ttu-id="71d1e-184">设置或获取从数据库中删除行时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="71d1e-185">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="71d1e-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="71d1e-186">删除命令类型</span><span class="sxs-lookup"><span data-stu-id="71d1e-186">DeleteCommandType</span></span>

<span data-ttu-id="71d1e-187">设置或获取删除命令的类型，SQL 查询（文本）或存储过程（存储过程）。</span><span class="sxs-lookup"><span data-stu-id="71d1e-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="71d1e-188">删除参数</span><span class="sxs-lookup"><span data-stu-id="71d1e-188">DeleteParameters</span></span>

<span data-ttu-id="71d1e-189">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 DeleteCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="71d1e-190">旧值参数格式字符串</span><span class="sxs-lookup"><span data-stu-id="71d1e-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="71d1e-191">此属性用于指定原始值参数的格式，在冲突检测属性设置为比较AllValue的情况下。</span><span class="sxs-lookup"><span data-stu-id="71d1e-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="71d1e-192">默认值表示{0}原始值参数的名称与原始参数相同。</span><span class="sxs-lookup"><span data-stu-id="71d1e-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="71d1e-193">换句话说，如果字段名称为 EmployID，则原始值参数将为@EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="71d1e-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="71d1e-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="71d1e-194">SelectCommand</span></span>

<span data-ttu-id="71d1e-195">设置或获取用于从数据库中检索数据的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="71d1e-196">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="71d1e-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="71d1e-197">选择命令类型</span><span class="sxs-lookup"><span data-stu-id="71d1e-197">SelectCommandType</span></span>

<span data-ttu-id="71d1e-198">设置或获取选择命令的类型，SQL 查询（文本）或存储过程（存储过程）。</span><span class="sxs-lookup"><span data-stu-id="71d1e-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="71d1e-199">选择参数</span><span class="sxs-lookup"><span data-stu-id="71d1e-199">SelectParameters</span></span>

<span data-ttu-id="71d1e-200">返回与 SqlDataSource 控件关联的 SqlDataSource 对象的 SelectCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="71d1e-201">排序参数名称</span><span class="sxs-lookup"><span data-stu-id="71d1e-201">SortParameterName</span></span>

<span data-ttu-id="71d1e-202">获取或设置在排序数据源控件检索的数据时使用的存储过程参数的名称。</span><span class="sxs-lookup"><span data-stu-id="71d1e-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="71d1e-203">仅当 SelectCommandType 设置为存储过程时才有效。</span><span class="sxs-lookup"><span data-stu-id="71d1e-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="71d1e-204">SqlCache 依赖性</span><span class="sxs-lookup"><span data-stu-id="71d1e-204">SqlCacheDependency</span></span>

<span data-ttu-id="71d1e-205">指定 SQL Server 缓存依赖项中使用的数据库和表的分号分隔字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="71d1e-206">（SQL 缓存依赖项将在后面的模块中讨论。</span><span class="sxs-lookup"><span data-stu-id="71d1e-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="71d1e-207">更新命令</span><span class="sxs-lookup"><span data-stu-id="71d1e-207">UpdateCommand</span></span>

<span data-ttu-id="71d1e-208">设置或获取更新数据库中的数据时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="71d1e-209">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="71d1e-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="71d1e-210">更新命令类型</span><span class="sxs-lookup"><span data-stu-id="71d1e-210">UpdateCommandType</span></span>

<span data-ttu-id="71d1e-211">设置或获取更新命令的类型，SQL 查询（文本）或存储过程（存储过程）。</span><span class="sxs-lookup"><span data-stu-id="71d1e-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="71d1e-212">更新参数</span><span class="sxs-lookup"><span data-stu-id="71d1e-212">UpdateParameters</span></span>

<span data-ttu-id="71d1e-213">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 UpdateCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="71d1e-214">访问数据源控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-214">The AccessDataSource Control</span></span>

<span data-ttu-id="71d1e-215">AccessDataSource 控件派生自 SqlDataSource 类，用于将数据绑定到 Microsoft Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="71d1e-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="71d1e-216">AccessDataSource 控件的 ConnectString 属性是只读属性。</span><span class="sxs-lookup"><span data-stu-id="71d1e-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="71d1e-217">DataFile 属性使用"连接字符串"属性，而不是使用 ConnectString 属性来指向访问数据库，如下所示。</span><span class="sxs-lookup"><span data-stu-id="71d1e-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="71d1e-218">AccessDataSource 将始终将基本 SqlDataSource 的提供程序名称设置为系统.Data.OleDb，并使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供程序连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="71d1e-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="71d1e-219">不能使用 AccessDataSource 控件连接到受密码保护的访问数据库。</span><span class="sxs-lookup"><span data-stu-id="71d1e-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="71d1e-220">如果必须连接到受密码保护的数据库，则应使用 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="71d1e-221">存储在网站中的访问数据库应放在应用\_数据目录中。</span><span class="sxs-lookup"><span data-stu-id="71d1e-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="71d1e-222">ASP.NET不允许浏览此目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="71d1e-223">使用 Access 数据库时，您需要向应用\_数据目录授予进程帐户"读取和写入"权限。</span><span class="sxs-lookup"><span data-stu-id="71d1e-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>

## <a name="the-xmldatasource-control"></a><span data-ttu-id="71d1e-224">XmlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-224">The XmlDataSource Control</span></span>

<span data-ttu-id="71d1e-225">XmlDataSource 用于将数据绑定 XML 数据到数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="71d1e-226">您可以使用 DataFile 属性绑定到 XML 文件，也可以使用 Data 属性绑定到 XML 字符串。</span><span class="sxs-lookup"><span data-stu-id="71d1e-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="71d1e-227">XmlDataSource 将 XML 属性公开为可绑定字段。</span><span class="sxs-lookup"><span data-stu-id="71d1e-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="71d1e-228">如果需要绑定到未表示为属性的值，则需要使用 XSL 转换。</span><span class="sxs-lookup"><span data-stu-id="71d1e-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="71d1e-229">您还可以使用 XPath 表达式来筛选 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="71d1e-230">请考虑以下 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="71d1e-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="71d1e-231">请注意，XmlDataSource 使用*人员/人员*的 XPath 属性来仅对&lt;人员&gt;节点进行筛选。</span><span class="sxs-lookup"><span data-stu-id="71d1e-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="71d1e-232">然后，使用 DataTextField 属性将数据绑定到姓氏属性。</span><span class="sxs-lookup"><span data-stu-id="71d1e-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="71d1e-233">虽然 XmlDataSource 控件主要用于将数据绑定到只读的 XML 数据，但可以编辑 XML 数据文件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="71d1e-234">请注意，在这种情况下，自动插入、更新和删除 XML 文件中的信息不会像在其他数据源控件中那样自动发生。</span><span class="sxs-lookup"><span data-stu-id="71d1e-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="71d1e-235">相反，您必须编写代码才能使用 XmlDataSource 控件的以下方法手动编辑数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="71d1e-236">获取Xml文档</span><span class="sxs-lookup"><span data-stu-id="71d1e-236">GetXmlDocument</span></span>

<span data-ttu-id="71d1e-237">检索包含 XmlDataSource 检索的 XML 代码的 XmlDocument 对象。</span><span class="sxs-lookup"><span data-stu-id="71d1e-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="71d1e-238">保存</span><span class="sxs-lookup"><span data-stu-id="71d1e-238">Save</span></span>

<span data-ttu-id="71d1e-239">将内存中的 XmlDocument 保存回数据源。</span><span class="sxs-lookup"><span data-stu-id="71d1e-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="71d1e-240">请务必了解，仅满足以下两个条件时，Save 方法才能工作：</span><span class="sxs-lookup"><span data-stu-id="71d1e-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="71d1e-241">XmlDataSource 正在使用 DataFile 属性绑定到 XML 文件，而不是数据属性以绑定到内存中的 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="71d1e-242">不会通过"转换"或"转换文件"属性指定转换。</span><span class="sxs-lookup"><span data-stu-id="71d1e-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="71d1e-243">另请注意，当多个用户同时调用 Save 方法时，可能会产生意外的结果。</span><span class="sxs-lookup"><span data-stu-id="71d1e-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="71d1e-244">对象数据源控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="71d1e-245">对于数据源控件直接与数据存储通信的两层应用程序而言，我们覆盖的数据源控件是绝佳的选择。</span><span class="sxs-lookup"><span data-stu-id="71d1e-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="71d1e-246">但是，许多实际应用程序是多层应用程序，其中数据源控件可能需要与业务对象通信，而业务对象又与数据层通信。</span><span class="sxs-lookup"><span data-stu-id="71d1e-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="71d1e-247">在这些情况下，ObjectDataSource 很好地填充了帐单。</span><span class="sxs-lookup"><span data-stu-id="71d1e-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="71d1e-248">ObjectDataSource 与源对象结合使用。</span><span class="sxs-lookup"><span data-stu-id="71d1e-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="71d1e-249">如果对象具有实例方法而不是静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将创建源对象的实例，调用指定的方法，并释放对象实例。</span><span class="sxs-lookup"><span data-stu-id="71d1e-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="71d1e-250">因此，对象必须是无状态的。</span><span class="sxs-lookup"><span data-stu-id="71d1e-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="71d1e-251">也就是说，对象应在单个请求的范围内获取和释放所有必需的资源。</span><span class="sxs-lookup"><span data-stu-id="71d1e-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="71d1e-252">您可以通过处理 ObjectDataSource 控件的对象创建事件来控制源对象的创建方式。</span><span class="sxs-lookup"><span data-stu-id="71d1e-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="71d1e-253">您可以创建源对象的实例，然后将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。</span><span class="sxs-lookup"><span data-stu-id="71d1e-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="71d1e-254">ObjectDataSource 控件将使用在对象创建事件中创建的实例，而不是自行创建实例。</span><span class="sxs-lookup"><span data-stu-id="71d1e-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="71d1e-255">如果 ObjectDataSource 控件的源对象公开可调用以检索和修改数据的公共静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将直接调用这些方法。</span><span class="sxs-lookup"><span data-stu-id="71d1e-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="71d1e-256">如果 ObjectDataSource 控件必须创建源对象的实例才能进行方法调用，则该对象必须包括一个不采用任何参数的公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="71d1e-257">当 ObjectDataSource 控件创建源对象的新实例时，它将调用此构造函数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="71d1e-258">如果源对象不包含没有参数的公共构造函数，则可以创建源对象的实例，该实例将由 ObjectDataSource 控件在 ObjectCreate 事件中使用。</span><span class="sxs-lookup"><span data-stu-id="71d1e-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="71d1e-259">指定对象方法</span><span class="sxs-lookup"><span data-stu-id="71d1e-259">Specifying Object Methods</span></span>

<span data-ttu-id="71d1e-260">ObjectDataSource 控件的源对象可以包含任意数量的用于选择、插入、更新或删除数据的方法。</span><span class="sxs-lookup"><span data-stu-id="71d1e-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="71d1e-261">这些方法由基于方法名称的 ObjectDataSource 控件调用，使用 ObjectDataSource 控件的 SelectMethod、插入方法、更新方法或 DeleteMethod 属性标识。</span><span class="sxs-lookup"><span data-stu-id="71d1e-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="71d1e-262">源对象还可以包括可选的 SelectCount 方法，该方法由使用 SelectCountMethod 属性的 ObjectDataSource 控件标识，该方法返回数据源中对象总数的计数。</span><span class="sxs-lookup"><span data-stu-id="71d1e-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="71d1e-263">在调用 Select 方法以检索数据源中用于分页时的记录总数后，ObjectDataSource 控件将调用 SelectCount 方法。</span><span class="sxs-lookup"><span data-stu-id="71d1e-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="71d1e-264">使用数据源控件的实验室</span><span class="sxs-lookup"><span data-stu-id="71d1e-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="71d1e-265">练习 1 - 使用 SqlDataSource 控件显示数据</span><span class="sxs-lookup"><span data-stu-id="71d1e-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="71d1e-266">以下练习使用 SqlDataSource 控件连接到北风数据库。</span><span class="sxs-lookup"><span data-stu-id="71d1e-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="71d1e-267">它假定您可以访问 SQL Server 2000 实例上的北风数据库。</span><span class="sxs-lookup"><span data-stu-id="71d1e-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="71d1e-268">创建新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="71d1e-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="71d1e-269">添加新的 Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="71d1e-270">右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="71d1e-271">从模板列表中选择 Web 配置文件，然后单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="71d1e-272">编辑&lt;连接字符串&gt;部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71d1e-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="71d1e-273">切换到代码视图，并将连接String 属性和 SelectCommand 属性添加到&lt;asp：SqlDataSource&gt;控件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71d1e-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="71d1e-274">从"设计"视图中，添加新的 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="71d1e-275">从 GridView 任务菜单中的"选择数据源"下拉列表，选择 SqlDataSource1。</span><span class="sxs-lookup"><span data-stu-id="71d1e-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="71d1e-276">右键单击 Default.aspx，然后从菜单中选择"在浏览器中查看"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="71d1e-277">当提示保存时，单击"是"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="71d1e-278">GridView 显示"产品"表中的数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="71d1e-279">练习 2 - 使用 SqlDataSource 控件编辑数据</span><span class="sxs-lookup"><span data-stu-id="71d1e-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="71d1e-280">下面的练习演示如何使用声明性语法对下拉列表控件进行数据绑定，并允许您编辑下拉列表控件中显示的数据。</span><span class="sxs-lookup"><span data-stu-id="71d1e-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="71d1e-281">在"设计"视图中，从 Default.aspx 中删除 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="71d1e-282">**重要提示**：将 SqlDataSource 控件保留在页面上。</span><span class="sxs-lookup"><span data-stu-id="71d1e-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="71d1e-283">将下拉列表控件添加到 Default.aspx。</span><span class="sxs-lookup"><span data-stu-id="71d1e-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="71d1e-284">切换到源视图。</span><span class="sxs-lookup"><span data-stu-id="71d1e-284">Switch to Source view.</span></span>
4. <span data-ttu-id="71d1e-285">将 DataSourceId、数据文本字段和 DataValueField 属性添加到&lt;asp：下拉&gt;列表控件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71d1e-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="71d1e-286">保存默认.aspx 并在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="71d1e-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="71d1e-287">请注意，下拉列表包含来自北风数据库的所有产品。</span><span class="sxs-lookup"><span data-stu-id="71d1e-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="71d1e-288">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="71d1e-288">Close the browser.</span></span>
7. <span data-ttu-id="71d1e-289">在 Default.aspx 的源视图中，在下拉列表控件下方添加新的 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="71d1e-290">将 TextBox 的 ID 属性更改为 txtProduct 名称。</span><span class="sxs-lookup"><span data-stu-id="71d1e-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="71d1e-291">在"文本框"控件下，添加新的"按钮"控件。</span><span class="sxs-lookup"><span data-stu-id="71d1e-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="71d1e-292">将按钮的 ID 属性更改为 btnUpdate，将文本属性更改为 **"更新产品名称**"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="71d1e-293">在 Default.aspx 的源视图中，向 SqlDataSource 标记添加 UpdateCommand 属性和两个新的 Update 参数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71d1e-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="71d1e-294">请注意，此代码中添加了两个更新参数（产品名称和产品 ID）。</span><span class="sxs-lookup"><span data-stu-id="71d1e-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="71d1e-295">这些参数映射到 txtProduct 名称文本框的文本属性和 ddlProducts 下拉列表的"选定值"属性。</span><span class="sxs-lookup"><span data-stu-id="71d1e-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="71d1e-296">切换到"设计"视图并双击"按钮"控件以添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="71d1e-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="71d1e-297">将以下代码添加到 btnUpdate\_单击代码：</span><span class="sxs-lookup"><span data-stu-id="71d1e-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="71d1e-298">右键单击 Default.aspx 并选择在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="71d1e-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="71d1e-299">当提示保存所有更改时，单击"是"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="71d1e-300">ASP.NET 2.0 部分类允许在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="71d1e-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="71d1e-301">无需构建应用程序，以便看到代码更改生效。</span><span class="sxs-lookup"><span data-stu-id="71d1e-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="71d1e-302">从下拉列表中选择产品。</span><span class="sxs-lookup"><span data-stu-id="71d1e-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="71d1e-303">在 TextBox 中输入所选产品的新名称，然后单击"更新"按钮。</span><span class="sxs-lookup"><span data-stu-id="71d1e-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="71d1e-304">产品名称在数据库中更新。</span><span class="sxs-lookup"><span data-stu-id="71d1e-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="71d1e-305">练习 3 使用对象数据源控件</span><span class="sxs-lookup"><span data-stu-id="71d1e-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="71d1e-306">本练习将演示如何使用 ObjectDataSource 控件和源对象与 Northwind 数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="71d1e-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="71d1e-307">右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="71d1e-308">在模板列表中选择"Web 窗体"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="71d1e-309">将名称更改为对象.aspx，然后单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="71d1e-310">右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="71d1e-311">在模板列表中选择类。</span><span class="sxs-lookup"><span data-stu-id="71d1e-311">Select Class in the templates list.</span></span> <span data-ttu-id="71d1e-312">将类的名称更改为NorthwindData.cs，然后单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="71d1e-313">当提示将类添加到应用\_代码文件夹时，单击"是"。</span><span class="sxs-lookup"><span data-stu-id="71d1e-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="71d1e-314">将以下代码添加到NorthwindData.cs文件：</span><span class="sxs-lookup"><span data-stu-id="71d1e-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="71d1e-315">将以下代码添加到对象的"源"视图.</span><span class="sxs-lookup"><span data-stu-id="71d1e-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="71d1e-316">保存所有文件和浏览对象.aspx。</span><span class="sxs-lookup"><span data-stu-id="71d1e-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="71d1e-317">通过查看详细信息、编辑员工、添加员工和删除员工与界面进行交互。</span><span class="sxs-lookup"><span data-stu-id="71d1e-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>

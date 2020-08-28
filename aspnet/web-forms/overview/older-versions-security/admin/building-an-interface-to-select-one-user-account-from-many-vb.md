---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 生成接口以从许多 (VB) 中选择一个用户帐户 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将使用分页的可筛选网格生成一个用户界面。 具体而言，我们的用户界面将包含一系列的 LinkButtons .。。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044579"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>生成用于从多个用户帐户中选择一个帐户的界面 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) 或 [下载 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 在本教程中，我们将使用分页的可筛选网格生成一个用户界面。 具体而言，我们的用户界面将包含一系列 LinkButtons，用于根据用户名的开始字母筛选结果，并包含一个用于显示匹配用户的 GridView 控件。 首先，在 GridView 中列出所有用户帐户。 然后，在步骤3中，将添加筛选器 LinkButtons。 步骤4查看分页的筛选结果。 在后续教程中，将使用步骤2到4中构造的接口来执行特定用户帐户的管理任务。

## <a name="introduction"></a>简介

在将 <a id="_msoanchor_1"></a> [*角色分配给用户*](../roles/assigning-roles-to-users-vb.md)教程教程中，我们为管理员创建了一个基本界面，用于选择用户和管理其角色。 具体而言，接口显示了管理员，其中包含所有用户的下拉列表。 此类接口适用于具有数百个或个用户帐户的，但对于具有数百个或数千个帐户的站点很难。 对于具有大型用户群的网站而言，页面上的可筛选网格是更适合的用户界面。

在本教程中，我们将构建此类用户界面。 具体而言，我们的用户界面将包含一系列 LinkButtons，用于根据用户名的开始字母筛选结果，并包含一个用于显示匹配用户的 GridView 控件。 首先，在 GridView 中列出所有用户帐户。 然后，在步骤3中，将添加筛选器 LinkButtons。 步骤4查看分页的筛选结果。 在后续教程中，将使用步骤2到4中构造的接口来执行特定用户帐户的管理任务。

让我们开始吧！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤1：添加新的 ASP.NET 页面

在本教程和接下来的两个教程中，我们将检查各种与管理相关的功能。 我们将需要一系列 ASP.NET 页面来实现这些教程中所讨论的主题。 让我们创建这些页面并更新站点图。

首先，在项目中创建一个名为的新文件夹 `Administration` 。 接下来，将两个新的 ASP.NET 页面添加到该文件夹，并将每个页面与母版页链接在一起 `Site.master` 。 命名页面：

- `ManageUsers.aspx`
- `UserInformation.aspx`

同时将两个页面添加到网站的根目录： `ChangePassword.aspx` 和 `RecoverPassword.aspx` 。

此时，这四个页面都应具有两个内容控件，每个控件分别对应于母版页的每个 Contentplaceholder： `MainContent` 和 `LoginContent` 。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

我们想要为这些页面显示 ContentPlaceHolder 的母版页默认标记 `LoginContent` 。 因此，删除内容控件的声明性标记 `Content2` 。 完成此操作后，页面的标记应该只包含一个内容控件。

文件夹中的 ASP.NET 页 `Administration` 仅适用于管理用户。 我们已在创建和管理角色教程中将管理员角色添加到系统中; 请将这 <a id="_msoanchor_2"></a> [*Creating and Managing Roles*](../roles/creating-and-managing-roles-vb.md)两个页面的访问权限限制为此角色。 若要实现此目的，请将 `Web.config` 文件添加到 `Administration` 文件夹中，并将其 `<authorization>` 元素配置为承认管理员角色中的用户并拒绝所有其他用户。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

此时，项目的解决方案资源管理器应类似于图1所示的屏幕截图。

[![网站中添加了四个新页面和一个 Web.config 文件](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**图 1**：四个新页面和一个 `Web.config` 文件已添加到网站 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png)) 

最后， () 更新站点图， `Web.sitemap` 以在页面中包含一项 `ManageUsers.aspx` 。 在为角色教程添加后，添加以下 XML `<siteMapNode>` 。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

更新站点地图后，通过浏览器访问站点。 如图2所示，左侧的导航包含管理教程中的项。

[![网站图包含标题为 "用户管理" 的节点](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**图 2**：网站图包含标题为 "用户管理" 的节点 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png)) 

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>步骤2：在 GridView 中列出所有用户帐户

本教程的最终目标是创建一个分页、可筛选的网格，管理员可通过该网格选择要管理的用户帐户。 首先，让我们以 GridView 列出 *所有* 用户。 完成此功能后，我们将添加筛选和分页界面和功能。

打开 `ManageUsers.aspx` 该文件夹中的页面， `Administration` 然后添加一个 GridView，稍后将其设置 `ID` 为 `UserAccounts` ，我们将使用 `Membership` 类的方法编写代码以将用户帐户集绑定到 GridView `GetAllUsers` 。 如前面的教程中所述， `GetAllUsers` 方法返回 `MembershipUserCollection` 对象，该对象是对象的集合 `MembershipUser` 。 `MembershipUser`集合中的每个都包括 `UserName` 、、等属性 `Email` `IsApproved` 。

为了在 GridView 中显示所需的用户帐户信息，请将 GridView 的属性设置为 False，并为、和属性 `AutoGenerateColumns` 添加 BoundFields，并 `UserName` `Email` `Comment` 为、和 `IsApproved` `IsLockedOut` 属性添加 CheckBoxFields `IsOnline` 。 此配置可通过控件的声明性标记或通过 "字段" 对话框应用。 图3显示 "字段" 对话框的屏幕截图，在 "自动生成字段" 复选框未选中并且已添加并配置 BoundFields 和 CheckBoxFields 之后。

[![向 GridView 添加三个 BoundFields 和三个 CheckBoxFields](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**图 3**：向 GridView 添加三个 BoundFields 和三个 CheckBoxFields ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png)) 

配置 GridView 后，请确保其声明性标记类似于以下内容：

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

接下来，我们需要编写代码将用户帐户绑定到 GridView。 创建一个名为的方法 `BindUserAccounts` 来执行此任务，然后从 `Page_Load` 第一页上的事件处理程序调用它。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

花点时间通过浏览器测试页面。 如图4所示， `UserAccounts` GridView 列出系统中所有用户的用户名、电子邮件地址和其他相关帐户信息。

[![用户帐户在 GridView 中列出](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**图 4**：用户帐户列在 GridView 中 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png)) 

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>步骤3：按用户名的第一个字母筛选结果

当前 `UserAccounts` GridView 显示 *所有* 用户帐户。 对于具有数百个或数千个用户帐户的网站，用户可以快速削减显示的帐户。 这可以通过将筛选 LinkButtons 添加到页面来实现。 让我们将 27 LinkButtons 添加到页面：其中一个标题与字母表中每个字母的一个 LinkButton 一起。 如果访问者单击 "所有 LinkButton"，则 GridView 将显示所有用户。 如果他们单击特定的字母，将只显示用户名以选定字母开头的用户。

我们的第一个任务是添加27个 LinkButton 控件。 一种选择是以声明方式创建 27 LinkButtons，一次一个。 一种更灵活的方法是将 Repeater 控件与 `ItemTemplate` 呈现 LinkButton 的一起使用，然后将筛选选项作为数组绑定到中继器 `String` 。

首先将 Repeater 控件添加到 GridView 之上的页面 `UserAccounts` 。 设置 Repeater 的 `ID` 属性以 `FilteringUI` 配置 repeater 的模板，使其 `ItemTemplate` 呈现 LinkButton `Text` ，其和 `CommandName` 属性绑定到当前数组元素。 正如我们 <a id="_msoanchor_3"></a> [*向用户分配角色*](../roles/assigning-roles-to-users-vb.md)教程中所述，可以使用 `Container.DataItem` 数据绑定语法完成此操作。 使用中继器在 `SeparatorTemplate` 每个链接之间显示竖线。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

若要使用所需的筛选选项填充此中继器，请创建一个名为的方法 `BindFilteringUI` 。 请确保 `Page_Load` 在第一页加载时从事件处理程序调用此方法。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

此方法将筛选选项指定为 `String` 数组中每个元素的数组中的元素 `filterOptions` ，Repeater 将呈现一个 LinkButton，并将其 `Text` 和 `CommandName` 属性分配给数组元素的值。

图5显示了 `ManageUsers.aspx` 通过浏览器查看的页面。

[![中继器列表27筛选 LinkButtons](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**图 5**：中继器列表27筛选 LinkButtons ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png)) 

> [!NOTE]
> 用户名可以以任意字符（包括数字和标点符号）开头。 若要查看这些帐户，管理员必须使用 All LinkButton 选项。 或者，你可以添加 LinkButton 以返回以数字开头的所有用户帐户。 我将此留给读者的练习。

单击任意筛选 LinkButtons 将导致回发并引发中继器 `ItemCommand` 事件，但在网格中没有更改，因为我们尚未编写任何代码来筛选结果。 `Membership`类包含一个[ `FindUsersByName` 方法](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)，该方法返回用户名与指定的搜索模式匹配的用户帐户。 我们可以使用此方法只检索其用户名以所单击的筛选 LinkButton 的所指定的字母开头的那些用户帐户 `CommandName` 。

首先更新 `ManageUser.aspx` 页面的代码隐藏类，使其包含一个名为 "此属性" 的属性，并在每个 `UsernameToMatch` 回发期间保持用户名筛选器字符串：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch`属性将 `ViewState` 使用键 "UsernameToMatch" 将其分配给集合的值。 当读取此属性的值时，它会检查集合中是否存在值 `ViewState` ; 如果不存在，则返回默认值（空字符串）。 `UsernameToMatch`属性显示一种常见模式，即保持值以查看状态，以便在回发之间保留对属性所做的任何更改。 有关此模式的详细信息，请阅读 [了解 ASP.NET 视图状态](https://msdn.microsoftn-us/library/ms972976.aspx)。

接下来，更新 `BindUserAccounts` 方法，使其调用，而不是调用，并 `Membership.GetAllUsers` `Membership.FindUsersByName` 传入 `UsernameToMatch` 附加了 SQL 通配符% 的属性的值。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

若要只显示用户名以字母 A 开头的用户，请将 `UsernameToMatch` 属性设置为，然后调用 `BindUserAccounts` 这会导致调用 `Membership.FindUsersByName("A%")` ，这将返回用户名以开头的所有用户。同样，若要返回 *所有* 用户，请为属性分配一个空字符串， `UsernameToMatch` 以便 `BindUserAccounts` 方法将调用 `Membership.FindUsersByName("%")` ，从而返回所有用户帐户。

为中继器事件创建事件处理程序 `ItemCommand` 。 单击其中一个筛选器 LinkButtons 时，将引发此事件。它通过对象传递被单击 LinkButton 的 `CommandName` 值 `RepeaterCommandEventArgs` 。 需要为属性分配适当的值 `UsernameToMatch` ，然后调用 `BindUserAccounts` 方法。 如果 `CommandName` 为 all，则将空字符串分配给， `UsernameToMatch` 以便显示所有用户帐户。 否则，将 `CommandName` 值分配给 `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

执行此代码后，请测试筛选功能。 第一次访问该页面时，将显示所有用户帐户 (请参阅图 5) 。 单击 LinkButton 将导致回发并筛选结果，只显示以开头的用户帐户。

[![使用筛选 LinkButtons 显示用户名以特定字母开头的用户](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**图 6**：使用筛选 LinkButtons 显示用户名以特定字母开头的用户 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png)) 

## <a name="step-4-updating-the-gridview-to-use-paging"></a>步骤4：更新 GridView 以使用分页

图5和6中所示的 GridView 列出了从方法返回的所有记录 `FindUsersByName` 。 如果有数百或数千个用户帐户，则在查看所有帐户时，这可能会导致信息重载 (在单击 "所有 LinkButton" 或最初访问页面时) 。 为了帮助在更易于管理的区块中显示用户帐户，我们将 GridView 配置为每次显示10个用户帐户。

GridView 控件提供两种类型的分页：

- **默认分页** -易于实现，但效率低下。 简而言之，使用默认分页时，GridView 需要其数据源中的 *所有* 记录。 然后，它仅显示适当的记录页。
- **自定义分页** -需要执行更多工作，但比默认分页更高效，因为使用自定义分页时，数据源仅返回要显示的精确记录集。

在通过成千上万条记录进行分页时，默认分页和自定义分页之间的性能差异可能非常大。 由于我们要构建此接口，假设可能有成百上千的用户帐户，我们使用自定义分页。

> [!NOTE]
> 若要深入了解默认和自定义分页之间的差异，以及实现自定义分页时所涉及的挑战，请参阅 [通过大量数据有效分页](https://asp.net/learn/data-access/tutorial-25-vb.aspx)。 有关默认和自定义分页之间性能差异的一些分析，请参阅 [ASP.NET 中的自定义分页 SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)。

若要实现自定义分页，我们首先需要一些机制，通过该机制检索 GridView 显示的精确记录子集。 好消息是， `Membership` 类的 `FindUsersByName` 方法具有一个重载，使我们能够指定页索引和页大小，并仅返回属于该记录范围内的用户帐户。

具体而言，此重载具有以下签名： [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) 。

*PageIndex*参数指定要返回的用户帐户的页;*pageSize*指示每页显示的记录数。 *TotalRecords*参数是一个 `ByRef` 参数，该参数返回用户存储中的用户帐户总数。

> [!NOTE]
> 返回的数据按 `FindUsersByName` 用户名排序; 无法自定义排序条件。

GridView 可以配置为使用自定义分页，但仅在绑定到 ObjectDataSource 控件时使用。 为了使 ObjectDataSource 控件实现自定义分页，它需要两个方法：一个传递起始行索引和要显示的最大记录数，并返回位于该范围内的精确记录子集;返回要分页到的记录总数的方法。 `FindUsersByName`重载接受页索引和页大小，并通过参数返回记录总数 `ByRef` 。 因此此处的接口不匹配。

一种选择是创建一个代理类，该类公开 ObjectDataSource 需要的接口，然后在内部调用 `FindUsersByName` 方法。 另一种方法是，我们将在本文中使用的另一种方法是创建自己的分页接口，并使用它来代替 GridView 的内置分页接口。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>创建第一个、上一个、下一个、上一个寻呼接口

让我们使用第一个、上一个、下一个和最后一个 LinkButtons 生成分页接口。 单击第一个 LinkButton 时，会将用户转到第一个数据页，而上一页将把他返回到上一页。 同样，"下一步" 和 "最后一个" 将分别将用户移动到下一页和最后一页。 在 GridView 下面添加四个 LinkButton 控件 `UserAccounts` 。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

接下来，为 LinkButton 的每个事件创建一个事件处理程序 `Click` 。

图7显示了通过 Visual Web Developer 设计视图查看的四个 LinkButtons。

[![在 GridView 下面添加 First、Previous、Next 和 Last LinkButtons](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**图 7**：在 GridView 下面添加第一个、上一个、下一个和最后一个 LinkButtons ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png)) 

### <a name="keeping-track-of-the-current-page-index"></a>跟踪当前页索引

当用户首次访问 `ManageUsers.aspx` 页面或单击其中一个筛选按钮时，我们希望在 GridView 中显示数据的第一页。 但是，当用户单击其中一个导航 LinkButtons 时，我们需要更新页面索引。 若要维护页索引和每页显示的记录数，请将以下两个属性添加到该页的代码隐藏类：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

与 `UsernameToMatch` 属性一样，属性会将 `PageIndex` 其值保持为视图状态。 只读 `PageSize` 属性返回硬编码值10。 我邀请感兴趣的读者更新此属性以使用与相同的模式 `PageIndex` ，然后再增加页面，以便 `ManageUsers.aspx` 访问页面的人员可以指定要在每页上显示多少个用户帐户。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>仅检索当前页的记录、更新页索引以及启用和禁用分页接口 LinkButtons

使用分页接口并 `PageIndex` 添加了和 `PageSize` 属性后，我们就可以更新 `BindUserAccounts` 方法，使其使用适当的 `FindUsersByName` 重载。 此外，我们还需要启用或禁用分页接口，具体取决于所显示的页面。 查看第一页数据时，应禁用第一个和前一个链接;查看最后一页时，应禁用 "下一步" 和 "最后一个"。

使用以下代码更新 `BindUserAccounts` 方法：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

请注意，要分页到的记录总数由方法的最后一个参数决定 `FindUsersByName` 。 返回用户帐户的指定页面后，将启用或禁用这四个 LinkButtons，具体取决于是否正在查看第一个或最后一个数据页。

最后一步是为四个 LinkButtons 的 `Click` 事件处理程序编写代码。 这些事件处理程序需要更新 `PageIndex` 属性，然后通过调用 `BindUserAccounts` 第一个、上一个和下一个事件处理程序来将数据重新绑定到 GridView。 `Click`不过，最后 LinkButton 的事件处理程序有点复杂，因为我们需要确定要显示的记录数，以便确定最后一页的索引。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

图8和9显示了操作中的自定义分页接口。 图8显示了 `ManageUsers.aspx` 查看所有用户帐户的第一页数据的页面。 请注意，只显示13个帐户中的10个。 单击 "下一步" 或 "最后一个链接" 将导致回发，将更新 `PageIndex` 为1，并将用户帐户的第二页绑定到网格 (参见图 9) 。

[![显示前10个用户帐户](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**图 8**：显示前10个用户帐户 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png)) 

[![单击 "下一步" 链接将显示用户帐户的第二页](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**图 9**：单击 "下一步" 链接将显示用户帐户的第二页 ([单击查看全尺寸图像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png)) 

## <a name="summary"></a>摘要

管理员通常需要从帐户列表中选择一个用户。 在前面的教程中，我们介绍了如何使用以用户填充的下拉列表，但此方法不能很好地进行缩放。 在本教程中，我们探讨了更好的替代方法：其结果显示在分页 GridView 中的可筛选接口。 利用此用户界面，管理员可以快速高效地查找和选择数千个用户帐户。

很高兴编程！

### <a name="further-reading"></a>深入阅读

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 中的自定义分页 SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [通过大量数据有效分页](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在上 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 或通过他的博客访问 Scott [http://ScottOnWriting.NET](http://scottonwriting.net/) 。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Alicja Maziarz。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在

> [!div class="step-by-step"]
> [上一页](unlocking-and-approving-user-accounts-cs.md)
> [下一页](recovering-and-changing-passwords-vb.md)

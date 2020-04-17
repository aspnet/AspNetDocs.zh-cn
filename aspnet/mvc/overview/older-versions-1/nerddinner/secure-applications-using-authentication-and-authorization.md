---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权的安全应用程序 |微软文档
author: rick-anderson
description: 步骤 9 演示如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站以创建...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542568"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>使用身份验证和授权保护应用程序

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第9步，该教程演示如何使用mVC 1 构建小型但完整的 Web 应用程序ASP.NET。
> 
> 步骤 9 演示如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站以创建新的晚餐，并且只有主持晚宴的用户才能稍后对其进行编辑。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>神经晚餐步骤 9：身份验证和授权

现在，我们的NerdDinner应用程序允许任何访问该网站的人能够创建和编辑任何晚餐的细节。 让我们更改此内容，以便用户需要注册并登录到网站以创建新的晚餐，并添加限制，以便只有主持晚宴的用户才能稍后对其进行编辑。

为了启用此功能，我们将使用身份验证和授权来保护我们的应用程序。

### <a name="understanding-authentication-and-authorization"></a>了解身份验证和授权

*身份验证*是标识和验证访问应用程序的客户端的标识的过程。 简单地说，它是关于确定最终用户在访问网站时的"谁"。 ASP.NET支持对浏览器用户进行身份验证的多种方法。 对于 Internet Web 应用程序，最常用的身份验证方法称为"表单身份验证"。 窗体身份验证使开发人员能够在其应用程序中创作 HTML 登录表单，然后根据数据库或其他密码凭据存储验证最终用户提交的用户名/密码。 如果用户名/密码组合正确，开发人员可以请求ASP.NET发出加密的 HTTP Cookie，以识别用户在未来的请求。 我们将使用表单身份验证来使用我们的 NerdDinner 应用程序。

*授权*是确定经过身份验证的用户是否具有访问特定 URL/资源或执行某些操作的权限的过程。 例如，在我们的 NerdDinner 应用程序中，我们希望授权只有登录的用户才能访问 */Dinners/创建*URL 并创建新的晚餐。 我们还希望添加授权逻辑，以便只有主持晚宴的用户才能对其进行编辑，并拒绝对所有其他用户进行编辑访问。

### <a name="forms-authentication-and-the-accountcontroller"></a>窗体身份验证和帐户控制器

ASP.NET MVC 的默认 Visual Studio 项目模板在创建新ASP.NET MVC 应用程序时自动启用表单身份验证。 它还会自动向项目添加预构建的帐户登录页实现，从而在站点中集成安全性非常容易。

默认的 Site.master 页在网站右上角显示"登录"链接，当用户访问该网站时未进行身份验证：

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

单击"登录"链接会将用户带到 */帐户/登录*URL：

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

尚未注册的访问者可以通过单击"注册"链接（该链接将他们带到 */帐户/注册*URL）并允许您输入帐户详细信息来执行此操作：

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

单击"注册"按钮将在ASP.NET成员资格系统中创建新用户，并使用表单身份验证对用户进行身份验证。

当用户登录时，Site.master 会更改页面的右上角以输出"欢迎 [用户名]！ 消息并呈现"注销"链接，而不是"登录"链接。 单击"注销"链接会注销用户：

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上述登录、注销和注册功能在帐户控制器类中实现，该类在创建项目时由 Visual Studio 添加到我们的项目中。 帐户控制器的 UI 使用 [Views_帐户目录中的视图模板] 实现：

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

帐户控制器类使用ASP.NET表单身份验证系统来发出加密的身份验证 Cookie，ASP.NET成员资格 API 来存储和验证用户名/密码。 ASP.NET成员资格 API 是可扩展的，并且允许使用任何密码凭据存储。 ASP.NET附带将用户名/密码存储在 SQL 数据库或活动目录中的内置成员资格提供程序实现。

我们可以通过打开项目根目录的"Web.config"文件并在其中查找&lt;成员资格&gt;部分来配置我们的 NerdDinner 应用程序应该使用的成员提供商。 创建项目时添加的默认 Web.config 会注册 SQL 成员资格提供程序，并将其配置为使用名为"应用程序服务"的连接字符串来指定数据库位置。

默认的"应用程序服务"连接字符串（在 Web.config &lt;&gt;文件的连接字符串部分中指定）配置为使用 SQL Express。 它指向名为"ASPNETDB"的 SQL Express 数据库。MDF"在应用程序的"应用\_数据"目录下。 如果首次在应用程序中使用成员资格 API 时此数据库不存在，ASP.NET将自动创建数据库并在其中预配适当的成员资格数据库架构：

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

如果我们不想使用 SQL Express，而是想要使用完整的 SQL Server 实例（或连接到远程数据库），我们只需更新 Web.config 文件中的"应用程序服务"连接字符串，并确保适当的成员资格架构已添加到它指向的数据库。 您可以在 [Windows_Microsoft.NET_Framework_v2.0.50727] 目录中运行"aspnet\_regsql.exe"实用程序，以将成员资格和其他ASP.NET应用程序服务的适当架构添加到数据库中。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>使用 [授权] 筛选器授权 /Dinners/创建 URL

我们不必编写任何代码来为 NerdDinner 应用程序启用安全的身份验证和帐户管理实现。 用户可以在我们的应用程序中注册新帐户，以及网站登录/注销。

现在，我们可以向应用程序添加授权逻辑，并使用访问者的身份验证状态和用户名来控制他们在网站内可以做什么和不能做什么。 让我们首先将授权逻辑添加到 DinnersController 类的"创建"操作方法。 具体来说，我们将要求访问 */Dinner/Create* URL 的用户必须登录。 如果他们没有登录，我们会将其重定向到登录页面，以便他们可以登录。

实现此逻辑非常简单。 我们只需要将 [授权] 筛选器属性添加到我们的"创建操作方法"中，如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 支持创建"操作筛选器"的能力，该筛选器可用于实现可声明应用于操作方法的可重用逻辑。 [授权] 筛选器是 ASP.NET MVC 提供的内置操作筛选器之一，它使开发人员能够声明授权规则应用于操作方法和控制器类。

在没有任何参数的情况下应用时（如上文所述），[授权] 筛选器强制必须登录执行操作方法请求的用户，如果浏览器未登录，则会自动将浏览器重定向到登录 URL。 执行此操作重定向时，最初请求的 URL 将作为查询字符串参数传递（例如：/帐户/LogOn？返回Url_%2fDinners%2f创建）。 然后，帐户控制器将在用户登录后将用户重定向回最初请求的 URL。

[授权] 筛选器可以选择支持指定"用户"或"角色"属性的能力，该属性可用于要求用户同时登录并登录允许的用户或允许的安全角色的成员列表中。 例如，下面的代码只允许两个特定用户"scottgu"和"billg"访问 /Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

不过，在代码中嵌入特定的用户名往往非常无法维护。 更好的方法是定义代码所针对的更高级别的"角色"，然后使用数据库或活动目录系统将用户映射到角色（使实际用户映射列表能够从代码外部存储）。 ASP.NET包括内置角色管理 API 以及一组内置角色提供程序（包括 SQL 和 Active Directory 的内置角色提供程序），可帮助执行此用户/角色映射。 然后，我们可以更新代码，仅允许特定"管理员"角色中的用户访问 /Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>创建晚餐时使用User.Identity.Name属性

我们可以使用 Controller 基类上公开的User.Identity.Name属性检索请求当前登录用户的用户名。

早些时候，当我们实现我们的Create（） 操作方法的HTTP-POST版本时，我们已经将 Dinner 的"托管比"属性硬编码为静态字符串。 我们现在可以更新此代码以改用User.Identity.Name属性，并为创建 Dinner 的主机自动添加 RSVP：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

由于我们已经向 Create（） 方法添加了 [授权] 属性，因此ASP.NET MVC 可确保仅当访问 /Dinners/Create URL 的用户登录站点时，才会执行操作方法。 因此，User.Identity.Name属性值将始终包含有效的用户名。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>编辑晚餐时使用User.Identity.Name属性

现在，让我们添加一些限制用户的授权逻辑，以便他们只能编辑自己托管的晚餐的属性。

为了帮助达到这一目的，我们将首先向 Dinner 对象添加"Is托管By（用户名）"帮助器方法（在之前构建的Dinner.cs部分类中）。 此帮助程序方法返回 true 或 false，具体取决于提供的用户名是否与 Dinner 托管 By 属性匹配，并封装执行不区分大小写的字符串比较所需的逻辑：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

然后，我们将向 DinnersController 类中的 Edit（） 操作方法添加 [授权] 属性。 这将确保用户必须登录才能请求 */Dinners/Edit/[id]* URL。

然后，我们可以向使用 Dinner.IsHostBy（用户名）帮助器方法的"编辑"方法添加代码，以验证登录用户是否与 Dinner 主机匹配。 如果用户不是主机，我们将显示"无效所有者"视图并终止请求。 执行此操作的代码如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

然后，我们可以右键单击 [Views_Dinners]目录，然后选择"添加&gt;-视图"菜单命令以创建新的"无效所有者"视图。 我们将用以下错误消息填充它：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

现在，当用户尝试编辑他们不拥有的晚餐时，他们会得到一条错误消息：

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

我们可以对控制器中的 Delete（） 操作方法重复相同的步骤，以锁定删除 Dinner 的权限，并确保只有晚餐的主持人才能删除它。

### <a name="showinghiding-edit-and-delete-links"></a>显示/隐藏编辑和删除链接

我们正在从"详细信息"URL 链接到"晚餐控制器"类的编辑和删除操作方法：

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

目前，我们显示"编辑和删除"操作链接，无论详细信息 URL 的访问者是否是晚宴的东道主。 让我们更改此内容，以便仅当访问用户是晚餐的所有者时才会显示链接。

晚餐控制器中的"详细信息（）"操作方法检索 Dinner 对象，然后将其作为模型对象传递给视图模板：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

我们可以更新视图模板，以便使用"晚餐.Is托管By"（）帮助器方法有条件地显示/隐藏"编辑"和"删除"链接，如下所示：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>后续步骤

现在，让我们来看看如何启用经过身份验证的用户到RSVP的晚餐使用AJAX。

> [!div class="step-by-step"]
> [上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)

---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: 使用表单身份验证 （C#） 对用户进行身份验证 |微软文档
author: rick-anderson
description: 了解如何使用 [授权] 属性来密码保护 MVC 应用程序中的特定页面。 您也了解如何使用网站管理...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540969"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>使用 Forms 身份验证对用户进行身份验证 (C#)

由[微软](https://github.com/microsoft)

> 了解如何使用 [授权] 属性来密码保护 MVC 应用程序中的特定页面。 您将了解如何使用网站管理工具创建和管理用户和角色。 您还了解如何配置用户帐户和角色信息的存储位置。

本教程的目的是说明如何使用窗体身份验证来密码保护ASP.NET MVC 应用程序中的视图。 您将了解如何使用网站管理工具创建用户和角色。 您还学习如何防止未经授权的用户调用控制器操作。 最后，您将了解如何配置用户名和密码的存储位置。

#### <a name="using-the-web-site-administration-tool"></a>使用网站管理工具

在做其他事情之前，我们应该从创建一些用户和角色开始。 创建新用户和角色的最简单方法是利用 Visual Studio 2008 网站管理工具。 您可以通过选择菜单选项 **"项目"ASP.NET 配置**启动此工具。 或者，您可以通过单击位于解决方案资源管理器窗口顶部的锤子（有点可怕）图标启动网站管理工具（参见图 1）。

**图 1 – 启动网站管理工具**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

在网站管理工具中，您可以通过选择"安全"选项卡创建新用户和角色。单击"**创建用户**"链接以创建名为 Stephen 的新用户（参见图 2）。 向 Stephen 用户提供所需的任何密码（例如，*机密*）。

**图 2 = 创建新用户**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

通过首先启用角色和定义一个或多个角色来创建新角色。 通过单击 **"启用角色"链接启用角色**。 接下来，通过单击 **"创建或管理角色"链接创建**名为 *"管理员*"的角色（参见图 3）。

**图 3 • 创建新角色**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

最后，通过单击"创建用户"链接并在创建 Sally 时选择管理员（参见图 4），创建名为 Sally 的新用户并将 Sally 与管理员角色相关联。

**图 4 = 将用户添加到角色**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

当所有说和完成，你应该有两个新的用户叫斯蒂芬和莎莉。 您还应具有名为"管理员"的新角色。 Sally 是管理员角色的成员，而斯蒂芬不是。

#### <a name="requiring-authorization"></a>需要授权

在用户调用控制器操作之前，可以通过将 [授权] 属性添加到操作，要求用户进行身份验证。 您可以将 [授权] 属性应用于单个控制器操作，也可以将此属性应用于整个控制器类。

例如，清单 1 中的控制器公开名为"公司机密"的操作。 由于此操作使用 [授权] 属性进行修饰，因此除非对用户进行身份验证，否则无法调用此操作。

**清单1 = 控制器\主控制器.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

如果您在浏览器的地址栏中输入 URL/Home/CompanySecrets 来调用公司机密（）操作，而您不是经过身份验证的用户，则将自动重定向到登录视图（参见图 5）。

**图 5 = 登录视图**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

您可以使用"登录"视图输入用户名和密码。 如果您不是注册用户，则可以单击**注册**链接以导航到"注册"视图（参见图 6）。 您可以使用"注册"视图创建新用户帐户。

**图 6 = 寄存器视图**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

成功登录后，您可以看到公司机密视图（参见图 7）。 默认情况下，您将继续登录，直到关闭浏览器窗口。

**图 7 = 公司机密视图**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>按用户名或用户角色授权

可以使用 [授权] 属性将对控制器操作的访问限制为一组特定用户或一组特定的用户角色。 例如，清单 2 中修改后的主控制器包含名为 StephenSecrets（） 和管理员机密（） 的两个新操作。

**清单2 = 控制器\主控制器.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

只有用户名为 Stephen 的用户才能调用 StephenSecrets（） 操作。 所有其他用户都重定向到"登录"视图。 "用户"属性接受用户帐户名称的逗号分隔列表。

只有管理员角色中的用户可以调用管理员机密（） 操作。 例如，由于 Sally 是管理员组的成员，因此她可以调用管理员机密（）操作。 所有其他用户都重定向到"登录"视图。 角色属性接受角色名称的逗号分隔列表。

#### <a name="configuring-authentication"></a>配置身份验证

此时，您可能想知道用户帐户和角色信息的存储位置。 默认情况下，信息存储在 MVC 应用程序的应用程序\_数据文件夹中，名为 ASPNETDB.mdf 的 （RANU） SQL Express 数据库中。 当您开始使用成员资格时，此数据库由ASP.NET框架自动生成。

要查看解决方案资源管理器窗口中的 ASPNETDB.mdf 数据库，首先需要选择菜单选项"项目"，显示所有文件。

开发应用程序时，可以使用默认 SQL Express 数据库。 但是，您很可能不希望为生产应用程序使用默认的 ASPNETDB.mdf 数据库。 在这种情况下，您可以通过完成以下两个步骤来更改用户帐户信息的存储位置：

1. 将应用程序服务数据库对象添加到生产数据库 - 更改应用程序连接字符串以指向生产数据库

第一步是将所有必要的数据库对象（表和存储过程）添加到生产数据库中。 将这些对象添加到新数据库的最简单方法是利用ASP.NET SQL 服务器设置向导（参见图 8）。 您可以通过从 Microsoft Visual Studio 2008 程序组打开 Visual Studio 2008 命令提示符并从命令提示符执行以下命令来启动此工具：

阿斯普内\_雷格斯

**图 8 = ASP.NET SQL 服务器设置向导**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

ASP.NET SQL 服务器设置向导使您能够在网络上选择 SQL Server 数据库，并安装ASP.NET应用程序服务所需的所有数据库对象。 数据库服务器不需要位于本地计算机上。

> [!NOTE] 
> 
> 如果不想使用ASP.NET SQL 服务器设置向导，则可以在以下文件夹中找到用于添加应用程序服务数据库对象的 SQL 脚本：
> 
> > C：[视窗]微软.NET_框架_v2.0.50727

创建必要的数据库对象后，需要修改 MVC 应用程序使用的数据库连接。 修改 Web 配置 （Web.config） 文件中的应用程序服务连接字符串，以便它指向生产数据库。 例如，清单中修改的连接指向名为 MyProductionDB 的数据库（原始应用程序服务连接字符串已注释掉）。

**清单3 = Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>配置数据库权限

如果使用集成安全连接到数据库，则需要添加正确的 Windows 用户帐户作为数据库的登录。 正确的帐户取决于您是使用ASP.NET开发服务器还是 Internet 信息服务作为 Web 服务器。 正确的用户帐户还取决于您的操作系统。

如果使用ASP.NET开发服务器（Visual Studio 使用的默认 Web 服务器），则应用程序将在 Windows 用户帐户的上下文中执行。 在这种情况下，您需要将 Windows 用户帐户添加为数据库服务器登录名。

或者，如果您使用的是互联网信息服务，则需要将 ASPNET 帐户或 NT AUTHORITY/网络服务帐户添加为数据库服务器登录名。 如果使用 Windows XP，则添加 ASPNET 帐户作为数据库的登录名。 如果您使用的是较新的操作系统，如 Windows Vista 或 Windows Server 2008，则添加 NT AUTHORITY/网络服务帐户作为数据库登录。

您可以使用 Microsoft SQL 服务器管理工作室向数据库添加新用户帐户（参见图 9）。

**图 9 = 创建新的 Microsoft SQL Server 登录名**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

创建所需的登录后，需要将登录映射到具有正确数据库角色的数据库用户。 双击登录名并选择"用户映射"选项卡。选择一个或多个应用程序服务数据库角色。 例如，为了对用户进行身份验证，您需要启用 aspnet\_成员资格\_基本访问数据库角色。 要创建新用户，您需要启用 aspnet\_成员资格\_完全访问数据库角色（参见图 10）。

**图 10 = 添加应用程序服务数据库角色**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>总结

在本教程中，您学习了在构建 ASP.NET MVC 应用程序时如何使用窗体身份验证。 首先，您学习了如何通过利用网站管理工具创建新用户和角色。 接下来，您学习了如何使用 [授权] 属性来防止未经授权的用户调用控制器操作。 最后，您学习了如何配置 MVC 应用程序以在生产数据库中存储用户和角色信息。

> [!div class="step-by-step"]
> [下一页](authenticating-users-with-windows-authentication-cs.md)

---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 将现有网站从 SQL 成员身份迁移到 ASP.NET Identity-ASP.NET 4。x
author: Rick-Anderson
description: 本教程演示了将现有 web 应用程序与使用 SQL 成员身份创建的用户和角色数据迁移到新 ASP.NET Identity .。。
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 2cfab96422340acc67ebb3b11f322ae1b258575d
ms.sourcegitcommit: 6727454a30f11ac2365e1cc8a37ef0005f5d15b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96934118"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>将现有网站从 SQL 成员身份迁移到 ASP.NET Identity

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)， [Suhas Joshi](https://github.com/suhasj)

> 本教程演示了将现有 web 应用程序与使用 SQL 成员身份创建的用户和角色数据迁移到新的 ASP.NET Identity 系统的步骤。 此方法涉及将现有数据库架构更改为 ASP.NET Identity 所需的架构，并将旧的/新类中的挂钩到它。 在采用此方法之后，迁移数据库后，将会轻松地处理对标识的后续更新。

对于本教程，我们将创建一个 web 应用程序模板 (使用 Visual Studio 2010 创建用户和角色数据) 创建的 Web 窗体。 然后，将使用 SQL 脚本将现有数据库迁移到标识系统所需的表。 接下来，我们将安装所需的 NuGet 包并添加新帐户管理页面，这些页面使用标识系统进行成员资格管理。 作为迁移的测试，使用 SQL 成员身份创建的用户应能够登录，并且新用户应该能够注册。 可在[此处](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)找到完整示例。 另请参阅 [从 ASP.NET 成员身份迁移到 ASP.NET Identity](https://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity/)。

## <a name="getting-started"></a>入门

### <a name="creating-an-application-with-sql-membership"></a>创建具有 SQL 成员身份的应用程序

1. 我们需要从使用 SQL 成员身份并且具有用户和角色数据的现有应用程序开始。 本文介绍如何在 Visual Studio 2010 中创建 web 应用程序。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. 使用 ASP.NET 配置工具创建2个用户： **oldAdminUser** 和 **oldUser。**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. 创建名为 Admin 的角色，并将 "oldAdminUser" 添加为该角色中的用户。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. 使用 default.aspx 创建网站的管理员部分。 将 web.config 文件中的授权标记设置为仅允许管理员角色中的用户访问。 可在此处找到详细信息 [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. 查看服务器资源管理器中的数据库，以了解 SQL 成员资格系统创建的表。 用户登录数据存储在 aspnet \_ 用户和 aspnet \_ 成员资格表中，而角色数据存储在 aspnet \_ 角色表中。 有关哪些用户是在 aspnet UsersInRoles 表中存储哪些角色的用户的信息 \_ 。 对于基本成员资格管理，足以将上述表中的信息移植到 ASP.NET Identity 系统。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>迁移到 Visual Studio 2013

1. 为 Web 或 Visual Studio 2013 安装 Visual Studio Express 2013 以及 [最新更新](https://www.microsoft.com/download/details.aspx?id=44921)。
2. 在已安装的 Visual Studio 版本中打开以上项目。 如果计算机上未安装 SQL Server Express，则打开项目时将显示一个提示，因为连接字符串使用 SQL Express。 您可以选择安装 SQL Express 或，因为它可以将连接字符串更改为 LocalDb。 对于本文，我们将其更改为 LocalDb。
3. 打开 web.config 并从中更改连接字符串。SQLExpress 到 (LocalDb) 版本11.0。 从连接字符串中删除 "User Instance = true"。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 打开服务器资源管理器，并验证是否可以观察到表架构和数据。
5. ASP.NET Identity 系统适用于 framework 4.5 或更高版本。 将应用程序重定向到4.5 或更高版本。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    生成项目以验证没有错误。

### <a name="installing-the-nuget-packages"></a>安装 Nuget 包

1. 在解决方案资源管理器中，右键单击项目 " &gt; **管理 NuGet 包**"。 在搜索框中，输入 "Asp.net Identity"。 在结果列表中选择包，然后单击 "安装"。 单击 "我接受" 按钮接受许可协议。 请注意，此包将安装依赖项包： EntityFramework 和 Microsoft ASP.NET 标识核心。 同样，如果不想启用 OAuth 登录) ，请安装以下程序包 (跳过最后4个 OWIN 包：

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Owin。
   - Owin。
   - Owin. MicrosoftAccount
   - Owin。

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>将数据库迁移到新的标识系统

下一步是将现有数据库迁移到 ASP.NET Identity 系统所需的架构。 若要实现此目的，我们将运行一个 SQL 脚本，该脚本包含一组命令，用于创建新表并将现有用户信息迁移到新表。 可在 [此处](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)找到该脚本文件。

此脚本文件特定于此示例。 如果自定义或修改了使用 SQL 成员身份创建的表的架构，则需要相应地更改脚本。

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>如何生成用于架构迁移的 SQL 脚本

为了使 ASP.NET Identity 类能够与现有用户的数据一起使用，我们需要将数据库架构迁移到 ASP.NET Identity 所需的架构。 为此，可以添加新表并将现有信息复制到这些表。 默认情况下 ASP.NET Identity 使用 EntityFramework 将标识模型类映射回数据库，以存储/检索信息。 这些模型类实现定义用户和角色对象的核心标识接口。 数据库中的表和列基于这些模型类。 标识 v 2.1.0 中的 EntityFramework 模型类及其属性如下所定义

| **IdentityUser** | **类型** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| ID | 字符串 | ID | RoleId | ProviderKey | ID |
| 用户名 | 字符串 | 名称 | UserId | UserId | ClaimType |
| PasswordHash | 字符串 |  |  | LoginProvider | ClaimValue |
| SecurityStamp | 字符串 |  |  |  | 用户 \_ Id |
| 电子邮件 | 字符串 |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | 字符串 |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

对于其中的每个模型，我们都需要具有与属性相对应的列。 类和表之间的映射是在的方法中定义的 `OnModelCreating` `IdentityDBContext` 。 这称为配置的 Fluent API 方法，可在 [此处](https://msdn.microsoft.com/data/jj591617.aspx)找到详细信息。 如下所述，类的配置如下所示

| **类** | **表** | **主密钥** | **外键** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | ID |  |
| IdentityRole | AspnetRoles | ID |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | 用户 \_ Id- &gt; AspnetUsers RoleId- &gt; AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId- &gt; AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | ID | 用户 \_ Id- &gt; AspnetUsers |

利用此信息，我们可以创建 SQL 语句来创建新表。 我们可以单独编写每个语句，或使用 EntityFramework PowerShell 命令生成整个脚本，然后可以根据需要进行编辑。 为此，请在 VS 从 "**视图**" 或 "**工具**" 菜单中打开 "**程序包管理器控制台**"

- 运行命令 "启用-迁移" 以启用 EntityFramework 迁移。
- 运行命令 "添加迁移初始"，它创建在 c # 中创建数据库的初始安装代码/VB。
- 最后一步是运行 "更新数据库-脚本" 命令，该命令基于模型类生成 SQL 脚本。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

此数据库生成脚本可用作开始，我们将在其中进行其他更改，以便添加新列和复制数据。 这种方法的优点是，我们会生成一个 `_MigrationHistory` 表，当 EntityFramework 使用该表来修改数据库架构时，此表将在标识版本的将来版本发生更改时修改数据库架构。

除了标识用户模型类中的属性以外，SQL 成员身份用户信息还包含其他属性，即电子邮件、密码尝试、上次登录日期、上次锁定日期等。这是有用的信息，我们希望将其传送到标识系统。 为此，可以向用户模型添加其他属性，并将它们映射回数据库中的表列。 为此，我们可以添加一个用于对模型进行分类的类 `IdentityUser` 。 我们可以将属性添加到此自定义类，并编辑 SQL 脚本，以便在创建表时添加相应的列。 本文进一步介绍了此类的代码。 `AspnetUsers`添加新属性后创建表的 SQL 脚本

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

接下来，需要将 SQL 成员资格数据库中的现有信息复制到新添加的用于标识的表中。 可以通过 SQL 将数据直接从一个表复制到另一个表来完成此操作。 若要在表的行中添加数据，请使用 `INSERT INTO [Table]` 构造。 若要从另一个表复制，可以将 `INSERT INTO` 语句与语句一起使用 `SELECT` 。 若要获取所有用户信息，我们需要查询 *aspnet \_ 用户* 和 *aspnet \_ 成员资格* 表，并将数据复制到 *AspNetUsers* 表中。 使用和以及 `INSERT INTO` `SELECT` `JOIN` 和 `LEFT OUTER JOIN` 语句。 有关在表之间查询和复制数据的详细信息，请参阅 [此](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) 链接。 此外，AspnetUserLogins 和 AspnetUserClaims 表都是空的，因为 SQL 成员身份默认情况下不会映射到此。 所复制的唯一信息是针对用户和角色。 对于在前面的步骤中创建的项目，将信息复制到用户表的 SQL 查询将是

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

在上面的 SQL 语句中，每个用户的有关 *aspnet \_ 用户* 和 *aspnet \_ 成员身份* 表的信息将被复制到 *AspnetUsers* 表的列中。 此处的唯一修改是在复制密码时执行的。 由于 SQL 成员身份中的密码加密算法使用了 "PasswordSalt" 和 "PasswordFormat"，因此我们会将它与哈希密码一起复制，以便可以使用它来按标识对密码进行解密。 当挂钩自定义密码 hasher 时，会在本文中进一步说明这一点。

此脚本文件特定于此示例。 对于具有其他表的应用程序，开发人员可以遵循类似的方法在用户模型类上添加其他属性，并将其映射到 AspnetUsers 表中的列。 若要运行该脚本，

1. 打开 Server Explorer。 展开 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 连接以显示表。 右键单击 "表" 节点，然后选择 "新建查询" 选项

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 在查询窗口中，复制并粘贴从 "迁移" 文件中的整个 SQL 脚本。 通过按 "执行" 箭头按钮来运行脚本文件。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    刷新服务器资源管理器窗口。 在数据库中创建了五个新表。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    下面介绍如何将 SQL 成员资格表中的信息映射到新的标识系统。

    aspnet \_ 角色-- &gt; AspNetRoles

    asp \_ netUsers 和 asp \_ netMembership-- &gt; AspNetUsers

    aspnet \_ UserInRoles-- &gt; AspNetUserRoles

    如上一节所述，AspNetUserClaims 表和 AspNetUserLogins 表是空的。 AspNetUser 表中的 "鉴别器" 字段应与定义为下一步的模型类名称匹配。 此外，PasswordHash 列的格式为 "加密密码 | 密码盐 | 密码格式"。 这使您可以使用特殊的 SQL 成员身份加密逻辑，以便您可以重复使用旧密码。 本文稍后将对此进行解释。

### <a name="creating-models-and-membership-pages"></a>创建模型和成员资格页

如前文所述，默认情况下，标识功能使用实体框架来与数据库进行通信以存储帐户信息。 若要处理表中的现有数据，需要创建模型类，这些类映射回表并在标识系统中将它们挂钩。 作为标识协定的一部分，模型类应实现在 EntityFramework 中定义的接口，或者可以扩展这些接口在中的现有实现方式。

在我们的示例中，AspNetRoles、AspNetUserClaims、AspNetLogins 和 AspNetUserRole 表中的列与标识系统的现有实现类似。 因此，我们可以重复使用现有类来映射到这些表。 AspNetUser 表包含一些额外的列，这些列用于存储 SQL 成员资格表中的附加信息。 这可以通过创建一个模型类来映射，此类扩展了 "IdentityUser" 的现有实现并添加了其他属性。

1. 在项目中创建一个模型文件夹并添加一个类用户。 类的名称应与 "AspnetUsers" 表的 "鉴别器" 列中添加的数据匹配。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    User 类应扩展 *EntityFramework* dll 中找到的 IdentityUser 类。 声明类中的属性，该属性映射回 AspNetUser 列。 "属性 ID"、"用户名"、"PasswordHash" 和 "SecurityStamp" 在 IdentityUser 中定义，因此将被忽略。 下面是包含所有属性的 User 类的代码

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. 需要实体框架 DbContext 类，以便将模型中的数据保存回表，并从表中检索数据以填充模型。 *EntityFramework* dll 定义与标识表交互以检索和存储信息的 IdentityDbContext 类。 IdentityDbContext &lt; tuser &gt; 使用一个 "tuser" 类，该类可以是扩展 IdentityUser 类的任何类。

    创建一个新类 ApplicationDBContext，它在 "模型" 文件夹下扩展 IdentityDbContext，并传入在步骤1中创建的 "User" 类

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 新标识系统中的用户管理是使用 &lt; &gt; *EntityFramework* Dll 中定义的 UserManager tuser 类完成的。 我们需要创建一个扩展 UserManager 的自定义类，并传入在步骤1中创建的 "User" 类。

    在 "模型" 文件夹中创建一个新类 UserManager，用于扩展 UserManager &lt; 用户&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 应用程序用户的密码已加密，并存储在数据库中。 SQL 成员身份中使用的加密算法不同于新标识系统中的加密算法。 若要重用旧密码，我们需要在使用 SQL 成员身份算法登录时有选择地解密密码，同时在新用户的标识中使用加密算法。

    UserManager 类具有属性 "中"，该属性存储实现 "IPasswordHasher" 接口的类的实例。 这用于在用户身份验证事务过程中对密码进行加密/解密。 在步骤3中定义的 UserManager 类中，创建一个新类 SQLPasswordHasher 并复制以下代码。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    通过导入 System.web 和 System.web 命名空间来解决编译错误。

    EncodePassword 方法根据默认的 SQL 成员身份加密实现对密码进行加密。 这是从 System.web dll 中获取的。 如果旧应用使用的是自定义实现，则应在此处反映。 我们需要定义两个其他方法 *HashPassword* 和 *VerifyHashedPassword* ，它们使用 *EncodePassword* 方法对给定的密码进行哈希处理，或使用数据库中的现有密码验证纯文本密码。

    SQL 成员身份系统在用户注册或更改密码时，使用 PasswordHash、PasswordSalt 和 PasswordFormat 对用户输入的密码进行哈希处理。 在迁移期间，所有三个字段均存储在 AspNetUser 表的 PasswordHash 列中，并以 "|" 字符分隔。 当用户登录并且密码包含这些字段时，我们使用 SQL 成员身份加密来检查密码;否则，我们使用标识系统的默认加密来验证密码。 这样一来，旧用户在迁移应用后就不必更改其密码。
5. 声明 UserManager 类的构造函数，并将其作为 SQLPasswordHasher 传递到构造函数中的属性。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>创建新的帐户管理页面

迁移的下一步是添加帐户管理页面，使用户能够注册并登录。 SQL 成员身份中的旧帐户页使用的控件不能用于新的标识系统。 若要添加新的用户管理页，请按照此链接上的教程操作，此链接 [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) 从步骤 "添加用于向应用程序注册用户的 Web 窗体" 开始，因为我们已经创建了该项目并添加了 NuGet 包。

对于该示例，我们需要进行一些更改，以便与我们在这里的项目一起工作。

- 类的 Register.aspx.cs 和 Login.aspx.cs 代码使用 `UserManager` 来自标识包的来创建用户。 对于本示例，请按照前面所述的步骤使用 "模型" 文件夹中添加的 UserManager。
- 使用创建的 User 类，而不是 Register.aspx.cs 和 Login.aspx.cs 代码隐藏类中的 IdentityUser。 这会在自定义用户类中挂接到标识系统。
- 可以跳过用于创建数据库的部分。
- 开发人员需要为新用户设置 ApplicationId，使其与当前应用程序 ID 匹配。 这可以通过在 Register.aspx.cs 类中创建用户对象并在创建用户之前进行设置之前，查询此应用程序的 ApplicationId 来完成。

    示例：

    在 Register.aspx.cs 页中定义一个方法，以查询 aspnet \_ 应用程序表并根据应用程序名称获取应用程序 Id

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    现在，对用户对象设置此设置

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

使用旧的用户名和密码登录现有用户。 使用 "注册" 页面创建新用户。 还要验证用户是否符合预期。

通过迁移到标识系统，用户可以向应用程序添加 (OAuth) 的开放身份验证。 请参阅 [此处](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) 已启用 OAuth 的示例。

## <a name="next-steps"></a>后续步骤

在本教程中，我们介绍了如何将用户从 SQL 成员身份移植到 ASP.NET Identity，但我们没有端口配置文件数据。 在下一教程中，我们将介绍如何将 SQL 成员身份的配置文件数据移植到新的标识系统。

你可以在本文底部留下反馈。

*感谢 Tom Dykstra 和 Rick Anderson 查看本文。*

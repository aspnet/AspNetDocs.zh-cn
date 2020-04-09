---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 使用贝宝结帐和付款 |微软文档
author: Erikre
description: 本教程系列将教您构建一个ASP.NET Web 表单应用程序的基础知识，使用ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 为我们...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675687"
---
# <a name="checkout-and-payment-with-paypal"></a>使用 PayPal 结帐和付款

由[埃里克·雷坦](https://github.com/Erikre)

[下载翼尖玩具样品项目 （C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 （PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教程系列将教您使用ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 为 Web 构建ASP.NET Web 表单应用程序的基础知识。 带有[C# 源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目可供本教程系列使用。

本教程介绍如何修改 Wingtip 玩具示例应用程序，以包括用户授权、注册和使用 PayPal 付款。 只有登录的用户才有权购买产品。 ASP.NET 4.5 Web 窗体项目模板的内置用户注册功能已经包含了您需要的大部分内容。 您将添加贝宝快速结帐功能。 在本教程中，您使用的是PayPal开发者测试环境，因此不会转移任何实际资金。 在本教程结束时，您将通过选择要添加到购物车的产品、单击结帐按钮以及将数据传输到 PayPal 测试网站来测试应用程序。 在PayPal测试网站上，您将确认您的运费和付款信息，然后返回当地的Wingtip玩具样品应用程序，以确认和完成购买。

有几个经验丰富的第三方支付处理器，专门从事在线购物，解决可扩展性和安全性。 ASP.NET开发人员在实施购物和购买解决方案之前应考虑使用第三方支付解决方案的优势。

> [!NOTE] 
> 
> Wingtip Toys 示例应用程序旨在显示ASP.NET网络开发人员可用的特定ASP.NET概念和功能。 此示例应用程序未针对可扩展性和安全性方面的所有可能情况进行优化。

## <a name="what-youll-learn"></a>学习内容：

- 如何限制对文件夹中特定页面的访问。
- 如何从匿名购物车创建已知的购物车。
- 如何为项目启用 SSL。
- 如何向项目添加 OAuth 提供程序。
- 如何使用PayPal使用PayPal测试环境购买产品。
- 如何在**详细信息查看**控件中显示来自 PayPal 的详细信息。
- 如何更新翼尖玩具应用程序的数据库与从PayPal获得的详细信息。

## <a name="adding-order-tracking"></a>添加订单跟踪

在本教程中，您将创建两个新类来跟踪用户创建的顺序中的数据。 这些课程将跟踪有关运输信息、采购总额和付款确认的数据。

### <a name="add-the-order-and-orderdetail-model-classes"></a>添加订单和订单详细信息模型类

在本教程系列的早期，通过在 *"模型"* 文件夹中创建`Category`、`Product`和`CartItem`类，定义类别、产品和购物车项目的架构。 现在，您将添加两个新类来定义产品订单的架构和订单的详细信息。

1. 在 **"模型"** 文件夹中，添加名为*Order.cs*的新类。   
   新的类文件显示在编辑器中。
2. 将默认代码替换为以下内容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 将*OrderDetail.cs*类添加到 *"模型"* 文件夹。
4. 将默认代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`和`OrderDetail`类包含用于定义用于采购和装运的订单信息的架构。

此外，您需要更新管理实体类并提供对数据库的数据访问的数据库上下文类。 为此，您将新创建的 Order 和`OrderDetail`模型类添加到`ProductContext`类中。

1. 在**解决方案资源管理器中**，查找并打开*ProductContext.cs*文件。
2. 将突出显示的代码添加到*ProductContext.cs*文件，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如本教程系列前面所述 *，ProductContext.cs*文件中的代码添加`System.Data.Entity`命名空间，以便您可以访问实体框架的所有核心功能。 此功能包括通过使用强类型对象来查询、插入、更新和删除数据的功能。 类中的`ProductContext`上述代码增加了实体框架对新添加`Order`的类和`OrderDetail`类的访问。

## <a name="adding-checkout-access"></a>添加签出访问权限

Wingtip玩具示例应用程序允许匿名用户查看产品并将其添加到购物车中。 但是，当匿名用户选择购买他们添加到购物车的产品时，他们必须登录到网站。 登录后，他们可以访问处理结帐和购买过程的 Web 应用程序的受限页面。 这些受限页面包含在应用程序的*签出*文件夹中。

### <a name="add-a-checkout-folder-and-pages"></a>添加结帐文件夹和页面

现在，您将创建 *"签出*"文件夹以及客户在结帐过程中将看到的页面。 本教程稍后将更新这些页面。

1. 右键单击**解决方案资源管理器**中的项目名称 （**翼尖玩具**） 并选择 **"添加新文件夹**"。 

    ![使用 PayPal 结帐和付款 - 新文件夹](checkout-and-payment-with-paypal/_static/image1.png)
2. 命名新文件夹*签出*。
3. 右键单击*签出*文件夹，然后选择"**添加新**-&gt;**项目**"。 

    ![使用PayPal结帐和付款 - 新项目](checkout-and-payment-with-paypal/_static/image2.png)
4. 随即出现“添加新项”**** 对话框。
5. 选择左侧的**可视化 C#**  - &gt; **Web**模板组。 然后，从中间窗格中，选择**带有母版页的 Web 窗体**并将其命名为 *"签出Start.aspx*"。 

    ![使用 PayPal 结帐和付款 - 添加新项目对话框](checkout-and-payment-with-paypal/_static/image3.png)
6. 与之前一样，选择*Site.Master*文件作为母版页。
7. 使用上述相同的步骤将以下其他页面添加到*签出*文件夹：   

    - 签出审查.aspx
    - 结帐完成.aspx
    - 结帐取消.aspx
    - 结帐错误.aspx

### <a name="add-a-webconfig-file"></a>添加 Web.config 文件

通过将新的*Web.config*文件添加到*签出*文件夹，您将能够限制对文件夹中包含的所有页面的访问。

1. 右键单击*签出*文件夹并选择"**添加新** -&gt;**项目**"。  
   随即出现“添加新项”**** 对话框。
2. 选择左侧的**可视化 C#**  - &gt; **Web**模板组。 然后，从中间窗格中，选择**Web 配置文件**，接受*Web.config*的默认名称，然后选择 **"添加**"。
3. 将*Web.config 文件中*的现有 XML 内容替换为以下内容：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 保存 *Web.config* 文件。

*Web.config 文件*指定必须拒绝 Web 应用程序的所有未知用户访问*签出*文件夹中的页面。 但是，如果用户已注册了帐户并登录了帐户，则他们将是已知用户，并有权访问 *"签出"* 文件夹中的页面。

请务必注意，ASP.NET配置遵循层次结构，其中每个*Web.config*文件将配置设置应用于它所在的文件夹及其下的所有子目录。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>为项目启用 SSL

 安全套接字层 (SSL) 是一种协议，定义为允许 Web 服务器与 Web 客户端通过使用加密以更安全的方式通信。 如果不使用 SSL，在客户端与服务器之间发送数据时，对网络具有实际访问权限的任何人都可以探查数据包。 此外，通过一般 HTTP 进行的几种常见身份验证方案也是不安全的。 尤其是，基本身份验证和窗体身份验证会发送未加密的凭据。 为确保安全，这些身份验证方案必须使用 SSL。 

1. 在 **"解决方案资源管理器"** 中，单击**WingtipToys**项目，然后按**F4**显示 **"属性"** 窗口。
2. 将**SSL** `true`更改为 。
3. 复制**SSL URL，** 以便以后可以使用。   
 SSL URL 将是`https://localhost:44300/`除非您以前创建了 SSL 网站（如下所示）。   
    ![项目属性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在**解决方案资源管理器**中，右键单击**WingtipToys**项目，然后单击**属性**。
5. 在左侧选项卡中，单击**Web**。
6. 更改**项目 URL**以使用之前保存的**SSL URL。**   
    ![项目 Web 属性](checkout-and-payment-with-paypal/_static/image5.png)
7. 通过按**CTRL_S**保存页面。
8. 按“Ctrl+F5” **** 运行应用程序。 Visual Studio 将显示一个选项用于避免 SSL 警告。
9. 单击"**是**"以信任 IIS Express SSL 证书并继续。   
    ![IIS Express SSL 证书详细信息](checkout-and-payment-with-paypal/_static/image6.png)  
 此时将显示一条安全警告。
10. 单击"**是**"将证书安装到本地主机。   
    ![“安全警告”对话框](checkout-and-payment-with-paypal/_static/image7.png)  
 此时将显示浏览器窗口。

现在，您可以使用 SSL 在本地轻松测试 Web 应用程序。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>添加 OAuth 2.0 提供程序

ASP.NET Web 窗体为成员资格和身份验证提供了增强的选项。 这些增强功能包括 OAuth。 OAuth 是一种开放协议，允许以一种简单而标准的方法从 Web、移动和桌面应用程序进行安全授权。 ASP.NET Web 表单模板使用 OAuth 公开 Facebook、Twitter、Google 和微软作为身份验证提供商。 虽然本教程仅使用 Google 作为身份验证提供程序，但你可轻松修改代码以使用任何提供程序。 实施其他提供程序的步骤与你将在本教程中看到的步骤非常类似。

除了身份验证外，本教程还将使用角色实施授权。 只有添加到角色的用户`canEdit`才能更改数据（创建、编辑或删除联系人）。

> [!NOTE] 
> 
> Windows Live 应用程序仅接受工作网站的实时 URL，因此不能使用本地网站 URL 来测试登录。

可以执行以下步骤来添加 Google 身份验证提供程序。

1. 打开*\_应用启动\启动.Auth.cs*文件。
2. 从`app.UseGoogleAuthentication()`方法中删除注释字符，以便该方法如下所示： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 导航到[谷歌开发者控制台](https://console.developers.google.com/)。 你还需要使用 Google 开发人员电子邮件帐户 (gmail.com） 登录。 如果您没有 Google 帐户，请选择"**创建帐户**"链接。   
   接下来，您将看到**谷歌开发者控制台**。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 单击"**创建项目**"按钮并输入项目名称和 ID（您可以使用默认值）。 然后，单击**协议复选框**和 **"创建**"按钮。  

    ![Google - 新建项目](checkout-and-payment-with-paypal/_static/image9.png)

   几秒钟后，将会创建新项目，并且浏览器将显示新项目页。
5. 在左侧选项卡中，单击**API &amp; auth，** 然后单击**凭据**。
6. 单击**OAuth**下的**创建新客户端 ID。**   
   将显示 **"创建客户端 ID"** 对话框。   
    ![谷歌 - 创建客户 ID](checkout-and-payment-with-paypal/_static/image10.png)
7. 在 **"创建客户端 ID"** 对话框中，保留应用程序类型的默认**Web 应用程序**。
8. 将**授权的 JavaScript 源**设置为本教程前面使用的 SSL URL（`https://localhost:44300/`除非您创建了其他 SSL 项目）。   
   此 URL 是应用程序的来源。 对于此示例，你只需输入 localhost 测试 URL。 但是，您可以输入多个 URL 来考虑本地主机和生产。
9. 将**授权重定向 URI**设置为以下内容： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 ASP.NET OAuth 用户与 Google OAuth 服务器通信时使用的 URI。 请记住上面使用的 SSL URL（`https://localhost:44300/`除非您创建了其他 SSL 项目）。
10. 单击"**创建客户端 ID"** 按钮。
11. 在 Google 开发人员控制台的左侧菜单中，单击 **"同意"屏幕**菜单项，然后设置您的电子邮件地址和产品名称。 填写完表单后，单击"**保存**"。
12. 单击**API**菜单项，向下滚动并单击**Google+ API**旁边的**关闭**按钮。   
    接受此选项将启用 Google+ API。
13. 您还必须将**Microsoft.Owin** NuGet 包更新为 3.0.0 版。   
    从 **"工具"** 菜单中，选择**NuGet 包管理器**，然后选择 **"管理解决方案的 NuGet 包**"。  
    从 **"管理 NuGet 包"** 窗口中查找**Microsoft.Owin**包并将其更新为版本 3.0.0。
14. 在 Visual Studio`UseGoogleAuthentication`中，通过将**客户端 ID**和**客户端机密**复制并粘贴到方法中，更新*Startup.Auth.cs*页的方法。 下面显示**的客户端 ID**和**客户端机密**值是示例，不起作用。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按**CTRL+F5**生成并运行应用程序。 单击**登录**链接。
16. 在 **"使用其他服务登录**"下，单击**Google**。  
    ![登录](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果你需要输入你的凭据，你将重定向到 google 站点将在此输入你的凭据。  
    ![Google - 登录](checkout-and-payment-with-paypal/_static/image12.png)
18. 输入凭据后，系统将提示您向刚刚创建的 Web 应用程序授予权限。  
    ![项目默认服务帐户](checkout-and-payment-with-paypal/_static/image13.png)
19. 单击“接受”****。 现在，您将被重定向回**WingtipToys**应用程序的**注册**页面，您可以在其中注册您的 Google 帐户。  
    ![使用你的 Google 帐户注册](checkout-and-payment-with-paypal/_static/image14.png)
20. 你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。 单击**如上所述的登录**。

### <a name="modifying-login-functionality"></a>修改登录功能

如本教程系列前面所述，默认情况下，ASP.NET Web 窗体模板中已包含许多用户注册功能。 现在，您将修改默认*的 Login.aspx*和*Register.aspx* `MigrateCart`页面来调用该方法。 该方法`MigrateCart`将新登录的用户与匿名购物车关联。 通过将用户和购物车关联，Wingtip 玩具示例应用程序将能够在访问之间维护用户的购物车。

1. 在**解决方案资源管理器中**，查找并打开 *"帐户"* 文件夹。
2. 修改名为*Login.aspx.cs*的代码后面页，以包括以黄色突出显示的代码，以便如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 保存*Login.aspx.cs*文件。

现在，您可以忽略方法没有定义的警告`MigrateCart`。 您将在本教程稍后添加它。

*Login.aspx.cs*代码背后的文件支持登录方法。 通过检查 Login.aspx 页面，您将看到此页面包含一个"登录"按钮，单击该按钮会在代码后面的`LogIn`处理程序触发该按钮。

调用Login.aspx.cs`Login`上的方法时*Login.aspx.cs*，将创建名为`usersShoppingCart`购物车的新实例。 购物车 （GUID） 的 ID 将检索并设置为`cartId`变量。 然后，调用`MigrateCart`该方法，将登录用户`cartId`和登录用户的名称传递给此方法。 迁移购物车时，用于标识匿名购物车的 GUID 将替换为用户名。

除了修改*Login.aspx.cs*代码背后的文件以在用户登录时迁移购物车外，还必须修改*Register.aspx.cs代码背后的文件*，以在用户创建新帐户并登录时迁移购物车。

1. 在 *"帐户"* 文件夹中，打开名为*Register.aspx.cs*的码隐藏文件。
2. 通过将代码以黄色表示修改代码后文件，以便它如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 保存*Register.aspx.cs*文件。 再次忽略有关方法的警告`MigrateCart`。

请注意，在`CreateUser_Click`事件处理程序中使用的代码与方法中使用的`LogIn`代码非常相似。 当用户注册或登录到站点时，将调用该方法`MigrateCart`。

## <a name="migrating-the-shopping-cart"></a>迁移购物车

现在，您已经更新了登录和注册过程，您可以添加代码以使用 方法`MigrateCart`迁移购物车。

1. 在**解决方案资源管理器**中，查找*逻辑*文件夹并打开*ShoppingCartActions.cs*类文件。
2. 将以黄色突出显示的代码添加到*ShoppingCartActions.cs*文件中的现有代码，以便*ShoppingCartActions.cs*文件中的代码如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

该方法`MigrateCart`使用现有的购物车 Id 查找用户的购物车。 接下来，代码循环遍历所有购物车项目，`CartId`并将属性（由`CartItem`架构指定）替换为登录的用户名。

### <a name="updating-the-database-connection"></a>更新数据库连接

如果您正在使用**预构建**的 Wingtip Toys 示例应用程序遵循本教程，则必须重新创建默认成员资格数据库。 通过修改默认连接字符串，将在下次应用程序运行时创建成员数据库。

1. 打开项目根目录的*Web.config*文件。
2. 更新默认连接字符串，使其如下所示：   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>整合贝宝

PayPal 是一个基于 Web 的计费平台，接受在线商家的付款。 本教程接下来将介绍如何将 PayPal 的快速结帐功能集成到您的应用程序中。 快速结帐允许您的客户使用 PayPal 支付已添加到购物车中的商品。

### <a name="create-paypal-test-accounts"></a>创建贝宝测试帐户

要使用 PayPal 测试环境，必须创建并验证开发人员测试帐户。 您将使用开发人员测试帐户创建买方测试帐户和卖方测试帐户。 开发人员测试帐户凭据也将允许翼尖玩具示例应用程序访问 PayPal 测试环境。

1. 在浏览器中，导航到 PayPal 开发人员测试站点：   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果您没有 PayPal 开发者帐户，请通过单击 **"注册"** 并按照注册步骤创建新帐户。 如果您有现有的 PayPal 开发者帐户，请通过单击"**登录**"登录。 您将需要您的PayPal开发者帐户来测试翼尖玩具示例应用程序稍后在本教程。
3. 如果您刚刚注册了您的PayPal开发者账户，您可能需要使用PayPal验证您的PayPal开发者账户。 您可以按照 PayPal 发送到您的电子邮件帐户的步骤验证您的帐户。 验证您的PayPal开发者帐户后，请返回PayPal开发者测试网站。
4. 使用 PayPal 开发者帐户登录 PayPal 开发者网站后，如果您还没有，则需要创建 PayPal 买家测试帐户。 要创建买家测试帐户，在 PayPal 网站上单击 **"应用程序**"选项卡，然后单击 **"沙盒帐户**"。   
 将显示沙**盒测试帐户**页面。   

    > [!NOTE] 
    > 
    > PayPal 开发者网站已经提供了商家测试帐户。

    ![使用 PayPal 结帐和付款 - 沙盒测试帐户](checkout-and-payment-with-paypal/_static/image15.png)
5. 在沙盒测试帐户页上，单击"**创建帐户**"。
6. 在 **"创建测试帐户"** 页上选择买家测试帐户电子邮件和您选择的密码。   

    > [!NOTE] 
    > 
    > 您将需要买家电子邮件地址和密码来测试翼尖玩具示例应用程序在本教程的末尾。

    ![使用 PayPal 结帐和付款 - 沙盒测试帐户](checkout-and-payment-with-paypal/_static/image16.png)
7. 通过单击"**创建帐户**"按钮创建买方测试帐户。  
 将显示 **"沙盒测试帐户"** 页。 

    ![使用贝宝结帐和付款 - 贝宝账户](checkout-and-payment-with-paypal/_static/image17.png)
8. 在**沙盒测试帐户**页面上，单击**主持人**电子邮件帐户。  
    将显示**配置文件**和**通知**选项。
9. 选择 **"配置文件"** 选项，然后单击**API 凭据**以查看商家测试帐户的 API 凭据。
10. 将 TEST API 凭据复制到记事本。

您需要显示的经典测试 API 凭据（用户名、密码和签名）才能从 Wingtip Toys 示例应用程序向 PayPal 测试环境进行 API 调用。 您将在下一步中添加凭据。

### <a name="add-paypal-class-and-api-credentials"></a>添加贝宝类和 API 凭据

您将将大多数 PayPal 代码放入单个类中。 此类包含用于与 PayPal 通信的方法。 此外，您将将您的 PayPal 凭据添加到此类。

1. 在 Visual Studio 中的 Wingtip 玩具示例应用程序中，右键单击**逻辑**文件夹，然后选择"**添加新** -&gt;**项目**"。   
   随即出现“添加新项”**** 对话框。
2. 在左侧 **"已安装**"窗格中的 **"可视 C#"** 下，选择 **"代码**"。
3. 从中间窗格中，选择 **"类**"。 PayPalFunctions.cs命名此新**类。**
4. 单击 **添加**。  
   新的类文件显示在编辑器中。
5. 将默认代码替换为以下代码：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 添加您在本教程前面显示的商家 API 凭据（用户名、密码和签名），以便您可以对 PayPal 测试环境进行函数调用。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此示例应用程序中，您只需向 C# 文件 （.cs） 添加凭据。 但是，在实施的解决方案中，应考虑在配置文件中加密凭据。

NVPAPICaller 类包含大多数 PayPal 功能。 类中的代码提供了从 PayPal 测试环境进行测试购买所需的方法。 以下三个 PayPal 功能用于购买：

- `SetExpressCheckout` 函数
- `GetExpressCheckoutDetails` 函数
- `DoExpressCheckoutPayment` 函数

该方法`ShortcutExpressCheckout`从购物车收集测试购买信息和产品详细信息，并调用`SetExpressCheckout`PayPal 功能。 该方法`GetCheckoutDetails`确认购买详细信息，并在进行测试`GetExpressCheckoutDetails`购买之前调用 PayPal 功能。 该方法`DoCheckoutPayment`通过调用 PayPal 函数完成从测试环境中购买的`DoExpressCheckoutPayment`测试。 其余代码支持 PayPal 方法和进程，例如编码字符串、解码字符串、处理数组和确定凭据。

> [!NOTE] 
> 
> PayPal允许您根据[PayPal的API规范](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)包括可选的购买详细信息。 通过扩展 Wingtip Toys 示例应用程序中的代码，您可以包括本地化详细信息、产品描述、税金、客户服务编号以及许多其他可选字段。

请注意，**在快捷方式 ExpressCheckout**方法中指定的返回和取消 URL 使用端口号。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

当可视化 Web 开发人员使用 SSL 运行 Web 项目时，端口 44300 通常用于 Web 服务器。 如上所述，端口号为 44300。 运行应用程序时，可以看到不同的端口号。 您的端口号需要在代码中正确设置，以便您可以在本教程末尾成功运行 Wingtip Toys 示例应用程序。 本教程的下一部分将介绍如何检索本地主机端口号并更新 PayPal 类。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 类中的本地主机端口号

翼尖玩具样品应用程序购买产品通过导航到PayPal测试网站，并返回到您的本地实例的Wingtip玩具样品应用程序。 为了使 PayPal 返回到正确的 URL，您需要在上面提到的 PayPal 代码中指定本地运行的示例应用程序的端口号。

1. 右键单击**解决方案资源管理器**中的项目名称 （**WingtipToys**） 并选择**属性**。
2. 在左列中，选择 **"Web"** 选项卡。
3. 从 **"项目 Url"** 框中检索端口号。
4. 如果需要，请更新*PayPalFunctions.cs*文件中`cancelURL`的 PayPal 类`NVPAPICaller`（ ） 中的`returnURL`和， 以使用 Web 应用程序的端口号：   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

现在，您添加的代码将与本地 Web 应用程序的预期端口匹配。 PayPal 将能够返回到您本地计算机上的正确 URL。

### <a name="add-the-paypal-checkout-button"></a>添加贝宝结帐按钮

现在，主要 PayPal 函数已添加到示例应用程序中，您可以开始添加调用这些函数所需的标记和代码。 首先，您必须添加用户将在购物车页面上看到的结帐按钮。

1. 打开*购物车.aspx*文件。
2. 滚动到文件底部并找到`<!--Checkout Placeholder -->`注释。
3. 将注释替换为`ImageButton`控件，以便按照如下方式替换标记：  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在*ShoppingCart.aspx.cs*文件中，在`UpdateBtn_Click`文件末尾的事件处理程序之后，添加`CheckOutBtn_Click`事件处理程序：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 此外，在*ShoppingCart.aspx.cs*文件中，添加对 的`CheckoutBtn`引用，以便引用新的图像按钮如下：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 将更改保存到*ShoppingCart.aspx*文件和*ShoppingCart.aspx.cs*文件。
7. 从菜单中，选择**调试**-&gt;**构建翼尖玩具**。  
   该项目将使用新添加的**ImageButton**控件进行重建。

### <a name="send-purchase-details-to-paypal"></a>向贝宝发送购买详情

当用户单击购物车页面上的 **"结帐**"按钮 *（ShoppingCart.aspx）* 时，他们将开始购买过程。 以下代码调用购买产品所需的第一个 PayPal 函数。

1. 从*签出*文件夹中，打开名为*CheckoutStart.aspx.cs*的代码隐藏文件。   
   请务必打开代码背后的文件。
2. 将现有代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

当应用程序的用户单击购物车页面上的 **"签出**"按钮时，浏览器将导航到 *"结帐开始".aspx*页面。 当*签出Start.aspx*页面加载时，`ShortcutExpressCheckout`将调用该方法。 此时，用户将转移到 PayPal 测试网站。 在PayPal网站上，用户输入其PayPal凭据，查看购买详情，接受PayPal协议，并返回到`ShortcutExpressCheckout`方法完成端的 Wingtip 玩具示例应用程序。 方法完成后，它将用户重定向到`ShortcutExpressCheckout`方法中指定的*CheckoutReview.aspx*页面。 `ShortcutExpressCheckout` 这允许用户从翼尖玩具示例应用程序中查看订单详细信息。

### <a name="review-order-details"></a>查看订单详细信息

从PayPal返回后，Wingtip玩具示例应用程序的*结帐审查.aspx*页面将显示订单详细信息。 此页面允许用户在购买产品之前查看订单详细信息。 "*结帐审核.aspx"* 页必须创建如下：

1. 在 *"签出"* 文件夹中，打开名为 *"签出Review.aspx"的*页面。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 打开名为*CheckoutReview.aspx.cs*的代码后面页，并将现有代码替换为以下内容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**"详细信息视图"** 控件用于显示从 PayPal 返回的订单详细信息。 此外，上述代码将订单详细信息作为`OrderDetail`对象保存到 Wingtip Toys 数据库。 当用户单击"**完成订单"** 按钮时，他们将重定向到 *"结帐完成.aspx"* 页。

> [!NOTE] 
> 
> **提示**
> 
> 在 *"结帐Review.aspx"* 页的标记中，请注意该`<ItemStyle>`标记用于更改页面底部附近的 **"详细信息查看"** 控件中的项样式。 通过在 **"设计视图**"中查看页面（通过在 Visual Studio 的左下角选择 **"设计**"），然后选择 **"详细信息视图"** 控件，然后选择**智能标记**（控件右上角的箭头图标），您将能够看到 **"详细信息查看任务**"。
> 
> ![使用 PayPal 结帐和付款 - 编辑字段](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 通过选择 **"编辑字段**"，"**字段"** 对话框将显示。 在此对话框中，您可以轻松地控制 **"详细信息视图"** 控件的可视属性，如**ItemStyle。**
> 
> ![使用 PayPal 结帐和付款 - 字段对话框](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完成购买

*结帐完成.aspx*页面从 PayPal 进行购买。 如上所述，用户必须先单击 **"完成订单"** 按钮，应用程序才能导航到 *"结帐完成.aspx"* 页。

1. 在 *"签出"* 文件夹中，打开名为 *"签出完成.aspx"* 的页面。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 打开名为*CheckoutComplete.aspx.cs*的代码后面页，并将现有代码替换为以下内容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

加载*签出完成.aspx*页时，`DoCheckoutPayment`将调用 该方法。 如前所述，`DoCheckoutPayment`该方法完成了从PayPal测试环境的购买。 一旦PayPal完成订单的购买，"*结帐完成.aspx"* 页面向购买者显示付款交易记录`ID`。

### <a name="handle-cancel-purchase"></a>处理取消购买

如果用户决定取消购买，他们将被定向到 *"结帐取消.aspx"* 页面，在那里他们将看到他们的订单已被取消。

1. 在 *"签出*"文件夹中打开名为 *"签出取消取消.aspx"* 的页面。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>处理购买错误

购买过程中的错误将由 *"结帐错误.aspx"* 页处理。 如果出现错误，"*结帐开始.aspx"* 页、*结帐审核.aspx*页和 *"结帐完成.aspx"* 页的代码将分别重定向到 *"结帐错误.aspx"* 页。

1. 在*签出*文件夹中打开名为 *"签出错误.aspx"* 的页面。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*签出错误.aspx*页面在结帐过程中发生错误时显示错误详细信息。

## <a name="running-the-application"></a>运行应用程序

运行应用程序以查看如何购买产品。 请注意，您将在 PayPal 测试环境中运行。 没有实际资金被兑换。

1. 请确保所有文件都保存在可视化工作室中。
2. 打开 Web 浏览器并导航[https://developer.paypal.com](https://developer.paypal.com/)到 。
3. 使用您在本教程中之前创建的 PayPal 开发者帐户登录。  
   对于 PayPal 的开发人员沙盒，您需要登录[https://developer.paypal.com](https://developer.paypal.com/)以测试快速结帐。 这仅适用于贝宝的沙盒测试，不适用于PayPal的现场环境。
4. 在视觉工作室中，按**F5**运行翼尖玩具示例应用程序。  
   重建数据库后，浏览器将打开并显示*Default.aspx*页面。
5. 通过选择产品类别（如"汽车"，然后单击每个产品旁边的 **"添加到购物车**"），将三种不同的产品添加到购物车中。  
   购物车将显示您选择的产品。
6. 单击 **"贝宝**"按钮进行结帐。 

    ![使用PayPal结帐和付款 - 购物车](checkout-and-payment-with-paypal/_static/image20.png)

   签出需要您拥有翼尖玩具示例应用程序的用户帐户。
7. 单击页面右侧的**Google**链接，使用现有的gmail.com电子邮件帐户登录。  
   如果您没有gmail.com帐户，则可以在[www.gmail.com](https://www.gmail.com/)创建一个帐户用于测试目的。 您也可以通过单击"注册"使用标准本地帐户。 

    ![使用 PayPal 结帐和付款 - 登录](checkout-and-payment-with-paypal/_static/image21.png)
8. 使用 gmail 帐户和密码登录。 

    ![使用PayPal结帐和付款 - Gmail登录](checkout-and-payment-with-paypal/_static/image22.png)
9. 单击**登录**按钮，使用翼尖玩具示例应用程序用户名注册您的 gmail 帐户。 

    ![使用PayPal结帐和付款 - 注册帐户](checkout-and-payment-with-paypal/_static/image23.png)
10. 在 PayPal 测试网站上，添加您在本教程中之前创建的**买家**电子邮件地址和密码，然后单击 **"登录**"按钮。 

    ![使用贝宝结帐和付款 - 贝宝登录](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 政策，然后单击 **"同意并继续"** 按钮。  
    请注意，此页面仅在您首次使用此 PayPal 帐户时显示。 再次注意，这是一个测试帐户，没有真正的钱交换。 

    ![使用贝宝结帐和付款 - 贝宝政策](checkout-and-payment-with-paypal/_static/image25.png)
12. 查看 PayPal 测试环境审核页面上的订单信息，然后单击"**继续**"。 

    ![使用 PayPal 结帐和付款 - 查看信息](checkout-and-payment-with-paypal/_static/image26.png)
13. 在 *"结帐审核.aspx"* 页上，验证订单金额并查看生成的送货地址。 然后，单击"**完成订单**"按钮。 

    ![使用 PayPal 结帐和付款 - 订单审核](checkout-and-payment-with-paypal/_static/image27.png)
14. **"结帐完成.aspx"** 页将显示付款交易记录 ID。 

    ![使用 PayPal 结帐和付款 - 结帐完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>查看数据库

通过在运行应用程序后查看 Wingtip Toys 示例应用程序数据库中的更新数据，您可以看到应用程序已成功记录产品的购买。

您可以使用**数据库资源管理器**窗口（Visual Studio 中的**服务器资源管理器**窗口）来检查*Wingtiptoys.mdf*数据库文件中的数据，就像本教程系列前面所做的那样。

1. 如果浏览器窗口仍然打开，则关闭它。
2. 在可视化工作室中，选择**解决方案资源管理器**顶部的 **"显示所有文件**"图标，以允许您展开**\_应用数据**文件夹。
3. 展开**应用\_数据**文件夹。  
 您可能需要为文件夹选择"**显示所有文件**"图标。
4. 右键单击*Wingtiptoys.mdf*数据库文件，然后选择 **"打开**"。  
    将显示**服务器资源管理器**。
5. 展开 **“表”** 文件夹。
6. 右键单击 **"订单**"表并选择 **"显示表数据**"。  
 将显示 **"订单**"表。
7. 查看 **"付款交易ID"** 列以确认成功交易。 

    ![使用 PayPal 结帐和付款 - 审核数据库](checkout-and-payment-with-paypal/_static/image29.png)
8. 关闭**订单**表窗口。
9. 在"服务器资源管理器"中，右键单击 **"订单详细信息**"表并选择 **"显示表数据**"。
10. 查看 **"订单详细信息**"表中 的`OrderId`和`Username`值。 请注意，这些值与 **"订单"** 表中包括 的`OrderId`和`Username`值匹配。
11. 关闭 **"订单详细信息**"表窗口。
12. 右键单击 Wingtip 玩具数据库文件 *（Wingtiptoys.mdf），* 然后选择 **"关闭连接**"。
13. 如果看不到**解决方案资源管理器**窗口，请单击**服务器资源管理器**窗口底部**的解决方案资源管理器**，以再次显示**解决方案资源管理器**。

## <a name="summary"></a>总结

在本教程中，您添加了订单和订单详细信息架构，以跟踪产品的购买情况。 您还可以将 PayPal 功能集成到翼尖玩具示例应用程序中。

## <a name="additional-resources"></a>其他资源

[ASP.NET配置概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[将具有成员资格、OAuth 和 SQL 数据库的安全ASP.NET Web 窗体应用部署到 Azure 应用服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[微软 Azure - 免费试用](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免责声明

本教程包含示例代码。 此类示例代码提供"有效"，不提供任何形式的担保。 因此，Microsoft 不保证示例代码的准确性、完整性或质量。 您同意自行承担使用示例代码的风险。 在任何情况下，Microsoft 均不对任何示例代码、内容（包括但不限于任何示例代码、内容中的任何错误或遗漏）或因使用任何示例代码而造成的任何损失或损坏承担任何责任。 特此通知您并同意对 Microsoft 的任何和所有损失、任何损失、伤害或损害索赔进行赔偿、保存和保持无害，包括但不限于您发布、传输、使用或依赖的材料引起的或由您所表达的意见引起的或产生的损失、伤害或损害。

> [!div class="step-by-step"]
> [上一页](shopping-cart.md)
> [下一页](membership-and-administration.md)

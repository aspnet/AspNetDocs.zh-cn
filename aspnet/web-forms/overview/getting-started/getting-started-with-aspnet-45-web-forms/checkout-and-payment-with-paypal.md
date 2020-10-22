---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 通过 PayPal 结帐和支付 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 .。。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345657"
---
# <a name="checkout-and-payment-with-paypal"></a>使用 PayPal 结帐和付款

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目 (c # ) ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 或 [下载电子书 (PDF) ](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有 [c # 源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 的 Visual Studio 2013 项目。

本教程介绍如何使用 PayPal 修改 Wingtip 玩具示例应用程序，以包括用户授权、注册和付款。 只有登录的用户才有权购买产品。 ASP.NET 4.5 Web 窗体项目模板的内置用户注册功能已包含所需的大部分内容。 你将添加 PayPal Express 结帐功能。 在本教程中，你将使用 PayPal 开发人员测试环境，因此不会传输实际资金。 在本教程结束时，你将通过选择要添加到购物车中的产品，单击 "结帐" 按钮，然后将数据传输到 PayPal 测试网站来测试应用程序。 在 PayPal 测试网站上，您将确认您的运费和付款信息，然后返回到本地 Wingtip 玩具示例应用程序以确认并完成购买。

有几个经验丰富的第三方支付处理器专用于在线购物，以应对可伸缩性和安全性。 ASP.NET 开发人员应考虑利用第三方支付解决方案的优点，然后再实施购物和采购解决方案。

> [!NOTE] 
> 
> Wingtip 玩具示例应用程序旨在演示 ASP.NET web 开发人员可用的特定 ASP.NET 概念和功能。 此示例应用程序未针对可伸缩性和安全性方面的所有可能情况进行优化。

## <a name="what-youll-learn"></a>学习内容：

- 如何限制对文件夹中特定页面的访问。
- 如何从匿名购物车创建已知购物车。
- 如何为项目启用 SSL。
- 如何将 OAuth 提供程序添加到项目。
- 如何使用 PayPal 测试环境购买产品。
- 如何在 **DetailsView** 控件中显示 PayPal 的详细信息。
- 如何用从 PayPal 获得的详细信息更新 Wingtip 玩具应用程序的数据库。

## <a name="adding-order-tracking"></a>添加订单跟踪

在本教程中，你将创建两个新类来跟踪用户创建的顺序中的数据。 类将跟踪有关装运信息、采购总额和付款确认的数据。

### <a name="add-the-order-and-orderdetail-model-classes"></a>添加 Order 和 OrderDetail 模型类

在本教程的前面部分中，通过在 `Category` `Product` `CartItem` " *模型* " 文件夹中创建、和类，为类别、产品和购物车项目定义了架构。 现在，您将添加两个新类来定义产品订单的架构和订单的详细信息。

1. 在 " **模型** " 文件夹中，添加名为 *Order.cs*的新类。   
   新的类文件将显示在编辑器中。
2. 将默认代码替换为以下内容：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. 将 *OrderDetail.cs* 类添加到 " *模型* " 文件夹。
4. 将默认代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`和 `OrderDetail` 类包含架构以定义用于购买和装运的订单信息。

此外，您还需要更新管理实体类的数据库上下文类，并提供对数据库的数据访问。 为此，您将向类中添加新创建的顺序和 `OrderDetail` 模型类 `ProductContext` 。

1. 在 **解决方案资源管理器**中，找到并打开 *ProductContext.cs* 文件。
2. 将突出显示的代码添加到 *ProductContext.cs* 文件，如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

如本系列教程前面所述， *ProductContext.cs* 文件中的代码将添加 `System.Data.Entity` 命名空间，以便您有权访问实体框架的所有核心功能。 此功能包括使用强类型对象查询、插入、更新和删除数据的功能。 类中的上述代码 `ProductContext` 将实体框架访问添加到新添加的 `Order` 和 `OrderDetail` 类。

## <a name="adding-checkout-access"></a>添加结帐访问

Wingtip 玩具示例应用程序允许匿名用户查看产品并将其添加到购物车。 但是，当匿名用户选择购买其添加到购物车的产品时，他们必须登录到网站。 登录后，他们可以访问处理结帐和购买过程的 Web 应用程序的受限页面。 这些受限页面包含在应用程序的 " *签出* " 文件夹中。

### <a name="add-a-checkout-folder-and-pages"></a>添加结帐文件夹和页面

你现在将创建 *结帐* 文件夹和其中的页面，客户将在结帐过程中看到该文件夹。 稍后将在本教程中更新这些页面。

1. 右键单击 " **Wingtip 玩具**) 中的项目名称 (**解决方案资源管理器** 并选择" **添加新文件夹**"。 

    ![通过 PayPal 结帐和付款-新建文件夹](checkout-and-payment-with-paypal/_static/image1.png)
2. 将新文件夹命名为 " *签出*"。
3. 右键单击 "*签出*" 文件夹，然后选择 "**添加** - &gt; **新项**"。 

    ![通过 PayPal 结帐和付款-新项目](checkout-and-payment-with-paypal/_static/image2.png)
4. 随即出现“添加新项”对话框。
5. 选择左侧的 " **Visual c #**  - &gt; **Web**模板" 组。 然后，在中间窗格中，选择 " **带有母版页的 Web 窗体**" 并将其命名为 *CheckoutStart*。 

    ![通过 PayPal 结帐和付款-"添加新项" 对话框](checkout-and-payment-with-paypal/_static/image3.png)
6. 与之前一样，选择 " *网站* " 作为母版页。
7. 使用上述相同步骤将以下附加页面添加到 *结帐* 文件夹：   

    - CheckoutReview .aspx
    - CheckoutComplete .aspx
    - CheckoutCancel .aspx
    - CheckoutError .aspx

### <a name="add-a-webconfig-file"></a>添加 Web.config 文件

通过将新的 *Web.config* 文件添加到 *结帐* 文件夹，你将能够限制对文件夹中包含的所有页面的访问。

1. 右键单击 "*签出*" 文件夹，然后选择 "**添加**  - &gt; **新项**"。  
   随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual c #**  - &gt; **Web**模板" 组。 然后，从中间窗格中选择 " **Web 配置文件**"，接受默认名称 " *Web.config*"，然后选择 " **添加**"。
3. 将 *Web.config* 文件中的现有 XML 内容替换为以下内容：  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. 保存 *Web.config* 文件。

*Web.config*文件指定必须对 Web 应用程序的所有未知用户拒绝对*签出*文件夹中包含的页的访问权限。 但是，如果用户注册了某个帐户并登录，则这些用户将是已知用户，并且将有权访问 *签出* 文件夹中的页面。

需要注意的是，ASP.NET 配置遵循层次结构，其中每个 *Web.config* 文件都将配置设置应用到它所在的文件夹以及其下的所有子目录。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>为项目启用 SSL

 安全套接字层 (SSL) 是一种协议，定义为允许 Web 服务器与 Web 客户端通过使用加密以更安全的方式通信。 如果不使用 SSL，在客户端与服务器之间发送数据时，对网络具有实际访问权限的任何人都可以探查数据包。 此外，通过一般 HTTP 进行的几种常见身份验证方案也是不安全的。 尤其是，基本身份验证和窗体身份验证会发送未加密的凭据。 为确保安全，这些身份验证方案必须使用 SSL。 

1. 在 **解决方案资源管理器**中，单击 " **WingtipToys** " 项目，然后按 **F4** 以显示 " **属性** " 窗口。
2. 将 **SSL** 更改为启用 `true` 。
3. 复制 **SSL URL** 以便以后使用。   
 SSL URL 将为， `https://localhost:44300/` 除非你之前已创建 Ssl 网站 (如下) 所示。   
    ![项目属性](checkout-and-payment-with-paypal/_static/image4.png)
4. 在 **解决方案资源管理器**中，右键单击 **WingtipToys** 项目，然后单击 " **属性**"。
5. 在左侧选项卡中，单击 " **Web**"。
6. 将 " **项目 Url** " 更改为使用前面保存的 **SSL Url** 。   
    ![项目 Web 属性](checkout-and-payment-with-paypal/_static/image5.png)
7. 按 **CTRL + S**保存页面。
8. 按“Ctrl+F5”  运行应用程序。 Visual Studio 将显示一个选项用于避免 SSL 警告。
9. 单击 **"是"** 以信任 IIS Express SSL 证书并继续。   
    ![IIS Express SSL 证书详细信息](checkout-and-payment-with-paypal/_static/image6.png)  
 此时将显示一条安全警告。
10. 单击 **"是"** 将证书安装到本地主机。   
    ![“安全警告”对话框](checkout-and-payment-with-paypal/_static/image7.png)  
 此时将显示浏览器窗口。

你现在可以使用 SSL 在本地轻松测试 Web 应用程序。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>添加 OAuth 2.0 提供程序

ASP.NET Web 窗体为成员资格和身份验证提供了增强的选项。 这些增强功能包括 OAuth。 OAuth 是一种开放协议，允许以一种简单而标准的方法从 Web、移动和桌面应用程序进行安全授权。 ASP.NET Web 窗体模板使用 OAuth 公开 Facebook、Twitter、Google 和 Microsoft 作为身份验证提供程序。 虽然本教程仅使用 Google 作为身份验证提供程序，但你可轻松修改代码以使用任何提供程序。 实施其他提供程序的步骤与你将在本教程中看到的步骤非常类似。

除了身份验证外，本教程还将使用角色实施授权。 只有添加到该角色的用户才能 `canEdit` 更改数据 (创建、编辑或删除联系人) 。

> [!NOTE] 
> 
> Windows Live 应用程序仅接受工作网站的实时 URL，因此不能使用本地网站 URL 来测试登录名。

可以执行以下步骤来添加 Google 身份验证提供程序。

1. 打开 *App \_ Start\Startup.Auth.cs* 文件。
2. 从方法中删除注释字符， `app.UseGoogleAuthentication()` 使该方法如下所示： 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. 导航到 [Google 开发人员控制台](https://console.developers.google.com/)。 你还需要使用 Google 开发人员电子邮件帐户 (gmail.com） 登录。 如果你没有 Google 帐户，请选择 " **创建帐户** " 链接。   
   接下来，你将看到 **Google 开发人员控制台**。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 单击 " **创建项目** " 按钮，然后输入项目名称和 ID (你可以使用) 的默认值。 然后，单击 " **协议" 复选框** 和 " **创建** " 按钮。  

    ![Google - 新建项目](checkout-and-payment-with-paypal/_static/image9.png)

   几秒钟后，将会创建新项目，并且浏览器将显示新项目页。
5. 在左侧选项卡中，单击 " **api &amp; 身份验证**"，然后单击 " **凭据**"。
6. 单击 " **OAuth**" 下的 "**创建新客户端 ID** "。   
   将显示 " **创建客户端 ID** " 对话框。   
    ![Google-创建客户端 ID](checkout-and-payment-with-paypal/_static/image10.png)
7. 在 " **创建客户端 ID** " 对话框中，保留应用程序类型的默认 **Web 应用程序** 。
8. 将 **授权的 JavaScript** 源设置为之前在本教程中使用的 ssl URL (`https://localhost:44300/` 除非已) 创建其他 ssl 项目。   
   此 URL 是应用程序的来源。 对于此示例，你只需输入 localhost 测试 URL。 但是，您可以输入多个 Url 来为 localhost 和生产提供帐户。
9. 将 **授权的重定向 URI** 设置为以下内容： 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   此值是 ASP.NET OAuth 用户与 Google OAuth 服务器通信时使用的 URI。 请记住上述 ( 的 SSL URL，    `https://localhost:44300/` 除非已) 创建其他 ssl 项目。
10. 单击 " **创建客户端 ID** " 按钮。
11. 在 Google 开发人员控制台的左侧菜单中，单击 " **同意屏幕** " 菜单项，然后设置你的电子邮件地址和产品名称。 完成表单后，单击 " **保存**"。
12. 单击 " **api** " 菜单项，向下滚动并单击 " **Google + API**" 旁边的 "**关闭**" 按钮。   
    接受此选项将启用 Google + API。
13. 还必须将 **Owin** NuGet 包更新到版本3.0.0。   
    从 " **工具** " 菜单中，选择 " **Nuget 包管理器** "，然后选择 " **管理解决方案的 NuGet 包**"。  
    在 " **管理 NuGet 包** " 窗口中，找到并将 **Owin** 包更新到版本3.0.0。
14. 在 Visual Studio 中， `UseGoogleAuthentication` 通过将**客户端 ID**和**客户端密码**复制并粘贴到方法中，更新*Startup.Auth.cs*页的方法。 下面显示的 **客户端 ID** 和 **客户端机密** 值为示例，将不起作用。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. 按 **CTRL + F5** 生成并运行应用程序。 单击 " **登录** " 链接。
16. 在 " **使用其他服务进行登录**" 下，单击 " **Google**"。  
    ![登录](checkout-and-payment-with-paypal/_static/image11.png)
17. 如果你需要输入你的凭据，你将重定向到 google 站点将在此输入你的凭据。  
    ![Google - 登录](checkout-and-payment-with-paypal/_static/image12.png)
18. 输入凭据后，系统会提示你向刚创建的 web 应用程序授予权限。  
    ![项目默认服务帐户](checkout-and-payment-with-paypal/_static/image13.png)
19. 单击“接受”。 你现在将重定向回**WingtipToys**应用程序的 "**注册**" 页，你可以在该应用程序中注册 Google 帐户。  
    ![使用你的 Google 帐户注册](checkout-and-payment-with-paypal/_static/image14.png)
20. 你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。 单击 " **登录"** ，如上所示。

### <a name="modifying-login-functionality"></a>修改登录功能

如本系列教程前面所述，在默认情况下，ASP.NET Web 窗体模板中包含了许多用户注册功能。 现在，你将修改默认的 *登录 .aspx* ，并 *注册 .aspx* 页以调用 `MigrateCart` 方法。 `MigrateCart`方法将新登录的用户与匿名购物车关联。 通过关联用户和购物车，Wingtip 玩具示例应用程序将能够在访问之间维护用户的购物车。

1. 在 **解决方案资源管理器**中，找到并打开 *帐户* 文件夹。
2. 修改名为 *Login.aspx.cs* 的代码隐藏页面，使其包含黄色突出显示的代码，使其显示如下：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. 保存 *Login.aspx.cs* 文件。

现在，你可以忽略此方法没有定义的警告 `MigrateCart` 。 你将在本教程的稍后部分中添加它。

*Login.aspx.cs*代码隐藏文件支持登录方法。 通过检查 "登录 .aspx" 页，您将看到此页包含一个 "登录" 按钮，当单击此按钮时，将触发 `LogIn` 代码隐藏中的处理程序。

`Login`调用*Login.aspx.cs*上的方法时，将创建一个名为的购物车的新实例 `usersShoppingCart` 。 将检索 (GUID) 的购物车 ID 并将其设置为 `cartId` 变量。 然后， `MigrateCart` 调用方法，同时将 `cartId` 已登录用户的和名称传递到此方法。 迁移购物车时，用于标识匿名购物车的 GUID 将替换为用户名。

除了修改 *Login.aspx.cs* 代码隐藏文件以便在用户登录时迁移购物车，还必须修改 *Register.aspx.cs 代码隐藏文件* ，以便在用户创建新帐户并登录时迁移购物车。

1. 在 *帐户* 文件夹中，打开名为 *Register.aspx.cs*的代码隐藏文件。
2. 通过将代码包括为黄色来修改代码隐藏文件，使其如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. 保存 *Register.aspx.cs* 文件。 再次忽略关于方法的警告 `MigrateCart` 。

请注意，在事件处理程序中使用的代码与 `CreateUser_Click` 在方法中使用的代码非常相似 `LogIn` 。 当用户注册或登录到站点时， `MigrateCart` 将对方法进行调用。

## <a name="migrating-the-shopping-cart"></a>迁移购物车

现在已更新登录和注册过程，可以使用方法添加代码以迁移购物车 `MigrateCart` 。

1. 在 **解决方案资源管理器**中，找到 *逻辑* 文件夹，然后打开 *ShoppingCartActions.cs* 类文件。
2. 将黄色突出显示的代码添加到 *ShoppingCartActions.cs* 文件中的现有代码，以便 *ShoppingCartActions.cs* 文件中的代码如下所示：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart`方法使用现有的 cartId 查找用户的购物车。 接下来，该代码遍历所有购物车项，并 `CartId` `CartItem` 使用已登录的用户名替换架构) 指定的属性 (。

### <a name="updating-the-database-connection"></a>更新数据库连接

如果在本教程中使用 **预** 生成的 Wingtip 玩具示例应用程序，则必须重新创建默认的成员资格数据库。 通过修改默认连接字符串，将在下一次运行应用程序时创建成员资格数据库。

1. 打开位于项目根目录的 *Web.config* 文件。
2. 更新默认连接字符串，使其显示如下：   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>集成 PayPal

PayPal 是一种基于 web 的计费平台，它接受在线商家支付的费用。 接下来，本教程介绍如何将 PayPal 的快速结帐功能集成到你的应用程序中。 快速结帐允许客户使用 PayPal 来支付他们已添加到购物车的物品。

### <a name="create-paypal-test-accounts"></a>创建 PayPal 测试帐户

若要使用 PayPal 测试环境，必须创建并验证开发人员测试帐户。 您将使用开发人员测试帐户来创建买家测试帐户和卖方测试帐户。 开发人员测试帐户凭据还会允许 Wingtip 玩具示例应用程序访问 PayPal 测试环境。

1. 在浏览器中，导航到 PayPal 开发人员测试网站：   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. 如果没有 PayPal 开发人员帐户，请单击 " **注册**" 并按照注册步骤创建一个新帐户。 如果拥有现有的 PayPal 开发人员帐户，请单击 " **登录**" 以登录。 稍后在本教程中，你将需要 PayPal 开发人员帐户来测试 Wingtip 玩具示例应用程序。
3. 如果你刚刚注册了 PayPal 开发者帐户，则可能需要使用 PayPal 验证 PayPal 开发人员帐户。 可以按照 PayPal 发送到你的电子邮件帐户的步骤来验证你的帐户。 验证 PayPal 开发人员帐户后，请重新登录到 PayPal 开发人员测试站点。
4. 使用 PayPal 开发人员帐户登录到 PayPal 开发人员站点后，需要创建一个 PayPal 买家测试帐户（如果还没有）。 若要创建买家测试帐户，请在 PayPal 网站上单击 " **应用程序** " 选项卡，然后单击 " **沙盒帐户**"。   
 将显示 " **沙盒测试帐户** " 页。   

    > [!NOTE] 
    > 
    > PayPal 开发人员网站已经提供了一个商家测试帐户。

    ![通过 PayPal-沙盒测试帐户结帐和付款](checkout-and-payment-with-paypal/_static/image15.png)
5. 在 "沙盒测试帐户" 页上，单击 " **创建帐户**"。
6. 在 " **创建测试帐户** " 页上，选择所选的买方测试帐户电子邮件和密码。   

    > [!NOTE] 
    > 
    > 在本教程结束时，你将需要购买者电子邮件地址和密码来测试 Wingtip 玩具示例应用程序。

    ![通过 PayPal-沙盒测试帐户结帐和付款](checkout-and-payment-with-paypal/_static/image16.png)
7. 单击 " **创建帐户** " 按钮，创建买家测试帐户。  
 将显示 " **沙盒测试帐户** " 页。 

    ![用 PayPal-PayPal 帐户结帐和付款](checkout-and-payment-with-paypal/_static/image17.png)
8. 在 " **沙盒测试帐户** " 页上，单击 **主持人** 电子邮件帐户。  
    显示**配置文件**和**通知**选项。
9. 选择 " **配置文件** " 选项，然后单击 " **API 凭据** " 查看商家测试帐户的 API 凭据。
10. 将测试 API 凭据复制到记事本。

需要 (用户名、密码和签名) 显示的经典测试 API 凭据，才能从 Wingtip 玩具示例应用程序向 PayPal 测试环境进行 API 调用。 你将在下一步中添加凭据。

### <a name="add-paypal-class-and-api-credentials"></a>添加 PayPal 类和 API 凭据

将大部分 PayPal 代码放在一个类中。 此类包含用于与 PayPal 进行通信的方法。 此外，还需要将 PayPal 凭据添加到此类。

1. 在 Visual Studio 中的 Wingtip 玩具示例应用程序中，右键单击**逻辑**文件夹，然后选择 "**添加**  - &gt; **新项**"。   
   随即出现“添加新项”对话框。
2. 在 **Visual c #** 中，从左侧的 " **已安装** " 窗格中选择 " **代码**"。
3. 从中间窗格中选择 " **类**"。 将此新类命名为 **PayPalFunctions.cs**。
4. 单击“添加”。  
   新的类文件将显示在编辑器中。
5. 将默认代码替换为以下代码：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 在本教程前面部分中显示的 " (用户名"、"密码" 和 "签名") 添加商家 API 凭据，以便可以对 PayPal 测试环境进行函数调用。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 在此示例应用程序中，只需将凭据添加到 c # 文件 ( .cs) 。 但是，在实现的解决方案中，应考虑在配置文件中加密凭据。

NVPAPICaller 类包含 PayPal 的大部分功能。 类中的代码提供了在 PayPal 测试环境中进行测试购买所需的方法。 以下三个 PayPal 函数用于进行购买：

- `SetExpressCheckout` 函数
- `GetExpressCheckoutDetails` 函数
- `DoExpressCheckoutPayment` 函数

`ShortcutExpressCheckout`方法收集购物车的测试购买信息和产品详细信息，并调用 `SetExpressCheckout` PayPal 函数。 此 `GetCheckoutDetails` 方法在进行测试前确认购买详细信息，并调用 `GetExpressCheckoutDetails` PayPal 函数。 `DoCheckoutPayment`方法通过调用 PayPal 函数完成测试环境中的测试购买 `DoExpressCheckoutPayment` 。 其余代码支持 PayPal 方法和过程，如编码字符串、对字符串进行解码、处理数组和确定凭据。

> [!NOTE] 
> 
> PayPal 允许根据 [paypal 的 API 规范](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)包含可选的购买详细信息。 通过扩展 Wingtip 玩具示例应用程序中的代码，你可以包括本地化详细信息、产品说明、税务、客户服务编号以及许多其他可选字段。

请注意， **ShortcutExpressCheckout** 方法中指定的返回和取消 url 使用端口号。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

当 Visual Web Developer 使用 SSL 运行 web 项目时，通常会将端口44300用于 Web 服务器。 如上所示，端口号为44300。 运行应用程序时，可能会看到不同的端口号。 需要在代码中正确设置端口号，以便在本教程结束时可以成功运行 Wingtip 玩具示例应用程序。 本教程的下一部分介绍如何检索本地主机端口号并更新 PayPal 类。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>更新 PayPal 类中的 LocalHost 端口号

Wingtip 玩具示例应用程序通过导航到 PayPal 测试网站并返回到 Wingtip 玩具示例应用程序的本地实例来购买产品。 为了让 PayPal 返回到正确的 URL，你需要在上面提到的 PayPal 代码中指定本地运行的示例应用程序的端口号。

1. 右键单击项目名称 ("中的" **WingtipToys**) " **解决方案资源管理器** 并选择" **属性**"。
2. 在左列中，选择 " **Web** " 选项卡。
3. 从 " **项目 Url** " 框中检索端口号。
4. 如有必要，请 `returnURL` 在 `cancelURL` PayPalFunctions.cs 文件中更新 PayPal 类 (`NVPAPICaller`) *PayPalFunctions.cs* ，以便使用 web 应用程序的端口号：   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

现在，你添加的代码将与本地 Web 应用程序的所需端口匹配。 PayPal 将能够返回到你的本地计算机上的正确 URL。

### <a name="add-the-paypal-checkout-button"></a>添加 PayPal 结帐按钮

由于已将主要 PayPal 函数添加到示例应用程序中，因此可以开始添加调用这些函数所需的标记和代码。 首先，必须添加用户将在 "购物车" 页上看到的 "签出" 按钮。

1. 打开 *ShoppingCart* 文件。
2. 滚动到文件的底部，找到 `<!--Checkout Placeholder -->` 注释。
3. 将注释替换为 `ImageButton` 控件，以便按如下所示替换标记：  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. 在 *ShoppingCart.aspx.cs* 文件中， `UpdateBtn_Click` 将事件处理程序添加到文件末尾附近，添加 `CheckOutBtn_Click` 事件处理程序：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 同样，在 *ShoppingCart.aspx.cs* 文件中，添加对的引用 `CheckoutBtn` ，以便按如下所示引用 "新图像" 按钮：  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 保存对 *ShoppingCart* 文件和 *ShoppingCart.aspx.cs* 文件的更改。
7. 从菜单中选择 "**调试** - &gt; **生成 WingtipToys**"。  
   将用新添加的 **ImageButton** 控件重新生成项目。

### <a name="send-purchase-details-to-paypal"></a>向 PayPal 发送购买详细信息

当用户单击 "购物车" 页上的 " **签出** " 按钮 (*ShoppingCart*) 时，他们将开始购买过程。 以下代码调用购买产品所需的第一个 PayPal 函数。

1. 在 *签出* 文件夹中，打开名为 *CheckoutStart.aspx.cs*的代码隐藏文件。   
   请确保打开代码隐藏文件。
2. 将现有代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

当应用程序的用户在 "购物车" 页上单击 " **签出** " 按钮时，浏览器将导航到 *CheckoutStart* 页。 加载 *CheckoutStart* 页面时，将 `ShortcutExpressCheckout` 调用方法。 此时，用户会传输到 PayPal 测试网站。 在 PayPal 网站上，用户输入其 PayPal 凭据，查看购买详细信息，接受 PayPal 协议，并返回到该方法完成的 Wingtip 玩具示例应用程序 `ShortcutExpressCheckout` 。 当 `ShortcutExpressCheckout` 方法完成时，它会将用户重定向到方法中指定的*CheckoutReview*页面。 `ShortcutExpressCheckout` 这允许用户在 Wingtip 玩具示例应用程序中查看订单详细信息。

### <a name="review-order-details"></a>查看订单详细信息

从 PayPal 返回后，Wingtip 玩具示例应用程序的 *CheckoutReview* 页将显示订单详细信息。 此页允许用户在购买产品之前查看订单详细信息。 必须按如下所示创建 *CheckoutReview* 页：

1. 在 " *签出* " 文件夹中，打开名为 *CheckoutReview*的页。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. 打开名为 *CheckoutReview.aspx.cs* 的代码隐藏页，并将现有代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

" **DetailsView** " 控件用于显示从 PayPal 返回的订单详细信息。 此外，上述代码将订单详细信息以对象的形式保存到 Wingtip 玩具数据库 `OrderDetail` 。 当用户单击 " **完成订单** " 按钮时，会将其重定向到 *CheckoutComplete* 页。

> [!NOTE] 
> 
> **提示**
> 
> 在 *CheckoutReview* 页的标记中，请注意， `<ItemStyle>` 标记用于更改 **DetailsView** 控件内靠近页面底部的项的样式。 通过在 "设计" **视图** 中查看页面 (选择 Visual Studio 左下角的 " **设计** ") ，然后选择 " **DetailsView** " 控件，并选择 **智能标记** (控件) 右上角的箭头图标，你将能够看到 **DetailsView 任务**。
> 
> ![通过 PayPal 编辑字段结帐和付款](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 通过选择 " **编辑字段**"，将显示 " **字段** " 对话框。 在此对话框中，可以轻松控制**DetailsView**控件的可视属性，如**ItemStyle**。
> 
> !["PayPal-字段" 对话框的 "结帐和付款"](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完成购买

*CheckoutComplete* 页可从 PayPal 购买。 如上所述，用户必须单击 " **完成订单** " 按钮，然后应用程序才会导航到 *CheckoutComplete* 页。

1. 在 " *签出* " 文件夹中，打开名为 *CheckoutComplete*的页。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. 打开名为 *CheckoutComplete.aspx.cs* 的代码隐藏页，并将现有代码替换为以下代码：   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

加载 *CheckoutComplete* 页面时，将 `DoCheckoutPayment` 调用方法。 如前文所述，该 `DoCheckoutPayment` 方法从 PayPal 测试环境中完成购买。 一旦 PayPal 完成了订单的购买， *CheckoutComplete* 页面就会向买方显示付款交易 `ID` 。

### <a name="handle-cancel-purchase"></a>处理取消购买

如果用户决定取消购买，则会将其定向到 " *CheckoutCancel* " 页，在该页面中，他们将看到已取消的订单。

1. 在*签出*文件夹中打开名为*CheckoutCancel*的页。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>处理采购错误

在购买过程中的错误将由 *CheckoutError* 页面处理。 如果发生错误，则 *CheckoutStart* 页的代码隐藏、 *CheckoutReview* 页和 *CheckoutComplete* 页将每个都重定向到 *CheckoutError* 页。

1. 在*签出*文件夹中打开名为*CheckoutError*的页。
2. 将现有标记替换为以下内容：   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

在签出过程中出现错误时，会显示 *CheckoutError* 页，其中包含错误详细信息。

## <a name="running-the-application"></a>运行应用程序

运行应用程序以了解如何购买产品。 请注意，你将在 PayPal 测试环境中运行。 不会交换实际资金。

1. 请确保所有文件都保存在 Visual Studio 中。
2. 打开 Web 浏览器并导航到 [https://developer.paypal.com](https://developer.paypal.com/) 。
3. 登录到你之前在本教程中创建的 PayPal 开发人员帐户。  
   对于 PayPal 的开发人员沙箱，你需要登录 [https://developer.paypal.com](https://developer.paypal.com/) 到，以便测试快速结帐。 这仅适用于 PayPal 的沙箱测试，而不适用于 PayPal 的实时环境。
4. 在 Visual Studio 中，按 **F5** 运行 "Wingtip 玩具" 示例应用程序。  
   重新生成数据库后，浏览器将打开并显示 *default.aspx* 页。
5. 选择产品类别（如 "汽车"），然后单击每个产品旁边的 " **添加到购物车** "，将三个不同的产品添加到购物车。  
   购物车将显示您选择的产品。
6. 单击 **PayPal** 按钮以结帐。 

    ![通过 PayPal 购物车结帐和付款](checkout-and-payment-with-paypal/_static/image20.png)

   签出将要求你拥有 Wingtip 玩具示例应用程序的用户帐户。
7. 单击页面右侧的 **Google** 链接，使用现有的 gmail.com 电子邮件帐户登录。  
   如果没有 gmail.com 帐户，可以在 [www.gmail.com](https://www.gmail.com/)上创建一个用于测试目的。 还可以通过单击 "注册" 来使用标准本地帐户。 

    ![签入并支付 PayPal-登录](checkout-and-payment-with-paypal/_static/image21.png)
8. 用 gmail 帐户和密码登录。 

    ![通过 PayPal 登录进行结帐和付款](checkout-and-payment-with-paypal/_static/image22.png)
9. 单击 " **登录** " 按钮，将 gmail 帐户注册到 Wingtip 玩具示例应用程序用户名。 

    ![签出并支付 PayPal-注册帐户](checkout-and-payment-with-paypal/_static/image23.png)
10. 在 PayPal 测试网站上，添加之前在本教程中创建的 **买家** 电子邮件地址和密码，并单击 " **登录** " 按钮。 

    ![通过 PayPal-PayPal 登录进行结帐和付款](checkout-and-payment-with-paypal/_static/image24.png)
11. 同意 PayPal 政策，并单击 " **同意并继续** " 按钮。  
    请注意，仅当首次使用此 PayPal 帐户时，才会显示此页。 再次请注意，这是一个测试帐户，不会交换真正的资金。 

    ![结帐和支付 PayPal-PayPal 政策](checkout-and-payment-with-paypal/_static/image25.png)
12. 查看 PayPal 测试环境检查页上的订单信息，然后单击 " **继续**"。 

    ![结帐和支付 PayPal-查看信息](checkout-and-payment-with-paypal/_static/image26.png)
13. 在 " *CheckoutReview* " 页上，验证订单量并查看生成的寄送地址。 然后单击 " **完成顺序** " 按钮。 

    ![通过 PayPal 订购审核结帐和付款](checkout-and-payment-with-paypal/_static/image27.png)
14. 将显示 **CheckoutComplete** 页，其中包含付款事务 ID。 

    ![通过 PayPal 结帐和付款-结帐完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>查看数据库

在运行应用程序后，通过查看 Wingtip 玩具示例应用程序数据库中的更新数据，可以看到该应用程序已成功记录产品的购买情况。

您可以使用 Visual) Studio 中的 "**数据库资源管理器**" 窗口 (**服务器资源管理器**"窗口中检查包含在*Wingtiptoys*数据库文件中的数据，如本系列教程前面所述。

1. 如果浏览器窗口仍处于打开状态，请将其关闭。
2. 在 Visual Studio 中，选择 "**解决方案资源管理器**顶部的"**显示所有文件**"图标，以允许你展开"**应用程序 \_ 数据**"文件夹。
3. 展开 " **应用程序 \_ 数据** " 文件夹。  
 可能需要选择文件夹的 " **显示所有文件** " 图标。
4. 右键单击 *Wingtiptoys* 数据库文件，然后选择 " **打开**"。  
    将显示**服务器资源管理器**。
5. 展开 **“表”** 文件夹。
6. 右键单击 **Orders**表，然后选择 " **显示表数据**"。  
 显示 " **订单** " 表。
7. 查看 " **PaymentTransactionID** " 列以确认事务是否成功。 

    ![签出和支付 PayPal-查看数据库](checkout-and-payment-with-paypal/_static/image29.png)
8. 关闭 " **订单** 表" 窗口。
9. 在服务器资源管理器中，右键单击 **OrderDetails** 表并选择 " **显示表数据**"。
10. 查看 `OrderId` `Username` **OrderDetails** 表中的和值。 请注意，这些值匹配 `OrderId` `Username` **Orders** 表中包含的和值。
11. 关闭 " **OrderDetails** 表" 窗口。
12. 右键单击 "Wingtip 玩具" 数据库文件 (*Wingtiptoys*) 并选择 " **关闭连接**"。
13. 如果看不到 "**解决方案资源管理器**" 窗口，请单击 "**服务器资源管理器**" 窗口底部的 "**解决方案资源管理器**以再次显示**解决方案资源管理器**。

## <a name="summary"></a>总结

在本教程中，您添加了订单和订单详细信息架构以跟踪产品的购买情况。 还将 PayPal 功能集成到了 Wingtip 玩具示例应用程序中。

## <a name="additional-resources"></a>其他资源

[ASP.NET 配置概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免责声明

本教程包含示例代码。 此类示例代码 "按原样" 提供，不提供任何形式的保证。 因此，Microsoft 不保证代码的准确性、完整性或质量。 您同意使用此示例代码的风险由您自己承担。 在任何情况下，Microsoft 都不会对任何示例代码、内容（包括但不限于）任何代码、内容或任何类型的任何错误或遗漏的任何错误或遗漏提供任何错误或遗漏，因为使用任何示例代码。 你将被特此通知，并在特此同意赔偿、节省和保持 Microsoft 免受任何损失、损失索赔、伤害或损坏（包括但不限于通过发布、传输、使用或依赖的内容，包括但不限于这些 occasioned，但不限于）。

> [!div class="step-by-step"]
> [上一页](shopping-cart.md)
> [下一页](membership-and-administration.md)

---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 防止机器人使用您的ASP.NET网络剃刀）网站 |微软文档
author: rick-anderson
description: 本文介绍如何使用 ReCaptcha（安全措施）来防止自动程序 （bot） 在ASP.NET网页 （Razor） 中执行任务...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543751"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>使用 CAPTCHA 防止机器人使用ASP.NET网络剃刀）网站

由[微软](https://github.com/microsoft)

> 本文介绍如何使用 ReCaptcha（安全措施）来防止自动程序 （bot） 在ASP.NET网页 （Razor） 网站中执行任务。
> 
> **学习内容：** 
> 
> - 如何向您的网站添加 CAPTCHA 测试。
> 
> 以下是本文介绍的ASP.NET功能：
> 
> - 帮手`ReCaptcha`
> 
> > [!NOTE]
> > 本文中的信息适用于ASP.NET网页 1.0 和网页 2。

## <a name="about-captchas"></a>关于 CAPTCHAs

任何时候，当你让人们在您的网站注册，甚至只是输入一个名字和URL（如博客评论），你可能会得到大量的假名。 这些通常由自动程序（机器人）留下，这些程序（机器人）试图在他们能找到的每个网站中保留 URL。 （一个常见的动机是发布要销售的产品的 URL。

通过使用*CAPTCHA*验证用户注册或以其他方式输入其名称和站点时，可以帮助确保用户是真实用户而不是计算机程序。 CAPTCHA 代表完全自动化的公共图灵测试，告诉计算机和人类分开。 CAPTCHA 是一种*质询-响应*测试，要求用户执行一些用户容易做的事情，但自动化程序却很难做到。 CAPTCHA 的最常见类型是看到一些扭曲的字母并被要求键入它们。 （失真应该使机器人很难破译这些字母。

## <a name="adding-a-recaptcha-test"></a>添加重新卡普查测试

在ASP.NET页中`ReCaptcha`，可以使用帮助程序呈现基于 ReCaptcha 服务 （的[http://recaptcha.net](http://recaptcha.net)CAPTCHA 测试）。 `ReCaptcha`帮助程序显示两个扭曲的单词的图像，用户在验证页面之前必须正确输入这些单词。 用户响应由ReCaptcha.Net服务验证。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. 在ReCaptcha.Net注册您的网站。[http://recaptcha.net](http://recaptcha.net) 完成注册后，您将获得公钥和私钥。
2. 将ASP.NET Web 帮助器库添加到您的网站，如[在ASP.NET网页网站中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)（如果您尚未）中所述。
3. 如果您还没有*\_AppStart.cshtml*文件，则在网站的根文件夹中创建名为*\_AppStart.cshtml*的文件。
4. 在`Recaptcha`*\_AppStart.cshtml*文件中添加以下帮助程序设置： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 使用您自己的`PublicKey`公共`PrivateKey`和私钥设置 和 属性。
6. 保存*\_AppStart.cshtml*文件并关闭它。
7. 在网站的根文件夹中，创建名为*Recaptcha.cshtml*的新页面。
8. 将现有内容替换为以下内容： 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 在浏览器中运行*Recaptcha.cshtml*页面。 如果`PrivateKey`该值有效，则页面将显示 ReCaptcha 控件和一个按钮。 如果未在*\_AppStart.html*中全局设置密钥，则页面将显示错误。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 输入测试的单词。 如果通过 ReCaptcha 测试，则会看到一条达到该效果的消息。 否则，您将看到一条错误消息，并重新显示 ReCaptcha 控件。

> [!NOTE]
> 如果您的计算机位于使用代理服务器的域中，则可能需要配置*Web.config* `defaultproxy`文件的元素。 下面的示例显示了一个*Web.config*文件`defaultproxy`，该文件配置了元素以使 ReCaptcha 服务正常工作。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [为ASP.NET网页网站自定义网站范围行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [雷卡普查网站](https://www.google.com/recaptcha)

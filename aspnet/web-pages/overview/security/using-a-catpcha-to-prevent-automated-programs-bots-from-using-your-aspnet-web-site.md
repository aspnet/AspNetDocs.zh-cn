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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="ba69a-103">使用 CAPTCHA 防止机器人使用ASP.NET网络剃刀）网站</span><span class="sxs-lookup"><span data-stu-id="ba69a-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="ba69a-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ba69a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ba69a-105">本文介绍如何使用 ReCaptcha（安全措施）来防止自动程序 （bot） 在ASP.NET网页 （Razor） 网站中执行任务。</span><span class="sxs-lookup"><span data-stu-id="ba69a-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="ba69a-106">**学习内容：**</span><span class="sxs-lookup"><span data-stu-id="ba69a-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="ba69a-107">如何向您的网站添加 CAPTCHA 测试。</span><span class="sxs-lookup"><span data-stu-id="ba69a-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="ba69a-108">以下是本文介绍的ASP.NET功能：</span><span class="sxs-lookup"><span data-stu-id="ba69a-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="ba69a-109">帮手`ReCaptcha`</span><span class="sxs-lookup"><span data-stu-id="ba69a-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="ba69a-110">本文中的信息适用于ASP.NET网页 1.0 和网页 2。</span><span class="sxs-lookup"><span data-stu-id="ba69a-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="ba69a-111">关于 CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="ba69a-111">About CAPTCHAs</span></span>

<span data-ttu-id="ba69a-112">任何时候，当你让人们在您的网站注册，甚至只是输入一个名字和URL（如博客评论），你可能会得到大量的假名。</span><span class="sxs-lookup"><span data-stu-id="ba69a-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="ba69a-113">这些通常由自动程序（机器人）留下，这些程序（机器人）试图在他们能找到的每个网站中保留 URL。</span><span class="sxs-lookup"><span data-stu-id="ba69a-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="ba69a-114">（一个常见的动机是发布要销售的产品的 URL。</span><span class="sxs-lookup"><span data-stu-id="ba69a-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="ba69a-115">通过使用*CAPTCHA*验证用户注册或以其他方式输入其名称和站点时，可以帮助确保用户是真实用户而不是计算机程序。</span><span class="sxs-lookup"><span data-stu-id="ba69a-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="ba69a-116">CAPTCHA 代表完全自动化的公共图灵测试，告诉计算机和人类分开。</span><span class="sxs-lookup"><span data-stu-id="ba69a-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="ba69a-117">CAPTCHA 是一种*质询-响应*测试，要求用户执行一些用户容易做的事情，但自动化程序却很难做到。</span><span class="sxs-lookup"><span data-stu-id="ba69a-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="ba69a-118">CAPTCHA 的最常见类型是看到一些扭曲的字母并被要求键入它们。</span><span class="sxs-lookup"><span data-stu-id="ba69a-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="ba69a-119">（失真应该使机器人很难破译这些字母。</span><span class="sxs-lookup"><span data-stu-id="ba69a-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="ba69a-120">添加重新卡普查测试</span><span class="sxs-lookup"><span data-stu-id="ba69a-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="ba69a-121">在ASP.NET页中`ReCaptcha`，可以使用帮助程序呈现基于 ReCaptcha 服务 （的[http://recaptcha.net](http://recaptcha.net)CAPTCHA 测试）。</span><span class="sxs-lookup"><span data-stu-id="ba69a-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="ba69a-122">`ReCaptcha`帮助程序显示两个扭曲的单词的图像，用户在验证页面之前必须正确输入这些单词。</span><span class="sxs-lookup"><span data-stu-id="ba69a-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="ba69a-123">用户响应由ReCaptcha.Net服务验证。</span><span class="sxs-lookup"><span data-stu-id="ba69a-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="ba69a-124">在ReCaptcha.Net注册您的网站。[http://recaptcha.net](http://recaptcha.net)</span><span class="sxs-lookup"><span data-stu-id="ba69a-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="ba69a-125">完成注册后，您将获得公钥和私钥。</span><span class="sxs-lookup"><span data-stu-id="ba69a-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="ba69a-126">将ASP.NET Web 帮助器库添加到您的网站，如[在ASP.NET网页网站中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)（如果您尚未）中所述。</span><span class="sxs-lookup"><span data-stu-id="ba69a-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="ba69a-127">如果您还没有*\_AppStart.cshtml*文件，则在网站的根文件夹中创建名为*\_AppStart.cshtml*的文件。</span><span class="sxs-lookup"><span data-stu-id="ba69a-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="ba69a-128">在`Recaptcha`*\_AppStart.cshtml*文件中添加以下帮助程序设置：</span><span class="sxs-lookup"><span data-stu-id="ba69a-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="ba69a-129">使用您自己的`PublicKey`公共`PrivateKey`和私钥设置 和 属性。</span><span class="sxs-lookup"><span data-stu-id="ba69a-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="ba69a-130">保存*\_AppStart.cshtml*文件并关闭它。</span><span class="sxs-lookup"><span data-stu-id="ba69a-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="ba69a-131">在网站的根文件夹中，创建名为*Recaptcha.cshtml*的新页面。</span><span class="sxs-lookup"><span data-stu-id="ba69a-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="ba69a-132">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="ba69a-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="ba69a-133">在浏览器中运行*Recaptcha.cshtml*页面。</span><span class="sxs-lookup"><span data-stu-id="ba69a-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="ba69a-134">如果`PrivateKey`该值有效，则页面将显示 ReCaptcha 控件和一个按钮。</span><span class="sxs-lookup"><span data-stu-id="ba69a-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="ba69a-135">如果未在*\_AppStart.html*中全局设置密钥，则页面将显示错误。</span><span class="sxs-lookup"><span data-stu-id="ba69a-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="ba69a-136">输入测试的单词。</span><span class="sxs-lookup"><span data-stu-id="ba69a-136">Enter the words for the test.</span></span> <span data-ttu-id="ba69a-137">如果通过 ReCaptcha 测试，则会看到一条达到该效果的消息。</span><span class="sxs-lookup"><span data-stu-id="ba69a-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="ba69a-138">否则，您将看到一条错误消息，并重新显示 ReCaptcha 控件。</span><span class="sxs-lookup"><span data-stu-id="ba69a-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="ba69a-139">如果您的计算机位于使用代理服务器的域中，则可能需要配置*Web.config* `defaultproxy`文件的元素。</span><span class="sxs-lookup"><span data-stu-id="ba69a-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="ba69a-140">下面的示例显示了一个*Web.config*文件`defaultproxy`，该文件配置了元素以使 ReCaptcha 服务正常工作。</span><span class="sxs-lookup"><span data-stu-id="ba69a-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ba69a-141">其他资源</span><span class="sxs-lookup"><span data-stu-id="ba69a-141">Additional Resources</span></span>

- [<span data-ttu-id="ba69a-142">为ASP.NET网页网站自定义网站范围行为</span><span class="sxs-lookup"><span data-stu-id="ba69a-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="ba69a-143">雷卡普查网站</span><span class="sxs-lookup"><span data-stu-id="ba69a-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)

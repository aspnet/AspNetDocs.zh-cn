---
title: 外部 OAuth 身份验证提供程序
author: rick-anderson
description: 发现适用于 ASP.NET Core 应用的外部 OAuth 身份验证提供程序。
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/otherlogins
ms.openlocfilehash: b69c366ec1bf12ccf434991fc8a79eaf8c09da3d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051194"
---
# <a name="external-oauth-authentication-providers"></a><span data-ttu-id="6cb93-103">外部 OAuth 身份验证提供程序</span><span class="sxs-lookup"><span data-stu-id="6cb93-103">External OAuth authentication providers</span></span>

<span data-ttu-id="6cb93-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Pranav rastogi 撰写](https://github.com/rustd)，和[Valeriy Novytskyy](https://github.com/01binary)</span><span class="sxs-lookup"><span data-stu-id="6cb93-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Pranav Rastogi](https://github.com/rustd), and [Valeriy Novytskyy](https://github.com/01binary)</span></span>

<span data-ttu-id="6cb93-105">以下列表包含常见外部 OAuth 身份验证提供程序可使用 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="6cb93-105">The following list includes common external OAuth authentication providers that work with ASP.NET Core apps.</span></span> <span data-ttu-id="6cb93-106">第三方 NuGet 包，如所维护的那些[aspnet contrib](https://www.nuget.org/packages?q=owners%3Aaspnet-contrib+title%3AOAuth)，可以用于补充由 ASP.NET Core 团队实现的身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="6cb93-106">Third-party NuGet packages, such as the ones maintained by [aspnet-contrib](https://www.nuget.org/packages?q=owners%3Aaspnet-contrib+title%3AOAuth), can be used to complement the authentication providers implemented by the ASP.NET Core team.</span></span>

* <span data-ttu-id="6cb93-107">[LinkedIn](https://www.linkedin.com/developer/apps) ([说明](https://developer.linkedin.com/docs/oauth2))</span><span class="sxs-lookup"><span data-stu-id="6cb93-107">[LinkedIn](https://www.linkedin.com/developer/apps) ([Instructions](https://developer.linkedin.com/docs/oauth2))</span></span>

* <span data-ttu-id="6cb93-108">[Instagram](https://www.instagram.com/developer/register/) ([说明](https://www.instagram.com/developer/authentication/))</span><span class="sxs-lookup"><span data-stu-id="6cb93-108">[Instagram](https://www.instagram.com/developer/register/) ([Instructions](https://www.instagram.com/developer/authentication/))</span></span>

* <span data-ttu-id="6cb93-109">[Reddit](https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps) ([说明](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example))</span><span class="sxs-lookup"><span data-stu-id="6cb93-109">[Reddit](https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps) ([Instructions](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example))</span></span>

* <span data-ttu-id="6cb93-110">[Github](https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew) ([说明](https://developer.github.com/v3/oauth/))</span><span class="sxs-lookup"><span data-stu-id="6cb93-110">[Github](https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew) ([Instructions](https://developer.github.com/v3/oauth/))</span></span>

* <span data-ttu-id="6cb93-111">[Yahoo](https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F) ([说明](https://developer.yahoo.com/bbauth/user.html))</span><span class="sxs-lookup"><span data-stu-id="6cb93-111">[Yahoo](https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F) ([Instructions](https://developer.yahoo.com/bbauth/user.html))</span></span>

* <span data-ttu-id="6cb93-112">[Tumblr](https://www.tumblr.com/oauth/apps) ([说明](https://www.tumblr.com/docs/api/v2#auth))</span><span class="sxs-lookup"><span data-stu-id="6cb93-112">[Tumblr](https://www.tumblr.com/oauth/apps) ([Instructions](https://www.tumblr.com/docs/api/v2#auth))</span></span>

* <span data-ttu-id="6cb93-113">[Pinterest](https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F) ([说明](https://developers.pinterest.com/docs/api/overview/?))</span><span class="sxs-lookup"><span data-stu-id="6cb93-113">[Pinterest](https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F) ([Instructions](https://developers.pinterest.com/docs/api/overview/?))</span></span>

* <span data-ttu-id="6cb93-114">[Pocket](https://getpocket.com/developer/apps/new) ([说明](https://getpocket.com/developer/docs/authentication))</span><span class="sxs-lookup"><span data-stu-id="6cb93-114">[Pocket](https://getpocket.com/developer/apps/new) ([Instructions](https://getpocket.com/developer/docs/authentication))</span></span>

* <span data-ttu-id="6cb93-115">[Flickr](https://www.flickr.com/services/apps/create) ([说明](https://www.flickr.com/services/api/auth.oauth.html))</span><span class="sxs-lookup"><span data-stu-id="6cb93-115">[Flickr](https://www.flickr.com/services/apps/create) ([Instructions](https://www.flickr.com/services/api/auth.oauth.html))</span></span>

* <span data-ttu-id="6cb93-116">[Dribble](https://dribbble.com/signup) ([说明](http://developer.dribbble.com/v1/oauth/))</span><span class="sxs-lookup"><span data-stu-id="6cb93-116">[Dribble](https://dribbble.com/signup) ([Instructions](http://developer.dribbble.com/v1/oauth/))</span></span>

* <span data-ttu-id="6cb93-117">[Vimeo](https://vimeo.com/join) ([说明](https://developer.vimeo.com/api/authentication))</span><span class="sxs-lookup"><span data-stu-id="6cb93-117">[Vimeo](https://vimeo.com/join) ([Instructions](https://developer.vimeo.com/api/authentication))</span></span>

* <span data-ttu-id="6cb93-118">[SoundCloud](https://soundcloud.com/you/apps/new) ([说明](https://developers.soundcloud.com/blog/we-love-oauth-2))</span><span class="sxs-lookup"><span data-stu-id="6cb93-118">[SoundCloud](https://soundcloud.com/you/apps/new) ([Instructions](https://developers.soundcloud.com/blog/we-love-oauth-2))</span></span>

* <span data-ttu-id="6cb93-119">[VK](https://vk.com/apps?act=manage) ([说明](https://vk.com/pages?oid=-17680044&p=Authorizing_Sites))</span><span class="sxs-lookup"><span data-stu-id="6cb93-119">[VK](https://vk.com/apps?act=manage) ([Instructions](https://vk.com/pages?oid=-17680044&p=Authorizing_Sites))</span></span>

[!INCLUDE[Multiple authentication providers](includes/chain-auth-providers.md)]

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

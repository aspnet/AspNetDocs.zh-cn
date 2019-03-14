---
ms.openlocfilehash: 6ceb4bd6580d11ee5d6ff57a895c499308035858
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064034"
---
# <a name="aspnet-core-authorization-sample"></a>ASP.NET Core 授权示例

此示例演示使用 Razor 页面授权约定。 此示例演示中所述的功能[Razor 页面授权约定](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization)主题。

在此示例中的用户授权使用 cookie 身份验证功能中所述[使用 cookie 身份验证，而无需 ASP.NET Core标识](https://docs.microsoft.com/aspnet/core/security/authentication/cookie)主题。 有关使用 ASP.NET Core 标识的信息，请参阅<xref:security/authentication/identity>。

运行示例时，使用电子邮件地址**maria.rodriguez@contoso.com**用户进行身份验证。

## <a name="examples-in-this-sample"></a>此示例中的示例

| 功能 | 描述 |
| --- | --- |
| [AuthorizePage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) | 将添加[AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到指定的路径包含的页。 |
| [AuthorizeFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) | 将添加[AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)所有具有指定路径的文件夹中的页。 |
| [AllowAnonymousToPage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) | 将添加[AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)到具有指定路径的页面。 |
| [AllowAnonymousToFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) | 将添加[AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter)所有具有指定路径的文件夹中的页。 |

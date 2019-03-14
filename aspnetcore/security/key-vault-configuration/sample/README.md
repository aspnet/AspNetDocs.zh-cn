---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045584"
---
# <a name="key-vault-configuration-provider-sample-app"></a>密钥保管库配置提供程序示例应用程序

此示例演示如何使用 Azure 密钥保管库配置提供程序。

该示例由两个模式之一中运行`#define`顶部的语句*Program.cs*文件。 有关说明，请参阅[示例代码中的预处理器指令](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):

* `Basic` &ndash; 演示如何使用 Azure 密钥保管库客户端 ID 和密码向 Azure Key Vault 中存储的访问密钥。 可以从部署到 Azure 应用服务或任何主机能够为 ASP.NET Core 应用提供服务的任何位置运行此版本的示例。
* `Managed` &ndash; 演示如何使用 Azure 的[托管服务标识](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)进行身份验证对 Azure Key Vault 应用程序与 Azure AD 身份验证，而无需在应用程序的代码或配置中的凭据。 Azure AD 客户端 ID 和机密不需要的应用程序以使用 Azure 密钥保管库进行身份验证。 此示例必须部署到 Azure 应用服务以浏览托管标识 scearnio。

有关详细信息，请参阅[Azure 密钥保管库配置提供程序](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration)。

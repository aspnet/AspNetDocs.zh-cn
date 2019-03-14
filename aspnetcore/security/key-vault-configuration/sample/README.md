---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045584"
---
# <a name="key-vault-configuration-provider-sample-app"></a><span data-ttu-id="390ac-101">密钥保管库配置提供程序示例应用程序</span><span class="sxs-lookup"><span data-stu-id="390ac-101">Key Vault Configuration Provider Sample App</span></span>

<span data-ttu-id="390ac-102">此示例演示如何使用 Azure 密钥保管库配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="390ac-102">This sample illustrates the use of the Azure Key Vault Configuration Provider.</span></span>

<span data-ttu-id="390ac-103">该示例由两个模式之一中运行`#define`顶部的语句*Program.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="390ac-103">The sample runs in one of two modes determined by the `#define` statement at the top of the *Program.cs* file.</span></span> <span data-ttu-id="390ac-104">有关说明，请参阅[示例代码中的预处理器指令](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):</span><span class="sxs-lookup"><span data-stu-id="390ac-104">For instructions, see [Preprocessor directives in sample code](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):</span></span>

* <span data-ttu-id="390ac-105">`Basic` &ndash; 演示如何使用 Azure 密钥保管库客户端 ID 和密码向 Azure Key Vault 中存储的访问密钥。</span><span class="sxs-lookup"><span data-stu-id="390ac-105">`Basic` &ndash; Demonstrates the use of an Azure Key Vault Client ID and Secret to access secrets stored in Azure Key Vault.</span></span> <span data-ttu-id="390ac-106">可以从部署到 Azure 应用服务或任何主机能够为 ASP.NET Core 应用提供服务的任何位置运行此版本的示例。</span><span class="sxs-lookup"><span data-stu-id="390ac-106">This version of the sample can be run from any location, deployed to Azure App Service or any host capable of serving an ASP.NET Core app.</span></span>
* <span data-ttu-id="390ac-107">`Managed` &ndash; 演示如何使用 Azure 的[托管服务标识](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)进行身份验证对 Azure Key Vault 应用程序与 Azure AD 身份验证，而无需在应用程序的代码或配置中的凭据。</span><span class="sxs-lookup"><span data-stu-id="390ac-107">`Managed` &ndash; Demonstrates how to use Azure's [Managed Service Identity](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) to authenticate the app to Azure Key Vault with Azure AD authentication without credentials in the app's code or configuration.</span></span> <span data-ttu-id="390ac-108">Azure AD 客户端 ID 和机密不需要的应用程序以使用 Azure 密钥保管库进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="390ac-108">An Azure AD Client ID and Secret aren't required for the app to authenticate with Azure Key Vault.</span></span> <span data-ttu-id="390ac-109">此示例必须部署到 Azure 应用服务以浏览托管标识 scearnio。</span><span class="sxs-lookup"><span data-stu-id="390ac-109">This sample must be deployed to Azure App Service to explore the Managed Identity scearnio.</span></span>

<span data-ttu-id="390ac-110">有关详细信息，请参阅[Azure 密钥保管库配置提供程序](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration)。</span><span class="sxs-lookup"><span data-stu-id="390ac-110">For more information, see [Azure Key Vault Configuration Provider](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration).</span></span>

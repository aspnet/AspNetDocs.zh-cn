---
title: 在 ASP.NET Core 中的 azure 密钥保管库配置提供程序
author: guardrex
description: 了解如何使用 Azure 密钥保管库配置提供程序来配置应用程序使用在运行时加载的名称 / 值对。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/22/2019
uid: security/key-vault-configuration
ms.openlocfilehash: 2188929d6f380327465e8ce0fd8ad659188416d3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048024"
---
# <a name="azure-key-vault-configuration-provider-in-aspnet-core"></a><span data-ttu-id="0aa60-103">在 ASP.NET Core 中的 azure 密钥保管库配置提供程序</span><span class="sxs-lookup"><span data-stu-id="0aa60-103">Azure Key Vault Configuration Provider in ASP.NET Core</span></span>

<span data-ttu-id="0aa60-104">通过[Luke Latham](https://github.com/guardrex)和[Andrew Stanton-nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="0aa60-104">By [Luke Latham](https://github.com/guardrex) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="0aa60-105">本文档介绍如何使用[Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/)配置提供程序将从 Azure Key Vault 机密中加载应用配置值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-105">This document explains how to use the [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) Configuration Provider to load app configuration values from Azure Key Vault secrets.</span></span> <span data-ttu-id="0aa60-106">Azure Key Vault 是基于云的服务，可帮助保护加密密钥和机密使用的应用和服务。</span><span class="sxs-lookup"><span data-stu-id="0aa60-106">Azure Key Vault is a cloud-based service that assists in safeguarding cryptographic keys and secrets used by apps and services.</span></span> <span data-ttu-id="0aa60-107">使用 ASP.NET Core 应用使用 Azure 密钥保管库的常见方案包括：</span><span class="sxs-lookup"><span data-stu-id="0aa60-107">Common scenarios for using Azure Key Vault with ASP.NET Core apps include:</span></span>

* <span data-ttu-id="0aa60-108">控制对敏感的配置数据的访问。</span><span class="sxs-lookup"><span data-stu-id="0aa60-108">Controlling access to sensitive configuration data.</span></span>
* <span data-ttu-id="0aa60-109">存储配置数据时，满足的要求 FIPS 140-2 级别 2 验证硬件安全模块 (HSM)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-109">Meeting the requirement for FIPS 140-2 Level 2 validated Hardware Security Modules (HSM's) when storing configuration data.</span></span>

<span data-ttu-id="0aa60-110">这种情况下是可用于应用程序面向 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="0aa60-110">This scenario is available for apps that target ASP.NET Core 2.1 or later.</span></span>

<span data-ttu-id="0aa60-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0aa60-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="packages"></a><span data-ttu-id="0aa60-112">包</span><span class="sxs-lookup"><span data-stu-id="0aa60-112">Packages</span></span>

<span data-ttu-id="0aa60-113">若要使用 Azure 密钥保管库配置提供程序，添加到包引用[Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/)包。</span><span class="sxs-lookup"><span data-stu-id="0aa60-113">To use the Azure Key Vault Configuration Provider, add a package reference to the [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/) package.</span></span>

<span data-ttu-id="0aa60-114">若要采用[托管于 Azure 资源的标识](/azure/active-directory/managed-identities-azure-resources/overview)方案中，添加到包引用[Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication/)包。</span><span class="sxs-lookup"><span data-stu-id="0aa60-114">To adopt the [Managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/overview) scenario, add a package reference to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication/) package.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa60-115">在撰写本文时，最新稳定版本的`Microsoft.Azure.Services.AppAuthentication`，版本`1.0.3`，提供对支持[系统分配给托管标识](/azure/active-directory/managed-identities-azure-resources/overview#how-does-the-managed-identities-for-azure-resources-worka-namehow-does-it-worka)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-115">At the time of writing, the latest stable release of `Microsoft.Azure.Services.AppAuthentication`, version `1.0.3`, provides support for [system-assigned managed identities](/azure/active-directory/managed-identities-azure-resources/overview#how-does-the-managed-identities-for-azure-resources-worka-namehow-does-it-worka).</span></span> <span data-ttu-id="0aa60-116">为支持*用户分配托管标识*现已推出`1.0.2-preview`包。</span><span class="sxs-lookup"><span data-stu-id="0aa60-116">Support for *user-assigned managed identities* is available in the `1.0.2-preview` package.</span></span> <span data-ttu-id="0aa60-117">本主题演示如何使用系统管理的标识，并提供的示例应用使用版本`1.0.3`的`Microsoft.Azure.Services.AppAuthentication`包。</span><span class="sxs-lookup"><span data-stu-id="0aa60-117">This topic demonstrates the use of system-managed identities, and the provided sample app uses version `1.0.3` of the `Microsoft.Azure.Services.AppAuthentication` package.</span></span>

## <a name="sample-app"></a><span data-ttu-id="0aa60-118">示例应用</span><span class="sxs-lookup"><span data-stu-id="0aa60-118">Sample app</span></span>

<span data-ttu-id="0aa60-119">由两种模式之一运行示例应用`#define`顶部的语句*Program.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="0aa60-119">The sample app runs in either of two modes determined by the `#define` statement at the top of the *Program.cs* file:</span></span>

* <span data-ttu-id="0aa60-120">`Basic` &ndash; 演示如何使用访问密钥保管库中存储的机密的 Azure 密钥保管库应用程序 ID 和密码 （客户端机密）。</span><span class="sxs-lookup"><span data-stu-id="0aa60-120">`Basic` &ndash; Demonstrates the use of an Azure Key Vault Application ID and Password (Client Secret) to access secrets stored in the key vault.</span></span> <span data-ttu-id="0aa60-121">部署`Basic`版本到任何主机能够为 ASP.NET Core 应用提供服务的示例。</span><span class="sxs-lookup"><span data-stu-id="0aa60-121">Deploy the `Basic` version of the sample to any host capable of serving an ASP.NET Core app.</span></span> <span data-ttu-id="0aa60-122">遵循中的指导[使用应用程序 ID 和 Azure 托管的应用程序的客户端机密](#use-application-id-and-client-secret-for-non-azure-hosted-apps)部分。</span><span class="sxs-lookup"><span data-stu-id="0aa60-122">Follow the guidance in the [Use Application ID and Client Secret for non-Azure-hosted apps](#use-application-id-and-client-secret-for-non-azure-hosted-apps) section.</span></span>
* <span data-ttu-id="0aa60-123">`Managed` &ndash; 演示如何使用[托管于 Azure 资源的标识](/azure/active-directory/managed-identities-azure-resources/overview)应用进行身份验证对 Azure Key Vault 与 Azure AD 身份验证而无需在应用程序的代码或配置中存储的凭据。</span><span class="sxs-lookup"><span data-stu-id="0aa60-123">`Managed` &ndash; Demonstrates how to use [Managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/overview) to authenticate the app to Azure Key Vault with Azure AD authentication without credentials stored in the app's code or configuration.</span></span> <span data-ttu-id="0aa60-124">当使用管理的标识进行身份验证，不需要的 Azure AD 应用程序 ID 和密码 （客户端机密）。</span><span class="sxs-lookup"><span data-stu-id="0aa60-124">When using managed identities to authenticate, an Azure AD Application ID and Password (Client Secret) aren't required.</span></span> <span data-ttu-id="0aa60-125">`Managed`示例的版本必须部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="0aa60-125">The `Managed` version of the sample must be deployed to Azure.</span></span> <span data-ttu-id="0aa60-126">遵循中的指导[使用 Azure 资源的托管标识](#use-managed-identities-for-azure-resources)部分。</span><span class="sxs-lookup"><span data-stu-id="0aa60-126">Follow the guidance in the [Use the Managed identities for Azure resources](#use-managed-identities-for-azure-resources) section.</span></span>

<span data-ttu-id="0aa60-127">有关如何配置使用预处理器指令的示例应用程序的详细信息 (`#define`)，请参阅<xref:index#preprocessor-directives-in-sample-code>。</span><span class="sxs-lookup"><span data-stu-id="0aa60-127">For more information on how to configure a sample app using preprocessor directives (`#define`), see <xref:index#preprocessor-directives-in-sample-code>.</span></span>

## <a name="secret-storage-in-the-development-environment"></a><span data-ttu-id="0aa60-128">在开发环境中的机密存储</span><span class="sxs-lookup"><span data-stu-id="0aa60-128">Secret storage in the Development environment</span></span>

<span data-ttu-id="0aa60-129">设置本地使用的机密[机密管理器工具](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-129">Set secrets locally using the [Secret Manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="0aa60-130">机密时在开发环境中在本地计算机上运行示例应用程序，将加载本地机密管理器存储中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-130">When the sample app runs on the local machine in the Development environment, secrets are loaded from the local Secret Manager store.</span></span>

<span data-ttu-id="0aa60-131">机密管理器工具需要`<UserSecretsId>`应用的项目文件中的属性。</span><span class="sxs-lookup"><span data-stu-id="0aa60-131">The Secret Manager tool requires a `<UserSecretsId>` property in the app's project file.</span></span> <span data-ttu-id="0aa60-132">设置属性值 (`{GUID}`) 为任何唯一的 GUID:</span><span class="sxs-lookup"><span data-stu-id="0aa60-132">Set the property value (`{GUID}`) to any unique GUID:</span></span>

```xml
<PropertyGroup>
  <UserSecretsId>{GUID}</UserSecretsId>
</PropertyGroup>
```

<span data-ttu-id="0aa60-133">以名称-值对的形式创建机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-133">Secrets are created as name-value pairs.</span></span> <span data-ttu-id="0aa60-134">层次结构的值 （配置节） 使用`:`（冒号） 作为分隔符，在[ASP.NET Core 配置](xref:fundamentals/configuration/index)密钥名称。</span><span class="sxs-lookup"><span data-stu-id="0aa60-134">Hierarchical values (configuration sections) use a `:` (colon) as a separator in [ASP.NET Core configuration](xref:fundamentals/configuration/index) key names.</span></span>

<span data-ttu-id="0aa60-135">机密管理器用于从命令行界面打开项目的内容根，其中`{SECRET NAME}`名称和`{SECRET VALUE}`的值：</span><span class="sxs-lookup"><span data-stu-id="0aa60-135">The Secret Manager is used from a command shell opened to the project's content root, where `{SECRET NAME}` is the name and `{SECRET VALUE}` is the value:</span></span>

```console
dotnet user-secrets set "{SECRET NAME}" "{SECRET VALUE}"
```

<span data-ttu-id="0aa60-136">在项目的内容根设置示例应用程序机密从命令行界面中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="0aa60-136">Execute the following commands in a command shell from the project's content root to set the secrets for the sample app:</span></span>

```console
dotnet user-secrets set "SecretName" "secret_value_1_dev"
dotnet user-secrets set "Section:SecretName" "secret_value_2_dev"
```

<span data-ttu-id="0aa60-137">如果为这些机密存储在 Azure 密钥保管库中[使用 Azure 密钥保管库在生产环境中的机密存储](#secret-storage-in-the-production-environment-with-azure-key-vault)部分中，`_dev`后缀更改为`_prod`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-137">When these secrets are stored in Azure Key Vault in the [Secret storage in the Production environment with Azure Key Vault](#secret-storage-in-the-production-environment-with-azure-key-vault) section, the `_dev` suffix is changed to `_prod`.</span></span> <span data-ttu-id="0aa60-138">后缀提供了在应用程序的输出中的源的配置值，该值指示一个视觉提示。</span><span class="sxs-lookup"><span data-stu-id="0aa60-138">The suffix provides a visual cue in the app's output indicating the source of the configuration values.</span></span>

## <a name="secret-storage-in-the-production-environment-with-azure-key-vault"></a><span data-ttu-id="0aa60-139">使用 Azure 密钥保管库在生产环境中的机密存储</span><span class="sxs-lookup"><span data-stu-id="0aa60-139">Secret storage in the Production environment with Azure Key Vault</span></span>

<span data-ttu-id="0aa60-140">提供的说明[快速入门：设置和使用 Azure CLI 的 Azure Key Vault 中检索机密](/azure/key-vault/quick-create-cli)主题摘要如下用于创建 Azure 密钥保管库和存储使用的示例应用程序机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-140">The instructions provided by the [Quickstart: Set and retrieve a secret from Azure Key Vault using Azure CLI](/azure/key-vault/quick-create-cli) topic are summarized here for creating an Azure Key Vault and storing secrets used by the sample app.</span></span> <span data-ttu-id="0aa60-141">请参阅本主题的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="0aa60-141">Refer to the topic for further details.</span></span>

1. <span data-ttu-id="0aa60-142">使用中的以下方法之一打开 Azure Cloud shell [Azure 门户](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="0aa60-142">Open Azure Cloud shell using any one of the following methods in the [Azure portal](https://portal.azure.com/):</span></span>

   * <span data-ttu-id="0aa60-143">选择**试用**代码块右上角。</span><span class="sxs-lookup"><span data-stu-id="0aa60-143">Select **Try It** in the upper-right corner of a code block.</span></span> <span data-ttu-id="0aa60-144">在文本框中使用的搜索字符串"Azure CLI"。</span><span class="sxs-lookup"><span data-stu-id="0aa60-144">Use the search string "Azure CLI" in the text box.</span></span>
   * <span data-ttu-id="0aa60-145">与在浏览器中打开 Cloud Shell**启动 Cloud Shell**按钮。</span><span class="sxs-lookup"><span data-stu-id="0aa60-145">Open Cloud Shell in your browser with the **Launch Cloud Shell** button.</span></span>
   * <span data-ttu-id="0aa60-146">选择**Cloud Shell**在 Azure 门户的右上角菜单上的按钮。</span><span class="sxs-lookup"><span data-stu-id="0aa60-146">Select the **Cloud Shell** button on the menu in the upper-right corner of the Azure portal.</span></span>

   <span data-ttu-id="0aa60-147">有关详细信息，请参阅[Azure 命令行接口 (CLI)](/cli/azure/)并[Azure Cloud Shell 的概述](/azure/cloud-shell/overview)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-147">For more information, see [Azure Command-Line Interface (CLI)](/cli/azure/) and [Overview of Azure Cloud Shell](/azure/cloud-shell/overview).</span></span>

1. <span data-ttu-id="0aa60-148">如果你不已通过身份验证，登录时使用`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="0aa60-148">If you aren't already authenticated, sign in with the `az login` command.</span></span>

1. <span data-ttu-id="0aa60-149">使用以下命令创建资源组位置`{RESOURCE GROUP NAME}`是新的资源组的资源组名称和`{LOCATION}`是 Azure 区域 （数据中心）：</span><span class="sxs-lookup"><span data-stu-id="0aa60-149">Create a resource group with the following command, where `{RESOURCE GROUP NAME}` is the resource group name for the new resource group and `{LOCATION}` is the Azure region (datacenter):</span></span>

   ```console
   az group create --name "{RESOURCE GROUP NAME}" --location {LOCATION}
   ```

1. <span data-ttu-id="0aa60-150">使用以下命令在资源组中创建密钥保管库位置`{KEY VAULT NAME}`是新的密钥保管库的名称和`{LOCATION}`是 Azure 区域 （数据中心）：</span><span class="sxs-lookup"><span data-stu-id="0aa60-150">Create a key vault in the resource group with the following command, where `{KEY VAULT NAME}` is the name for the new key vault and `{LOCATION}` is the Azure region (datacenter):</span></span>

   ```console
   az keyvault create --name "{KEY VAULT NAME}" --resource-group "{RESOURCE GROUP NAME}" --location {LOCATION}
   ```

1. <span data-ttu-id="0aa60-151">以名称-值对的形式，在密钥保管库中创建机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-151">Create secrets in the key vault as name-value pairs.</span></span>

   <span data-ttu-id="0aa60-152">Azure 密钥保管库机密名称被限制为字母数字字符和短划线。</span><span class="sxs-lookup"><span data-stu-id="0aa60-152">Azure Key Vault secret names are limited to alphanumeric characters and dashes.</span></span> <span data-ttu-id="0aa60-153">层次结构的值 （配置节） 使用`--`（两个短划线） 作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="0aa60-153">Hierarchical values (configuration sections) use `--` (two dashes) as a separator.</span></span> <span data-ttu-id="0aa60-154">通常用于分隔部分中的一个子项中的冒号[ASP.NET Core 配置](xref:fundamentals/configuration/index)，不允许在密钥保管库机密名称。</span><span class="sxs-lookup"><span data-stu-id="0aa60-154">Colons, which are normally used to delimit a section from a subkey in [ASP.NET Core configuration](xref:fundamentals/configuration/index), aren't allowed in key vault secret names.</span></span> <span data-ttu-id="0aa60-155">因此，两个短划线的使用和机密加载到应用的配置时交换的冒号。</span><span class="sxs-lookup"><span data-stu-id="0aa60-155">Therefore, two dashes are used and swapped for a colon when the secrets are loaded into the app's configuration.</span></span>

   <span data-ttu-id="0aa60-156">以下密文密码是用于示例应用。</span><span class="sxs-lookup"><span data-stu-id="0aa60-156">The following secrets are for use with the sample app.</span></span> <span data-ttu-id="0aa60-157">值包括`_prod`后缀，以便区分从`_dev`后缀用户机密从开发环境中加载的值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-157">The values include a `_prod` suffix to distinguish them from the `_dev` suffix values loaded in the Development environment from User Secrets.</span></span> <span data-ttu-id="0aa60-158">替换为`{KEY VAULT NAME}`之前步骤中创建的密钥保管库的名称：</span><span class="sxs-lookup"><span data-stu-id="0aa60-158">Replace `{KEY VAULT NAME}` with the name of the key vault that you created in the prior step:</span></span>

   ```console
   az keyvault secret set --vault-name "{KEY VAULT NAME}" --name "SecretName" --value "secret_value_1_prod"
   az keyvault secret set --vault-name "{KEY VAULT NAME}" --name "Section--SecretName" --value "secret_value_2_prod"
   ```

## <a name="use-application-id-and-client-secret-for-non-azure-hosted-apps"></a><span data-ttu-id="0aa60-159">使用 Azure 托管的应用程序的应用程序 ID 和客户端机密</span><span class="sxs-lookup"><span data-stu-id="0aa60-159">Use Application ID and Client Secret for non-Azure-hosted apps</span></span>

<span data-ttu-id="0aa60-160">配置 Azure AD、 Azure 密钥保管库，并应用使用的应用程序 ID 和密码 （客户端机密） 到密钥保管库进行身份验证**当应用程序承载在 Azure 外部**。</span><span class="sxs-lookup"><span data-stu-id="0aa60-160">Configure Azure AD, Azure Key Vault, and the app to use an Application ID and Password (Client Secret) to authenticate to a key vault **when the app is hosted outside of Azure**.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa60-161">尽管对于在 Azure 中托管的应用支持使用应用程序 ID 和密码 （客户端机密），我们建议使用[托管于 Azure 资源的标识](#use-managed-identities-for-azure-resources)托管在 Azure 中的应用时。</span><span class="sxs-lookup"><span data-stu-id="0aa60-161">Although using an Application ID and Password (Client Secret) is supported for apps hosted in Azure, we recommend using [Managed identities for Azure resources](#use-managed-identities-for-azure-resources) when hosting an app in Azure.</span></span> <span data-ttu-id="0aa60-162">管理的标识不需要将凭据存储在应用程序或其配置，因此它被视为通常更安全的方法。</span><span class="sxs-lookup"><span data-stu-id="0aa60-162">Managed identities doesn't require storing credentials in the app or its configuration, so it's regarded as a generally safer approach.</span></span>

<span data-ttu-id="0aa60-163">示例应用时使用的应用程序 ID 和密码 （客户端机密）`#define`顶部的语句*Program.cs*文件设置为`Basic`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-163">The sample app uses an Application ID and Password (Client Secret) when the `#define` statement at the top of the *Program.cs* file is set to `Basic`.</span></span>

1. <span data-ttu-id="0aa60-164">与 Azure AD 注册应用程序和建立应用的标识的密码 （客户端机密）。</span><span class="sxs-lookup"><span data-stu-id="0aa60-164">Register the app with Azure AD and establish a Password (Client Secret) for the app's identity.</span></span>
1. <span data-ttu-id="0aa60-165">将密钥保管库名称、 应用程序 ID 和客户端密码/密钥存储在应用程序的*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="0aa60-165">Store the key vault name, Application ID, and Password/Client Secret in the app's *appsettings.json* file.</span></span>
1. <span data-ttu-id="0aa60-166">导航到**密钥保管库**在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-166">Navigate to **Key vaults** in the Azure portal.</span></span>
1. <span data-ttu-id="0aa60-167">选择你在中创建的密钥保管库[使用 Azure 密钥保管库在生产环境中的机密存储](#secret-storage-in-the-production-environment-with-azure-key-vault)部分。</span><span class="sxs-lookup"><span data-stu-id="0aa60-167">Select the key vault that you created in the [Secret storage in the Production environment with Azure Key Vault](#secret-storage-in-the-production-environment-with-azure-key-vault) section.</span></span>
1. <span data-ttu-id="0aa60-168">选择**访问策略**。</span><span class="sxs-lookup"><span data-stu-id="0aa60-168">Select **Access policies**.</span></span>
1. <span data-ttu-id="0aa60-169">选择**添加新**。</span><span class="sxs-lookup"><span data-stu-id="0aa60-169">Select **Add new**.</span></span>
1. <span data-ttu-id="0aa60-170">选择**选择主体**并按名称选择已注册的应用。</span><span class="sxs-lookup"><span data-stu-id="0aa60-170">Select **Select principal** and select the registered app by name.</span></span> <span data-ttu-id="0aa60-171">选择**选择**按钮。</span><span class="sxs-lookup"><span data-stu-id="0aa60-171">Select the **Select** button.</span></span>
1. <span data-ttu-id="0aa60-172">打开**机密权限**，并提供应用程序与**获取**并**列表**权限。</span><span class="sxs-lookup"><span data-stu-id="0aa60-172">Open **Secret permissions** and provide the app with **Get** and **List** permissions.</span></span>
1. <span data-ttu-id="0aa60-173">选择 **确定**。</span><span class="sxs-lookup"><span data-stu-id="0aa60-173">Select **OK**.</span></span>
1. <span data-ttu-id="0aa60-174">选择“保存”。</span><span class="sxs-lookup"><span data-stu-id="0aa60-174">Select **Save**.</span></span>
1. <span data-ttu-id="0aa60-175">将应用部署。</span><span class="sxs-lookup"><span data-stu-id="0aa60-175">Deploy the app.</span></span>

<span data-ttu-id="0aa60-176">`Basic`示例应用程序获取从其配置值`IConfigurationRoot`具有作为机密名称相同的名称：</span><span class="sxs-lookup"><span data-stu-id="0aa60-176">The `Basic` sample app obtains its configuration values from `IConfigurationRoot` with the same name as the secret name:</span></span>

* <span data-ttu-id="0aa60-177">非层次结构的值：值`SecretName`一起被获取`config["SecretName"]`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-177">Non-hierarchical values: The value for `SecretName` is obtained with `config["SecretName"]`.</span></span>
* <span data-ttu-id="0aa60-178">层次结构的值 （部分）：使用`:`（冒号） 表示法或`GetSection`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="0aa60-178">Hierarchical values (sections): Use `:` (colon) notation or the `GetSection` extension method.</span></span> <span data-ttu-id="0aa60-179">使用任一方法获取的配置值：</span><span class="sxs-lookup"><span data-stu-id="0aa60-179">Use either of these approaches to obtain the configuration value:</span></span>
  * `config["Section:SecretName"]`
  * `config.GetSection("Section")["SecretName"]`

<span data-ttu-id="0aa60-180">应用程序调用`AddAzureKeyVault`提供的值与*appsettings.json*文件：</span><span class="sxs-lookup"><span data-stu-id="0aa60-180">The app calls `AddAzureKeyVault` with values supplied by the *appsettings.json* file:</span></span>

[!code-csharp[](key-vault-configuration/sample/Program.cs?name=snippet1&highlight=11-14)]

<span data-ttu-id="0aa60-181">示例值：</span><span class="sxs-lookup"><span data-stu-id="0aa60-181">Example values:</span></span>

* <span data-ttu-id="0aa60-182">密钥保管库名称： `contosovault`</span><span class="sxs-lookup"><span data-stu-id="0aa60-182">Key vault name: `contosovault`</span></span>
* <span data-ttu-id="0aa60-183">应用程序 ID: `627e911e-43cc-61d4-992e-12db9c81b413`</span><span class="sxs-lookup"><span data-stu-id="0aa60-183">Application ID: `627e911e-43cc-61d4-992e-12db9c81b413`</span></span>
* <span data-ttu-id="0aa60-184">密码： `g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=`</span><span class="sxs-lookup"><span data-stu-id="0aa60-184">Password: `g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=`</span></span>

<span data-ttu-id="0aa60-185">appsettings.json：</span><span class="sxs-lookup"><span data-stu-id="0aa60-185">*appsettings.json*:</span></span>

[!code-json[](key-vault-configuration/sample/appsettings.json)]

<span data-ttu-id="0aa60-186">在运行应用时，网页显示加载的机密值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-186">When you run the app, a webpage shows the loaded secret values.</span></span> <span data-ttu-id="0aa60-187">在开发环境中，密钥值将加载与`_dev`后缀。</span><span class="sxs-lookup"><span data-stu-id="0aa60-187">In the Development environment, secret values load with the `_dev` suffix.</span></span> <span data-ttu-id="0aa60-188">在生产环境中，值将加载与`_prod`后缀。</span><span class="sxs-lookup"><span data-stu-id="0aa60-188">In the Production environment, the values load with the `_prod` suffix.</span></span>

## <a name="use-managed-identities-for-azure-resources"></a><span data-ttu-id="0aa60-189">使用 Azure 资源的托管标识</span><span class="sxs-lookup"><span data-stu-id="0aa60-189">Use Managed identities for Azure resources</span></span>

<span data-ttu-id="0aa60-190">**应用程序部署到 Azure**可以充分利用[管理 Azure 资源的标识](/azure/active-directory/managed-identities-azure-resources/overview)，它允许应用程序以使用 Azure 密钥保管库进行身份验证使用 Azure AD 身份验证，而无需凭据 (应用程序 ID 和Password/Client 机密) 存储在应用程序中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-190">**An app deployed to Azure** can take advantage of [Managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/overview), which allows the app to authenticate with Azure Key Vault using Azure AD authentication without credentials (Application ID and Password/Client Secret) stored in the app.</span></span>

<span data-ttu-id="0aa60-191">示例应用程序使用托管标识的 Azure 资源时`#define`顶部的语句*Program.cs*文件设置为`Managed`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-191">The sample app uses Managed identities for Azure resources when the `#define` statement at the top of the *Program.cs* file is set to `Managed`.</span></span>

<span data-ttu-id="0aa60-192">输入到应用中的保管库名称*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="0aa60-192">Enter the vault name into the app's *appsettings.json* file.</span></span> <span data-ttu-id="0aa60-193">示例应用程序不需要的应用程序 ID 和密码 （客户端机密） 设置为时`Managed`版本，因此可以忽略这些配置条目。</span><span class="sxs-lookup"><span data-stu-id="0aa60-193">The sample app doesn't require an Application ID and Password (Client Secret) when set to the `Managed` version, so you can ignore those configuration entries.</span></span> <span data-ttu-id="0aa60-194">将应用部署到 Azure 和 Azure 进行身份验证应用程序访问 Azure 密钥保管库仅使用保管库名称存储在*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="0aa60-194">The app is deployed to Azure, and Azure authenticates the app to access Azure Key Vault only using the vault name stored in the *appsettings.json* file.</span></span>

<span data-ttu-id="0aa60-195">将示例应用程序部署到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="0aa60-195">Deploy the sample app to Azure App Service.</span></span>

<span data-ttu-id="0aa60-196">与 Azure AD 创建服务时自动注册到 Azure 应用服务部署的应用。</span><span class="sxs-lookup"><span data-stu-id="0aa60-196">An app deployed to Azure App Service is automatically registered with Azure AD when the service is created.</span></span> <span data-ttu-id="0aa60-197">从以下命令中使用的部署中获取的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="0aa60-197">Obtain the Object ID from the deployment for use in the following command.</span></span> <span data-ttu-id="0aa60-198">在 Azure 门户上显示对象 ID**标识**面板中的应用服务。</span><span class="sxs-lookup"><span data-stu-id="0aa60-198">The Object ID is shown in the Azure portal on the **Identity** panel of the App Service.</span></span>

<span data-ttu-id="0aa60-199">使用 Azure CLI 和应用程序的对象 ID，提供应用程序与`list`和`get`权限访问密钥保管库：</span><span class="sxs-lookup"><span data-stu-id="0aa60-199">Using Azure CLI and the app's Object ID, provide the app with `list` and `get` permissions to access the key vault:</span></span>

```console
az keyvault set-policy --name '{KEY VAULT NAME}' --object-id {OBJECT ID} --secret-permissions get list
```

<span data-ttu-id="0aa60-200">**重启应用**使用 Azure CLI、 PowerShell 或 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="0aa60-200">**Restart the app** using Azure CLI, PowerShell, or the Azure portal.</span></span>

<span data-ttu-id="0aa60-201">应用程序示例：</span><span class="sxs-lookup"><span data-stu-id="0aa60-201">The sample app:</span></span>

* <span data-ttu-id="0aa60-202">创建的实例`AzureServiceTokenProvider`类，而连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0aa60-202">Creates an instance of the `AzureServiceTokenProvider` class without a connection string.</span></span> <span data-ttu-id="0aa60-203">时未提供连接字符串，该提供程序将尝试从 Azure 资源的托管标识获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="0aa60-203">When a connection string isn't provided, the provider attempts to obtain an access token from Managed identities for Azure resources.</span></span>
* <span data-ttu-id="0aa60-204">一个新`KeyVaultClient`使用创建`AzureServiceTokenProvider`实例令牌回调。</span><span class="sxs-lookup"><span data-stu-id="0aa60-204">A new `KeyVaultClient` is created with the `AzureServiceTokenProvider` instance token callback.</span></span>
* <span data-ttu-id="0aa60-205">`KeyVaultClient`实例使用的默认实现`IKeyVaultSecretManager`的加载所有机密值，并替换双短划线 (`--`) 用冒号 (`:`) 密钥名称。</span><span class="sxs-lookup"><span data-stu-id="0aa60-205">The `KeyVaultClient` instance is used with a default implementation of `IKeyVaultSecretManager` that loads all secret values and replaces double-dashes (`--`) with colons (`:`) in key names.</span></span>

[!code-csharp[](key-vault-configuration/sample/Program.cs?name=snippet2&highlight=13-21)]

<span data-ttu-id="0aa60-206">在运行应用时，网页显示加载的机密值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-206">When you run the app, a webpage shows the loaded secret values.</span></span> <span data-ttu-id="0aa60-207">在开发环境中，机密值具有`_dev`后缀，因为它们由用户机密提供。</span><span class="sxs-lookup"><span data-stu-id="0aa60-207">In the Development environment, secret values have the `_dev` suffix because they're provided by User Secrets.</span></span> <span data-ttu-id="0aa60-208">在生产环境中，值将加载与`_prod`后缀，因为它们由 Azure 密钥保管库提供。</span><span class="sxs-lookup"><span data-stu-id="0aa60-208">In the Production environment, the values load with the `_prod` suffix because they're provided by Azure Key Vault.</span></span>

<span data-ttu-id="0aa60-209">如果你收到`Access denied`错误，确认应用注册到 Azure AD 并提供访问密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="0aa60-209">If you receive an `Access denied` error, confirm that the app is registered with Azure AD and provided access to the key vault.</span></span> <span data-ttu-id="0aa60-210">确认已重新启动了该服务在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-210">Confirm that you've restarted the service in Azure.</span></span>

## <a name="use-a-key-name-prefix"></a><span data-ttu-id="0aa60-211">使用密钥名称前缀</span><span class="sxs-lookup"><span data-stu-id="0aa60-211">Use a key name prefix</span></span>

<span data-ttu-id="0aa60-212">`AddAzureKeyVault` 提供了接受的实现的重载`IKeyVaultSecretManager`，可用于控制如何密钥保管库机密将转换为配置项。</span><span class="sxs-lookup"><span data-stu-id="0aa60-212">`AddAzureKeyVault` provides an overload that accepts an implementation of `IKeyVaultSecretManager`, which allows you to control how key vault secrets are converted into configuration keys.</span></span> <span data-ttu-id="0aa60-213">例如，可以实现的接口来加载基于你在应用启动时提供的前缀值的机密值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-213">For example, you can implement the interface to load secret values based on a prefix value you provide at app startup.</span></span> <span data-ttu-id="0aa60-214">这可以使您例如，若要加载基于应用的版本的密钥。</span><span class="sxs-lookup"><span data-stu-id="0aa60-214">This allows you, for example, to load secrets based on the version of the app.</span></span>

> [!WARNING]
> <span data-ttu-id="0aa60-215">若要将多个应用的机密放入同一个密钥保管库或将环境机密不使用在密钥保管库机密的前缀 (例如，*开发*而不是*生产*机密) 到相同保管库。</span><span class="sxs-lookup"><span data-stu-id="0aa60-215">Don't use prefixes on key vault secrets to place secrets for multiple apps into the same key vault or to place environmental secrets (for example, *development* versus *production* secrets) into the same vault.</span></span> <span data-ttu-id="0aa60-216">我们建议，不同的应用程序和开发/生产环境使用单独的密钥保管库来隔离应用环境的最高级别的安全性。</span><span class="sxs-lookup"><span data-stu-id="0aa60-216">We recommend that different apps and development/production environments use separate key vaults to isolate app environments for the highest level of security.</span></span>

<span data-ttu-id="0aa60-217">在以下示例中，机密建立在密钥保管库 （和为开发环境中使用机密管理器工具） 的`5000-AppSecret`（句点不允许在密钥保管库机密名称）。</span><span class="sxs-lookup"><span data-stu-id="0aa60-217">In the following example, a secret is established in the key vault (and using the Secret Manager tool for the Development environment) for `5000-AppSecret` (periods aren't allowed in key vault secret names).</span></span> <span data-ttu-id="0aa60-218">此密钥表示为 5.0.0.0 版本的应用的应用程序机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-218">This secret represents an app secret for version 5.0.0.0 of the app.</span></span> <span data-ttu-id="0aa60-219">另一个版本的应用程序中，5.1.0.0，机密添加到密钥保管库 （并使用机密管理器工具） 的`5100-AppSecret`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-219">For another version of the app, 5.1.0.0, a secret is added to the key vault (and using the Secret Manager tool) for `5100-AppSecret`.</span></span> <span data-ttu-id="0aa60-220">每个应用程序版本将其版本控制的机密值加载到作为其配置`AppSecret`、 在加载机密的版本剥离。</span><span class="sxs-lookup"><span data-stu-id="0aa60-220">Each app version loads its versioned secret value into its configuration as `AppSecret`, stripping off the version as it loads the secret.</span></span>

<span data-ttu-id="0aa60-221">`AddAzureKeyVault` 使用自定义调用`IKeyVaultSecretManager`:</span><span class="sxs-lookup"><span data-stu-id="0aa60-221">`AddAzureKeyVault` is called with a custom `IKeyVaultSecretManager`:</span></span>

[!code-csharp[](key-vault-configuration/sample_snapshot/Program.cs?name=snippet1&highlight=22)]

<span data-ttu-id="0aa60-222">通过提供密钥保管库名称、 应用程序 ID 和密码 （客户端机密） 的值*appsettings.json*文件：</span><span class="sxs-lookup"><span data-stu-id="0aa60-222">The values for key vault name, Application ID, and Password (Client Secret) are provided by the *appsettings.json* file:</span></span>

[!code-json[](key-vault-configuration/sample/appsettings.json)]

<span data-ttu-id="0aa60-223">示例值：</span><span class="sxs-lookup"><span data-stu-id="0aa60-223">Example values:</span></span>

* <span data-ttu-id="0aa60-224">密钥保管库名称： `contosovault`</span><span class="sxs-lookup"><span data-stu-id="0aa60-224">Key vault name: `contosovault`</span></span>
* <span data-ttu-id="0aa60-225">应用程序 ID: `627e911e-43cc-61d4-992e-12db9c81b413`</span><span class="sxs-lookup"><span data-stu-id="0aa60-225">Application ID: `627e911e-43cc-61d4-992e-12db9c81b413`</span></span>
* <span data-ttu-id="0aa60-226">密码： `g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=`</span><span class="sxs-lookup"><span data-stu-id="0aa60-226">Password: `g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=`</span></span>

<span data-ttu-id="0aa60-227">`IKeyVaultSecretManager`实现应对要加载到配置的正确密钥的机密的版本前缀：</span><span class="sxs-lookup"><span data-stu-id="0aa60-227">The `IKeyVaultSecretManager` implementation reacts to the version prefixes of secrets to load the proper secret into configuration:</span></span>

[!code-csharp[](key-vault-configuration/sample_snapshot/Startup.cs?name=snippet1)]

<span data-ttu-id="0aa60-228">`Load`方法调用循环访问保管库机密以找出具有版本前缀的提供程序算法。</span><span class="sxs-lookup"><span data-stu-id="0aa60-228">The `Load` method is called by a provider algorithm that iterates through the vault secrets to find the ones that have the version prefix.</span></span> <span data-ttu-id="0aa60-229">当版本前缀找到`Load`，该算法使用`GetKey`方法返回的机密名称的配置名称。</span><span class="sxs-lookup"><span data-stu-id="0aa60-229">When a version prefix is found with `Load`, the algorithm uses the `GetKey` method to return the configuration name of the secret name.</span></span> <span data-ttu-id="0aa60-230">它剥离机密的名称从版本前缀，并返回到应用程序的配置名称-值对的加载的机密名称的其余部分。</span><span class="sxs-lookup"><span data-stu-id="0aa60-230">It strips off the version prefix from the secret's name and returns the rest of the secret name for loading into the app's configuration name-value pairs.</span></span>

<span data-ttu-id="0aa60-231">当此方法的实现：</span><span class="sxs-lookup"><span data-stu-id="0aa60-231">When this approach is implemented:</span></span>

1. <span data-ttu-id="0aa60-232">应用程序的项目文件中指定的应用程序的版本。</span><span class="sxs-lookup"><span data-stu-id="0aa60-232">The app's version specified in the app's project file.</span></span> <span data-ttu-id="0aa60-233">在以下示例中，应用程序的版本设置为`5.0.0.0`:</span><span class="sxs-lookup"><span data-stu-id="0aa60-233">In the following example, the app's version is set to `5.0.0.0`:</span></span>

   ```xml
   <PropertyGroup>
     <Version>5.0.0.0</Version>
   </PropertyGroup>
   ```

1. <span data-ttu-id="0aa60-234">确认`<UserSecretsId>`应用程序的项目文件中存在属性，则其中`{GUID}`是用户提供的 GUID:</span><span class="sxs-lookup"><span data-stu-id="0aa60-234">Confirm that a `<UserSecretsId>` property is present in the app's project file, where `{GUID}` is a user-supplied GUID:</span></span>

   ```xml
   <PropertyGroup>
     <UserSecretsId>{GUID}</UserSecretsId>
   </PropertyGroup>
   ```

   <span data-ttu-id="0aa60-235">保存使用在本地的以下机密[机密管理器工具](xref:security/app-secrets):</span><span class="sxs-lookup"><span data-stu-id="0aa60-235">Save the following secrets locally with the [Secret Manager tool](xref:security/app-secrets):</span></span>

   ```console
   dotnet user-secrets set "5000-AppSecret" "5.0.0.0_secret_value_dev"
   dotnet user-secrets set "5100-AppSecret" "5.1.0.0_secret_value_dev"
   ```

1. <span data-ttu-id="0aa60-236">使用以下 Azure CLI 命令在 Azure 密钥保管库中保存的机密：</span><span class="sxs-lookup"><span data-stu-id="0aa60-236">Secrets are saved in Azure Key Vault using the following Azure CLI commands:</span></span>

   ```console
   az keyvault secret set --vault-name "{KEY VAULT NAME}" --name "5000-AppSecret" --value "5.0.0.0_secret_value_prod"
   az keyvault secret set --vault-name "{KEY VAULT NAME}" --name "5100-AppSecret" --value "5.1.0.0_secret_value_prod"
   ```

1. <span data-ttu-id="0aa60-237">当应用运行时，会加载密钥保管库机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-237">When the app is run, the key vault secrets are loaded.</span></span> <span data-ttu-id="0aa60-238">字符串机密`5000-AppSecret`与应用程序的项目文件中指定的应用程序的版本匹配 (`5.0.0.0`)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-238">The string secret for `5000-AppSecret` is matched to the app's version specified in the app's project file (`5.0.0.0`).</span></span>

1. <span data-ttu-id="0aa60-239">版本，`5000`去除 （替换为短划线），的键名。</span><span class="sxs-lookup"><span data-stu-id="0aa60-239">The version, `5000` (with the dash), is stripped from the key name.</span></span> <span data-ttu-id="0aa60-240">在整个应用，使用密钥读取配置`AppSecret`加载机密值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-240">Throughout the app, reading configuration with the key `AppSecret` loads the secret value.</span></span>

1. <span data-ttu-id="0aa60-241">如果在项目文件中更改应用的版本`5.1.0.0`并再次运行应用时，返回的机密值是`5.1.0.0_secret_value_dev`开发环境中和`5.1.0.0_secret_value_prod`在生产环境中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-241">If the app's version is changed in the project file to `5.1.0.0` and the app is run again, the secret value returned is `5.1.0.0_secret_value_dev` in the Development environment and `5.1.0.0_secret_value_prod` in Production.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa60-242">您还可以提供您自己`KeyVaultClient`实现`AddAzureKeyVault`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-242">You can also provide your own `KeyVaultClient` implementation to `AddAzureKeyVault`.</span></span> <span data-ttu-id="0aa60-243">自定义客户端允许在应用之间共享客户端的单个实例。</span><span class="sxs-lookup"><span data-stu-id="0aa60-243">A custom client permits sharing a single instance of the client across the app.</span></span>

## <a name="authenticate-to-azure-key-vault-with-an-x509-certificate"></a><span data-ttu-id="0aa60-244">使用 X.509 证书对 Azure 密钥保管库</span><span class="sxs-lookup"><span data-stu-id="0aa60-244">Authenticate to Azure Key Vault with an X.509 certificate</span></span>

<span data-ttu-id="0aa60-245">在开发环境支持证书中的.NET Framework 应用时，可以使用 X.509 证书验证到 Azure 密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="0aa60-245">When developing a .NET Framework app in an environment that supports certificates, you can authenticate to Azure Key Vault with an X.509 certificate.</span></span> <span data-ttu-id="0aa60-246">X.509 证书的私钥由操作系统管理。</span><span class="sxs-lookup"><span data-stu-id="0aa60-246">The X.509 certificate's private key is managed by the OS.</span></span> <span data-ttu-id="0aa60-247">有关详细信息，请参阅[使用证书而不是客户端密码进行身份验证](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-247">For more information, see [Authenticate with a Certificate instead of a Client Secret](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret).</span></span> <span data-ttu-id="0aa60-248">使用`AddAzureKeyVault`接受重载`X509Certificate2`(`_env`在下面的示例：</span><span class="sxs-lookup"><span data-stu-id="0aa60-248">Use the `AddAzureKeyVault` overload that accepts an `X509Certificate2` (`_env` in the following example :</span></span>

```csharp
var builtConfig = config.Build();

var store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
var cert = store.Certificates
    .Find(X509FindType.FindByThumbprint, 
        config["CertificateThumbprint"], false);

config.AddAzureKeyVault(
    builtConfig["KeyVaultName"],
    builtConfig["AzureADApplicationId"],
    cert.OfType<X509Certificate2>().Single(),
    new EnvironmentSecretManager(context.HostingEnvironment.ApplicationName));

store.Close();
```

## <a name="bind-an-array-to-a-class"></a><span data-ttu-id="0aa60-249">将数组绑定至类</span><span class="sxs-lookup"><span data-stu-id="0aa60-249">Bind an array to a class</span></span>

<span data-ttu-id="0aa60-250">提供程序支持的配置值读入数组绑定到 POCO 数组。</span><span class="sxs-lookup"><span data-stu-id="0aa60-250">The provider is capable of reading configuration values into an array for binding to a POCO array.</span></span>

<span data-ttu-id="0aa60-251">从允许包含冒号的键的配置源读取数据时 (`:`) 使用分隔符，数字键段来区分对数组组成的密钥 (`:0:`， `:1:`，...</span><span class="sxs-lookup"><span data-stu-id="0aa60-251">When reading from a configuration source that allows keys to contain colon (`:`) separators, a numeric key segment is used to distinguish the keys that make up an array (`:0:`, `:1:`, …</span></span> <span data-ttu-id="0aa60-252">`:{n}:`）格式模式中出现的位置生成。</span><span class="sxs-lookup"><span data-stu-id="0aa60-252">`:{n}:`).</span></span> <span data-ttu-id="0aa60-253">有关详细信息，请参阅[配置：将数组绑定到一个类](xref:fundamentals/configuration/index#bind-an-array-to-a-class)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-253">For more information, see [Configuration: Bind an array to a class](xref:fundamentals/configuration/index#bind-an-array-to-a-class).</span></span>

<span data-ttu-id="0aa60-254">Azure 密钥保管库密钥不能使用冒号作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="0aa60-254">Azure Key Vault keys can't use a colon as a separator.</span></span> <span data-ttu-id="0aa60-255">本主题中介绍的方法使用双短划线 (`--`) 作为 （部分） 的层次结构值的分隔符。</span><span class="sxs-lookup"><span data-stu-id="0aa60-255">The approach described in this topic uses double dashes (`--`) as a separator for hierarchical values (sections).</span></span> <span data-ttu-id="0aa60-256">使用双短划线和数值的关键段数组密钥存储在 Azure 密钥保管库 (`--0--`， `--1--`，...</span><span class="sxs-lookup"><span data-stu-id="0aa60-256">Array keys are stored in Azure Key Vault with double dashes and numeric key segments (`--0--`, `--1--`, …</span></span> <span data-ttu-id="0aa60-257">`--{n}--`）格式模式中出现的位置生成。</span><span class="sxs-lookup"><span data-stu-id="0aa60-257">`--{n}--`).</span></span>

<span data-ttu-id="0aa60-258">请参阅以下[Serilog](https://serilog.net/)日志记录提供程序配置提供的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="0aa60-258">Examine the following [Serilog](https://serilog.net/) logging provider configuration provided by a JSON file.</span></span> <span data-ttu-id="0aa60-259">有两个对象中定义的文本`WriteTo`数组，它反映两个 Serilog*接收器*，其中介绍了日志记录输出的目标：</span><span class="sxs-lookup"><span data-stu-id="0aa60-259">There are two object literals defined in the `WriteTo` array that reflect two Serilog *sinks*, which describe destinations for logging output:</span></span>

```json
"Serilog": {
  "WriteTo": [
    {
      "Name": "AzureTableStorage",
      "Args": {
        "storageTableName": "logs",
        "connectionString": "DefaultEnd...ountKey=Eby8...GMGw=="
      }
    },
    {
      "Name": "AzureDocumentDB",
      "Args": {
        "endpointUrl": "https://contoso.documents.azure.com:443",
        "authorizationKey": "Eby8...GMGw=="
      }
    }
  ]
}
```

<span data-ttu-id="0aa60-260">在上面的 JSON 文件中所示的配置存储在 Azure 密钥保管库中使用双短划线 (`--`) 表示法和数字段：</span><span class="sxs-lookup"><span data-stu-id="0aa60-260">The configuration shown in the preceding JSON file is stored in Azure Key Vault using double dash (`--`) notation and numeric segments:</span></span>

| <span data-ttu-id="0aa60-261">键</span><span class="sxs-lookup"><span data-stu-id="0aa60-261">Key</span></span> | <span data-ttu-id="0aa60-262">“值”</span><span class="sxs-lookup"><span data-stu-id="0aa60-262">Value</span></span> |
| --- | ----- |
| `Serilog--WriteTo--0--Name` | `AzureTableStorage` |
| `Serilog--WriteTo--0--Args--storageTableName` | `logs` |
| `Serilog--WriteTo--0--Args--connectionString` | `DefaultEnd...ountKey=Eby8...GMGw==` |
| `Serilog--WriteTo--1--Name` | `AzureDocumentDB` |
| `Serilog--WriteTo--1--Args--endpointUrl` | `https://contoso.documents.azure.com:443` |
| `Serilog--WriteTo--1--Args--authorizationKey` | `Eby8...GMGw==` |

## <a name="reload-secrets"></a><span data-ttu-id="0aa60-263">重新加载机密</span><span class="sxs-lookup"><span data-stu-id="0aa60-263">Reload secrets</span></span>

<span data-ttu-id="0aa60-264">机密缓存，直至`IConfigurationRoot.Reload()`调用。</span><span class="sxs-lookup"><span data-stu-id="0aa60-264">Secrets are cached until `IConfigurationRoot.Reload()` is called.</span></span> <span data-ttu-id="0aa60-265">已过期，已禁用，并且已更新密钥保管库中的机密不遵循之前应用此`Reload`执行。</span><span class="sxs-lookup"><span data-stu-id="0aa60-265">Expired, disabled, and updated secrets in the key vault are not respected by the app until `Reload` is executed.</span></span>

```csharp
Configuration.Reload();
```

## <a name="disabled-and-expired-secrets"></a><span data-ttu-id="0aa60-266">已禁用和过期的机密</span><span class="sxs-lookup"><span data-stu-id="0aa60-266">Disabled and expired secrets</span></span>

<span data-ttu-id="0aa60-267">已禁用并已过期机密引发`KeyVaultClientException`。</span><span class="sxs-lookup"><span data-stu-id="0aa60-267">Disabled and expired secrets throw a `KeyVaultClientException`.</span></span> <span data-ttu-id="0aa60-268">若要防止应用引发，将为您的应用程序或更新已禁用或已过期机密。</span><span class="sxs-lookup"><span data-stu-id="0aa60-268">To prevent your app from throwing, replace your app or update the disabled/expired secret.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="0aa60-269">疑难解答</span><span class="sxs-lookup"><span data-stu-id="0aa60-269">Troubleshoot</span></span>

<span data-ttu-id="0aa60-270">如果应用程序无法加载使用提供程序的配置，一条错误消息写入到[ASP.NET Core 日志记录基础结构](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-270">When the app fails to load configuration using the provider, an error message is written to the [ASP.NET Core Logging infrastructure](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="0aa60-271">以下条件下将不加载配置：</span><span class="sxs-lookup"><span data-stu-id="0aa60-271">The following conditions will prevent configuration from loading:</span></span>

* <span data-ttu-id="0aa60-272">应用未正确配置 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="0aa60-272">The app isn't configured correctly in Azure Active Directory.</span></span>
* <span data-ttu-id="0aa60-273">密钥保管库不存在于 Azure 密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="0aa60-273">The key vault doesn't exist in Azure Key Vault.</span></span>
* <span data-ttu-id="0aa60-274">应用程序无权访问密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="0aa60-274">The app isn't authorized to access the key vault.</span></span>
* <span data-ttu-id="0aa60-275">访问策略不包括`Get`和`List`权限。</span><span class="sxs-lookup"><span data-stu-id="0aa60-275">The access policy doesn't include `Get` and `List` permissions.</span></span>
* <span data-ttu-id="0aa60-276">在密钥保管库，配置数据 （名称 / 值对） 是错误命名为，缺少，禁用，或已过期。</span><span class="sxs-lookup"><span data-stu-id="0aa60-276">In the key vault, the configuration data (name-value pair) is incorrectly named, missing, disabled, or expired.</span></span>
* <span data-ttu-id="0aa60-277">应用了错误的密钥保管库名称 (`KeyVaultName`)，Azure AD 应用程序 Id (`AzureADApplicationId`)，或 Azure AD 密码 （客户端机密） (`AzureADPassword`)。</span><span class="sxs-lookup"><span data-stu-id="0aa60-277">The app has the wrong key vault name (`KeyVaultName`), Azure AD Application Id (`AzureADApplicationId`), or Azure AD Password (Client Secret) (`AzureADPassword`).</span></span>
* <span data-ttu-id="0aa60-278">Azure AD 密码 （客户端机密） (`AzureADPassword`) 已过期。</span><span class="sxs-lookup"><span data-stu-id="0aa60-278">The Azure AD Password (Client Secret) (`AzureADPassword`) is expired.</span></span>
* <span data-ttu-id="0aa60-279">配置密钥 （名称） 不正确的应用中的想要加载的值。</span><span class="sxs-lookup"><span data-stu-id="0aa60-279">The configuration key (name) is incorrect in the app for the value you're trying to load.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aa60-280">其他资源</span><span class="sxs-lookup"><span data-stu-id="0aa60-280">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* [<span data-ttu-id="0aa60-281">Microsoft Azure:密钥保管库</span><span class="sxs-lookup"><span data-stu-id="0aa60-281">Microsoft Azure: Key Vault</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="0aa60-282">Microsoft Azure:密钥保管库文档</span><span class="sxs-lookup"><span data-stu-id="0aa60-282">Microsoft Azure: Key Vault Documentation</span></span>](/azure/key-vault/)
* [<span data-ttu-id="0aa60-283">如何生成和传输受 HSM 保护密钥的 Azure 密钥保管库</span><span class="sxs-lookup"><span data-stu-id="0aa60-283">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>](/azure/key-vault/key-vault-hsm-protected-keys)
* [<span data-ttu-id="0aa60-284">KeyVaultClient 类</span><span class="sxs-lookup"><span data-stu-id="0aa60-284">KeyVaultClient Class</span></span>](/dotnet/api/microsoft.azure.keyvault.keyvaultclient)

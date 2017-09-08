---
title: "適用於 .NET 的 Azure Key Vault 程式庫"
description: "適用於 .NET 的 Azure Key Vault 程式庫參考"
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 77a4e710e858bbeb98579a7b540b52b4cb9dd7b0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="a2544-104">適用於 .NET 的 Azure Key Vault 程式庫</span><span class="sxs-lookup"><span data-stu-id="a2544-104">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a2544-105">概觀</span><span class="sxs-lookup"><span data-stu-id="a2544-105">Overview</span></span>

<span data-ttu-id="a2544-106">Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="a2544-106">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="a2544-107">深入了解[什麼是 Key Vault？](/azure/key-vault/key-vault-whatis)然後[開始使用 Azure Key Vault](/azure/key-vault/key-vault-get-started) 或深入了解如何[從 Web 應用程式使用 Key Vault](/azure/key-vault/key-vault-use-from-web-application)。</span><span class="sxs-lookup"><span data-stu-id="a2544-107">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="a2544-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a2544-108">Client library</span></span>

<span data-ttu-id="a2544-109">使用用戶端程式庫來管理金鑰和相關的資產，例如憑證和祕密。</span><span class="sxs-lookup"><span data-stu-id="a2544-109">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="a2544-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a2544-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a2544-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a2544-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="a2544-112">範例</span><span class="sxs-lookup"><span data-stu-id="a2544-112">Example</span></span>

<span data-ttu-id="a2544-113">下列範例會擷取在應用程式設定中所識別特定金鑰的祕密。</span><span class="sxs-lookup"><span data-stu-id="a2544-113">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2544-114">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="a2544-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="a2544-115">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="a2544-115">Management library</span></span>

<span data-ttu-id="a2544-116">使用管理程式庫來建立、刪除和查詢金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="a2544-116">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="a2544-117">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a2544-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a2544-118">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a2544-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="a2544-119">範例</span><span class="sxs-lookup"><span data-stu-id="a2544-119">Example</span></span>

<span data-ttu-id="a2544-120">下列範例示範如何為指定的資源群組和位置建立新的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="a2544-120">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

```csharp
using (KeyVaultManagementClient client = new KeyVaultManagementClient(
    new TokenCloudCredentials(subscriptionId, accessToken)))
{
    client.Vaults.CreateOrUpdate(resourceGroupName, "myKeyVault", new VaultCreateOrUpdateParameters
    {
        Properties = new VaultProperties
        {
            EnabledForDeployment = true,
            EnabledForDiskEncryption = true,
            EnabledForTemplateDeployment = true,
            Location = resourceGroupLocation,
            // SKU level, access policies, tenants, etc.
        }
    });
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2544-121">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="a2544-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="a2544-122">範例</span><span class="sxs-lookup"><span data-stu-id="a2544-122">Samples</span></span>

* [<span data-ttu-id="a2544-123">下載 Azure Key Vault 用戶端範例</span><span class="sxs-lookup"><span data-stu-id="a2544-123">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="a2544-124">開始使用 .NET 的 Azure 用戶端加密</span><span class="sxs-lookup"><span data-stu-id="a2544-124">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="a2544-125">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="a2544-125">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package

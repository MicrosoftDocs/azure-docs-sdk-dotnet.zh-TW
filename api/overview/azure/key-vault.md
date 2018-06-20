---
title: 適用於 .NET 的 Azure Key Vault 程式庫
description: 適用於 .NET 的 Azure Key Vault 程式庫參考
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3b8bcb9135794592f493db679e60fd40116d05e6
ms.sourcegitcommit: 4114b8821f20e02f4185fcea7549d716f29b9c90
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
ms.locfileid: "23489182"
---
# <a name="azure-key-vault-libraries-for-net"></a>適用於 .NET 的 Azure Key Vault 程式庫

## <a name="overview"></a>概觀

Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。

深入了解[什麼是 Key Vault？](/azure/key-vault/key-vault-whatis)然後[開始使用 Azure Key Vault](/azure/key-vault/key-vault-get-started) 或深入了解如何[從 Web 應用程式使用 Key Vault](/azure/key-vault/key-vault-use-from-web-application)。

## <a name="client-library"></a>用戶端程式庫

使用用戶端程式庫來管理金鑰和相關的資產，例如憑證和祕密。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a>範例

下列範例會擷取在應用程式設定中所識別特定金鑰的祕密。

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a>管理程式庫

使用管理程式庫來建立、刪除和查詢金鑰保存庫。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a>範例

下列範例示範如何為指定的資源群組和位置建立新的金鑰保存庫。

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
> [探索管理 API](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a>範例

* [下載 Azure Key Vault 用戶端範例](https://www.microsoft.com/download/details.aspx?id=45343)
* [開始使用 .NET 的 Azure 用戶端加密](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure 復原服務和備份程式庫
description: 適用於 .NET 的 Azure 復原服務和備份程式庫
ms.date: 10/19/2017
ms.topic: reference
ms.service: recovery-services
ms.openlocfilehash: c0381ce9a566b5371faca24307edc7b26174e785
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190786"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a>適用於 .NET 的 Azure 復原服務和備份程式庫

## <a name="overview"></a>概觀

Azure 復原服務是一套資料復原服務，包括 [Azure 備份](/azure/backup/)和 [Azure 復原服務](/azure/site-recovery/)。

## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a>程式碼範例

下列程式碼範例會使用管理程式庫來觸發備份。

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

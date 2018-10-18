---
title: 適用於 .NET 的 Azure 復原服務和備份程式庫
description: 適用於 .NET 的 Azure 復原服務和備份程式庫
ms.date: 10/19/2017
ms.topic: reference
ms.service: backup
ms.openlocfilehash: c2faef5c83f28cb35158609b92f0334671161d1d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348170"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="e1234-103">適用於 .NET 的 Azure 復原服務和備份程式庫</span><span class="sxs-lookup"><span data-stu-id="e1234-103">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e1234-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e1234-104">Overview</span></span>

<span data-ttu-id="e1234-105">Azure 復原服務是一套資料復原服務，包括 [Azure 備份](/azure/backup/)和 [Azure 復原服務](/azure/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="e1234-105">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="e1234-106">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="e1234-106">Management library</span></span>

<span data-ttu-id="e1234-107">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="e1234-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e1234-108">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="e1234-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="e1234-109">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e1234-109">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1234-110">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="e1234-110">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="e1234-111">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="e1234-111">Code Example</span></span>

<span data-ttu-id="e1234-112">下列程式碼範例會使用管理程式庫來觸發備份。</span><span class="sxs-lookup"><span data-stu-id="e1234-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure 復原服務和備份程式庫
description: 適用於 .NET 的 Azure 復原服務和備份程式庫
keywords: Azure, .NET, SDK, API, 復原服務、備份
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: recovery-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3b399827f187fc2cb59c8698a555e63d08cee6c7
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566109"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="a1b33-104">適用於 .NET 的 Azure 復原服務和備份程式庫</span><span class="sxs-lookup"><span data-stu-id="a1b33-104">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a1b33-105">概觀</span><span class="sxs-lookup"><span data-stu-id="a1b33-105">Overview</span></span>

<span data-ttu-id="a1b33-106">Azure 復原服務是一套資料復原服務，包括 [Azure 備份](/azure/backup/)和 [Azure 復原服務](/azure/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="a1b33-106">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="a1b33-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="a1b33-107">Management library</span></span>

<span data-ttu-id="a1b33-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a1b33-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a1b33-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a1b33-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="a1b33-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a1b33-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1b33-111">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="a1b33-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="a1b33-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a1b33-112">Code Example</span></span>

<span data-ttu-id="a1b33-113">下列程式碼範例會使用管理程式庫來觸發備份。</span><span class="sxs-lookup"><span data-stu-id="a1b33-113">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

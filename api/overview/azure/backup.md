---
title: "適用於 .NET 的 Azure 備份程式庫"
description: "適用於 .NET 的 Azure 備份程式庫參考"
keywords: "Azure, .NET, SDK, API, 備份"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 93eeaeda1860e3b7190dfb0ae917b4b85b5a3609
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-backup-libraries-for-net"></a><span data-ttu-id="937c6-104">適用於 .NET 的 Azure 備份程式庫</span><span class="sxs-lookup"><span data-stu-id="937c6-104">Azure Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="937c6-105">概觀</span><span class="sxs-lookup"><span data-stu-id="937c6-105">Overview</span></span>

<span data-ttu-id="937c6-106">Azure 備份是一項雲端服務，您可用來備份、保護和還原資料。</span><span class="sxs-lookup"><span data-stu-id="937c6-106">Azure Backup is the cloud service you can use to back up, protect, and restore your data.</span></span>

<span data-ttu-id="937c6-107">若要深入了解 Azure 備份，請參閱[什麼是 Azure 備份？](/azure/backup/backup-introduction-to-azure-backup)。</span><span class="sxs-lookup"><span data-stu-id="937c6-107">Learn more about Azure Backup by reading [What is Azure Backup?](/azure/backup/backup-introduction-to-azure-backup).</span></span>

## <a name="management-library"></a><span data-ttu-id="937c6-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="937c6-108">Management library</span></span>

<span data-ttu-id="937c6-109">使用備份管理程式庫來管理備份並設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="937c6-109">Use the backup management library to manage backups and set up Recovery Services vaults.</span></span>

<span data-ttu-id="937c6-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="937c6-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="937c6-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="937c6-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

<span data-ttu-id="937c6-112">下列程式碼範例會使用管理程式庫來觸發備份。</span><span class="sxs-lookup"><span data-stu-id="937c6-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="937c6-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="937c6-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

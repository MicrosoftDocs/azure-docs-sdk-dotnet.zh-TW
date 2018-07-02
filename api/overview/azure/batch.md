---
title: 適用於 .NET 的 Azure Batch 程式庫
description: 適用於 .NET 的 Azure Batch 程式庫參考
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b6053e19d26247dd36ed7e38fc33030f96aecca8
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065555"
---
# <a name="azure-batch-libraries-for-net"></a>適用於 .NET 的 Azure Batch 程式庫

Azure Batch 是一項平台服務，可用於在雲端有效地執行大規模的平行和高效能運算 (HPC) 應用程式。 Azure Batch 可排程要在一組受控虛擬機器上執行的計算密集型工作，而且可以調整計算資源以符合工作的需求。

使用 Batch 時，您可以輕鬆定義用來大規模平行執行應用程式的 Azure 計算資源。 不需要手動建立、設定和管理 HPC 叢集、個別的虛擬機器、虛擬網路或複雜的作業和工作排程基礎結構。 Azure Batch 會為您自動執行或簡化這些工作。

深入了解如何[使用 Batch 執行本質平行的工作負載](/azure/batch/batch-technical-overview)。 您可以了解如何[開始使用適用於 .NET 的 Batch 用戶端程式庫來建置解決方案](/azure/batch/batch-dotnet-get-started)。 探索如何[使用適用於 .NET 的 Batch 管理程式庫來管理 Batch 帳戶和配額](/azure/batch/batch-management-dotnet)。

## <a name="client-library"></a>用戶端程式庫

使用用戶端程式庫以 Batch 執行平行的工作負載。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Azure.Batch)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a>範例

下列範例會使用用戶端 SDK 來建立要在 Azure Batch 中執行的工作。

```csharp
/*
using Microsoft.Azure.Batch.Auth;
using Microsoft.Azure.Batch;
*/
BatchSharedKeyCredentials credentials = new BatchSharedKeyCredentials(batchUrl, accountName, accountKey);
using (BatchClient batchClient = await BatchClient.OpenAsync(credentials))
{
    //set up pool specification and information along with resource files here
    JobManagerTask jobManagerTask = new JobManagerTask()
    {
        ResourceFiles = jobManagerResourceFiles,
        CommandLine = Constants.JobManagerExecutable,

        //Determines if the job should terminate when the job manager process exits.
        KillJobOnCompletion = true,
        Id = jobManagerTaskId
    };

    string jobId = Environment.GetEnvironmentVariable("USERNAME") + DateTime.UtcNow.ToString("yyyyMMdd-HHmmss");

    CloudJob unboundJob = batchClient.JobOperations.CreateJob(jobId, poolInformation);
    unboundJob.JobManagerTask = jobManagerTask;

    // now interact with the job ...
}
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a>管理程式庫

使用管理程式庫透過程式設計方式管理 Batch 帳戶、配額和應用程式套件。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a>範例

取出下列範例會擷取訂用帳戶的配額、建立帳戶，並重新產生主要帳戶金鑰。

```csharp
/*
using Microsoft.Azure.Management.Batch;
using Microsoft.Azure.Management.Batch.Models;
using Microsoft.Rest;
*/
using (BatchManagementClient batchManagementClient = new BatchManagementClient(new TokenCredentials(accessToken)))
{
    batchManagementClient.SubscriptionId = subscriptionId;

    // Get the account quota for the subscription
    BatchLocationQuota quotaResponse = await batchManagementClient.Location.GetQuotasAsync(location);
    Console.WriteLine("Your subscription can create {0} account(s) in the {1} region.", quotaResponse.AccountQuota, location);

    // Create account
    await batchManagementClient.BatchAccount.CreateAsync(ResourceGroupName, accountName, 
        new BatchAccountCreateParameters() { Location = location });

    // Regenerate primary account key
    BatchAccountKeys newKeys = await batchManagementClient.BatchAccount.RegenerateKeyAsync(
        ResourceGroupName, account.Name, AccountKeyType.Primary);
}
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a>範例

* [適用於 .NET 的 Azure Batch 用戶端和管理 SDK 範例](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

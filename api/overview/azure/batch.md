---
title: 適用於 .NET 的 Azure Batch 程式庫
description: 適用於 .NET 的 Azure Batch 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: batch
ms.openlocfilehash: 4220faacc9b8cbe394f98eaccd1e71aaf4ab8f0d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190111"
---
# <a name="azure-batch-libraries-for-net"></a><span data-ttu-id="9b9ed-103">適用於 .NET 的 Azure Batch 程式庫</span><span class="sxs-lookup"><span data-stu-id="9b9ed-103">Azure Batch libraries for .NET</span></span>

<span data-ttu-id="9b9ed-104">Azure Batch 是一項平台服務，可用於在雲端有效地執行大規模的平行和高效能運算 (HPC) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-104">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="9b9ed-105">Azure Batch 可排程要在一組受控虛擬機器上執行的計算密集型工作，而且可以調整計算資源以符合工作的需求。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-105">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="9b9ed-106">使用 Batch 時，您可以輕鬆定義用來大規模平行執行應用程式的 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-106">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="9b9ed-107">不需要手動建立、設定和管理 HPC 叢集、個別的虛擬機器、虛擬網路或複雜的作業和工作排程基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-107">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="9b9ed-108">Azure Batch 會為您自動執行或簡化這些工作。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-108">Azure Batch automates or simplifies these tasks for you.</span></span>

<span data-ttu-id="9b9ed-109">深入了解如何[使用 Batch 執行本質平行的工作負載](/azure/batch/batch-technical-overview)。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-109">Read more about how to [run intrinsically parallel workloads with Batch](/azure/batch/batch-technical-overview).</span></span> <span data-ttu-id="9b9ed-110">您可以了解如何[開始使用適用於 .NET 的 Batch 用戶端程式庫來建置解決方案](/azure/batch/batch-dotnet-get-started)。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-110">You can also learn how to [get started building solutions with the Batch client library for .NET](/azure/batch/batch-dotnet-get-started).</span></span> <span data-ttu-id="9b9ed-111">探索如何[使用適用於 .NET 的 Batch 管理程式庫來管理 Batch 帳戶和配額](/azure/batch/batch-management-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-111">Discover how to [manage Batch accounts and quotas with the Batch Management library for .NET](/azure/batch/batch-management-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="9b9ed-112">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="9b9ed-112">Client library</span></span>

<span data-ttu-id="9b9ed-113">使用用戶端程式庫以 Batch 執行平行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-113">Use the client library to run parallel workloads with Batch.</span></span>

<span data-ttu-id="9b9ed-114">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Azure.Batch)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-114">Install the [NuGet package](https://www.nuget.org/packages/Azure.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9b9ed-115">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9b9ed-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="9b9ed-116">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="9b9ed-116">.NET Core CLI</span></span>

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a><span data-ttu-id="9b9ed-117">範例</span><span class="sxs-lookup"><span data-stu-id="9b9ed-117">Example</span></span>

<span data-ttu-id="9b9ed-118">下列範例會使用用戶端 SDK 來建立要在 Azure Batch 中執行的工作。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-118">The following example uses the client SDK to create a job to run in Azure Batch.</span></span>

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
> [<span data-ttu-id="9b9ed-119">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="9b9ed-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a><span data-ttu-id="9b9ed-120">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="9b9ed-120">Management library</span></span>

<span data-ttu-id="9b9ed-121">使用管理程式庫透過程式設計方式管理 Batch 帳戶、配額和應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-121">Use the management library to programmatically manage Batch accounts, quotas, and application packages.</span></span>

<span data-ttu-id="9b9ed-122">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-122">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9b9ed-123">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9b9ed-123">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="9b9ed-124">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="9b9ed-124">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a><span data-ttu-id="9b9ed-125">範例</span><span class="sxs-lookup"><span data-stu-id="9b9ed-125">Example</span></span>

<span data-ttu-id="9b9ed-126">取出下列範例會擷取訂用帳戶的配額、建立帳戶，並重新產生主要帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-126">The following example retrieves the quota for the subscription, creates an account, and regenerates the primary account key.</span></span>

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
> [<span data-ttu-id="9b9ed-127">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="9b9ed-127">Explore the management APIs</span></span>](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a><span data-ttu-id="9b9ed-128">範例</span><span class="sxs-lookup"><span data-stu-id="9b9ed-128">Samples</span></span>

* [<span data-ttu-id="9b9ed-129">適用於 .NET 的 Azure Batch 用戶端和管理 SDK 範例</span><span class="sxs-lookup"><span data-stu-id="9b9ed-129">Azure Batch Client and Management SDK for .NET Samples</span></span>](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

<span data-ttu-id="9b9ed-130">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="9b9ed-130">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

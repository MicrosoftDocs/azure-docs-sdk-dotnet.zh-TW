---
title: "適用於 .NET 的 Azure Data Lake Store 程式庫"
description: "適用於 .NET 的 Azure Data Lake Store 程式庫參考"
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 18746d745d64065a3d92215e704bce575130bdb0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="5ad45-104">適用於 .NET 的 Azure Data Lake Store 程式庫</span><span class="sxs-lookup"><span data-stu-id="5ad45-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5ad45-105">概觀</span><span class="sxs-lookup"><span data-stu-id="5ad45-105">Overview</span></span>

<span data-ttu-id="5ad45-106">Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。</span><span class="sxs-lookup"><span data-stu-id="5ad45-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="5ad45-107">Azure Data Lake 可讓您在單一位置擷取任何大小、類型和擷取速度的資料，以便進行運作和探究分析。</span><span class="sxs-lookup"><span data-stu-id="5ad45-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="5ad45-108">若要進一步了解，請參閱 [Azure Data Lake Store 概觀](/azure/data-lake-store/data-lake-store-overview)。</span><span class="sxs-lookup"><span data-stu-id="5ad45-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="5ad45-109">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="5ad45-109">Management library</span></span>

<span data-ttu-id="5ad45-110">使用管理程式庫來連線並管理您的巨量資料存放庫。</span><span class="sxs-lookup"><span data-stu-id="5ad45-110">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="5ad45-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5ad45-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5ad45-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5ad45-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a><span data-ttu-id="5ad45-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5ad45-113">Code Example</span></span>

<span data-ttu-id="5ad45-114">此範例會向分析帳戶和存放區進行驗證，並建立管理所需的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ad45-114">This example authenticates to an analytics account and store and creates the clients necessary for management.</span></span>

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ad45-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="5ad45-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="5ad45-116">範例</span><span class="sxs-lookup"><span data-stu-id="5ad45-116">Samples</span></span>

* [<span data-ttu-id="5ad45-117">Azure Data Lake .NET 用戶端範例</span><span class="sxs-lookup"><span data-stu-id="5ad45-117">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="5ad45-118">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="5ad45-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package

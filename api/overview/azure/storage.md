---
title: "Azure .NET 儲存體 API"
description: "適用於 .NET 的 Azure 儲存體程式庫參考"
keywords: "Azure, .NET, SDK, API, 儲存體, blob"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f9928736fa024258bcf19ba5ad91f0a328aa05a8
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="5bc2a-104">適用於 .NET 的 Azure 儲存體 API</span><span class="sxs-lookup"><span data-stu-id="5bc2a-104">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5bc2a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="5bc2a-105">Overview</span></span>

<span data-ttu-id="5bc2a-106">使用 [Azure 儲存體](https://review.docs.microsoft.com/en-us/azure/storage/storage-introduction)從 .NET 應用程式讀取和寫入檔案、blob (物件) 資料、機碼值組以及訊息。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-106">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://review.docs.microsoft.com/en-us/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="5bc2a-107">若要開始使用 Azure 儲存體，請參閱[以 .NET 開始使用 Azure Blob 儲存體](/azure/storage/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-107">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="5bc2a-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="5bc2a-108">Client library</span></span>

<span data-ttu-id="5bc2a-109">使用[連接字串](/azure/storage/storage-create-storage-account#manage-your-storage-account)來連線到 Azure 儲存體帳戶，然後使用用戶端程式庫的類別和方法來處理 blob、資料表、檔案或佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-109">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="5bc2a-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/WindowsAzure.Storage)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-110">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5bc2a-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5bc2a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="5bc2a-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5bc2a-112">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="5bc2a-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5bc2a-113">Code Example</span></span>

<span data-ttu-id="5bc2a-114">此範例會在現有的儲存體帳戶中，將新的 blob 建立至新的容器。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-114">This example creates a new blob to a new container in an existing storage account.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
*/

string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=[Storage Account Name]"
    + ";AccountKey=[Storage Account Key]"
    + ";EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
CloudBlobClient serviceClient = account.CreateCloudBlobClient();

// Create container. Name must be lower case.
Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("mycontainer");
container.CreateIfNotExistsAsync().Wait();

// write a blob to the container
CloudBlockBlob blob = container.GetBlockBlobReference("helloworld.txt");
blob.UploadTextAsync("Hello, World!").Wait();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="5bc2a-115">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="5bc2a-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="5bc2a-116">管理 API</span><span class="sxs-lookup"><span data-stu-id="5bc2a-116">Management APIs</span></span>

<span data-ttu-id="5bc2a-117">使用管理 API 建立及管理 Azure 儲存體帳戶和連線金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="5bc2a-118">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5bc2a-119">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5bc2a-119">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="5bc2a-120">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5bc2a-120">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="5bc2a-121">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5bc2a-121">Code Example</span></span>

<span data-ttu-id="5bc2a-122">此範例會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-122">This example creates a storage account.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Management.Storage.Fluent
*/

IStorageAccount storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .Create();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="5bc2a-123">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="5bc2a-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="5bc2a-124">範例</span><span class="sxs-lookup"><span data-stu-id="5bc2a-124">Samples</span></span>

* [<span data-ttu-id="5bc2a-125">在 .NET 中開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="5bc2a-125">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [<span data-ttu-id="5bc2a-126">在 .NET 中開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="5bc2a-126">Get started with Azure Queue Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

<span data-ttu-id="5bc2a-127">檢視 Azure 儲存體範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage)。</span><span class="sxs-lookup"><span data-stu-id="5bc2a-127">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
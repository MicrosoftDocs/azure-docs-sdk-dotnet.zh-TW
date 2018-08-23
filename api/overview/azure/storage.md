---
title: Azure .NET 儲存體 API
description: 適用於 .NET 的 Azure 儲存體程式庫參考
keywords: Azure, .NET, SDK, API, 儲存體, blob
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e953f38f103631f94b844d803d20a6576e841ed3
ms.sourcegitcommit: 2a00655810b9b2c78a3edb31c974a9989bff8bc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2018
ms.locfileid: "42623353"
---
# <a name="azure-storage-apis-for-net"></a>適用於 .NET 的 Azure 儲存體 API

## <a name="overview"></a>概觀

使用 [Azure 儲存體](https://docs.microsoft.com/azure/storage/storage-introduction)從 .NET 應用程式讀取和寫入檔案、blob (物件) 資料、機碼值組以及訊息。

若要開始使用 Azure 儲存體，請參閱[以 .NET 開始使用 Azure Blob 儲存體](/azure/storage/storage-dotnet-how-to-use-blobs)。

## <a name="client-library"></a>用戶端程式庫

使用[連接字串](/azure/storage/storage-create-storage-account#manage-your-storage-account)來連線到 Azure 儲存體帳戶，然後使用用戶端程式庫的類別和方法來處理 blob、資料表、檔案或佇列儲存體。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/WindowsAzure.Storage)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a>程式碼範例

此範例會在現有的儲存體帳戶中，將新的 blob 建立至新的容器。

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
> [探索用戶端 API](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a>管理 API

使用管理 API 建立及管理 Azure 儲存體帳戶和連線金鑰。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a>程式碼範例

此範例會建立儲存體帳戶。

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
> [探索管理 API](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a>範例

* [在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [在 .NET 中開始使用 Azure 佇列儲存體](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

檢視 Azure 儲存體範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
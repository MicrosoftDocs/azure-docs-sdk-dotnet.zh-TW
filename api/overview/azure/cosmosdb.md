---
title: "適用於 .NET 的 Azure CosmosDB 程式庫"
description: "適用於 .NET 的 Azure CosmosDB 程式庫參考"
keywords: Azure, .NET, SDK, API, CosmosDB
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: babf34e98dae439a2dc3d4c63bd638335428e935
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="40a13-104">適用於 .NET 的 Azure CosmosDB 程式庫</span><span class="sxs-lookup"><span data-stu-id="40a13-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="40a13-105">概觀</span><span class="sxs-lookup"><span data-stu-id="40a13-105">Overview</span></span>

<span data-ttu-id="40a13-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分散式且可擴充的資料存放區，可支援多個不同類型的資料庫。</span><span class="sxs-lookup"><span data-stu-id="40a13-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

## <a name="client-library"></a><span data-ttu-id="40a13-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="40a13-107">Client library</span></span>

<span data-ttu-id="40a13-108">您可以使用 CosmosDB .NET 用戶端程式庫來存取並儲存 CosmosDB 資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="40a13-108">Use the CosmosDB .NET client library to access and store data in a CosmosDB data store.</span></span>

<span data-ttu-id="40a13-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="40a13-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="40a13-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="40a13-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="40a13-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="40a13-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="40a13-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="40a13-112">Code Example</span></span>

<span data-ttu-id="40a13-113">這個範例會連線到現有的 CosmosDB DocumentDB API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。</span><span class="sxs-lookup"><span data-stu-id="40a13-113">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
// "Item" is a class defined elsewhere...
Item item = client.ReadDocumentAsync<Item>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="40a13-114">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="40a13-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="40a13-115">範例</span><span class="sxs-lookup"><span data-stu-id="40a13-115">Samples</span></span>

* [<span data-ttu-id="40a13-116">使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="40a13-116">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="40a13-117">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="40a13-117">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure Cosmos DB 程式庫
description: 適用於 .NET 的 Azure Cosmos DB 程式庫參考
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 95fcd8468c3d472cfcadeaae3b56ae789c3b1e7a
ms.sourcegitcommit: 55ee51501678d1575e5159f0ac0e475b5bf9daf3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2019
ms.locfileid: "54453992"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="167b2-103">適用於 .NET 的 Azure Cosmos DB 程式庫</span><span class="sxs-lookup"><span data-stu-id="167b2-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="167b2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="167b2-104">Overview</span></span>

<span data-ttu-id="167b2-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是全域散發的多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="167b2-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="167b2-106">此服務的設計目的，是可透過全方位的 SLA，以有彈性且獨立的方式調整地理區域 (數量不限) 的輸送量及儲存空間。</span><span class="sxs-lookup"><span data-stu-id="167b2-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="167b2-107">透過 Azure Cosmos DB，您可以使用 API 和程式設計模型來儲存並存取文件、索引鍵/值組、寬列資料行以及圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="167b2-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="167b2-108">[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="167b2-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="167b2-109">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="167b2-109">Client library</span></span>

<span data-ttu-id="167b2-110">您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="167b2-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="167b2-111">請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="167b2-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="167b2-112">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="167b2-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="167b2-113">若要安裝版本 2.x：</span><span class="sxs-lookup"><span data-stu-id="167b2-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="167b2-114">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="167b2-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="167b2-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="167b2-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="167b2-116">若要安裝目標為 .NET Standard 的版本 3.0 預覽版本：</span><span class="sxs-lookup"><span data-stu-id="167b2-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="167b2-117">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="167b2-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="167b2-118">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="167b2-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="167b2-119">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="167b2-119">Code Example</span></span>

<span data-ttu-id="167b2-120">這個範例會連線到現有的 Azure Cosmos DB SQL API 資料庫，從集合中讀取文件，並將其還原序列化為 `TodoItem` 物件。</span><span class="sxs-lookup"><span data-stu-id="167b2-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `TodoItem` object.</span></span> <span data-ttu-id="167b2-121">此範例使用 .NET SDK 的 2.x 版本。</span><span class="sxs-lookup"><span data-stu-id="167b2-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

<span data-ttu-id="167b2-122">此範例會連線至現有的 Azure Cosmos DB SQL API 資料庫、建立新資料庫和容器、從容器中讀取項目並將其還原序列化至 `TodoItem` 物件。</span><span class="sxs-lookup"><span data-stu-id="167b2-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="167b2-123">此範例使用 .NET SDK 的 3.x 版本。</span><span class="sxs-lookup"><span data-stu-id="167b2-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="167b2-124">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="167b2-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="167b2-125">範例</span><span class="sxs-lookup"><span data-stu-id="167b2-125">Samples</span></span>

* [<span data-ttu-id="167b2-126">使用 Azure Cosmos DB 的 SQL API 開發 .NET 應用程式 (版本 2.x)</span><span class="sxs-lookup"><span data-stu-id="167b2-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="167b2-127">使用 Azure Cosmos DB 的 SQL API 開發 .NET 應用程式 (版本 3.x 預覽版)</span><span class="sxs-lookup"><span data-stu-id="167b2-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="167b2-128">使用 Azure Cosmos DB 的 SQL API 開發 .NET Core 應用程式 (版本 3.x 預覽版)</span><span class="sxs-lookup"><span data-stu-id="167b2-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="167b2-129">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="167b2-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

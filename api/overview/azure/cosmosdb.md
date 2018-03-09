---
title: "適用於 .NET 的 Azure CosmosDB 程式庫"
description: "適用於 .NET 的 Azure CosmosDB 程式庫參考"
keywords: Azure, .NET, SDK, API, CosmosDB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4791e00c18d00fbed13bdf2c626a24fed2ff2863
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="ba5c6-104">適用於 .NET 的 Azure CosmosDB 程式庫</span><span class="sxs-lookup"><span data-stu-id="ba5c6-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ba5c6-105">概觀</span><span class="sxs-lookup"><span data-stu-id="ba5c6-105">Overview</span></span>

<span data-ttu-id="ba5c6-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分散式且可擴充的資料存放區，可支援多個不同類型的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="ba5c6-107">[開始使用 CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span><span class="sxs-lookup"><span data-stu-id="ba5c6-107">[Get started with CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="ba5c6-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ba5c6-108">Client library</span></span>

<span data-ttu-id="ba5c6-109">您可以使用 CosmosDB .NET 用戶端程式庫來存取並在現有的 CosmosDB 資料存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-109">Use the CosmosDB .NET client library to access and store data in an existing CosmosDB data store.</span></span>  <span data-ttu-id="ba5c6-110">要自動建立新的 Cosmos 帳戶，請使用 Azure 入口網站、CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-110">To automate creation of a new CosmosDB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="ba5c6-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ba5c6-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="ba5c6-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="ba5c6-113">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="ba5c6-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="ba5c6-114">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="ba5c6-114">Code Example</span></span>

<span data-ttu-id="ba5c6-115">這個範例會連線到現有的 CosmosDB DocumentDB API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-115">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba5c6-116">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="ba5c6-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="ba5c6-117">範例</span><span class="sxs-lookup"><span data-stu-id="ba5c6-117">Samples</span></span>

* [<span data-ttu-id="ba5c6-118">使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba5c6-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="ba5c6-119">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="ba5c6-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

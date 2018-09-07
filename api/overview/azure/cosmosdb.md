---
title: 適用於 .NET 的 Azure Cosmos DB 程式庫
description: 適用於 .NET 的 Azure Cosmos DB 程式庫參考
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/31/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4928c1dfdb7a5bb50ca4f5023cbfec71e05e9061
ms.sourcegitcommit: 299aa7bdbb9cec1b56e42e25550999e53e23de2c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43839494"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="c88f0-104">適用於 .NET 的 Azure Cosmos DB 程式庫</span><span class="sxs-lookup"><span data-stu-id="c88f0-104">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c88f0-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c88f0-105">Overview</span></span>

<span data-ttu-id="c88f0-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是全域散發的多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="c88f0-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="c88f0-107">此服務的設計目的，是可透過全方位的 SLA，以有彈性且獨立的方式調整地理區域 (數量不限) 的輸送量及儲存空間。</span><span class="sxs-lookup"><span data-stu-id="c88f0-107">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="c88f0-108">透過 Azure Cosmos DB，您可以使用 API 和程式設計模型來儲存並存取文件、索引鍵/值組、寬列資料行以及圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="c88f0-108">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="c88f0-109">[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="c88f0-109">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="c88f0-110">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="c88f0-110">Client library</span></span>

<span data-ttu-id="c88f0-111">您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="c88f0-111">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="c88f0-112">請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c88f0-112">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="c88f0-113">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="c88f0-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c88f0-114">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="c88f0-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="c88f0-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="c88f0-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="c88f0-116">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c88f0-116">Code Example</span></span>

<span data-ttu-id="c88f0-117">這個範例會連線到現有的 Azure Cosmos DB SQL API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。</span><span class="sxs-lookup"><span data-stu-id="c88f0-117">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c88f0-118">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="c88f0-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="c88f0-119">範例</span><span class="sxs-lookup"><span data-stu-id="c88f0-119">Samples</span></span>

* [<span data-ttu-id="c88f0-120">使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="c88f0-120">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="c88f0-121">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="c88f0-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure Cosmos DB 程式庫
description: 適用於 .NET 的 Azure Cosmos DB 程式庫參考
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 21a2f2168259528a0d27103783e34aa532d7e17a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190787"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="c2c05-103">適用於 .NET 的 Azure Cosmos DB 程式庫</span><span class="sxs-lookup"><span data-stu-id="c2c05-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c2c05-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c2c05-104">Overview</span></span>

<span data-ttu-id="c2c05-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是全域散發的多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="c2c05-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="c2c05-106">此服務的設計目的，是可透過全方位的 SLA，以有彈性且獨立的方式調整地理區域 (數量不限) 的輸送量及儲存空間。</span><span class="sxs-lookup"><span data-stu-id="c2c05-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="c2c05-107">透過 Azure Cosmos DB，您可以使用 API 和程式設計模型來儲存並存取文件、索引鍵/值組、寬列資料行以及圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="c2c05-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="c2c05-108">[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="c2c05-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="c2c05-109">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="c2c05-109">Client library</span></span>

<span data-ttu-id="c2c05-110">您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="c2c05-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="c2c05-111">請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c2c05-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="c2c05-112">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="c2c05-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c2c05-113">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="c2c05-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="c2c05-114">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="c2c05-114">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="c2c05-115">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c2c05-115">Code Example</span></span>

<span data-ttu-id="c2c05-116">這個範例會連線到現有的 Azure Cosmos DB SQL API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。</span><span class="sxs-lookup"><span data-stu-id="c2c05-116">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2c05-117">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="c2c05-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="c2c05-118">範例</span><span class="sxs-lookup"><span data-stu-id="c2c05-118">Samples</span></span>

* [<span data-ttu-id="c2c05-119">使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="c2c05-119">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="c2c05-120">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="c2c05-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

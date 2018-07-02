---
title: 適用於 .NET 的 Azure Cosmos DB 程式庫
description: 適用於 .NET 的 Azure Cosmos DB 程式庫參考
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4407e59cbcc7ceedc0c7964981d29d6e14a4aa95
ms.sourcegitcommit: 903457bd531e77797a86e6aedcfc94c1fb79fe6d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37132049"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="98ca2-104">適用於 .NET 的 Azure Cosmos DB 程式庫</span><span class="sxs-lookup"><span data-stu-id="98ca2-104">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="98ca2-105">概觀</span><span class="sxs-lookup"><span data-stu-id="98ca2-105">Overview</span></span>

<span data-ttu-id="98ca2-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分散式且可擴充的資料存放區，可支援多個不同類型的資料庫。</span><span class="sxs-lookup"><span data-stu-id="98ca2-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="98ca2-107">[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="98ca2-107">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="98ca2-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="98ca2-108">Client library</span></span>

<span data-ttu-id="98ca2-109">您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="98ca2-109">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span>  <span data-ttu-id="98ca2-110">請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="98ca2-110">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="98ca2-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="98ca2-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="98ca2-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="98ca2-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="98ca2-113">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="98ca2-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="98ca2-114">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="98ca2-114">Code Example</span></span>

<span data-ttu-id="98ca2-115">這個範例會連線到現有的 Azure Cosmos DB SQL API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。</span><span class="sxs-lookup"><span data-stu-id="98ca2-115">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString().Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="98ca2-116">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="98ca2-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="98ca2-117">範例</span><span class="sxs-lookup"><span data-stu-id="98ca2-117">Samples</span></span>

* [<span data-ttu-id="98ca2-118">使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="98ca2-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="98ca2-119">檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="98ca2-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

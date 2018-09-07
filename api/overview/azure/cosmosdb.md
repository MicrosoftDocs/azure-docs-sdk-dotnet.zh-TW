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
# <a name="azure-cosmos-db-libraries-for-net"></a>適用於 .NET 的 Azure Cosmos DB 程式庫

## <a name="overview"></a>概觀

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是全域散發的多模型資料庫服務。 此服務的設計目的，是可透過全方位的 SLA，以有彈性且獨立的方式調整地理區域 (數量不限) 的輸送量及儲存空間。 透過 Azure Cosmos DB，您可以使用 API 和程式設計模型來儲存並存取文件、索引鍵/值組、寬列資料行以及圖形資料庫。 

[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。

## <a name="client-library"></a>用戶端程式庫

您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。 請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>程式碼範例

這個範例會連線到現有的 Azure Cosmos DB SQL API 資料庫，從集合中讀取文件，並將其還原序列化為 `Item` 物件。   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>範例

* [使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

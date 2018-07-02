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
# <a name="azure-cosmos-db-libraries-for-net"></a>適用於 .NET 的 Azure Cosmos DB 程式庫

## <a name="overview"></a>概觀

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分散式且可擴充的資料存放區，可支援多個不同類型的資料庫。

[開始使用 Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。

## <a name="client-library"></a>用戶端程式庫

您可以使用 Azure Cosmos DB .NET 用戶端程式庫來存取，並在現有的 Azure Cosmos DB 資料存放區中儲存資料。  請使用 Azure 入口網站、CLI 或 PowerShell，自動建立新的 Azure Cosmos DB 帳戶。

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
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString().Result;
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>範例

* [使用 Azure Cosmos DB 的 MongoDB API 開發 .NET 應用程式](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

檢視 Azure Cosmos DB 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

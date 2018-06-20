---
title: 適用於 .NET 的 Azure 搜尋服務程式庫
description: 適用於 .NET 的 Azure 搜尋服務程式庫參考
keywords: Azure, .NET, SDK, API, 搜尋服務
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: search
ms.custom: devcenter, svc-overview
ms.openlocfilehash: bd0899d6dbc6d474389eebac78a77a62b86c5255
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566299"
---
# <a name="azure-search-libraries-for-net"></a>適用於 .NET 的 Azure 搜尋服務程式庫

## <a name="overview"></a>概觀

[Azure 搜尋服務](https://docs.microsoft.com/azure/search/search-what-is-azure-search)是受到完整管理的雲端搜尋服務，可透過在 Web、行動和企業應用程式中的資料提供豐富的搜尋體驗。

## <a name="client-library"></a>用戶端程式庫

使用 Azure 搜尋服務用戶端程式庫來存取及執行搜尋服務、索引、文件或其他物件的索引和搜尋作業。 如需逐步簡介，請參閱[如何從 .NET 應用程式使用 Azure 搜尋服務](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Search)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a>程式碼範例

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a>管理程式庫

使用 Azure 搜尋服務管理程式庫來佈建服務、管理 API 金鑰並調整資源。 在 Azure Resource Manager 中，服務管理針對訂閱者和租用戶識別碼具有相依性。 通常，支援工作流程也需要使用 Azure Active Directory 來驗證和註冊應用程式。 如需 Azure 搜尋服務佈建的簡介，請參閱[如何使用管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api)。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Search)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a>範例

 + [Azure 範例/search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [Azure 範例/search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api)

在 Github 的 [Azure 範例存放庫](https://github.com/Azure-Samples/)上尋找更多搜尋範例。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

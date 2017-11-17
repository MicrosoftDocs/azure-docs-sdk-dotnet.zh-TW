---
title: "適用於 .NET 的 Azure 搜尋服務程式庫"
description: "適用於 .NET 的 Azure 搜尋服務程式庫參考"
keywords: "Azure, .NET, SDK, API, 搜尋服務"
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
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="522aa-104">適用於 .NET 的 Azure 搜尋服務程式庫</span><span class="sxs-lookup"><span data-stu-id="522aa-104">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="522aa-105">概觀</span><span class="sxs-lookup"><span data-stu-id="522aa-105">Overview</span></span>

<span data-ttu-id="522aa-106">[Azure 搜尋服務](https://docs.microsoft.com/azure/search/search-what-is-azure-search)是受到完整管理的雲端搜尋服務，可透過在 Web、行動和企業應用程式中的資料提供豐富的搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="522aa-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="522aa-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="522aa-107">Client library</span></span>

<span data-ttu-id="522aa-108">使用 Azure 搜尋服務用戶端程式庫來存取及執行搜尋服務、索引、文件或其他物件的索引和搜尋作業。</span><span class="sxs-lookup"><span data-stu-id="522aa-108">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="522aa-109">如需逐步簡介，請參閱[如何從 .NET 應用程式使用 Azure 搜尋服務](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。</span><span class="sxs-lookup"><span data-stu-id="522aa-109">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="522aa-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Search)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="522aa-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="522aa-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="522aa-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="522aa-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="522aa-112">Code Example</span></span>

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
> [<span data-ttu-id="522aa-113">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="522aa-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="522aa-114">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="522aa-114">Management library</span></span>

<span data-ttu-id="522aa-115">使用 Azure 搜尋服務管理程式庫來佈建服務、管理 API 金鑰並調整資源。</span><span class="sxs-lookup"><span data-stu-id="522aa-115">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="522aa-116">在 Azure Resource Manager 中，服務管理針對訂閱者和租用戶識別碼具有相依性。</span><span class="sxs-lookup"><span data-stu-id="522aa-116">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="522aa-117">通常，支援工作流程也需要使用 Azure Active Directory 來驗證和註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="522aa-117">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="522aa-118">如需 Azure 搜尋服務佈建的簡介，請參閱[如何使用管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="522aa-118">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="522aa-119">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Search)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="522aa-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="522aa-120">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="522aa-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="522aa-121">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="522aa-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="522aa-122">範例</span><span class="sxs-lookup"><span data-stu-id="522aa-122">Samples</span></span>

 + [<span data-ttu-id="522aa-123">Azure 範例/search-dotnet-getting-started</span><span class="sxs-lookup"><span data-stu-id="522aa-123">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="522aa-124">Azure 範例/search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="522aa-124">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="522aa-125">在 Github 的 [Azure 範例存放庫](https://github.com/Azure-Samples/)上尋找更多搜尋範例。</span><span class="sxs-lookup"><span data-stu-id="522aa-125">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

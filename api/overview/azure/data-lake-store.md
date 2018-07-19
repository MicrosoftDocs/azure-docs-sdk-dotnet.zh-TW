---
title: 適用於 .NET 的 Azure Data Lake Store 程式庫
description: 適用於 .NET 的 Azure Data Lake Store 程式庫參考
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 7bbc8c6c5a71d16372d7ab756a5188d90503f52a
ms.sourcegitcommit: 512e031ead61a578ac96835c8ea01829842740bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39116684"
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="49317-104">適用於 .NET 的 Azure Data Lake Store 程式庫</span><span class="sxs-lookup"><span data-stu-id="49317-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="49317-105">概觀</span><span class="sxs-lookup"><span data-stu-id="49317-105">Overview</span></span>

<span data-ttu-id="49317-106">Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。</span><span class="sxs-lookup"><span data-stu-id="49317-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="49317-107">Azure Data Lake 可讓您在單一位置擷取任何大小、類型和擷取速度的資料，以便進行運作和探究分析。</span><span class="sxs-lookup"><span data-stu-id="49317-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="49317-108">若要進一步了解，請參閱 [Azure Data Lake Store 概觀](/azure/data-lake-store/data-lake-store-overview)。</span><span class="sxs-lookup"><span data-stu-id="49317-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="client-library"></a><span data-ttu-id="49317-109">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="49317-109">Client library</span></span>

<span data-ttu-id="49317-110">使用用戶端程式庫在 Data Lake Store 上執行檔案系統作業，例如在 Data Lake Store 帳戶中建立資料夾、上傳及下載檔案。</span><span class="sxs-lookup"><span data-stu-id="49317-110">Use the client library to perform filesystem operations on Data Lake Store, such as creating folders in a Data Lake Store account, uploading files, and downloading files.</span></span>  <span data-ttu-id="49317-111">如果使用 Data Lake Store 搭配 .NET 的完整教學課程，請參閱[在 Azure Data Lake Store 上使用 .NET SDK 的檔案系統作業](/azure/data-lake-store/data-lake-store-data-operations-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="49317-111">For a full tutorial on using Data Lake Store with .NET, see [Filesystem operations on Azure Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span></span>

<span data-ttu-id="49317-112">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="49317-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="49317-113">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="49317-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a><span data-ttu-id="49317-114">驗證</span><span class="sxs-lookup"><span data-stu-id="49317-114">Authentication</span></span>

* <span data-ttu-id="49317-115">如需讓應用程式進行使用者驗證，請參閱[使用 .NET SDK 向 Data Lake Store 進行使用者驗證](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="49317-115">For end-user authentication for your application, see [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).</span></span>
* <span data-ttu-id="49317-116">如需讓應用程式進行服務對服務驗證，請參閱[使用 .NET SDK 向 Data Lake Store 進行服務對服務驗證](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="49317-116">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).</span></span>

### <a name="code-example"></a><span data-ttu-id="49317-117">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="49317-117">Code Example</span></span>

<span data-ttu-id="49317-118">下列程式碼片段會建立 Data Lake Store 檔案系統用戶端物件，以便對服務發出要求。</span><span class="sxs-lookup"><span data-stu-id="49317-118">The following snippet creates the Data Lake Store filesystem client object, which is used to issue requests to the service.</span></span>

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="49317-119">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="49317-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a><span data-ttu-id="49317-120">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="49317-120">Management library</span></span>

<span data-ttu-id="49317-121">使用管理程式庫來連線並管理您的巨量資料存放庫。</span><span class="sxs-lookup"><span data-stu-id="49317-121">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="49317-122">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="49317-122">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="49317-123">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="49317-123">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="49317-124">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="49317-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a><span data-ttu-id="49317-125">範例</span><span class="sxs-lookup"><span data-stu-id="49317-125">Samples</span></span>

* [<span data-ttu-id="49317-126">Azure Data Lake .NET 用戶端範例</span><span class="sxs-lookup"><span data-stu-id="49317-126">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="49317-127">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="49317-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

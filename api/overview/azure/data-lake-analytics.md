---
title: 適用於 .NET 的 Azure Data Lake Analytics 程式庫
description: 適用於 .NET 的 Azure Data Lake Analytics 程式庫參考
keywords: Azure, .NET, SDK, API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a4340844906d7ccf2612ce17dae13e1fce257da0
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065678"
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a><span data-ttu-id="cfb5a-104">適用於 .NET 的 Azure Data Lake Analytics 程式庫</span><span class="sxs-lookup"><span data-stu-id="cfb5a-104">Azure Data Lake Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="cfb5a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="cfb5a-105">Overview</span></span>

<span data-ttu-id="cfb5a-106">Azure Data Lake Analytics 是隨選分析作業服務，可簡化巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-106">Azure Data Lake Analytics is an on-demand analytics job service to simplify big data analytics.</span></span>

<span data-ttu-id="cfb5a-107">若要進一步了解，請參閱 [Microsoft Azure Data Lake Analytics 概觀](/azure/data-lake-analytics/data-lake-analytics-overview)。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-107">To learn more, see [Overview of Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="cfb5a-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="cfb5a-108">Management library</span></span>

<span data-ttu-id="cfb5a-109">使用管理程式庫連線到服務及管理分析作業。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-109">Use the management library to connect to the service and manage analytics jobs.</span></span>

<span data-ttu-id="cfb5a-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="cfb5a-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="cfb5a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a><span data-ttu-id="cfb5a-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="cfb5a-112">Code Example</span></span>

<span data-ttu-id="cfb5a-113">這個範例會建立用戶端以連線及管理分析帳戶。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-113">This example creates the clients to connect with and manage the analytics account.</span></span>

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cfb5a-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="cfb5a-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="cfb5a-115">範例</span><span class="sxs-lookup"><span data-stu-id="cfb5a-115">Samples</span></span>
* [<span data-ttu-id="cfb5a-116">Azure Data Lake .NET 用戶端範例</span><span class="sxs-lookup"><span data-stu-id="cfb5a-116">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="cfb5a-117">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="cfb5a-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

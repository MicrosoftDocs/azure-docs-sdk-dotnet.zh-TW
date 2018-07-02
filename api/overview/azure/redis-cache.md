---
title: 適用於 .NET 的 Azure Redis 快取程式庫
description: 適用於 .NET 的 Azure Redis 快取程式庫參考
keywords: Azure, .NET, SDK, API, Redis 快取
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: redis-cache
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 879f42aa254103239fb0dceeb25cb99a7d5e9814
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065918"
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="571ed-104">適用於 .NET 的 Azure Redis 快取程式庫</span><span class="sxs-lookup"><span data-stu-id="571ed-104">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="571ed-105">概觀</span><span class="sxs-lookup"><span data-stu-id="571ed-105">Overview</span></span>

<span data-ttu-id="571ed-106">Azure Redis 快取是安全的資料快取和訊息代理程式，為應用程式提供高輸送量且低延遲的資料存取。</span><span class="sxs-lookup"><span data-stu-id="571ed-106">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="571ed-107">如需詳細資訊，請參閱[如何使用 Redis 快取](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="571ed-107">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="571ed-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="571ed-108">Client library</span></span>

<span data-ttu-id="571ed-109">Azure Redis 快取適用於任何 Redis 用戶端 API，包括 `StackExchange.Redis`。</span><span class="sxs-lookup"><span data-stu-id="571ed-109">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="571ed-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/StackExchange.Redis)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="571ed-110">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="571ed-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="571ed-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="571ed-112">範例</span><span class="sxs-lookup"><span data-stu-id="571ed-112">Example</span></span>

<span data-ttu-id="571ed-113">這個範例會連線到 Redis 快取資料庫執行個體、將某些字串依名稱加入快取，並再次擷取它們。</span><span class="sxs-lookup"><span data-stu-id="571ed-113">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

```csharp
/* Include this "using" directive.
using StackExchange.Redis;
*/

ConnectionMultiplexer connection = 
    ConnectionMultiplexer.Connect("contoso.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    IDatabase cache = connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

## <a name="management-library"></a><span data-ttu-id="571ed-114">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="571ed-114">Management library</span></span>

<span data-ttu-id="571ed-115">Redis 快取管理程式庫可讓您管理 Redis 快取資源以及存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="571ed-115">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="571ed-116">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="571ed-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="571ed-117">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="571ed-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="571ed-118">範例</span><span class="sxs-lookup"><span data-stu-id="571ed-118">Example</span></span>

<span data-ttu-id="571ed-119">這個範例會建立新的 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="571ed-119">This example creates a new Redis Cache.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.Redis.Fluent;
*/

IRedisCache redisCache1 = azure.RedisCaches.Define("RedisCacheName")
    .WithRegion(Region.USCentral)
    .WithNewResourceGroup("ResourceGroupName")
    .WithBasicSku()
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="571ed-120">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="571ed-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="571ed-121">範例</span><span class="sxs-lookup"><span data-stu-id="571ed-121">Samples</span></span>

* [<span data-ttu-id="571ed-122">Redis 使用者入門 - 管理 Redis - 在 .NET 中</span><span class="sxs-lookup"><span data-stu-id="571ed-122">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure Service Fabric 程式庫
description: 適用於 .NET 的 Azure Service Fabric 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-fabric
ms.openlocfilehash: 064f95a4eae3182c4ac5b31779a5d22b592a75b2
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190761"
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="63b66-103">適用於 .NET 的 Azure Service Fabric 程式庫</span><span class="sxs-lookup"><span data-stu-id="63b66-103">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="63b66-104">概觀</span><span class="sxs-lookup"><span data-stu-id="63b66-104">Overview</span></span>

<span data-ttu-id="63b66-105">Azure Service Fabric 是一個分散式系統平台，可讓您輕鬆封裝、部署及管理可調整和可信賴的微服務與容器。</span><span class="sxs-lookup"><span data-stu-id="63b66-105">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="63b66-106">如需詳細資訊，請參閱 [Azure Service Fabric 文件](/azure/service-fabric/)。</span><span class="sxs-lookup"><span data-stu-id="63b66-106">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="63b66-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="63b66-107">Client library</span></span>

<span data-ttu-id="63b66-108">使用 Service Fabric 用戶端程式庫與現有的 Service Fabric 叢集互動。</span><span class="sxs-lookup"><span data-stu-id="63b66-108">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="63b66-109">程式庫包含 3 種 API 類別：</span><span class="sxs-lookup"><span data-stu-id="63b66-109">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="63b66-110">**用戶端** API 用於管理、調整及回收叢集，以及部署應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="63b66-110">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="63b66-111">**執行階段** API 用於讓應用程式與其主機伺服器互動。</span><span class="sxs-lookup"><span data-stu-id="63b66-111">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="63b66-112">**一般** API 包含在**用戶端**及**執行階段** API 中使用的類型。</span><span class="sxs-lookup"><span data-stu-id="63b66-112">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="63b66-113">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ServiceFabric)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="63b66-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="63b66-114">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="63b66-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="63b66-115">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="63b66-115">Code Examples</span></span>

<span data-ttu-id="63b66-116">下列範例指令碼會使用 Service Fabric **用戶端** API 將應用程式套件複製到映像存放區、佈建應用程式類型，並建立應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="63b66-116">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

```csharp
/* Include these dependencies
using System.Fabric;
using System.Fabric.Description;
*/

// Connect to the cluster.
FabricClient fabricClient = new FabricClient(clusterConnection);

// Copy the application package to a location in the image store
fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);

// Provision the application.
fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

//  Create the application instance.
ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="63b66-117">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="63b66-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="63b66-118">此範例會使用託管應用程式中的 Service Fabric **執行階段**及**一般** API，在執行階段更新 [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections)。</span><span class="sxs-lookup"><span data-stu-id="63b66-118">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

```csharp
using System.Fabric;
using Microsoft.ServiceFabric.Data.Collections;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

/// <summary>
/// This is the main entry point for your service replica.
/// This method executes when this replica of your service becomes primary and has write status.
/// </summary>
/// <param name="cancellationToken">Canceled when Service Fabric needs to shut down this service replica.</param>
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();
        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }
        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="63b66-119">探索執行階段 API</span><span class="sxs-lookup"><span data-stu-id="63b66-119">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="63b66-120">探索一般 API</span><span class="sxs-lookup"><span data-stu-id="63b66-120">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="63b66-121">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="63b66-121">Management Library</span></span>

<span data-ttu-id="63b66-122">管理程式庫用來建立、更新及刪除 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="63b66-122">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="63b66-123">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="63b66-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="63b66-124">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="63b66-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="63b66-125">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="63b66-125">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="63b66-126">範例</span><span class="sxs-lookup"><span data-stu-id="63b66-126">Samples</span></span>

* [<span data-ttu-id="63b66-127">使用 FabricClient 來部署和移除應用程式</span><span class="sxs-lookup"><span data-stu-id="63b66-127">Deploy and remove applications using FabricClient</span></span>](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

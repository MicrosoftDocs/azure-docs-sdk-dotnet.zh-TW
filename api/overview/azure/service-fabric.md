---
title: "適用於 .NET 的 Azure Service Fabric 程式庫"
description: "適用於 .NET 的 Azure Service Fabric 程式庫參考"
keywords: Azure, .NET, SDK, API, Service Fabric
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-fabric
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f4b54933d31a4e1fc4c390baa57469cc1c02783a
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a>適用於 .NET 的 Azure Service Fabric 程式庫

## <a name="overview"></a>概觀

Azure Service Fabric 是一個分散式系統平台，可讓您輕鬆封裝、部署及管理可調整和可信賴的微服務與容器。  如需詳細資訊，請參閱 [Azure Service Fabric 文件](/azure/service-fabric/)。

## <a name="client-library"></a>用戶端程式庫

使用 Service Fabric 用戶端程式庫與現有的 Service Fabric 叢集互動。  程式庫包含 3 種 API 類別：

* **用戶端** API 用於管理、調整及回收叢集，以及部署應用程式套件。
* **執行階段** API 用於讓應用程式與其主機伺服器互動。
* **一般** API 包含在**用戶端**及**執行階段** API 中使用的類型。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ServiceFabric)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a>程式碼範例

下列範例指令碼會使用 Service Fabric **用戶端** API 將應用程式套件複製到映像存放區、佈建應用程式類型，並建立應用程式執行個體。

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
> [探索用戶端 API](/dotnet/api/overview/azure/servicefabric/client)

此範例會使用託管應用程式中的 Service Fabric **執行階段**及**一般** API，在執行階段更新 [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections)。

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
> [探索執行階段 API](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [探索一般 API](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a>管理程式庫

管理程式庫用來建立、更新及刪除 Service Fabric 叢集。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a>範例

* [使用 FabricClient 來部署和移除應用程式](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

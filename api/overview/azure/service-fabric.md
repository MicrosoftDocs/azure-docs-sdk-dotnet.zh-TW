---
title: "適用於 .NET 的 Azure Service Fabric 程式庫"
description: "適用於 .NET 的 Azure Service Fabric 程式庫參考"
keywords: Azure, .NET, SDK, API, Service Fabric
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: c708ae06fa4b5165e3f615abf636b11bfd95cd3b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="c8e52-104">適用於 .NET 的 Azure Service Fabric 程式庫</span><span class="sxs-lookup"><span data-stu-id="c8e52-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c8e52-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c8e52-105">Overview</span></span>

<span data-ttu-id="c8e52-106">Azure Service Fabric 是一個分散式系統平台，可讓您輕鬆封裝、部署及管理可調整和可信賴的微服務與容器。</span><span class="sxs-lookup"><span data-stu-id="c8e52-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>

## <a name="client-library"></a><span data-ttu-id="c8e52-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="c8e52-107">Client library</span></span>

<span data-ttu-id="c8e52-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ServiceFabric)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="c8e52-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c8e52-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="c8e52-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-example"></a><span data-ttu-id="c8e52-110">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c8e52-110">Code Example</span></span>

<span data-ttu-id="c8e52-111">下列範例指令碼會將應用程式套件複製到映像存放區、佈建應用程式類型，並建立應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8e52-111">The following example copies an application package to the image store, provisions the application type, and creates an application instance.</span></span>

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
> [<span data-ttu-id="c8e52-112">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="c8e52-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

## <a name="samples"></a><span data-ttu-id="c8e52-113">範例</span><span class="sxs-lookup"><span data-stu-id="c8e52-113">Samples</span></span>

* [<span data-ttu-id="c8e52-114">使用 FabricClient 來部署和移除應用程式</span><span class="sxs-lookup"><span data-stu-id="c8e52-114">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package

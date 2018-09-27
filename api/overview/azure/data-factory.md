---
title: 適用於 .NET 的 Azure Data Factory 程式庫
description: 適用於 .NET 的 Azure Data Factory 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-factory
ms.openlocfilehash: 9a779f223cd0e158e99afcf1ee011d121f2fe838
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190321"
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="9132e-103">適用於 .NET 的 Azure Data Factory 程式庫</span><span class="sxs-lookup"><span data-stu-id="9132e-103">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9132e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9132e-104">Overview</span></span>

<span data-ttu-id="9132e-105">Azure Data Factory 是以雲端為基礎的資料整合服務。</span><span class="sxs-lookup"><span data-stu-id="9132e-105">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="9132e-106">可讓您在雲端建立資料驅動工作流程，以便協調及自動進行資料移動和資料轉換。</span><span class="sxs-lookup"><span data-stu-id="9132e-106">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="9132e-107">若要進一步了解，請參閱 [Azure Data Factory 簡介](/azure/data-factory/data-factory-introduction)。</span><span class="sxs-lookup"><span data-stu-id="9132e-107">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="9132e-108">管理程式庫 - Data Factory V2 (預覽)</span><span class="sxs-lookup"><span data-stu-id="9132e-108">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="9132e-109">使用管理程式庫來建立和排程 Data Factory V2 (預覽) 中的資料導向工作流程 (管線)。</span><span class="sxs-lookup"><span data-stu-id="9132e-109">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="9132e-110">如需詳細資訊，請參閱[使用 .NET SDK建立資料處理站和管線](/azure/data-factory/quickstart-create-data-factory-dot-net)。</span><span class="sxs-lookup"><span data-stu-id="9132e-110">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="9132e-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9132e-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9132e-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9132e-112">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="9132e-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="9132e-113">Code Example</span></span>

<span data-ttu-id="9132e-114">下列程式碼範例會使用管理程式庫來建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9132e-114">The following example uses the management library to create a data factory.</span></span>

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9132e-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="9132e-115">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="9132e-116">管理程式庫 - Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="9132e-116">Management library - Data Factory V1</span></span>

<span data-ttu-id="9132e-117">使用管理程式庫來建立和排程 Data Factory V1 中的資料導向工作流程 (管線)。</span><span class="sxs-lookup"><span data-stu-id="9132e-117">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="9132e-118">如需詳細資訊，請檢閱[Data Factory 版本 1](/azure/data-factory/v1/data-factory-introduction) 文件。</span><span class="sxs-lookup"><span data-stu-id="9132e-118">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="9132e-119">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9132e-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9132e-120">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9132e-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="9132e-121">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="9132e-121">Code Example</span></span>

<span data-ttu-id="9132e-122">下列程式碼範例會使用管理程式庫來建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="9132e-122">The following example uses the management library to create a data factory.</span></span>

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9132e-123">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="9132e-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="9132e-124">範例</span><span class="sxs-lookup"><span data-stu-id="9132e-124">Samples</span></span>

* <span data-ttu-id="9132e-125">[MyDriving - Azure IOT 與行動範例應用程式](https://azure.microsoft.com/resources/samples/mydriving/)，使用 Data Factory 來推動深入解析。</span><span class="sxs-lookup"><span data-stu-id="9132e-125">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="9132e-126">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="9132e-126">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: "適用於 .NET 的 Azure Data Factory 程式庫"
description: "適用於 .NET 的 Azure Data Factory 程式庫參考"
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="1b725-104">適用於 .NET 的 Azure Data Factory 程式庫</span><span class="sxs-lookup"><span data-stu-id="1b725-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1b725-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1b725-105">Overview</span></span>

<span data-ttu-id="1b725-106">Azure Data Factory 是以雲端為基礎的資料整合服務。</span><span class="sxs-lookup"><span data-stu-id="1b725-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="1b725-107">可讓您在雲端建立資料驅動工作流程，以便協調及自動進行資料移動和資料轉換。</span><span class="sxs-lookup"><span data-stu-id="1b725-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="1b725-108">若要進一步了解，請參閱 [Azure Data Factory 簡介](/azure/data-factory/data-factory-introduction)。</span><span class="sxs-lookup"><span data-stu-id="1b725-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library"></a><span data-ttu-id="1b725-109">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="1b725-109">Management library</span></span>

<span data-ttu-id="1b725-110">使用管理程式庫來建立和排程資料驅動的工作流程 (管線)。</span><span class="sxs-lookup"><span data-stu-id="1b725-110">Use the management library to create and schedule data-driven workflows (pipelines).</span></span>

<span data-ttu-id="1b725-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="1b725-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1b725-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="1b725-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="1b725-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1b725-113">Code Example</span></span>

<span data-ttu-id="1b725-114">下列程式碼範例會使用管理程式庫來建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="1b725-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="1b725-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="1b725-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="1b725-116">範例</span><span class="sxs-lookup"><span data-stu-id="1b725-116">Samples</span></span>

* <span data-ttu-id="1b725-117">[MyDriving - Azure IOT 與行動範例應用程式](https://azure.microsoft.com/resources/samples/mydriving/)，使用 Data Factory 來推動深入解析。</span><span class="sxs-lookup"><span data-stu-id="1b725-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="1b725-118">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="1b725-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

---
title: 適用於 .NET 的 Azure Data Factory 程式庫
description: 適用於 .NET 的 Azure Data Factory 程式庫參考
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b3c492fbfe4a4afa6f06f8c48a370c554a01719c
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065788"
---
# <a name="azure-data-factory-libraries-for-net"></a>適用於 .NET 的 Azure Data Factory 程式庫

## <a name="overview"></a>概觀

Azure Data Factory 是以雲端為基礎的資料整合服務。 可讓您在雲端建立資料驅動工作流程，以便協調及自動進行資料移動和資料轉換。

若要進一步了解，請參閱 [Azure Data Factory 簡介](/azure/data-factory/data-factory-introduction)。

## <a name="management-library---data-factory-v2-preview"></a>管理程式庫 - Data Factory V2 (預覽)

使用管理程式庫來建立和排程 Data Factory V2 (預覽) 中的資料導向工作流程 (管線)。  如需詳細資訊，請參閱[使用 .NET SDK建立資料處理站和管線](/azure/data-factory/quickstart-create-data-factory-dot-net)。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a>程式碼範例

下列程式碼範例會使用管理程式庫來建立資料處理站。

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
> [探索管理 API](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a>管理程式庫 - Data Factory V1

使用管理程式庫來建立和排程 Data Factory V1 中的資料導向工作流程 (管線)。  如需詳細資訊，請檢閱[Data Factory 版本 1](/azure/data-factory/v1/data-factory-introduction) 文件。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a>程式碼範例

下列程式碼範例會使用管理程式庫來建立資料處理站。

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
> [探索管理 API](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a>範例

* [MyDriving - Azure IOT 與行動範例應用程式](https://azure.microsoft.com/resources/samples/mydriving/)，使用 Data Factory 來推動深入解析。

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

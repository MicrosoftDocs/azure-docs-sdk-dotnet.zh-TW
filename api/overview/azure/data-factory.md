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
# <a name="azure-data-factory-libraries-for-net"></a>適用於 .NET 的 Azure Data Factory 程式庫

## <a name="overview"></a>概觀

Azure Data Factory 是以雲端為基礎的資料整合服務。 可讓您在雲端建立資料驅動工作流程，以便協調及自動進行資料移動和資料轉換。

若要進一步了解，請參閱 [Azure Data Factory 簡介](/azure/data-factory/data-factory-introduction)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫來建立和排程資料驅動的工作流程 (管線)。

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

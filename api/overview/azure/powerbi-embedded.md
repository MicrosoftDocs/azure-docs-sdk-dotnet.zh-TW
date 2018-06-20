---
title: 適用於 .NET 的 Power BI Embedded 程式庫
description: 適用於 .NET 的 Power BI Embedded 程式庫參考
keywords: Azure, .NET, SDK, API, Power BI Embedded
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f61c931d930fce75d038af8b8f1355f1de9cde7c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487521"
---
# <a name="power-bi-embedded-libraries-for-net"></a>適用於 .NET 的 Power BI Embedded 程式庫

[Power BI](https://powerbi.microsoft.com/) 是以雲端為基礎的商務分析服務，可讓您單一檢視最重要的商務資料。

若要了解有關搭配 .NET 使用 Power BI 的詳細資訊，請參閱[使用 Power BI 內嵌](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。

## <a name="client-library"></a>用戶端程式庫

使用用戶端程式庫來連線 Power BI API，以存取資料集和報表並與之互動。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a>範例

下列範例會擷取並顯示資料集和報表的清單。

```csharp
/* Include these'using' directive:
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;
*/
using (PowerBIClient client = new PowerBIClient(new Uri(apiUrl), tokenCredentials))
{

    Console.WriteLine("\r*** DATASETS ***\r");

    // List of datasets in a group/app workspace
    ODataResponseListDataset datasetList = client.Datasets.GetDatasetsInGroup(groupId);

    foreach(Dataset ds in datasetList.Value)
    {
        Console.WriteLine(ds.Id + " | " + ds.Name);
    }

    Console.WriteLine("\r*** REPORTS ***\r");

    // List of reports in a group/app workspace
    ODataResponseListReport reportList = client.Reports.GetReportsInGroup(groupId);

    foreach (Report rpt in reportList.Value)
    {
        Console.WriteLine(rpt.Id + " | " + rpt.Name +  " | DatasetID = " + rpt.DatasetId);
    }
}
```

> [!div class="nextstepaction"]
> [探索用戶端 API](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a>範例

* [Power BI 開發人員範例](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Power BI.NET GitHub 存放庫](https://github.com/Microsoft/PowerBI-CSharp)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console

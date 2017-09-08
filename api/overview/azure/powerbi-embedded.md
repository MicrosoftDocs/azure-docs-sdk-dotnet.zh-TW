---
title: "適用於 .NET 的 Power BI Embedded 程式庫"
description: "適用於 .NET 的 Power BI Embedded 程式庫參考"
keywords: Azure, .NET, SDK, API, Power BI Embedded
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: f9a6aac8dbb3c284948e9140ad87aff5e415d9fb
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="64229-104">適用於 .NET 的 Power BI Embedded 程式庫</span><span class="sxs-lookup"><span data-stu-id="64229-104">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="64229-105">[Power BI](https://powerbi.microsoft.com/) 是以雲端為基礎的商務分析服務，可讓您單一檢視最重要的商務資料。</span><span class="sxs-lookup"><span data-stu-id="64229-105">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="64229-106">若要了解有關搭配 .NET 使用 Power BI 的詳細資訊，請參閱[使用 Power BI 內嵌](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。</span><span class="sxs-lookup"><span data-stu-id="64229-106">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="64229-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="64229-107">Client library</span></span>

<span data-ttu-id="64229-108">使用用戶端程式庫來連線 Power BI API，以存取資料集和報表並與之互動。</span><span class="sxs-lookup"><span data-stu-id="64229-108">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="64229-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。</span><span class="sxs-lookup"><span data-stu-id="64229-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="64229-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="64229-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="64229-111">範例</span><span class="sxs-lookup"><span data-stu-id="64229-111">Example</span></span>

<span data-ttu-id="64229-112">下列範例會擷取並顯示資料集和報表的清單。</span><span class="sxs-lookup"><span data-stu-id="64229-112">The following example retrieves and displays a list of datasets and reports.</span></span>

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
> [<span data-ttu-id="64229-113">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="64229-113">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="64229-114">範例</span><span class="sxs-lookup"><span data-stu-id="64229-114">Samples</span></span>

* [<span data-ttu-id="64229-115">Power BI 開發人員範例</span><span class="sxs-lookup"><span data-stu-id="64229-115">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="64229-116">Power BI.NET GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="64229-116">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="64229-117">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="64229-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console

---
title: 適用於 .NET 的 Power BI Embedded 程式庫
description: 適用於 .NET 的 Power BI Embedded 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: acb327b56e89522142e51016a6a9b279f995a674
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190371"
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="1bbc2-103">適用於 .NET 的 Power BI Embedded 程式庫</span><span class="sxs-lookup"><span data-stu-id="1bbc2-103">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="1bbc2-104">[Power BI](https://powerbi.microsoft.com/) 是以雲端為基礎的商務分析服務，可讓您單一檢視最重要的商務資料。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-104">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="1bbc2-105">若要了解有關搭配 .NET 使用 Power BI 的詳細資訊，請參閱[使用 Power BI 內嵌](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-105">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="1bbc2-106">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="1bbc2-106">Client library</span></span>

<span data-ttu-id="1bbc2-107">使用用戶端程式庫來連線 Power BI API，以存取資料集和報表並與之互動。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-107">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="1bbc2-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1bbc2-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="1bbc2-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="1bbc2-110">範例</span><span class="sxs-lookup"><span data-stu-id="1bbc2-110">Example</span></span>

<span data-ttu-id="1bbc2-111">下列範例會擷取並顯示資料集和報表的清單。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-111">The following example retrieves and displays a list of datasets and reports.</span></span>

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
> [<span data-ttu-id="1bbc2-112">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="1bbc2-112">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="1bbc2-113">範例</span><span class="sxs-lookup"><span data-stu-id="1bbc2-113">Samples</span></span>

* [<span data-ttu-id="1bbc2-114">Power BI 開發人員範例</span><span class="sxs-lookup"><span data-stu-id="1bbc2-114">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="1bbc2-115">Power BI.NET GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="1bbc2-115">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="1bbc2-116">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="1bbc2-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console

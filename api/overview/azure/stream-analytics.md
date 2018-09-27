---
title: 適用於 .NET 的 Azure 串流分析程式庫
description: 適用於 .NET 的 Azure 串流分析程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: stream-analytics
ms.openlocfilehash: c04a5c8a7b1d7e0f283d4fb81bd772de24f195eb
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190451"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="5da3a-103">適用於 .NET 的 Azure 串流分析程式庫</span><span class="sxs-lookup"><span data-stu-id="5da3a-103">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5da3a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5da3a-104">Overview</span></span>

<span data-ttu-id="5da3a-105">[Azure 串流分析](/azure/stream-analytics/stream-analytics-introduction)是完全受控的事件處理引擎，可讓您設定串流資料的即時分析計算。</span><span class="sxs-lookup"><span data-stu-id="5da3a-105">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="5da3a-106">資料可來自裝置、感應器、網站、社交媒體摘要、應用程式和基礎結構系統等等。</span><span class="sxs-lookup"><span data-stu-id="5da3a-106">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="5da3a-107">若要深入了解 Azure 串流分析，請參閱[開始使用 Azure 串流分析即時詐騙偵測](/azure/stream-analytics/stream-analytics-real-time-fraud-detection)。</span><span class="sxs-lookup"><span data-stu-id="5da3a-107">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="5da3a-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="5da3a-108">Management library</span></span>

<span data-ttu-id="5da3a-109">使用 Azure 串流分析管理程式庫來建立、啟動及停止 Azure 串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="5da3a-109">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="5da3a-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5da3a-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5da3a-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5da3a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="5da3a-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5da3a-112">Code Example</span></span>

<span data-ttu-id="5da3a-113">此範例會具現化資料流分析用戶端，並建立資料流作業。</span><span class="sxs-lookup"><span data-stu-id="5da3a-113">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5da3a-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="5da3a-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="5da3a-115">範例</span><span class="sxs-lookup"><span data-stu-id="5da3a-115">Samples</span></span>

- [<span data-ttu-id="5da3a-116">管理 .NET SDK：透過適用於 .NET 的 Azure 串流分析 API 來設定及執行分析作業</span><span class="sxs-lookup"><span data-stu-id="5da3a-116">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="5da3a-117">檢視 Azure 串流分析範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="5da3a-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

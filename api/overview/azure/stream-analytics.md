---
title: 適用於 .NET 的 Azure 串流分析程式庫
description: 適用於 .NET 的 Azure 串流分析程式庫參考
keywords: Azure, .NET, SDK, API, 串流分析
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: stream-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4fc8c5700122a82a5e31df870787a67dad277542
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065928"
---
# <a name="azure-stream-analytics-libraries-for-net"></a>適用於 .NET 的 Azure 串流分析程式庫

## <a name="overview"></a>概觀

[Azure 串流分析](/azure/stream-analytics/stream-analytics-introduction)是完全受控的事件處理引擎，可讓您設定串流資料的即時分析計算。 資料可來自裝置、感應器、網站、社交媒體摘要、應用程式和基礎結構系統等等。 

若要深入了解 Azure 串流分析，請參閱[開始使用 Azure 串流分析即時詐騙偵測](/azure/stream-analytics/stream-analytics-real-time-fraud-detection)。


## <a name="management-library"></a>管理程式庫

使用 Azure 串流分析管理程式庫來建立、啟動及停止 Azure 串流分析作業。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a>程式碼範例

此範例會具現化資料流分析用戶端，並建立資料流作業。

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
> [探索管理 API](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a>範例

- [管理 .NET SDK：透過適用於 .NET 的 Azure 串流分析 API 來設定及執行分析作業](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

檢視 Azure 串流分析範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

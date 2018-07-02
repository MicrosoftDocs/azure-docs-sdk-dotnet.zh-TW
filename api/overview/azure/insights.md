---
title: 適用於 .NET 的 Azure Application Insights 程式庫
description: 適用於 .NET 的 Azure Application Insights 程式庫參考
keywords: Azure, .NET, SDK, API, 應用程式 AppInsights
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: application-insights
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3cbd4a874edfa6de26d3edf4d151d2c4006ab9c3
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065838"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="da0f2-104">適用於 .NET 的 Azure Application Insights 程式庫</span><span class="sxs-lookup"><span data-stu-id="da0f2-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="da0f2-105">概觀</span><span class="sxs-lookup"><span data-stu-id="da0f2-105">Overview</span></span>

<span data-ttu-id="da0f2-106">Application Insights 是 web 開發人員的可延伸監視與診斷服務，具有強大的臨機操作分析功能。</span><span class="sxs-lookup"><span data-stu-id="da0f2-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="da0f2-107">您可以使用 ApplicationInsights 命名空間中的類別，來設定遙測收集並從需要監視的應用程式傳送任何自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="da0f2-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="da0f2-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="da0f2-108">Client library</span></span>

<span data-ttu-id="da0f2-109">適用於 .NET 的 Application Insights 用戶端 SDK 可讓您將事件、彙總資料、例外狀況、相依性和計量記錄至 Azure，以供日後進行分析。</span><span class="sxs-lookup"><span data-stu-id="da0f2-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="da0f2-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ApplicationInsights )，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="da0f2-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="da0f2-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="da0f2-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="da0f2-112">範例</span><span class="sxs-lookup"><span data-stu-id="da0f2-112">Example</span></span>

<span data-ttu-id="da0f2-113">這個範例會追蹤 Application Insights 的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="da0f2-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="da0f2-114">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="da0f2-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="da0f2-115">範例</span><span class="sxs-lookup"><span data-stu-id="da0f2-115">Samples</span></span>

- [<span data-ttu-id="da0f2-116">使用 OpenSchema 的 Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="da0f2-116">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="da0f2-117">檢視 Azure Application Insights 範例的[完整清單](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="da0f2-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

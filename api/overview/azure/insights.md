---
title: 適用於 .NET 的 Azure Application Insights 程式庫
description: 適用於 .NET 的 Azure Application Insights 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: application-insights
ms.openlocfilehash: 10b65f536c6461959b0be9b8f9bd3ec56a307bea
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190833"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="e2f49-103">適用於 .NET 的 Azure Application Insights 程式庫</span><span class="sxs-lookup"><span data-stu-id="e2f49-103">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e2f49-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e2f49-104">Overview</span></span>

<span data-ttu-id="e2f49-105">Application Insights 是 web 開發人員的可延伸監視與診斷服務，具有強大的臨機操作分析功能。</span><span class="sxs-lookup"><span data-stu-id="e2f49-105">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="e2f49-106">您可以使用 ApplicationInsights 命名空間中的類別，來設定遙測收集並從需要監視的應用程式傳送任何自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="e2f49-106">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="e2f49-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e2f49-107">Client library</span></span>

<span data-ttu-id="e2f49-108">適用於 .NET 的 Application Insights 用戶端 SDK 可讓您將事件、彙總資料、例外狀況、相依性和計量記錄至 Azure，以供日後進行分析。</span><span class="sxs-lookup"><span data-stu-id="e2f49-108">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="e2f49-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ApplicationInsights )，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="e2f49-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e2f49-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="e2f49-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="e2f49-111">範例</span><span class="sxs-lookup"><span data-stu-id="e2f49-111">Example</span></span>

<span data-ttu-id="e2f49-112">這個範例會追蹤 Application Insights 的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="e2f49-112">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2f49-113">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="e2f49-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="e2f49-114">範例</span><span class="sxs-lookup"><span data-stu-id="e2f49-114">Samples</span></span>

- [<span data-ttu-id="e2f49-115">使用 OpenSchema 的 Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="e2f49-115">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="e2f49-116">檢視 Azure Application Insights 範例的[完整清單](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e2f49-116">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

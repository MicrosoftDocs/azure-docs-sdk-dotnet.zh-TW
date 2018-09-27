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
# <a name="azure-application-insights-libraries-for-net"></a>適用於 .NET 的 Azure Application Insights 程式庫

## <a name="overview"></a>概觀

Application Insights 是 web 開發人員的可延伸監視與診斷服務，具有強大的臨機操作分析功能。 您可以使用 ApplicationInsights 命名空間中的類別，來設定遙測收集並從需要監視的應用程式傳送任何自訂遙測。

## <a name="client-library"></a>用戶端程式庫

適用於 .NET 的 Application Insights 用戶端 SDK 可讓您將事件、彙總資料、例外狀況、相依性和計量記錄至 Azure，以供日後進行分析。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.ApplicationInsights )，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a>範例

這個範例會追蹤 Application Insights 的自訂事件。

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>範例

- [使用 OpenSchema 的 Application Insights Analytics](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

檢視 Azure Application Insights 範例的[完整清單](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

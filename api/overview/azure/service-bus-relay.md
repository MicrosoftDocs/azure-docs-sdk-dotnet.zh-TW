---
title: 適用於 .NET 的 Azure 服務匯流排轉送程式庫
description: 適用於 .NET 的 Azure 服務匯流排轉送程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 75c481ab23e461c5194a9eeb0ca668af98f4d2d7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189981"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a>適用於 .NET 的 Azure 服務匯流排轉送程式庫

## <a name="overview"></a>概觀

Azure 轉送服務可建立混合式應用程式，方法是讓您以安全的方式向公用雲端公開位於企業網路內部的服務，而無需開啟防火牆連線或要求對企業網路基礎結構的進行侵入式變更。 轉送支援各種不同的傳輸通訊協定和 Web 服務標準。
          
深入了解 [Azure 轉送](/azure/service-bus-relay/relay-what-is-it)。

## <a name="client-library"></a>用戶端程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Relay)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a>範例

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
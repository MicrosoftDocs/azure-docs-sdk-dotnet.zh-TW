---
title: "適用於 .NET 的 Azure 服務匯流排轉送程式庫"
description: "適用於 .NET 的 Azure 服務匯流排轉送程式庫參考"
keywords: "Azure, .NET, SDK, API, 服務匯流排轉送"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/14/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 13a875b837648a05401453e975c9cd70d5e203a1
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-bus-relay-libraries-for-net"></a>適用於 .NET 的 Azure 服務匯流排轉送程式庫

## <a name="overview"></a>概觀

Azure 轉送服務可建立混合式應用程式，方法是讓您以安全的方式向公用雲端公開位於企業網路內部的服務，而無需開啟防火牆連線或要求對企業網路基礎結構的進行侵入式變更。 轉送支援各種不同的傳輸通訊協定和 Web 服務標準。
          
深入了解 [Azure 轉送](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it)。

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
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
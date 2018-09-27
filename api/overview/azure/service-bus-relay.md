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
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="72493-103">適用於 .NET 的 Azure 服務匯流排轉送程式庫</span><span class="sxs-lookup"><span data-stu-id="72493-103">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="72493-104">概觀</span><span class="sxs-lookup"><span data-stu-id="72493-104">Overview</span></span>

<span data-ttu-id="72493-105">Azure 轉送服務可建立混合式應用程式，方法是讓您以安全的方式向公用雲端公開位於企業網路內部的服務，而無需開啟防火牆連線或要求對企業網路基礎結構的進行侵入式變更。</span><span class="sxs-lookup"><span data-stu-id="72493-105">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="72493-106">轉送支援各種不同的傳輸通訊協定和 Web 服務標準。</span><span class="sxs-lookup"><span data-stu-id="72493-106">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="72493-107">深入了解 [Azure 轉送](/azure/service-bus-relay/relay-what-is-it)。</span><span class="sxs-lookup"><span data-stu-id="72493-107">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="72493-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="72493-108">Client library</span></span>

<span data-ttu-id="72493-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Relay)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="72493-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="72493-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="72493-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="72493-111">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="72493-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="72493-112">範例</span><span class="sxs-lookup"><span data-stu-id="72493-112">Samples</span></span>

<span data-ttu-id="72493-113">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="72493-113">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
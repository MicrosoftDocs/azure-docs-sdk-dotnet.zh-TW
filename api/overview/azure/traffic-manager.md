---
title: 適用於 .NET 的 Azure 流量管理員程式庫
description: 適用於 .NET 的 Azure 流量管理員程式庫參考
keywords: Azure, .NET, SDK, API, 流量管理員
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 491a8b12146882b32f7fc6d85ad58cca1d00fd04
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566095"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="fe94f-104">適用於 .NET 的 Azure 流量管理員程式庫</span><span class="sxs-lookup"><span data-stu-id="fe94f-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="fe94f-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fe94f-105">Overview</span></span>

<span data-ttu-id="fe94f-106">Microsoft Azure 流量管理員可讓您控制使用者流量，將流量分散到不同資料中心的服務端點。</span><span class="sxs-lookup"><span data-stu-id="fe94f-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="fe94f-107">流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fe94f-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="fe94f-108">您也可以將流量管理員使用於外部、非 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="fe94f-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="fe94f-109">深入了解 [Azure 流量管理員](/azure/traffic-manager/traffic-manager-overview)。</span><span class="sxs-lookup"><span data-stu-id="fe94f-109">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="fe94f-110">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="fe94f-110">Management library</span></span>

<span data-ttu-id="fe94f-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="fe94f-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fe94f-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="fe94f-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe94f-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="fe94f-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="fe94f-114">範例</span><span class="sxs-lookup"><span data-stu-id="fe94f-114">Samples</span></span>

<span data-ttu-id="fe94f-115">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="fe94f-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
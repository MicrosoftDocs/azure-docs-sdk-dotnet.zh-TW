---
title: "適用於 .NET 的 Azure 流量管理員程式庫"
description: "適用於 .NET 的 Azure 流量管理員程式庫參考"
keywords: "Azure, .NET, SDK, API, 流量管理員"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0fc747c25fe368b5d67f70af1e2b9afc5e07f615
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="0d5dd-104">適用於 .NET 的 Azure 流量管理員程式庫</span><span class="sxs-lookup"><span data-stu-id="0d5dd-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0d5dd-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0d5dd-105">Overview</span></span>

<span data-ttu-id="0d5dd-106">Microsoft Azure 流量管理員可讓您控制使用者流量，將流量分散到不同資料中心的服務端點。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="0d5dd-107">流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="0d5dd-108">您也可以將流量管理員使用於外部、非 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="0d5dd-109">深入了解 [Azure 流量管理員](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview)。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-109">Learn more about [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="0d5dd-110">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="0d5dd-110">Management library</span></span>

<span data-ttu-id="0d5dd-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0d5dd-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="0d5dd-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d5dd-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="0d5dd-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="0d5dd-114">範例</span><span class="sxs-lookup"><span data-stu-id="0d5dd-114">Samples</span></span>

<span data-ttu-id="0d5dd-115">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="0d5dd-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
---
title: 適用於 .NET 的 Azure App Service 程式庫
description: 適用於 .NET 的 Azure App Service 程式庫參考
keywords: Azure, .NET, SDK, API, Web Apps, 應用程式服務, 行動, asp.net
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 356a86e8fa70512b6f31c6e237173a74d1c6f60a
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="4bcb8-104">適用於 .NET 的 Azure App Service 程式庫</span><span class="sxs-lookup"><span data-stu-id="4bcb8-104">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4bcb8-105">概觀</span><span class="sxs-lookup"><span data-stu-id="4bcb8-105">Overview</span></span>

<span data-ttu-id="4bcb8-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) 可讓您部署及調整網站、Web 應用程式、服務和 REST API。</span><span class="sxs-lookup"><span data-stu-id="4bcb8-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="4bcb8-107">管理 API</span><span class="sxs-lookup"><span data-stu-id="4bcb8-107">Management API</span></span>

<span data-ttu-id="4bcb8-108">使用管理 API 來部署、管理及調整裝載在 Azure App Service 中的元素。</span><span class="sxs-lookup"><span data-stu-id="4bcb8-108">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="4bcb8-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="4bcb8-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4bcb8-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="4bcb8-110">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="4bcb8-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="4bcb8-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="4bcb8-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="4bcb8-112">Code Example</span></span>

<span data-ttu-id="4bcb8-113">建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bcb8-113">Create a new web app.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4bcb8-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="4bcb8-114">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="4bcb8-115">範例</span><span class="sxs-lookup"><span data-stu-id="4bcb8-115">Samples</span></span>

* [<span data-ttu-id="4bcb8-116">使用適用於 Azure 的 .NET SDK 來管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4bcb8-116">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="4bcb8-117">Azure App Service 的 ASP.NET 範例</span><span class="sxs-lookup"><span data-stu-id="4bcb8-117">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="4bcb8-118">檢視 Azure App Service 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。</span><span class="sxs-lookup"><span data-stu-id="4bcb8-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
---
title: 適用於 .NET 的 Azure App Service 程式庫
description: 適用於 .NET 的 Azure App Service 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: app-service
ms.openlocfilehash: 82f8eccfafd2f7b1cf1df1ce0f40212509ccddd3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189991"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="6ce12-103">適用於 .NET 的 Azure App Service 程式庫</span><span class="sxs-lookup"><span data-stu-id="6ce12-103">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6ce12-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6ce12-104">Overview</span></span>

<span data-ttu-id="6ce12-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) 可讓您部署及調整網站、Web 應用程式、服務和 REST API。</span><span class="sxs-lookup"><span data-stu-id="6ce12-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="6ce12-106">管理 API</span><span class="sxs-lookup"><span data-stu-id="6ce12-106">Management API</span></span>

<span data-ttu-id="6ce12-107">使用管理 API 來部署、管理及調整裝載在 Azure App Service 中的元素。</span><span class="sxs-lookup"><span data-stu-id="6ce12-107">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="6ce12-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="6ce12-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ce12-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="6ce12-109">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="6ce12-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6ce12-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="6ce12-111">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6ce12-111">Code Example</span></span>

<span data-ttu-id="6ce12-112">建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ce12-112">Create a new web app.</span></span>

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
> [<span data-ttu-id="6ce12-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="6ce12-113">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="6ce12-114">範例</span><span class="sxs-lookup"><span data-stu-id="6ce12-114">Samples</span></span>

* [<span data-ttu-id="6ce12-115">使用適用於 Azure 的 .NET SDK 來管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6ce12-115">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="6ce12-116">Azure App Service 的 ASP.NET 範例</span><span class="sxs-lookup"><span data-stu-id="6ce12-116">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="6ce12-117">檢視 Azure App Service 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。</span><span class="sxs-lookup"><span data-stu-id="6ce12-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
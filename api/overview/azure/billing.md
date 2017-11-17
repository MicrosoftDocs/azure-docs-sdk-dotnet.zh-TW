---
title: "適用於 .NET 的 Azure 計費程式庫"
description: "適用於 .NET 的 Azure 計費程式庫參考"
keywords: "Azure, .NET, SDK, API, 計費"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8df15d55a80991f29b694f4af06a20514bf20b32
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="1ac22-104">適用於 .NET 的 Azure 計費程式庫</span><span class="sxs-lookup"><span data-stu-id="1ac22-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1ac22-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1ac22-105">Overview</span></span>

<span data-ttu-id="1ac22-106">Azure 計費 API (預覽) 提供以程式設計方式存取您的 Azure 計費資訊和發票。</span><span class="sxs-lookup"><span data-stu-id="1ac22-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="1ac22-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="1ac22-107">Management library</span></span>

<span data-ttu-id="1ac22-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="1ac22-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1ac22-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="1ac22-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="1ac22-110">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1ac22-110">Code Example</span></span>

<span data-ttu-id="1ac22-111">登入 Azure 並取得發票清單。</span><span class="sxs-lookup"><span data-stu-id="1ac22-111">Connect to Azure and get a list of invoices.</span></span>

```csharp
/* Include these directives
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Billing;
using Microsoft.Azure.Management.Billing.Models;
*/

// Log into Azure
var serviceCreds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var billingClient = new BillingClient(serviceCreds);
billingClient.SubscriptionId = subscriptionId;

// Get list of invoices
billingClient.Invoices.List();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ac22-112">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="1ac22-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="1ac22-113">範例</span><span class="sxs-lookup"><span data-stu-id="1ac22-113">Samples</span></span>

* [<span data-ttu-id="1ac22-114">使用量 API</span><span class="sxs-lookup"><span data-stu-id="1ac22-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="1ac22-115">RateCard API</span><span class="sxs-lookup"><span data-stu-id="1ac22-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="1ac22-116">多租用戶 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac22-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

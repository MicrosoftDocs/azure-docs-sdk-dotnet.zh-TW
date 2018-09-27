---
title: 適用於 .NET 的 Azure 計費程式庫
description: 適用於 .NET 的 Azure 計費程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 88b90c71d29eacf61e4da2099f8a054d74df4a83
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190251"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="c442e-103">適用於 .NET 的 Azure 計費程式庫</span><span class="sxs-lookup"><span data-stu-id="c442e-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c442e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c442e-104">Overview</span></span>

<span data-ttu-id="c442e-105">Azure 計費 API (預覽) 提供以程式設計方式存取您的 Azure 計費資訊和發票。</span><span class="sxs-lookup"><span data-stu-id="c442e-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="c442e-106">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="c442e-106">Management library</span></span>

<span data-ttu-id="c442e-107">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="c442e-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c442e-108">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="c442e-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="c442e-109">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c442e-109">Code Example</span></span>

<span data-ttu-id="c442e-110">登入 Azure 並取得發票清單。</span><span class="sxs-lookup"><span data-stu-id="c442e-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="c442e-111">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="c442e-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="c442e-112">範例</span><span class="sxs-lookup"><span data-stu-id="c442e-112">Samples</span></span>

* [<span data-ttu-id="c442e-113">使用量 API</span><span class="sxs-lookup"><span data-stu-id="c442e-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="c442e-114">RateCard API</span><span class="sxs-lookup"><span data-stu-id="c442e-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="c442e-115">多租用戶 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c442e-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

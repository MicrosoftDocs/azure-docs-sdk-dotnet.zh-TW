---
title: 適用於 .NET 的 Azure DNS 程式庫
description: 適用於 .NET 的 Azure DNS 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190191"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="a3576-103">適用於 .NET 的 Azure DNS 程式庫</span><span class="sxs-lookup"><span data-stu-id="a3576-103">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="a3576-104">使用適用於 .NET 的 Microsoft Azure DNS 程式庫，來建立及修改裝載於 Azure 的 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="a3576-104">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="a3576-105">區域和記錄會作為 Azure 資源來管理。</span><span class="sxs-lookup"><span data-stu-id="a3576-105">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="a3576-106">如需詳細資訊，請參閱 [Azure DNS 概觀](/azure/dns/dns-overview)。</span><span class="sxs-lookup"><span data-stu-id="a3576-106">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="a3576-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="a3576-107">Management library</span></span>

<span data-ttu-id="a3576-108">使用管理程式庫來建立及修改裝載於 Azure 的 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="a3576-108">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="a3576-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a3576-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a3576-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a3576-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="a3576-111">範例</span><span class="sxs-lookup"><span data-stu-id="a3576-111">Example</span></span>

<span data-ttu-id="a3576-112">下列範例會建立新的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="a3576-112">The following example creates a new DNS zone.</span></span>

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3576-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="a3576-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="a3576-114">範例</span><span class="sxs-lookup"><span data-stu-id="a3576-114">Samples</span></span>

* [<span data-ttu-id="a3576-115">Azure DNS .NET SDK 範例專案</span><span class="sxs-lookup"><span data-stu-id="a3576-115">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="a3576-116">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="a3576-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

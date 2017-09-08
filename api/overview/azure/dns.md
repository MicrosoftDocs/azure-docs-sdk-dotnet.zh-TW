---
title: "適用於 .NET 的 Azure DNS 程式庫"
description: "適用於 .NET 的 Azure DNS 程式庫參考"
keywords: Azure, .NET, SDK, API, DNS
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 57c578f12ea426dc5784658338473f0044d21e5c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="71ad2-104">適用於 .NET 的 Azure DNS 程式庫</span><span class="sxs-lookup"><span data-stu-id="71ad2-104">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="71ad2-105">使用適用於 .NET 的 Microsoft Azure DNS 程式庫，來建立及修改裝載於 Azure 的 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="71ad2-105">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="71ad2-106">區域和記錄會作為 Azure 資源來管理。</span><span class="sxs-lookup"><span data-stu-id="71ad2-106">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="71ad2-107">如需詳細資訊，請參閱 [Azure DNS 概觀](/azure/dns/dns-overview)。</span><span class="sxs-lookup"><span data-stu-id="71ad2-107">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="71ad2-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="71ad2-108">Management library</span></span>

<span data-ttu-id="71ad2-109">使用管理程式庫來建立及修改裝載於 Azure 的 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="71ad2-109">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="71ad2-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="71ad2-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="71ad2-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="71ad2-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="71ad2-112">範例</span><span class="sxs-lookup"><span data-stu-id="71ad2-112">Example</span></span>

<span data-ttu-id="71ad2-113">下列範例會建立新的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="71ad2-113">The following example creates a new DNS zone.</span></span>

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
> [<span data-ttu-id="71ad2-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="71ad2-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="71ad2-115">範例</span><span class="sxs-lookup"><span data-stu-id="71ad2-115">Samples</span></span>

* [<span data-ttu-id="71ad2-116">Azure DNS .NET SDK 範例專案</span><span class="sxs-lookup"><span data-stu-id="71ad2-116">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="71ad2-117">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="71ad2-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

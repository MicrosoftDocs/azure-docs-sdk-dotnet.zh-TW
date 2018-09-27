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
# <a name="azure-dns-libraries-for-net"></a>適用於 .NET 的 Azure DNS 程式庫

使用適用於 .NET 的 Microsoft Azure DNS 程式庫，來建立及修改裝載於 Azure 的 DNS 區域和記錄。 區域和記錄會作為 Azure 資源來管理。 如需詳細資訊，請參閱 [Azure DNS 概觀](/azure/dns/dns-overview)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫來建立及修改裝載於 Azure 的 DNS 區域和記錄。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a>範例

下列範例會建立新的 DNS 區域。

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
> [探索管理 API](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a>範例

* [Azure DNS .NET SDK 範例專案](https://www.microsoft.com/download/details.aspx?id=47268)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

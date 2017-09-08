---
title: "適用於 .NET 的 Azure 虛擬網路程式庫"
description: "適用於 .NET 的 Azure 虛擬網路程式庫參考"
keywords: "Azure, .NET, SDK, API, 虛擬網路"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: ea605dbd632ef4deb9c97c8de3474246dd4be30d
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-network-libraries-for-net"></a>適用於 .NET 的 Azure 虛擬網路程式庫

## <a name="overview"></a>概觀
[Azure 虛擬網路服務](/azure/virtual-network/virtual-networks-overview)可讓 Azure 資源與虛擬網路 (VNet) 安全地彼此連線。 VNet 是您的網路在雲端中的身分。 您也可以將 VNet 互相連線，讓連線至任一 VNet 的資源能夠彼此通訊。 

## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a>程式碼範例
此範例會示範如何建立虛擬網路。

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a>範例
- [使用子網路管理虛擬網路](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

深入探索可在應用程式中使用的 [.NET 範例程式碼](https://azure.microsoft.com/resources/samples/?platform=dotnet)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

